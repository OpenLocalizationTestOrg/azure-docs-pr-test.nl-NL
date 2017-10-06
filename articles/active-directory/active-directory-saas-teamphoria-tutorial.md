---
title: 'Zelfstudie: Azure Active Directory-integratie met Teamphoria | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Teamphoria.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="d8daf-103">Zelfstudie: Azure Active Directory-integratie met Teamphoria</span><span class="sxs-lookup"><span data-stu-id="d8daf-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="d8daf-104">In deze zelfstudie leert u hoe toointegrate Teamphoria met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d8daf-104">In this tutorial, you learn how toointegrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d8daf-105">Teamphoria integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d8daf-105">Integrating Teamphoria with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d8daf-106">U kunt beheren in Azure AD die tooTeamphoria toegang heeft</span><span class="sxs-lookup"><span data-stu-id="d8daf-106">You can control in Azure AD who has access tooTeamphoria</span></span>
- <span data-ttu-id="d8daf-107">U kunt uw gebruikers tooautomatically get aangemelde tooTeamphoria (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="d8daf-107">You can enable your users tooautomatically get signed-on tooTeamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d8daf-108">U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="d8daf-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="d8daf-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d8daf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="d8daf-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d8daf-110">Prerequisites</span></span>

<span data-ttu-id="d8daf-111">Azure AD-integratie met Teamphoria tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="d8daf-111">tooconfigure Azure AD integration with Teamphoria, you need hello following items:</span></span>

- <span data-ttu-id="d8daf-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="d8daf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d8daf-113">Een Teamphoria eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="d8daf-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d8daf-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d8daf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d8daf-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="d8daf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d8daf-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d8daf-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d8daf-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d8daf-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d8daf-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d8daf-118">Scenario description</span></span>
<span data-ttu-id="d8daf-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d8daf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d8daf-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d8daf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d8daf-121">Het toevoegen van Teamphoria van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="d8daf-121">Adding Teamphoria from hello gallery</span></span>
2. <span data-ttu-id="d8daf-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d8daf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-hello-gallery"></a><span data-ttu-id="d8daf-123">Het toevoegen van Teamphoria van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="d8daf-123">Adding Teamphoria from hello gallery</span></span>
<span data-ttu-id="d8daf-124">tooconfigure hello integratie van Teamphoria in Azure AD, moet u tooadd Teamphoria uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d8daf-124">tooconfigure hello integration of Teamphoria into Azure AD, you need tooadd Teamphoria from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d8daf-125">**tooadd Teamphoria via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d8daf-125">**tooadd Teamphoria from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8daf-126">In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d8daf-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d8daf-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d8daf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d8daf-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d8daf-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d8daf-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="d8daf-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d8daf-133">Typ in het zoekvak Hallo **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="d8daf-133">In hello search box, type **Teamphoria**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="d8daf-135">Selecteer in het deelvenster resultaten hello, **Teamphoria**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d8daf-135">In hello results panel, select **Teamphoria**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d8daf-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d8daf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d8daf-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Teamphoria op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="d8daf-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d8daf-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Teamphoria is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8daf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamphoria is tooa user in Azure AD.</span></span> <span data-ttu-id="d8daf-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Teamphoria toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="d8daf-140">In other words, a link relationship between an Azure AD user and hello related user in Teamphoria needs toobe established.</span></span>

<span data-ttu-id="d8daf-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="d8daf-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamphoria.</span></span>

<span data-ttu-id="d8daf-142">tooconfigure en eenmalige aanmelding Azure AD-test met Teamphoria, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d8daf-142">tooconfigure and test Azure AD single sign-on with Teamphoria, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d8daf-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="d8daf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d8daf-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d8daf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d8daf-145">**[Maken van een testgebruiker Teamphoria](#creating-a-teamphoria-test-user)**  -toohave een equivalent van Britta Simon in Teamphoria die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="d8daf-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - toohave a counterpart of Britta Simon in Teamphoria that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="d8daf-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d8daf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d8daf-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d8daf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d8daf-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d8daf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d8daf-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding in uw toepassing Teamphoria configureren.</span><span class="sxs-lookup"><span data-stu-id="d8daf-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="d8daf-150">**Azure AD tooconfigure eenmalige aanmelding met Teamphoria, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d8daf-150">**tooconfigure Azure AD single sign-on with Teamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8daf-151">In hello Azure Management portal op Hallo **Teamphoria** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d8daf-151">In hello Azure Management portal, on hello **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d8daf-153">Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d8daf-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="d8daf-155">Op Hallo **Teamphoria domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d8daf-155">On hello **Teamphoria Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="d8daf-157">a.</span><span class="sxs-lookup"><span data-stu-id="d8daf-157">a.</span></span> <span data-ttu-id="d8daf-158">In Hallo **aanmeldings-URL** textbox type Hallo URL met Hallo patroon volgen:`https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="d8daf-158">In hello **Sign-on URL** textbox, type hello URL using hello following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="d8daf-159">Houd er rekening mee dat deze niet Hallo echte waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="d8daf-159">Please note that these are not hello real values.</span></span> <span data-ttu-id="d8daf-160">U hebt tooupdate deze waarden Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="d8daf-160">You have tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="d8daf-161">Neem contact op met [Teamphoria Client ondersteuningsteam](https://www.teamphoria.com/) tooget Hallo aanmelding URL.</span><span class="sxs-lookup"><span data-stu-id="d8daf-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) tooget hello Sign-on URL.</span></span> 

4. <span data-ttu-id="d8daf-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla Hallo certificaat op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d8daf-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="d8daf-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d8daf-164">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d8daf-166">Op Hallo **Teamphoria configuratie** sectie, klikt u op **configureren Teamphoria** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="d8daf-166">On hello **Teamphoria Configuration** section, click **Configure Teamphoria** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d8daf-167">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="d8daf-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="d8daf-169">tooconfigure eenmalige aanmelding op **Teamphoria** side, aanmelding tooyour Teamphoria toepassing als beheerder.</span><span class="sxs-lookup"><span data-stu-id="d8daf-169">tooconfigure single sign-on on **Teamphoria** side, Login tooyour Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="d8daf-170">Ga te**BEHEERDERSINSTELLINGEN** optie in het linkerdeelvenster werkbalk Hallo en onder Hallo Hallo tabblad configureren, klikt u op **SINGLE SIGN-ON** venster tooopen Hallo SSO-configuratie.</span><span class="sxs-lookup"><span data-stu-id="d8daf-170">Go too**ADMIN SETTINGS** option in hello left toolbar and under hello hello Configure Tab click on **SINGLE SIGN-ON** tooopen hello SSO configuration window.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="d8daf-172">Klik op **IDENTITEITSPROVIDER toevoegen** optie op Hallo rechterbovenhoek tooopen Hallo formulier voor het Hallo-instellingen voor eenmalige aanmelding toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="d8daf-172">Click on **ADD NEW IDENTITY PROVIDER** option in hello top right corner tooopen hello form for adding hello settings for SSO.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="d8daf-174">Voer Hallo details in de velden Hallo beschreven onderstaande-</span><span class="sxs-lookup"><span data-stu-id="d8daf-174">Enter hello details in hello fields as described below-</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="d8daf-176">a.</span><span class="sxs-lookup"><span data-stu-id="d8daf-176">a.</span></span> <span data-ttu-id="d8daf-177">**WEERGAVENAAM** : Voer Hallo weergavenaam van de invoegtoepassing Hallo op Hallo beheerpagina.</span><span class="sxs-lookup"><span data-stu-id="d8daf-177">**DISPLAY NAME** : Enter hello display name of hello plugin on hello admin page.</span></span>

    <span data-ttu-id="d8daf-178">b.</span><span class="sxs-lookup"><span data-stu-id="d8daf-178">b.</span></span> <span data-ttu-id="d8daf-179">**NAAM van de knop** : Hallo-naam van het Hallo-tabblad dat wordt weergegeven op de aanmeldingspagina Hallo voor logboekregistratie in via eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d8daf-179">**BUTTON NAME** : hello name of hello tab which will display on hello login page for logging in via SSO.</span></span>

    <span data-ttu-id="d8daf-180">c.</span><span class="sxs-lookup"><span data-stu-id="d8daf-180">c.</span></span> <span data-ttu-id="d8daf-181">**CERTIFICAAT** : Open Hallo certificaat eerder hebt gedownload van Azure-portal in Kladblok kopie Hallo inhoud Hallo Hallo dezelfde en plakt u deze hier in Hallo vak.</span><span class="sxs-lookup"><span data-stu-id="d8daf-181">**CERTIFICATE** : Open hello Certificate downloaded earlier from hello Azure portal in notepad, copy hello contents of hello same and paste it here in hello box.</span></span>

    <span data-ttu-id="d8daf-182">d.</span><span class="sxs-lookup"><span data-stu-id="d8daf-182">d.</span></span> <span data-ttu-id="d8daf-183">**TOEGANGSPUNT** : plakken Hallo **SAML Single Sign-On Service-URL** gekopieerd eerdere formulier hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d8daf-183">**ENTRY POINT** : Paste hello **SAML Single Sign-On Service URL** copied earlier form hello Azure portal.</span></span>

    <span data-ttu-id="d8daf-184">e.</span><span class="sxs-lookup"><span data-stu-id="d8daf-184">e.</span></span> <span data-ttu-id="d8daf-185">Hallo-optie te schakelen**ON** en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d8daf-185">Switch hello option too**ON** and click on **SAVE**.</span></span> 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d8daf-186">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d8daf-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="d8daf-187">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d8daf-187">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d8daf-189">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d8daf-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8daf-190">In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d8daf-190">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d8daf-192">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d8daf-192">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d8daf-194">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d8daf-194">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d8daf-196">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d8daf-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d8daf-198">a.</span><span class="sxs-lookup"><span data-stu-id="d8daf-198">a.</span></span> <span data-ttu-id="d8daf-199">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d8daf-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d8daf-200">b.</span><span class="sxs-lookup"><span data-stu-id="d8daf-200">b.</span></span> <span data-ttu-id="d8daf-201">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d8daf-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d8daf-202">c.</span><span class="sxs-lookup"><span data-stu-id="d8daf-202">c.</span></span> <span data-ttu-id="d8daf-203">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d8daf-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d8daf-204">d.</span><span class="sxs-lookup"><span data-stu-id="d8daf-204">d.</span></span> <span data-ttu-id="d8daf-205">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d8daf-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="d8daf-206">Een testgebruiker Teamphoria maken</span><span class="sxs-lookup"><span data-stu-id="d8daf-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="d8daf-207">In de volgorde tooenable Azure AD gebruikers toolog in Teamphoria, moeten ze worden ingericht in Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="d8daf-207">In order tooenable Azure AD users toolog into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="d8daf-208">In geval van Teamphoria Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="d8daf-208">In hello case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="d8daf-209">**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**</span><span class="sxs-lookup"><span data-stu-id="d8daf-209">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8daf-210">Aanmelden tooyour Teamphoria bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="d8daf-210">Log in tooyour Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="d8daf-211">Klik op **ADMIN** instellingen op de werkbalk van Hallo links en onder Hallo **beheren** Klik op tabblad **gebruikers** tooopen Hallo beheerpagina voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d8daf-211">Click on **ADMIN** settings on hello left toolbar and under hello **MANAGE** tab Click on **USERS** tooopen hello admin page for users.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="d8daf-213">Klik op Hallo **handmatig uit te NODIGEN** optie.</span><span class="sxs-lookup"><span data-stu-id="d8daf-213">Click on hello **MANUAL INVITE** option.</span></span>

    ![Personen uitnodigen](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="d8daf-215">Uitvoeren na de actie op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="d8daf-215">On this page, perform following action.</span></span> 
    
    ![Personen uitnodigen](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="d8daf-217">a.</span><span class="sxs-lookup"><span data-stu-id="d8daf-217">a.</span></span> <span data-ttu-id="d8daf-218">In Hallo **e-MAILADRES** textbox Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d8daf-218">In hello **EMAIL ADDRESS** textbox, hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d8daf-219">b.</span><span class="sxs-lookup"><span data-stu-id="d8daf-219">b.</span></span> <span data-ttu-id="d8daf-220">In Hallo **VOORNAAM** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d8daf-220">In hello **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="d8daf-221">c.</span><span class="sxs-lookup"><span data-stu-id="d8daf-221">c.</span></span> <span data-ttu-id="d8daf-222">In Hallo **ACHTERNAAM** textbox type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d8daf-222">In hello **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="d8daf-223">d.</span><span class="sxs-lookup"><span data-stu-id="d8daf-223">d.</span></span> <span data-ttu-id="d8daf-224">Klik op **uitnodiging 1 gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="d8daf-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="d8daf-225">Gebruiker moet tooaccept Hallo uitnodiging tooget in Hallo systeem gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d8daf-225">User needs tooaccept hello invite tooget created in hello system.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d8daf-226">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8daf-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d8daf-227">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooTeamphoria toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="d8daf-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamphoria.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d8daf-229">**tooassign Britta Simon tooTeamphoria, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d8daf-229">**tooassign Britta Simon tooTeamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8daf-230">Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d8daf-230">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d8daf-232">Selecteer in de lijst met de toepassingen van Hallo **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="d8daf-232">In hello applications list, select **Teamphoria**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="d8daf-234">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d8daf-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d8daf-236">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d8daf-236">Click **Add** button.</span></span> <span data-ttu-id="d8daf-237">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d8daf-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d8daf-239">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="d8daf-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d8daf-240">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d8daf-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d8daf-241">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d8daf-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d8daf-242">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d8daf-242">Testing single sign-on</span></span>

<span data-ttu-id="d8daf-243">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="d8daf-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d8daf-244">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="d8daf-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="d8daf-245">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="d8daf-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d8daf-246">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d8daf-246">Additional resources</span></span>

* [<span data-ttu-id="d8daf-247">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8daf-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d8daf-248">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d8daf-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

