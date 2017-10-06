---
title: 'Zelfstudie: Azure Active Directory-integratie met adaptieve Suite | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en adaptieve Suite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: af309c27ab74098c1e229c80adb11c96dc2774fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="6021b-103">Zelfstudie: Azure Active Directory-integratie met adaptieve Suite</span><span class="sxs-lookup"><span data-stu-id="6021b-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>

<span data-ttu-id="6021b-104">In deze zelfstudie leert u hoe toointegrate adaptieve Suite met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6021b-104">In this tutorial, you learn how toointegrate Adaptive Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6021b-105">Adaptieve Suite integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6021b-105">Integrating Adaptive Suite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6021b-106">U kunt beheren in Azure AD wie toegang tot tooAdaptive Suite heeft</span><span class="sxs-lookup"><span data-stu-id="6021b-106">You can control in Azure AD who has access tooAdaptive Suite</span></span>
- <span data-ttu-id="6021b-107">U kunt uw gebruikers tooautomatically get aangemelde tooAdaptive Suite (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="6021b-107">You can enable your users tooautomatically get signed-on tooAdaptive Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6021b-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6021b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6021b-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6021b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6021b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6021b-110">Prerequisites</span></span>

<span data-ttu-id="6021b-111">Azure AD-integratie met adaptieve Suite tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="6021b-111">tooconfigure Azure AD integration with Adaptive Suite, you need hello following items:</span></span>

- <span data-ttu-id="6021b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6021b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6021b-113">Een adaptieve Suite eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6021b-113">An Adaptive Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6021b-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6021b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6021b-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6021b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6021b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6021b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6021b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6021b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6021b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6021b-118">Scenario description</span></span>
<span data-ttu-id="6021b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6021b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6021b-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6021b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6021b-121">Het toevoegen van adaptieve Suite van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="6021b-121">Adding Adaptive Suite from hello gallery</span></span>
2. <span data-ttu-id="6021b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6021b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-suite-from-hello-gallery"></a><span data-ttu-id="6021b-123">Het toevoegen van adaptieve Suite van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="6021b-123">Adding Adaptive Suite from hello gallery</span></span>
<span data-ttu-id="6021b-124">tooconfigure hello integratie van adaptieve Suite in Azure AD, moet u tooadd adaptieve Suite van Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6021b-124">tooconfigure hello integration of Adaptive Suite into Azure AD, you need tooadd Adaptive Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6021b-125">**tooadd adaptieve Suite van Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6021b-125">**tooadd Adaptive Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6021b-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6021b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6021b-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6021b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6021b-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6021b-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6021b-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6021b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6021b-133">Typ in het zoekvak Hallo **adaptieve Suite**.</span><span class="sxs-lookup"><span data-stu-id="6021b-133">In hello search box, type **Adaptive Suite**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. <span data-ttu-id="6021b-135">Selecteer in het deelvenster resultaten hello, **adaptieve Suite**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6021b-135">In hello results panel, select **Adaptive Suite**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6021b-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6021b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6021b-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met adaptieve Suite op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6021b-138">In this section, you configure and test Azure AD single sign-on with Adaptive Suite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6021b-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in adaptieve Suite is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6021b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adaptive Suite is tooa user in Azure AD.</span></span> <span data-ttu-id="6021b-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in adaptieve Suite toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="6021b-140">In other words, a link relationship between an Azure AD user and hello related user in Adaptive Suite needs toobe established.</span></span>

<span data-ttu-id="6021b-141">In adaptieve Suite Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="6021b-141">In Adaptive Suite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6021b-142">tooconfigure en test eenmalige aanmelding Azure AD met adaptieve Suite, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6021b-142">tooconfigure and test Azure AD single sign-on with Adaptive Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6021b-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="6021b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6021b-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6021b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6021b-145">**[Maken van een testgebruiker adaptieve Suite](#creating-an-adaptive-suite-test-user)**  -toohave een equivalent van Britta Simon in adaptieve-pakket dat is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6021b-145">**[Creating an Adaptive Suite test user](#creating-an-adaptive-suite-test-user)** - toohave a counterpart of Britta Simon in Adaptive Suite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6021b-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6021b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6021b-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6021b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6021b-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6021b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6021b-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing adaptieve Suite.</span><span class="sxs-lookup"><span data-stu-id="6021b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adaptive Suite application.</span></span>

<span data-ttu-id="6021b-150">**Voer tooconfigure Azure AD eenmalige aanmelding met adaptieve Suite Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6021b-150">**tooconfigure Azure AD single sign-on with Adaptive Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="6021b-151">In de Azure-portal op Hallo Hallo **adaptieve Suite** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6021b-151">In hello Azure portal, on hello **Adaptive Suite** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6021b-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6021b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="6021b-155">Op Hallo **adaptieve Suite domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6021b-155">On hello **Adaptive Suite Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="6021b-157">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span><span class="sxs-lookup"><span data-stu-id="6021b-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="6021b-158">U kunt deze waarde niet ophalen uit Hallo adaptieve Suite van **SAML SSO instellingen** pagina.</span><span class="sxs-lookup"><span data-stu-id="6021b-158">You can get this value from hello Adaptive Suite’s **SAML SSO Settings** page.</span></span>
    >  

4. <span data-ttu-id="6021b-159">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6021b-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. <span data-ttu-id="6021b-161">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6021b-161">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6021b-163">Op Hallo **geavanceerde configuratie van de Suite** sectie, klikt u op **adaptieve Suite configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="6021b-163">On hello **Adaptive Suite Configuration** section, click **Configure Adaptive Suite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6021b-164">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="6021b-164">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="6021b-166">In een ander browservenster, meld u aan tooyour adaptieve Suite bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="6021b-166">In a different web browser window, log in tooyour Adaptive Suite company site as an administrator.</span></span>

8. <span data-ttu-id="6021b-167">Ga te**Admin**.</span><span class="sxs-lookup"><span data-stu-id="6021b-167">Go too**Admin**.</span></span>
   
    <span data-ttu-id="6021b-168">![Beheerder](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="6021b-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="6021b-169">In Hallo **gebruikers en rollen** sectie, klikt u op **SAML SSO-instellingen beheren**.</span><span class="sxs-lookup"><span data-stu-id="6021b-169">In hello **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
    <span data-ttu-id="6021b-170">![SAML SSO-instellingen beheren](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "SAML SSO-instellingen beheren")</span><span class="sxs-lookup"><span data-stu-id="6021b-170">![Manage SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="6021b-171">Op Hallo **SAML SSO instellingen** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6021b-171">On hello **SAML SSO Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="6021b-172">![Instellingen voor eenmalige aanmelding SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO-instellingen")</span><span class="sxs-lookup"><span data-stu-id="6021b-172">![SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="6021b-173">a.</span><span class="sxs-lookup"><span data-stu-id="6021b-173">a.</span></span> <span data-ttu-id="6021b-174">In Hallo **identiteit providernaam** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="6021b-174">In hello **Identity provider name** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="6021b-175">b.</span><span class="sxs-lookup"><span data-stu-id="6021b-175">b.</span></span> <span data-ttu-id="6021b-176">Plakken Hallo **SAML entiteit-ID** waarde gekopieerd vanuit Azure-portal naar Hallo **identiteitsprovider entiteit-ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="6021b-176">Paste hello **SAML Entity ID** value copied from Azure portal into hello **Identity provider Entity ID** textbox.</span></span>
  
    <span data-ttu-id="6021b-177">c.</span><span class="sxs-lookup"><span data-stu-id="6021b-177">c.</span></span> <span data-ttu-id="6021b-178">Plakken Hallo **SAML Single Sign-On Service-URL** waarde gekopieerd vanuit Azure-portal naar Hallo **identiteitsprovider URL SSO** textbox.</span><span class="sxs-lookup"><span data-stu-id="6021b-178">Paste hello **SAML Single Sign-On Service URL** value copied from Azure portal into hello **Identity provider SSO URL** textbox.</span></span>
  
    <span data-ttu-id="6021b-179">d.</span><span class="sxs-lookup"><span data-stu-id="6021b-179">d.</span></span> <span data-ttu-id="6021b-180">Plakken Hallo **SAML Single Sign-On Service-URL** waarde gekopieerd vanuit Azure-portal naar Hallo **aangepaste afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="6021b-180">Paste hello **SAML Single Sign-On Service URL** value copied from Azure portal into hello **Custom logout URL** textbox.</span></span>
  
    <span data-ttu-id="6021b-181">e.</span><span class="sxs-lookup"><span data-stu-id="6021b-181">e.</span></span> <span data-ttu-id="6021b-182">tooupload uw gedownloade certificaat, klik op **bestand kiezen**.</span><span class="sxs-lookup"><span data-stu-id="6021b-182">tooupload your downloaded certificate, click **Choose file**.</span></span>
  
    <span data-ttu-id="6021b-183">f.</span><span class="sxs-lookup"><span data-stu-id="6021b-183">f.</span></span> <span data-ttu-id="6021b-184">Selecteer de volgende hello, voor:</span><span class="sxs-lookup"><span data-stu-id="6021b-184">Select hello following, for:</span></span>
    * <span data-ttu-id="6021b-185">**Gebruikers-id van SAML**, selecteer **adaptieve Insights gebruiker gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="6021b-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="6021b-186">**Locatie van het SAML-id**, selecteer **gebruikers-id in NameID van onderwerp**.</span><span class="sxs-lookup"><span data-stu-id="6021b-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="6021b-187">**SAML NameID indeling**, selecteer **e-mailadres**.</span><span class="sxs-lookup"><span data-stu-id="6021b-187">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="6021b-188">**SAML inschakelen**, selecteer **toestaan SAML SSO en direct adaptieve Insights aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="6021b-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
    
    <span data-ttu-id="6021b-189">g.</span><span class="sxs-lookup"><span data-stu-id="6021b-189">g.</span></span> <span data-ttu-id="6021b-190">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6021b-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6021b-191">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="6021b-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6021b-192">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="6021b-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6021b-193">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6021b-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6021b-194">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6021b-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="6021b-195">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6021b-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6021b-197">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6021b-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6021b-198">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6021b-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6021b-200">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6021b-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6021b-202">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="6021b-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6021b-204">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6021b-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6021b-206">a.</span><span class="sxs-lookup"><span data-stu-id="6021b-206">a.</span></span> <span data-ttu-id="6021b-207">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6021b-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6021b-208">b.</span><span class="sxs-lookup"><span data-stu-id="6021b-208">b.</span></span> <span data-ttu-id="6021b-209">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6021b-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6021b-210">c.</span><span class="sxs-lookup"><span data-stu-id="6021b-210">c.</span></span> <span data-ttu-id="6021b-211">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6021b-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6021b-212">d.</span><span class="sxs-lookup"><span data-stu-id="6021b-212">d.</span></span> <span data-ttu-id="6021b-213">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6021b-213">Click **Create**.</span></span>
 
### <a name="creating-an-adaptive-suite-test-user"></a><span data-ttu-id="6021b-214">Maken van een testgebruiker adaptieve Suite</span><span class="sxs-lookup"><span data-stu-id="6021b-214">Creating an Adaptive Suite test user</span></span>

<span data-ttu-id="6021b-215">Azure AD tooenable gebruikers toolog in tooAdaptive Suite, moeten ze worden ingericht in adaptieve Suite.</span><span class="sxs-lookup"><span data-stu-id="6021b-215">tooenable Azure AD users toolog in tooAdaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="6021b-216">In geval van adaptieve Suite Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="6021b-216">In hello case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="6021b-217">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="6021b-217">**tooconfigure user provisioning, perform hello following steps:**</span></span> 

1. <span data-ttu-id="6021b-218">Meld u bij tooyour **adaptieve Suite** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="6021b-218">Log in tooyour **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="6021b-219">Ga te**Admin**.</span><span class="sxs-lookup"><span data-stu-id="6021b-219">Go too**Admin**.</span></span>
   
   <span data-ttu-id="6021b-220">![Beheerder](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="6021b-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="6021b-221">In Hallo **gebruikers en rollen** sectie, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6021b-221">In hello **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="6021b-222">![Gebruiker toevoegen](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="6021b-222">![Add User](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="6021b-223">In Hallo **nieuwe gebruiker** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6021b-223">In hello **New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="6021b-224">![Indienen](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "verzenden")</span><span class="sxs-lookup"><span data-stu-id="6021b-224">![Submit](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Submit")</span></span>   

   <span data-ttu-id="6021b-225">a.</span><span class="sxs-lookup"><span data-stu-id="6021b-225">a.</span></span> <span data-ttu-id="6021b-226">Type Hallo **naam**, **aanmelding**, **e**, **wachtwoord** van een geldige Azure Active Directory-gebruiker gewenste tooprovision in Hallo gerelateerd tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="6021b-226">Type hello **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want tooprovision into hello related textboxes.</span></span>
  
   <span data-ttu-id="6021b-227">b.</span><span class="sxs-lookup"><span data-stu-id="6021b-227">b.</span></span> <span data-ttu-id="6021b-228">Selecteer een **rol**.</span><span class="sxs-lookup"><span data-stu-id="6021b-228">Select a **Role**.</span></span>
  
   <span data-ttu-id="6021b-229">c.</span><span class="sxs-lookup"><span data-stu-id="6021b-229">c.</span></span> <span data-ttu-id="6021b-230">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="6021b-230">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="6021b-231">U kunt andere adaptieve Suite gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door adaptieve Suite tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="6021b-231">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6021b-232">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6021b-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6021b-233">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooAdaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="6021b-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdaptive Suite.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6021b-235">**tooassign Britta Simon tooAdaptive Suite Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6021b-235">**tooassign Britta Simon tooAdaptive Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="6021b-236">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6021b-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6021b-238">Selecteer in de lijst met de toepassingen van Hallo **adaptieve Suite**.</span><span class="sxs-lookup"><span data-stu-id="6021b-238">In hello applications list, select **Adaptive Suite**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. <span data-ttu-id="6021b-240">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6021b-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6021b-242">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6021b-242">Click **Add** button.</span></span> <span data-ttu-id="6021b-243">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6021b-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6021b-245">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="6021b-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6021b-246">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6021b-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6021b-247">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6021b-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6021b-248">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6021b-248">Testing single sign-on</span></span>

<span data-ttu-id="6021b-249">Hallo-doel van deze sectie is tootest uw Microsoft Azure AD Single Sign-On configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="6021b-249">hello objective of this section is tootest your Microsoft Azure AD Single Sign-On configuration using hello Access Panel.</span></span>

<span data-ttu-id="6021b-250">Als u op Hallo adaptieve Suite tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour adaptieve Suite-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6021b-250">When you click hello Adaptive Suite tile in hello Access Panel, you should get automatically signed-on tooyour Adaptive Suite application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="6021b-251">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6021b-251">Additional resources</span></span>

* [<span data-ttu-id="6021b-252">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6021b-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6021b-253">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6021b-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

