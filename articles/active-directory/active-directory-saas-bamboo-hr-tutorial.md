---
title: 'Zelfstudie: Azure Active Directory-integratie met BambooHR | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en BambooHR.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f826b5d2-9c64-47df-bbbf-0adf9eb0fa71
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: jeedes
ms.openlocfilehash: f9083f846beb3a4bf4cebbf18b42aba2dfef2472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bamboohr"></a><span data-ttu-id="dee6d-103">Zelfstudie: Azure Active Directory-integratie met BambooHR</span><span class="sxs-lookup"><span data-stu-id="dee6d-103">Tutorial: Azure Active Directory integration with BambooHR</span></span>

<span data-ttu-id="dee6d-104">In deze zelfstudie leert u hoe toointegrate BambooHR met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dee6d-104">In this tutorial, you learn how toointegrate BambooHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dee6d-105">BambooHR integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="dee6d-105">Integrating BambooHR with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dee6d-106">U kunt beheren in Azure AD die tooBambooHR toegang heeft</span><span class="sxs-lookup"><span data-stu-id="dee6d-106">You can control in Azure AD who has access tooBambooHR</span></span>
- <span data-ttu-id="dee6d-107">U kunt uw gebruikers tooautomatically get aangemelde tooBambooHR (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="dee6d-107">You can enable your users tooautomatically get signed-on tooBambooHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dee6d-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="dee6d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dee6d-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dee6d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dee6d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="dee6d-110">Prerequisites</span></span>

<span data-ttu-id="dee6d-111">Azure AD-integratie met BambooHR tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="dee6d-111">tooconfigure Azure AD integration with BambooHR, you need hello following items:</span></span>

- <span data-ttu-id="dee6d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="dee6d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dee6d-113">Een BambooHR eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="dee6d-113">A BambooHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dee6d-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="dee6d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dee6d-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="dee6d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dee6d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="dee6d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dee6d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dee6d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dee6d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="dee6d-118">Scenario description</span></span>
<span data-ttu-id="dee6d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="dee6d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dee6d-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="dee6d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dee6d-121">Het toevoegen van BambooHR van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="dee6d-121">Adding BambooHR from hello gallery</span></span>
2. <span data-ttu-id="dee6d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="dee6d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bamboohr-from-hello-gallery"></a><span data-ttu-id="dee6d-123">Het toevoegen van BambooHR van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="dee6d-123">Adding BambooHR from hello gallery</span></span>
<span data-ttu-id="dee6d-124">tooconfigure hello integratie van BambooHR in Azure AD, moet u tooadd BambooHR uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="dee6d-124">tooconfigure hello integration of BambooHR into Azure AD, you need tooadd BambooHR from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dee6d-125">**tooadd BambooHR via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="dee6d-125">**tooadd BambooHR from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dee6d-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="dee6d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dee6d-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dee6d-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="dee6d-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dee6d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="dee6d-133">Typ in het zoekvak Hallo **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-133">In hello search box, type **BambooHR**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_search.png)

5. <span data-ttu-id="dee6d-135">Selecteer in het deelvenster resultaten hello, **BambooHR**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="dee6d-135">In hello results panel, select **BambooHR**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dee6d-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="dee6d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dee6d-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met BambooHR op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="dee6d-138">In this section, you configure and test Azure AD single sign-on with BambooHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dee6d-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in BambooHR is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dee6d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BambooHR is tooa user in Azure AD.</span></span> <span data-ttu-id="dee6d-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in BambooHR toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="dee6d-140">In other words, a link relationship between an Azure AD user and hello related user in BambooHR needs toobe established.</span></span>

<span data-ttu-id="dee6d-141">Wijs in BambooHR, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="dee6d-141">In BambooHR, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dee6d-142">tooconfigure en eenmalige aanmelding Azure AD-test met BambooHR, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dee6d-142">tooconfigure and test Azure AD single sign-on with BambooHR, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dee6d-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="dee6d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dee6d-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dee6d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dee6d-145">**[Maken van een testgebruiker BambooHR](#creating-a-bamboohr-test-user)**  -toohave een equivalent van Britta Simon in BambooHR die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="dee6d-145">**[Creating a BambooHR test user](#creating-a-bamboohr-test-user)** - toohave a counterpart of Britta Simon in BambooHR that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dee6d-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="dee6d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dee6d-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="dee6d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dee6d-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="dee6d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dee6d-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing BambooHR configureren.</span><span class="sxs-lookup"><span data-stu-id="dee6d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BambooHR application.</span></span>

<span data-ttu-id="dee6d-150">**Azure AD tooconfigure eenmalige aanmelding met BambooHR, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="dee6d-150">**tooconfigure Azure AD single sign-on with BambooHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="dee6d-151">In de Azure-portal op Hallo Hallo **BambooHR** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-151">In hello Azure portal, on hello **BambooHR** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="dee6d-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="dee6d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_samlbase.png)

3. <span data-ttu-id="dee6d-155">Op Hallo **BambooHR domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dee6d-155">On hello **BambooHR Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_url.png)

    <span data-ttu-id="dee6d-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company>.bamboohr.com`</span><span class="sxs-lookup"><span data-stu-id="dee6d-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.bamboohr.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="dee6d-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="dee6d-158">This value is not real.</span></span> <span data-ttu-id="dee6d-159">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="dee6d-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="dee6d-160">Neem contact op met [BambooHR Client ondersteuningsteam](https://www.bamboohr.com/contact.php) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="dee6d-160">Contact [BambooHR Client support team](https://www.bamboohr.com/contact.php) tooget this value.</span></span> 
 
4. <span data-ttu-id="dee6d-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="dee6d-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_certificate.png) 

5. <span data-ttu-id="dee6d-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="dee6d-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dee6d-165">Op Hallo **BambooHR configuratie** sectie, klikt u op **configureren BambooHR** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="dee6d-165">On hello **BambooHR Configuration** section, click **Configure BambooHR** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dee6d-166">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="dee6d-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_configure.png) 

6. <span data-ttu-id="dee6d-168">In een ander browservenster, meld u bij uw bedrijf BambooHR site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="dee6d-168">In a different web browser window, log into your BambooHR company site as an administrator.</span></span>

7. <span data-ttu-id="dee6d-169">Voer op Hallo-startpagina Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dee6d-169">On hello homepage, perform hello following steps:</span></span>
   
    <span data-ttu-id="dee6d-170">![Eenmalige aanmelding](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="dee6d-170">![Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span></span>   

    <span data-ttu-id="dee6d-171">a.</span><span class="sxs-lookup"><span data-stu-id="dee6d-171">a.</span></span> <span data-ttu-id="dee6d-172">Klik op **Apps**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-172">Click **Apps**.</span></span>
   
    <span data-ttu-id="dee6d-173">b.</span><span class="sxs-lookup"><span data-stu-id="dee6d-173">b.</span></span> <span data-ttu-id="dee6d-174">Hallo apps menu aan de linkerkant Hallo en klik op **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-174">In hello apps menu on hello left, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="dee6d-175">c.</span><span class="sxs-lookup"><span data-stu-id="dee6d-175">c.</span></span> <span data-ttu-id="dee6d-176">Klik op **SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-176">Click **SAML Single Sign-On**.</span></span>

8. <span data-ttu-id="dee6d-177">In Hallo **SAML Single Sign-On** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dee6d-177">In hello **SAML Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="dee6d-178">![Eenmalige aanmelding SAML](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="dee6d-178">![SAML Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML Single Sign-On")</span></span>
   
    <span data-ttu-id="dee6d-179">a.</span><span class="sxs-lookup"><span data-stu-id="dee6d-179">a.</span></span> <span data-ttu-id="dee6d-180">Plakken Hallo **SAML Single Sign-On Service-URL** waarde in Hallo **aanmeldings-Url voor eenmalige aanmelding** textbox.</span><span class="sxs-lookup"><span data-stu-id="dee6d-180">Paste hello **SAML Single Sign-On Service URL** value into hello **SSO Login Url** textbox.</span></span>
      
    <span data-ttu-id="dee6d-181">b.</span><span class="sxs-lookup"><span data-stu-id="dee6d-181">b.</span></span> <span data-ttu-id="dee6d-182">Open base-64 gecodeerde certificaat gedownload vanuit Azure-portal in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **X.509-certificaat** tekstvak</span><span class="sxs-lookup"><span data-stu-id="dee6d-182">Open base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>
   
    <span data-ttu-id="dee6d-183">c.</span><span class="sxs-lookup"><span data-stu-id="dee6d-183">c.</span></span> <span data-ttu-id="dee6d-184">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="dee6d-185">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="dee6d-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dee6d-186">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="dee6d-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dee6d-187">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dee6d-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dee6d-188">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="dee6d-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="dee6d-189">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="dee6d-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="dee6d-191">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="dee6d-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dee6d-192">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="dee6d-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dee6d-194">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dee6d-196">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="dee6d-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dee6d-198">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dee6d-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dee6d-200">a.</span><span class="sxs-lookup"><span data-stu-id="dee6d-200">a.</span></span> <span data-ttu-id="dee6d-201">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dee6d-202">b.</span><span class="sxs-lookup"><span data-stu-id="dee6d-202">b.</span></span> <span data-ttu-id="dee6d-203">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dee6d-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dee6d-204">c.</span><span class="sxs-lookup"><span data-stu-id="dee6d-204">c.</span></span> <span data-ttu-id="dee6d-205">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dee6d-206">d.</span><span class="sxs-lookup"><span data-stu-id="dee6d-206">d.</span></span> <span data-ttu-id="dee6d-207">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-207">Click **Create**.</span></span>
 
### <a name="creating-a-bamboohr-test-user"></a><span data-ttu-id="dee6d-208">Een testgebruiker BambooHR maken</span><span class="sxs-lookup"><span data-stu-id="dee6d-208">Creating a BambooHR test user</span></span>

<span data-ttu-id="dee6d-209">Azure AD tooenable gebruikers toolog in tooBambooHR, ze in BambooHR moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="dee6d-209">tooenable Azure AD users toolog in tooBambooHR, they must be provisioned into BambooHR.</span></span>  

<span data-ttu-id="dee6d-210">In geval van BambooHR Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="dee6d-210">In hello case of BambooHR, provisioning is a manual task.</span></span>

<span data-ttu-id="dee6d-211">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="dee6d-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="dee6d-212">Meld u bij tooyour **BambooHR** site als administrator.</span><span class="sxs-lookup"><span data-stu-id="dee6d-212">Log in tooyour **BambooHR** site as administrator.</span></span>

2. <span data-ttu-id="dee6d-213">Klik in de werkbalk bovenaan Hallo Hallo op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-213">In hello toolbar on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="dee6d-214">![Instelling](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "instelling")</span><span class="sxs-lookup"><span data-stu-id="dee6d-214">![Setting](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Setting")</span></span>

3. <span data-ttu-id="dee6d-215">Klik op **overzicht**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-215">Click **Overview**.</span></span>

4. <span data-ttu-id="dee6d-216">Ga te in Hallo navigatiedeelvenster links**beveiliging \> gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-216">In hello left navigation pane, go too**Security \> Users**.</span></span>

5. <span data-ttu-id="dee6d-217">Type Hallo-gebruikersnaam, wachtwoord en e-mailadres van een geldige AAD-account dat u wilt dat tooprovision in Hallo gerelateerd tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="dee6d-217">Type hello user name, password, and email address of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

6. <span data-ttu-id="dee6d-218">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-218">Click **Save**.</span></span>
        
>[!NOTE]
><span data-ttu-id="dee6d-219">U kunt andere BambooHR gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door BambooHR tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="dee6d-219">You can use any other BambooHR user account creation tools or APIs provided by BambooHR tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dee6d-220">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="dee6d-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dee6d-221">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooBambooHR toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="dee6d-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBambooHR.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="dee6d-223">**tooassign Britta Simon tooBambooHR, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="dee6d-223">**tooassign Britta Simon tooBambooHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="dee6d-224">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="dee6d-226">Selecteer in de lijst met de toepassingen van Hallo **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-226">In hello applications list, select **BambooHR**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_app.png) 

3. <span data-ttu-id="dee6d-228">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="dee6d-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="dee6d-230">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="dee6d-230">Click **Add** button.</span></span> <span data-ttu-id="dee6d-231">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dee6d-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="dee6d-233">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="dee6d-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dee6d-234">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dee6d-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dee6d-235">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dee6d-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dee6d-236">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="dee6d-236">Testing single sign-on</span></span>

<span data-ttu-id="dee6d-237">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="dee6d-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dee6d-238">Als u op Hallo BambooHR tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour BambooHR toepassing.</span><span class="sxs-lookup"><span data-stu-id="dee6d-238">When you click hello BambooHR tile in hello Access Panel, you should get automatically signed-on tooyour BambooHR application.</span></span>
<span data-ttu-id="dee6d-239">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dee6d-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="dee6d-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="dee6d-240">Additional resources</span></span>

* [<span data-ttu-id="dee6d-241">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dee6d-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dee6d-242">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dee6d-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_203.png

