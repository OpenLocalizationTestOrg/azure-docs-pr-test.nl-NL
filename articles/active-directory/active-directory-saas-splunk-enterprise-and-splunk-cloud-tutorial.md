---
title: 'Zelfstudie: Azure Active Directory-integratie met Splunk Enterprise en Splunk Cloud | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Splunk Enterprise en Splunk Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="f1b6b-103">Zelfstudie: Azure Active Directory-integratie met Splunk Enterprise en Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="f1b6b-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="f1b6b-104">In deze zelfstudie leert u hoe toointegrate Splunk Enterprise en Splunk Cloud met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f1b6b-104">In this tutorial, you learn how toointegrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1b6b-105">Splunk Enterprise en Splunk Cloud integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f1b6b-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f1b6b-106">U kunt beheren in Azure AD die toegang heeft tooSplunk Enterprise en Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="f1b6b-106">You can control in Azure AD who has access tooSplunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="f1b6b-107">U kunt uw gebruikers tooautomatically get aangemelde tooSplunk Enterprise en Splunk Cloud eenmalige aanmelding (SSO) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="f1b6b-107">You can enable your users tooautomatically get signed-on tooSplunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1b6b-108">U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f1b6b-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="f1b6b-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f1b6b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1b6b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f1b6b-110">Prerequisites</span></span>

<span data-ttu-id="f1b6b-111">Azure AD-integratie met Splunk Enterprise en Splunk Cloud tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="f1b6b-111">tooconfigure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need hello following items:</span></span>

- <span data-ttu-id="f1b6b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f1b6b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1b6b-113">Een Splunk Enterprise of Splunk Cloud SSO ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f1b6b-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="f1b6b-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="f1b6b-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f1b6b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1b6b-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f1b6b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1b6b-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="f1b6b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f1b6b-118">Scenario description</span></span>
<span data-ttu-id="f1b6b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="f1b6b-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f1b6b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1b6b-121">Splunk Enterprise en Splunk Cloud toe te voegen uit Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f1b6b-121">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
2. <span data-ttu-id="f1b6b-122">Configureren en testen van Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="f1b6b-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a><span data-ttu-id="f1b6b-123">Splunk Enterprise en Splunk Cloud uit Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f1b6b-123">Add Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
<span data-ttu-id="f1b6b-124">tooconfigure hello integratie van Splunk Enterprise en Splunk Cloud met Azure AD, moet u tooadd Splunk Enterprise en Splunk Cloud uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-124">tooconfigure hello integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need tooadd Splunk Enterprise and Splunk Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f1b6b-125">**tooadd Splunk Enterprise en Splunk Cloud uit de galerie hello, voert Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f1b6b-125">**tooadd Splunk Enterprise and Splunk Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1b6b-126">In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="f1b6b-128">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="f1b6b-129">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Toepassingen][2]

4. <span data-ttu-id="f1b6b-131">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Toepassingen][3]

5. <span data-ttu-id="f1b6b-133">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![Toepassingen][4]

6. <span data-ttu-id="f1b6b-135">Typ in het zoekvak Hallo **Splunk Enterprise of Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-135">In hello search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="f1b6b-137">Selecteer in het deelvenster met resultaten Hallo **Splunk Enterprise en Splunk Cloud**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-137">In hello results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f1b6b-139">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1b6b-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="f1b6b-140">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Splunk voor ondernemingen en Splunk Cloud op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f1b6b-141">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Splunk Enterprise en Splunk Cloud is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Splunk Enterprise and Splunk Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="f1b6b-142">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Splunk Enterprise en Splunk Cloud toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-142">In other words, a link relationship between an Azure AD user and hello related user in Splunk Enterprise and Splunk Cloud needs toobe established.</span></span>

<span data-ttu-id="f1b6b-143">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Splunk Enterprise en Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="f1b6b-144">tooconfigure en eenmalige aanmelding Azure AD-test met Splunk Enterprise en Splunk Cloud, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f1b6b-144">tooconfigure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f1b6b-145">**[Configureren van eenmalige aanmelding Azure AD](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f1b6b-146">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1b6b-147">**[Maken van een testgebruiker Splunk Enterprise en Splunk Cloud](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave een equivalent van Britta Simon in de onderneming Splunk en Splunk Cloud die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - toohave a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="f1b6b-148">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1b6b-149">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f1b6b-150">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f1b6b-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f1b6b-151">In dit gedeelte Azure AD-eenmalige aanmelding inschakelen in de klassieke portal Hallo en eenmalige aanmelding configureren in uw toepassing Splunk Enterprise en Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-151">In this section, you enable Azure AD SSO in hello classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="f1b6b-152">**tooconfigure eenmalige aanmelding Azure AD met Splunk Enterprise en Splunk Cloud, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f1b6b-152">**tooconfigure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1b6b-153">In de klassieke portal Hallo op Hallo **Splunk Enterprise en Splunk Cloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren Single Sign-On** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-153">In hello classic portal, on hello **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Eenmalige aanmelding configureren][6] 

2. <span data-ttu-id="f1b6b-155">Op Hallo **hoe wilt u dat gebruikers toosign op tooSplunk Enterprise en Splunk Cloud** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-155">On hello **How would you like users toosign on tooSplunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="f1b6b-157">Op Hallo **App-instellingen configureren** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f1b6b-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="f1b6b-159">In Hallo **aanmelding op URL** textbox type Hallo-URL die wordt gebruikt door uw gebruikers toosign op tooyour Splunk Enterprise en Splunk cloudtoepassing met Hallo patroon volgen:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="f1b6b-159">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Splunk Enterprise and Splunk Cloud application using hello following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="f1b6b-160">In Hallo **id** textbox type Hallo-URL van uw Splunk Server.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-160">In hello **Identifier** textbox, type hello URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="f1b6b-161">In Hallo **antwoord-URL** textbox, typ de URL van de Hallo Hello patroon volgen:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="f1b6b-161">In hello **Reply URL** textbox, type hello URL with hello following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="f1b6b-162">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="f1b6b-163">Op Hallo **op Splunk Enterprise- en Splunk Cloud eenmalige aanmelding configureren** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f1b6b-163">On hello **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="f1b6b-165">Klik op **metagegevens downloaden**, en sla Hallo-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-165">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="f1b6b-166">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-166">Click **Next**.</span></span>

5. <span data-ttu-id="f1b6b-167">tooget SSO is geconfigureerd voor uw toepassing contact opnemen met Splunk Enterprise en Splunk Cloud ondersteuningsteam en voorzien Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="f1b6b-167">tooget SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with hello following:</span></span>

    * <span data-ttu-id="f1b6b-168">Hallo gedownload **federaton metagegevens**</span><span class="sxs-lookup"><span data-stu-id="f1b6b-168">hello downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="f1b6b-169">In de klassieke portal hello, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-169">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD voor eenmalige aanmelding][10]

7. <span data-ttu-id="f1b6b-171">Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-171">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD voor eenmalige aanmelding][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f1b6b-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f1b6b-173">Create an Azure AD test user</span></span>
<span data-ttu-id="f1b6b-174">In deze sectie kunt u een testgebruiker maken in de klassieke portal Hallo Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-174">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][20]

<span data-ttu-id="f1b6b-176">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f1b6b-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1b6b-177">In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-177">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="f1b6b-179">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-179">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="f1b6b-180">Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-180">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1b6b-182">Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-182">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="f1b6b-184">Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f1b6b-184">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="f1b6b-186">Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="f1b6b-187">In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-187">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="f1b6b-188">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-188">Click **Next**.</span></span>

6.  <span data-ttu-id="f1b6b-189">Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f1b6b-189">On hello **User Profile** dialog page, perform hello following steps:</span></span>
  
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="f1b6b-191">In Hallo **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-191">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="f1b6b-192">In Hallo **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-192">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="f1b6b-193">In Hallo **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-193">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="f1b6b-194">In Hallo **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-194">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="f1b6b-195">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-195">Click **Next**.</span></span>

7. <span data-ttu-id="f1b6b-196">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-196">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="f1b6b-198">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f1b6b-198">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="f1b6b-200">Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-200">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="f1b6b-201">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="f1b6b-202">Een Splunk Enterprise en Splunk Cloud testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f1b6b-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="f1b6b-203">In deze sectie maakt u een gebruiker met de naam Britta Simon in de onderneming Splunk en Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="f1b6b-204">Neem contact op met Splunk Enterprise en Splunk Cloud support team tooadd Hallo gebruikers in Hallo Splunk Enterprise en Splunk Cloud-platform.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-204">Please work with Splunk Enterprise and Splunk Cloud support team tooadd hello users in hello Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="f1b6b-205">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1b6b-205">Assign hello Azure AD test user</span></span>

<span data-ttu-id="f1b6b-206">In deze sectie maakt inschakelen u Britta Simon toouse Azure SSOy verlenen haar toegang tooSplunk Enterprise en Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-206">In this section, you enable Britta Simon toouse Azure SSOy granting her access tooSplunk Enterprise and Splunk Cloud.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f1b6b-208">**tooassign Britta Simon tooSplunk Enterprise en Splunk Cloud uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f1b6b-208">**tooassign Britta Simon tooSplunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="f1b6b-209">Klik op Hallo klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-209">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f1b6b-211">Selecteer in de lijst met de toepassingen van Hallo **Splunk Enterprise en Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-211">In hello applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="f1b6b-213">Klik in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-213">In hello menu on hello top, click **Users**.</span></span>

    ![Gebruiker toewijzen][203]

4. <span data-ttu-id="f1b6b-215">Selecteer in de lijst gebruikers Hallo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-215">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="f1b6b-216">Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-216">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Gebruiker toewijzen][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="f1b6b-218">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f1b6b-218">Test single sign-on</span></span>

<span data-ttu-id="f1b6b-219">In deze sectie kunt u uw Azure AD-SSOonfiguration Hallo Toegangsvenster met testen.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-219">In this section, you test your Azure AD SSOonfiguration using hello Access Panel.</span></span>

<span data-ttu-id="f1b6b-220">Wanneer u hello Splunk Enterprise- en Splunk Cloud-tegel in Hallo toegangsvenster klikt, krijgt u automatisch aangemelde tooyour Splunk Enterprise en Splunk Cloud-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1b6b-220">When you click hello Splunk Enterprise and Splunk Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f1b6b-221">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f1b6b-221">Additional resources</span></span>

* [<span data-ttu-id="f1b6b-222">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1b6b-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1b6b-223">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f1b6b-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
