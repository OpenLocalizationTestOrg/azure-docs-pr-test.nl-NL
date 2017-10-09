---
title: 'Zelfstudie: Azure Active Directory-integratie met Soonr werkplek | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Soonr werkplek.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="b9f1c-103">Zelfstudie: Azure Active Directory-integratie met Soonr werkplek</span><span class="sxs-lookup"><span data-stu-id="b9f1c-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="b9f1c-104">Hallo-doel van deze zelfstudie is tooshow u hoe toointegrate Soonr werkplek met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9f1c-104">hello objective of this tutorial is tooshow you how toointegrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="b9f1c-105">Soonr werkplek integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b9f1c-105">Integrating Soonr Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b9f1c-106">U kunt beheren in Azure AD wie toegang tot tooSoonr werkplek heeft</span><span class="sxs-lookup"><span data-stu-id="b9f1c-106">You can control in Azure AD who has access tooSoonr Workplace</span></span>
- <span data-ttu-id="b9f1c-107">U kunt uw gebruikers tooautomatically get aangemelde tooSoonr werkplek (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="b9f1c-107">You can enable your users tooautomatically get signed-on tooSoonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b9f1c-108">U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b9f1c-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="b9f1c-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b9f1c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9f1c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b9f1c-110">Prerequisites</span></span>

<span data-ttu-id="b9f1c-111">Azure AD-integratie met Soonr werkplek tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="b9f1c-111">tooconfigure Azure AD integration with Soonr Workplace, you need hello following items:</span></span>

- <span data-ttu-id="b9f1c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b9f1c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9f1c-113">Een Soonr werkplek eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b9f1c-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="b9f1c-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="b9f1c-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b9f1c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9f1c-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b9f1c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9f1c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="b9f1c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b9f1c-118">Scenario description</span></span>
<span data-ttu-id="b9f1c-119">Hallo-doel van deze zelfstudie is tooenable u tootest Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="b9f1c-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b9f1c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9f1c-121">Het toevoegen van Soonr werkplek van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="b9f1c-121">Adding Soonr Workplace from hello gallery</span></span>
2. <span data-ttu-id="b9f1c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b9f1c-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-hello-gallery"></a><span data-ttu-id="b9f1c-123">Het toevoegen van Soonr werkplek van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="b9f1c-123">Adding Soonr Workplace from hello gallery</span></span>
<span data-ttu-id="b9f1c-124">tooconfigure hello integratie van Soonr werkplek in Azure AD, moet u tooadd Soonr werkplek uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-124">tooconfigure hello integration of Soonr Workplace into Azure AD, you need tooadd Soonr Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b9f1c-125">**tooadd Soonr werkplek via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b9f1c-125">**tooadd Soonr Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9f1c-126">In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b9f1c-128">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="b9f1c-129">tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Toepassingen][2]

4. <span data-ttu-id="b9f1c-131">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Toepassingen][3]

5. <span data-ttu-id="b9f1c-133">Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
 
    ![Toepassingen][4]

6. <span data-ttu-id="b9f1c-135">Typ in het zoekvak Hallo **Soonr werkplek**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-135">In hello search box, type **Soonr Workplace**.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="b9f1c-137">Selecteer in het deelvenster met resultaten Hallo **Soonr werkplek**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-137">In hello results pane, select **Soonr Workplace**, and then click **Complete** tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b9f1c-139">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b9f1c-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b9f1c-140">Hallo-doel van deze sectie is tooshow u hoe tooconfigure en test eenmalige aanmelding Azure AD bij Soonr werkplek op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b9f1c-141">Voor één aanmelding toowork moet Azure AD tooknow welke gebruiker Hallo equivalent in Soonr werkplek tooan gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Soonr Workplace tooan user in Azure AD is.</span></span> <span data-ttu-id="b9f1c-142">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Soonr werkplek toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-142">In other words, a link relationship between an Azure AD user and hello related user in Soonr Workplace needs toobe established.</span></span>  

<span data-ttu-id="b9f1c-143">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Soonr werkplek.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="b9f1c-144">tooconfigure en test eenmalige aanmelding Azure AD bij Soonr werkplek, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b9f1c-144">tooconfigure and test Azure AD single sign-on with Soonr Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b9f1c-145">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b9f1c-146">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9f1c-147">**[Maken van een testgebruiker Soonr werkplek](#creating-a-soonr-workplace-test-user)**  -toohave een equivalent van Britta Simon in Soonr werkplek die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - toohave a counterpart of Britta Simon in Soonr Workplace that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="b9f1c-148">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9f1c-149">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b9f1c-150">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b9f1c-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b9f1c-151">In deze sectie Azure AD eenmalige aanmelding in de klassieke portal Hallo inschakelen en configureren van eenmalige aanmelding in uw toepassing Soonr werkplek.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="b9f1c-152">**Voer tooconfigure Azure AD eenmalige aanmelding bij Soonr werkplek, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b9f1c-152">**tooconfigure Azure AD single sign-on with Soonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9f1c-153">In de klassieke Azure-portal op Hallo Hallo **Soonr werkplek** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren Single Sign-On**  het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-153">In hello Azure classic portal, on hello **Soonr Workplace** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>

    ![Eenmalige aanmelding configureren][6] 

2. <span data-ttu-id="b9f1c-155">Op Hallo **wilt u hoe gebruikers toosign op tooSoonr werkplek** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-155">On hello **How would you like users toosign on tooSoonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="b9f1c-157">Op Hallo **App-instellingen configureren** dialoogvenster pagina, voert u Hallo volgende stappen uit:.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-157">On hello **Configure App Settings** dialog page, perform hello following steps:.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="b9f1c-159">a.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-159">a.</span></span> <span data-ttu-id="b9f1c-160">In Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-160">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="b9f1c-161">b.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-161">b.</span></span> <span data-ttu-id="b9f1c-162">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b9f1c-163">Houd er rekening mee dat dit geen Hallo echte waarde is.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-163">Please note that this is not hello real value.</span></span> <span data-ttu-id="b9f1c-164">U hebt deze waarde Hello werkelijke aanmelden URL tooupdate.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-164">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="b9f1c-165">Neem contact op met de werkplek Soonr support team tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-165">Contact Soonr Workplace support team tooget this value.</span></span>

4. <span data-ttu-id="b9f1c-166">Op Hallo **eenmalige aanmelding configureren op de werkplek Soonr** pagina, klikt u op **metagegevens downloaden** en sla Hallo-bestand op uw computer:</span><span class="sxs-lookup"><span data-stu-id="b9f1c-166">On hello **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save hello file on your computer:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="b9f1c-168">tooget SSO is geconfigureerd voor uw toepassing, neem contact op met het ondersteuningsteam Soonr werkplek en voorzien Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="b9f1c-168">tooget SSO configured for your application, contact your Soonr Workplace support team and provide them with hello following:</span></span> 

    <span data-ttu-id="b9f1c-169">• Hallo gedownload **metagegevens** bestand</span><span class="sxs-lookup"><span data-stu-id="b9f1c-169">•  hello downloaded **Metadata** file</span></span>

    <span data-ttu-id="b9f1c-170">• Hallo **URL-verlener**</span><span class="sxs-lookup"><span data-stu-id="b9f1c-170">•  hello **Issuer URL**</span></span>

    <span data-ttu-id="b9f1c-171">• Hallo **SAML-URL voor eenmalige aanmelding**</span><span class="sxs-lookup"><span data-stu-id="b9f1c-171">•  hello **SAML SSO URL**</span></span>

    <span data-ttu-id="b9f1c-172">• Hallo **Service-URL met eenmalige Sign-Out**</span><span class="sxs-lookup"><span data-stu-id="b9f1c-172">•  hello **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="b9f1c-173">Deze toepassing wordt vervangen door <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask werkplek</a> en u kunt verwijzen <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">dit</a> zelfstudie voor het configureren van de toepassing hello met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring hello application with Azure AD.</span></span>
   
6. <span data-ttu-id="b9f1c-174">In de klassieke Azure-portal hello, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-174">In hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Azure AD voor eenmalige aanmelding][10]

7. <span data-ttu-id="b9f1c-176">Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-176">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Azure AD voor eenmalige aanmelding][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b9f1c-178">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b9f1c-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="b9f1c-179">Hallo-doel van deze sectie is toocreate een testgebruiker in Hallo klassieke Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-179">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Azure AD-gebruiker maken][20]

<span data-ttu-id="b9f1c-181">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b9f1c-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9f1c-182">In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-182">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="b9f1c-184">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-184">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="b9f1c-185">Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-185">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b9f1c-187">Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-187">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="b9f1c-189">Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b9f1c-189">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="b9f1c-191">a.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-191">a.</span></span> <span data-ttu-id="b9f1c-192">Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="b9f1c-193">b.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-193">b.</span></span> <span data-ttu-id="b9f1c-194">In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-194">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9f1c-195">c.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-195">c.</span></span> <span data-ttu-id="b9f1c-196">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-196">Click **Next**.</span></span>

6.  <span data-ttu-id="b9f1c-197">Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b9f1c-197">On hello **User Profile** dialog page, perform hello following steps:</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="b9f1c-199">a.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-199">a.</span></span> <span data-ttu-id="b9f1c-200">In Hallo **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-200">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="b9f1c-201">b.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-201">b.</span></span> <span data-ttu-id="b9f1c-202">In Hallo **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-202">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="b9f1c-203">c.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-203">c.</span></span> <span data-ttu-id="b9f1c-204">In Hallo **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-204">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="b9f1c-205">d.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-205">d.</span></span> <span data-ttu-id="b9f1c-206">In Hallo **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-206">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="b9f1c-207">e.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-207">e.</span></span> <span data-ttu-id="b9f1c-208">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-208">Click **Next**.</span></span>

7. <span data-ttu-id="b9f1c-209">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-209">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="b9f1c-211">Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b9f1c-211">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="b9f1c-213">a.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-213">a.</span></span> <span data-ttu-id="b9f1c-214">Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-214">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="b9f1c-215">b.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-215">b.</span></span> <span data-ttu-id="b9f1c-216">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="b9f1c-217">Maken van een testgebruiker Soonr werkplek</span><span class="sxs-lookup"><span data-stu-id="b9f1c-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="b9f1c-218">Hallo-doel van deze sectie is toocreate een gebruiker Britta Simon aangeroepen in Soonr werkplek.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-218">hello objective of this section is toocreate a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="b9f1c-219">Neem contact op met de werkplek Soonr support team toocreate een gebruiker in het Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-219">Please work with Soonr Workplace support team toocreate a user in hello platform.</span></span> <span data-ttu-id="b9f1c-220">U kunt verhogen Hallo ondersteuningsticket met Soonr van <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">hier</a>.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-220">You can raise hello support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b9f1c-221">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9f1c-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b9f1c-222">Hallo-doel van deze sectie is tooenabling Britta Simon toouse Azure eenmalige aanmelding haar toegang tooSoonr werkplek verleent.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-222">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSoonr Workplace.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b9f1c-224">**tooassign Britta Simon tooSoonr werkplek, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b9f1c-224">**tooassign Britta Simon tooSoonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9f1c-225">Klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, klik op Hallo Azure **toepassingen** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-225">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b9f1c-227">Selecteer in de lijst met de toepassingen van Hallo **Soonr werkplek**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-227">In hello applications list, select **Soonr Workplace**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="b9f1c-229">Klik in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-229">In hello menu on hello top, click **Users**.</span></span>

    ![Gebruiker toewijzen][203] 

1. <span data-ttu-id="b9f1c-231">Selecteer in de lijst gebruikers Hallo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-231">In hello Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="b9f1c-232">Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-232">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Gebruiker toewijzen][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="b9f1c-234">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b9f1c-234">Testing single sign-on</span></span>

<span data-ttu-id="b9f1c-235">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="b9f1c-236">Als u op Hallo Soonr werkplek-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Soonr werkplek toepassing.</span><span class="sxs-lookup"><span data-stu-id="b9f1c-236">When you click hello Soonr Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b9f1c-237">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b9f1c-237">Additional resources</span></span>

* [<span data-ttu-id="b9f1c-238">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9f1c-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9f1c-239">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b9f1c-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
