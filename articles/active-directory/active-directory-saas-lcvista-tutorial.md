---
title: 'Zelfstudie: Azure Active Directory-integratie met LCVista | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en LCVista.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 5a4c7eb7d54b8b68c8241a97b9e516a3f6e55c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="1050a-103">Zelfstudie: Azure Active Directory-integratie met LCVista</span><span class="sxs-lookup"><span data-stu-id="1050a-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="1050a-104">In deze zelfstudie leert u hoe toointegrate LCVista met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1050a-104">In this tutorial, you learn how toointegrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1050a-105">LCVista integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1050a-105">Integrating LCVista with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1050a-106">U kunt beheren in Azure AD die tooLCVista toegang heeft</span><span class="sxs-lookup"><span data-stu-id="1050a-106">You can control in Azure AD who has access tooLCVista</span></span>
- <span data-ttu-id="1050a-107">U kunt uw gebruikers tooautomatically get aangemelde tooLCVista (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="1050a-107">You can enable your users tooautomatically get signed-on tooLCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1050a-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="1050a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1050a-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1050a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1050a-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1050a-110">Prerequisites</span></span>

<span data-ttu-id="1050a-111">Azure AD-integratie met LCVista tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="1050a-111">tooconfigure Azure AD integration with LCVista, you need hello following items:</span></span>

- <span data-ttu-id="1050a-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1050a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1050a-113">Een LCVista eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="1050a-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1050a-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1050a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1050a-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1050a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1050a-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1050a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1050a-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1050a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1050a-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1050a-118">Scenario description</span></span>
<span data-ttu-id="1050a-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1050a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1050a-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1050a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1050a-121">Het toevoegen van LCVista van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="1050a-121">Adding LCVista from hello gallery</span></span>
2. <span data-ttu-id="1050a-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1050a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-hello-gallery"></a><span data-ttu-id="1050a-123">Het toevoegen van LCVista van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="1050a-123">Adding LCVista from hello gallery</span></span>
<span data-ttu-id="1050a-124">tooconfigure hello integratie van LCVista in Azure AD, moet u tooadd LCVista uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1050a-124">tooconfigure hello integration of LCVista into Azure AD, you need tooadd LCVista from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1050a-125">**tooadd LCVista via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1050a-125">**tooadd LCVista from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1050a-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1050a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1050a-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1050a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1050a-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1050a-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="1050a-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1050a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="1050a-133">Typ in het zoekvak Hallo **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="1050a-133">In hello search box, type **LCVista**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="1050a-135">Selecteer in het deelvenster resultaten hello, **LCVista**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="1050a-135">In hello results panel, select **LCVista**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1050a-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1050a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1050a-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met LCVista op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="1050a-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1050a-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in LCVista is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1050a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LCVista is tooa user in Azure AD.</span></span> <span data-ttu-id="1050a-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in LCVista toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="1050a-140">In other words, a link relationship between an Azure AD user and hello related user in LCVista needs toobe established.</span></span>

<span data-ttu-id="1050a-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in LCVista.</span><span class="sxs-lookup"><span data-stu-id="1050a-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LCVista.</span></span>

<span data-ttu-id="1050a-142">tooconfigure en eenmalige aanmelding Azure AD-test met LCVista, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1050a-142">tooconfigure and test Azure AD single sign-on with LCVista, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1050a-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="1050a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1050a-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1050a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1050a-145">**[Maken van een testgebruiker LCVista](#creating-a-lcvista-test-user)**  -toohave een equivalent van Britta Simon in LCVista die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1050a-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - toohave a counterpart of Britta Simon in LCVista that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1050a-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1050a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1050a-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1050a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1050a-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1050a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1050a-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing LCVista configureren.</span><span class="sxs-lookup"><span data-stu-id="1050a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="1050a-150">**Azure AD tooconfigure eenmalige aanmelding met LCVista, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1050a-150">**tooconfigure Azure AD single sign-on with LCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="1050a-151">In de Azure-portal op Hallo Hallo **LCVista** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1050a-151">In hello Azure portal, on hello **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1050a-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1050a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="1050a-155">Op Hallo **LCVista domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1050a-155">On hello **LCVista Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="1050a-157">a.</span><span class="sxs-lookup"><span data-stu-id="1050a-157">a.</span></span> <span data-ttu-id="1050a-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.lcvista.com/rainier/login`</span><span class="sxs-lookup"><span data-stu-id="1050a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="1050a-159">b.</span><span class="sxs-lookup"><span data-stu-id="1050a-159">b.</span></span> <span data-ttu-id="1050a-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="1050a-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="1050a-161">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="1050a-161">These values are not hello real.</span></span> <span data-ttu-id="1050a-162">Bijwerken van deze waarden met de werkelijke Hallo-id en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="1050a-162">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="1050a-163">Neem contact op met [LCVista Client ondersteuningsteam](https://lcvista.com/contact) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="1050a-163">Contact [LCVista Client support team](https://lcvista.com/contact) tooget these values.</span></span> 

4. <span data-ttu-id="1050a-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1050a-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="1050a-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1050a-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="1050a-168">Op Hallo **LCVista configuratie** sectie, klikt u op **configureren LCVista** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="1050a-168">On hello **LCVista Configuration** section, click **Configure LCVista** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1050a-169">Kopiëren Hallo **SAML entiteit-ID** en **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="1050a-169">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="1050a-171">Meld u aan op tooyour LCVista toepassing als beheerder.</span><span class="sxs-lookup"><span data-stu-id="1050a-171">Sign on tooyour LCVista application as an administrator.</span></span>

8. <span data-ttu-id="1050a-172">In Hallo **SAML-Config** sectie, controleert u Hallo **SAML inschakelen aanmelding** en Voer Hallo details, zoals vermeld in onderstaande afbeelding.</span><span class="sxs-lookup"><span data-stu-id="1050a-172">In hello **SAML Config** section, check hello **Enable SAML login** and enter hello details as mentioned in below image.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="1050a-174">a.</span><span class="sxs-lookup"><span data-stu-id="1050a-174">a.</span></span> <span data-ttu-id="1050a-175">Plakken Hallo **URL-verlener** die u hebt gekopieerd uit Azure AD in Hallo **entiteit-ID** sectie.</span><span class="sxs-lookup"><span data-stu-id="1050a-175">Paste hello **Issuer URL** which you have copied from Azure AD in hello **Entity ID** section.</span></span> 

    <span data-ttu-id="1050a-176">b.</span><span class="sxs-lookup"><span data-stu-id="1050a-176">b.</span></span> <span data-ttu-id="1050a-177">Plakken Hallo **Single Sign-On Service-URL** die u hebt gekopieerd uit Azure AD in Hallo **URL** sectie.</span><span class="sxs-lookup"><span data-stu-id="1050a-177">Paste hello **Single Sign-On Service URL** which you have copied from Azure AD in hello **URL** section.</span></span>

    <span data-ttu-id="1050a-178">c.</span><span class="sxs-lookup"><span data-stu-id="1050a-178">c.</span></span> <span data-ttu-id="1050a-179">Van metagegevens (XML) die u vanuit Azure-portal hebt gedownload, kopieert u Hallo waarde **X509Certificate** en plak deze in Hallo **x509-certificaat** sectie.</span><span class="sxs-lookup"><span data-stu-id="1050a-179">From Metadata (XML) which you have downloaded from Azure portal, copy hello value **X509Certificate** and paste it in hello **x509 Certificate** section.</span></span>

    <span data-ttu-id="1050a-180">d.</span><span class="sxs-lookup"><span data-stu-id="1050a-180">d.</span></span> <span data-ttu-id="1050a-181">In Hallo **voornaam kenmerk** textbox plakken Hallo waarde `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="1050a-181">In hello **First name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="1050a-182">e.</span><span class="sxs-lookup"><span data-stu-id="1050a-182">e.</span></span> <span data-ttu-id="1050a-183">In Hallo **laatste naamkenmerk** textbox plakken Hallo waarde `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="1050a-183">In hello **Last name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="1050a-184">f.</span><span class="sxs-lookup"><span data-stu-id="1050a-184">f.</span></span> <span data-ttu-id="1050a-185">In Hallo **e kenmerk** textbox plakken Hallo waarde `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="1050a-185">In hello **Email attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="1050a-186">g.</span><span class="sxs-lookup"><span data-stu-id="1050a-186">g.</span></span> <span data-ttu-id="1050a-187">In Hallo **kenmerk Username** textbox plakken Hallo waarde `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="1050a-187">In hello **Username attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="1050a-188">e.</span><span class="sxs-lookup"><span data-stu-id="1050a-188">e.</span></span> <span data-ttu-id="1050a-189">Klik op **opslaan** toosave Hallo instellingen.</span><span class="sxs-lookup"><span data-stu-id="1050a-189">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="1050a-190">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="1050a-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1050a-191">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="1050a-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1050a-192">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1050a-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1050a-193">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1050a-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="1050a-194">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1050a-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="1050a-196">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1050a-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1050a-197">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1050a-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1050a-199">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1050a-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1050a-201">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="1050a-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1050a-203">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1050a-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1050a-205">a.</span><span class="sxs-lookup"><span data-stu-id="1050a-205">a.</span></span> <span data-ttu-id="1050a-206">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1050a-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1050a-207">b.</span><span class="sxs-lookup"><span data-stu-id="1050a-207">b.</span></span> <span data-ttu-id="1050a-208">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1050a-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1050a-209">c.</span><span class="sxs-lookup"><span data-stu-id="1050a-209">c.</span></span> <span data-ttu-id="1050a-210">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1050a-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1050a-211">d.</span><span class="sxs-lookup"><span data-stu-id="1050a-211">d.</span></span> <span data-ttu-id="1050a-212">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1050a-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="1050a-213">Een testgebruiker LCVista maken</span><span class="sxs-lookup"><span data-stu-id="1050a-213">Creating a LCVista test user</span></span>

<span data-ttu-id="1050a-214">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in LCVista maken.</span><span class="sxs-lookup"><span data-stu-id="1050a-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="1050a-215">U moet toocontact [LCVista Client ondersteuningsteam](https://lcvista.com/contact) tooadd Hallo gebruikers in Hallo LCVista toepassing.</span><span class="sxs-lookup"><span data-stu-id="1050a-215">You need toocontact [LCVista Client support team](https://lcvista.com/contact) tooadd hello users in hello LCVista application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1050a-216">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1050a-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1050a-217">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooLCVista toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="1050a-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLCVista.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="1050a-219">**tooassign Britta Simon tooLCVista, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1050a-219">**tooassign Britta Simon tooLCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="1050a-220">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1050a-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1050a-222">Selecteer in de lijst met de toepassingen van Hallo **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="1050a-222">In hello applications list, select **LCVista**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="1050a-224">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1050a-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="1050a-226">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1050a-226">Click **Add** button.</span></span> <span data-ttu-id="1050a-227">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1050a-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="1050a-229">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="1050a-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1050a-230">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1050a-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1050a-231">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1050a-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1050a-232">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1050a-232">Testing single sign-on</span></span>

<span data-ttu-id="1050a-233">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="1050a-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="1050a-234">Klik op Hallo LCVista tegel in Hallo Toegangsvenster, kunt u zich tooOrganization aanmelding pagina omgeleid.</span><span class="sxs-lookup"><span data-stu-id="1050a-234">Click hello LCVista tile in hello Access Panel, you will be redirected tooOrganization sign on page.</span></span> <span data-ttu-id="1050a-235">Worden ondertekend op tooyour LCVista toepassing na geslaagde aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1050a-235">After successful login, you will be signed-on tooyour LCVista application.</span></span> <span data-ttu-id="1050a-236">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="1050a-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1050a-237">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1050a-237">Additional resources</span></span>

* [<span data-ttu-id="1050a-238">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1050a-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1050a-239">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1050a-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png

