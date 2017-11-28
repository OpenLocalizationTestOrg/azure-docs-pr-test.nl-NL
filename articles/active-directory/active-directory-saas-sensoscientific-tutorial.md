---
title: 'Zelfstudie: Azure Active Directory-integratie met SensoScientific draadloze temperatuur Monitoring System | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SensoScientific draadloze temperatuur Monitoring System.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 4eabf7fc6457c217fd5c0c2539ab88c8110055e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a><span data-ttu-id="327a9-103">Zelfstudie: Azure Active Directory-integratie met SensoScientific draadloze temperatuur Monitoring System</span><span class="sxs-lookup"><span data-stu-id="327a9-103">Tutorial: Azure Active Directory integration with SensoScientific Wireless Temperature Monitoring System</span></span>

<span data-ttu-id="327a9-104">In deze zelfstudie leert u hoe toointegrate SensoScientific draadloze temperatuur Monitoring System met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="327a9-104">In this tutorial, you learn how toointegrate SensoScientific Wireless Temperature Monitoring System with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="327a9-105">SensoScientific draadloze temperatuur Monitoring System integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="327a9-105">Integrating SensoScientific Wireless Temperature Monitoring System with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="327a9-106">U kunt beheren in Azure AD wie toegang tot tooSensoScientific draadloze temperatuur Monitoring System heeft</span><span class="sxs-lookup"><span data-stu-id="327a9-106">You can control in Azure AD who has access tooSensoScientific Wireless Temperature Monitoring System</span></span>
- <span data-ttu-id="327a9-107">U kunt uw gebruikers tooautomatically get aangemelde tooSensoScientific draadloze temperatuur Monitoring System (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="327a9-107">You can enable your users tooautomatically get signed-on tooSensoScientific Wireless Temperature Monitoring System (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="327a9-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="327a9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="327a9-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="327a9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="327a9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="327a9-110">Prerequisites</span></span>

<span data-ttu-id="327a9-111">Azure AD-integratie met SensoScientific draadloze temperatuur Monitoring System tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="327a9-111">tooconfigure Azure AD integration with SensoScientific Wireless Temperature Monitoring System, you need hello following items:</span></span>

- <span data-ttu-id="327a9-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="327a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="327a9-113">Een SensoScientific draadloze temperatuur Monitoring System eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="327a9-113">A SensoScientific Wireless Temperature Monitoring System single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="327a9-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="327a9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="327a9-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="327a9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="327a9-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="327a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="327a9-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="327a9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="327a9-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="327a9-118">Scenario description</span></span>
<span data-ttu-id="327a9-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="327a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="327a9-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="327a9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="327a9-121">Het toevoegen van SensoScientific draadloze temperatuur Monitoring System van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="327a9-121">Adding SensoScientific Wireless Temperature Monitoring System from hello gallery</span></span>
2. <span data-ttu-id="327a9-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="327a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-hello-gallery"></a><span data-ttu-id="327a9-123">Het toevoegen van SensoScientific draadloze temperatuur Monitoring System van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="327a9-123">Adding SensoScientific Wireless Temperature Monitoring System from hello gallery</span></span>
<span data-ttu-id="327a9-124">tooconfigure hello integratie van SensoScientific draadloze temperatuur-bewakingssysteem in Azure AD, moet u tooadd SensoScientific draadloze temperatuur Monitoring System uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="327a9-124">tooconfigure hello integration of SensoScientific Wireless Temperature Monitoring System into Azure AD, you need tooadd SensoScientific Wireless Temperature Monitoring System from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="327a9-125">**tooadd SensoScientific draadloze temperatuur Monitoring System via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="327a9-125">**tooadd SensoScientific Wireless Temperature Monitoring System from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="327a9-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="327a9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="327a9-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="327a9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="327a9-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="327a9-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="327a9-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="327a9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="327a9-133">Typ in het zoekvak Hallo **SensoScientific draadloze temperatuur Monitoring System**.</span><span class="sxs-lookup"><span data-stu-id="327a9-133">In hello search box, type **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. <span data-ttu-id="327a9-135">Selecteer in het deelvenster resultaten hello, **SensoScientific draadloze temperatuur Monitoring System**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="327a9-135">In hello results panel, select **SensoScientific Wireless Temperature Monitoring System**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="327a9-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="327a9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="327a9-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met SensoScientific draadloze temperatuur Monitoring System op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="327a9-138">In this section, you configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="327a9-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in SensoScientific draadloze temperatuur Monitoring System is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="327a9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SensoScientific Wireless Temperature Monitoring System is tooa user in Azure AD.</span></span> <span data-ttu-id="327a9-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in SensoScientific draadloze temperatuur Monitoring System toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="327a9-140">In other words, a link relationship between an Azure AD user and hello related user in SensoScientific Wireless Temperature Monitoring System needs toobe established.</span></span>

<span data-ttu-id="327a9-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in SensoScientific draadloze temperatuur Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="327a9-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SensoScientific Wireless Temperature Monitoring System.</span></span>

<span data-ttu-id="327a9-142">tooconfigure en eenmalige aanmelding Azure AD-test met SensoScientific draadloze temperatuur Monitoring System, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="327a9-142">tooconfigure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="327a9-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="327a9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="327a9-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="327a9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="327a9-145">**[Maken van een testgebruiker SensoScientific draadloze temperatuur Monitoring System](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  -toohave een equivalent van Britta Simon in SensoScientific draadloze temperatuur bewakingssysteem die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="327a9-145">**[Creating a SensoScientific Wireless Temperature Monitoring System test user](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)** - toohave a counterpart of Britta Simon in SensoScientific Wireless Temperature Monitoring System that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="327a9-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="327a9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="327a9-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="327a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="327a9-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="327a9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="327a9-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing SensoScientific draadloze temperatuur Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="327a9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SensoScientific Wireless Temperature Monitoring System application.</span></span>

<span data-ttu-id="327a9-150">**tooconfigure eenmalige aanmelding Azure AD met SensoScientific draadloze temperatuur Monitoring System, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="327a9-150">**tooconfigure Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, perform hello following steps:**</span></span>

1. <span data-ttu-id="327a9-151">In Azure-portal op Hallo Hallo **SensoScientific draadloze temperatuur Monitoring System** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="327a9-151">In hello Azure portal, on hello **SensoScientific Wireless Temperature Monitoring System** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="327a9-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="327a9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. <span data-ttu-id="327a9-155">Op Hallo **SensoScientific draadloze temperatuur bewaking systeemdomein en URL's** sectie geen noodzaak tooperform eventuele stappen als Hallo app al vooraf is geïntegreerd met Azure:</span><span class="sxs-lookup"><span data-stu-id="327a9-155">On hello **SensoScientific Wireless Temperature Monitoring System Domain and URLs** section, no need tooperform any steps as hello app is already pre-integrated with Azure:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. <span data-ttu-id="327a9-157">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="327a9-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. <span data-ttu-id="327a9-159">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="327a9-159">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="327a9-161">Op Hallo **SensoScientific draadloze temperatuur bewaking systeemconfiguratie** sectie, klikt u op **configureren SensoScientific draadloze temperatuur Monitoring System** tooopen  **Eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="327a9-161">On hello **SensoScientific Wireless Temperature Monitoring System Configuration** section, click **Configure SensoScientific Wireless Temperature Monitoring System** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="327a9-162">Kopiëren Hallo **Sign-Out-URL, de entiteit-ID SAML** en **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="327a9-162">Copy hello **Sign-Out URL, SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. <span data-ttu-id="327a9-164">Meld u aan op tooyour SensoScientific draadloze temperatuur bewaking systeemtoepassing als beheerder.</span><span class="sxs-lookup"><span data-stu-id="327a9-164">Sign on tooyour SensoScientific Wireless Temperature Monitoring System application as an administrator.</span></span>

8. <span data-ttu-id="327a9-165">Klik in het navigatiemenu Hallo Hallo bovenaan op **configuratie** en Ga naar **configureren** onder **eenmalige aanmelding** tooopen Hallo eenmalige aanmelding op instellingen.</span><span class="sxs-lookup"><span data-stu-id="327a9-165">In hello navigation menu on hello top, click **Configuration** and goto **Configure** under **Single Sign On** tooopen hello Single Sign On Settings.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. <span data-ttu-id="327a9-167">In **eenmalige aanmelding op instellingen** formulier Hallo stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="327a9-167">In **Single Sign On Settings** form perform hello following steps:</span></span>
 
    <span data-ttu-id="327a9-168">a.</span><span class="sxs-lookup"><span data-stu-id="327a9-168">a.</span></span> <span data-ttu-id="327a9-169">Selecteer **certificaatverlener** als Azure AD.</span><span class="sxs-lookup"><span data-stu-id="327a9-169">Select **Issuer Name** as Azure AD.</span></span>
    
    <span data-ttu-id="327a9-170">b.</span><span class="sxs-lookup"><span data-stu-id="327a9-170">b.</span></span> <span data-ttu-id="327a9-171">Plakken Hallo **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal in URL-verlener tekstvak.</span><span class="sxs-lookup"><span data-stu-id="327a9-171">Paste hello **SAML Entity ID** which you have copied from Azure portal into Issuer URL textbox.</span></span>
    
    <span data-ttu-id="327a9-172">c.</span><span class="sxs-lookup"><span data-stu-id="327a9-172">c.</span></span> <span data-ttu-id="327a9-173">Plakken Hallo **SAML Single Sign-On Service-URL** die u in één Service-URL aanmelding tekstvak vanuit Azure-portal hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="327a9-173">Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal into Single Sign-On Service URL textbox.</span></span>

    <span data-ttu-id="327a9-174">d.</span><span class="sxs-lookup"><span data-stu-id="327a9-174">d.</span></span> <span data-ttu-id="327a9-175">Plakken Hallo **Sign-Out URL** die u in het tekstvak voor de Service-URL met eenmalige Sign-Out vanuit Azure-portal hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="327a9-175">Paste hello **Sign-Out URL** which you have copied from Azure portal into Single Sign-Out Service URL textbox.</span></span>

    <span data-ttu-id="327a9-176">e.</span><span class="sxs-lookup"><span data-stu-id="327a9-176">e.</span></span> <span data-ttu-id="327a9-177">Blader Hallo-certificaat dat u hebt gedownload vanuit Azure-portal en hier uploaden.</span><span class="sxs-lookup"><span data-stu-id="327a9-177">Browse hello certificate which you have downloaded from Azure portal and upload here.</span></span>
    
    <span data-ttu-id="327a9-178">f.</span><span class="sxs-lookup"><span data-stu-id="327a9-178">f.</span></span> <span data-ttu-id="327a9-179">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="327a9-179">Click **Save**.</span></span>
  
> [!TIP]
> <span data-ttu-id="327a9-180">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="327a9-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="327a9-181">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="327a9-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="327a9-182">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="327a9-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="327a9-183">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="327a9-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="327a9-184">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="327a9-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="327a9-186">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="327a9-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="327a9-187">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="327a9-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="327a9-189">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="327a9-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="327a9-191">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="327a9-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="327a9-193">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="327a9-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="327a9-195">a.</span><span class="sxs-lookup"><span data-stu-id="327a9-195">a.</span></span> <span data-ttu-id="327a9-196">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="327a9-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="327a9-197">b.</span><span class="sxs-lookup"><span data-stu-id="327a9-197">b.</span></span> <span data-ttu-id="327a9-198">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="327a9-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="327a9-199">c.</span><span class="sxs-lookup"><span data-stu-id="327a9-199">c.</span></span> <span data-ttu-id="327a9-200">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="327a9-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="327a9-201">d.</span><span class="sxs-lookup"><span data-stu-id="327a9-201">d.</span></span> <span data-ttu-id="327a9-202">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="327a9-202">Click **Create**.</span></span>
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a><span data-ttu-id="327a9-203">Maken van een testgebruiker SensoScientific draadloze temperatuur Monitoring System</span><span class="sxs-lookup"><span data-stu-id="327a9-203">Creating a SensoScientific Wireless Temperature Monitoring System test user</span></span>

<span data-ttu-id="327a9-204">Azure AD tooenable gebruikers toolog in tooSensoScientific draadloze temperatuur Monitoring System, ze in SensoScientific draadloze temperatuur bewakingssysteem moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="327a9-204">tooenable Azure AD users toolog in tooSensoScientific Wireless Temperature Monitoring System, they must be provisioned into SensoScientific Wireless Temperature Monitoring System.</span></span> <span data-ttu-id="327a9-205">Werken met [SensoScientific draadloze temperatuur Monitoring System ondersteuningsteam](https://www.sensoscientific.com/contact-us/) Hallo gebruikers toevoegen in Hallo SensoScientific draadloze temperatuur Monitoring System platform.</span><span class="sxs-lookup"><span data-stu-id="327a9-205">Work with [SensoScientific Wireless Temperature Monitoring System support team](https://www.sensoscientific.com/contact-us/) to add hello users in hello SensoScientific Wireless Temperature Monitoring System platform.</span></span> <span data-ttu-id="327a9-206">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="327a9-206">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="327a9-207">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="327a9-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="327a9-208">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSensoScientific draadloze temperatuur Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="327a9-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSensoScientific Wireless Temperature Monitoring System.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="327a9-210">**tooassign Britta Simon tooSensoScientific draadloze temperatuur Monitoring System Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="327a9-210">**tooassign Britta Simon tooSensoScientific Wireless Temperature Monitoring System, perform hello following steps:**</span></span>

1. <span data-ttu-id="327a9-211">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="327a9-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="327a9-213">Selecteer in de lijst met de toepassingen van Hallo **SensoScientific draadloze temperatuur Monitoring System**.</span><span class="sxs-lookup"><span data-stu-id="327a9-213">In hello applications list, select **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. <span data-ttu-id="327a9-215">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="327a9-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="327a9-217">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="327a9-217">Click **Add** button.</span></span> <span data-ttu-id="327a9-218">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="327a9-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="327a9-220">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="327a9-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="327a9-221">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="327a9-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="327a9-222">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="327a9-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="327a9-223">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="327a9-223">Testing single sign-on</span></span>

<span data-ttu-id="327a9-224">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="327a9-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="327a9-225">Klik op Hallo SensoScientific draadloze temperatuur Monitoring System tegel in het deelvenster toegang hello, kunt u zich automatisch aangemelde tooyour SensoScientific draadloze temperatuur Monitoring-toepassing.</span><span class="sxs-lookup"><span data-stu-id="327a9-225">Click hello SensoScientific Wireless Temperature Monitoring System tile in hello Access Panel, you will be automatically signed-on tooyour SensoScientific Wireless Temperature Monitoring System application.</span></span> <span data-ttu-id="327a9-226">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="327a9-226">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="327a9-227">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="327a9-227">Additional resources</span></span>

* [<span data-ttu-id="327a9-228">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="327a9-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="327a9-229">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="327a9-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

