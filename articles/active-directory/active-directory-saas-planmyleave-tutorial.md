---
title: 'Zelfstudie: Azure Active Directory-integratie met PlanMyLeave | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en PlanMyLeave.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 44a6782e44ef22fc957544960be1742f9eed6e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="3785d-103">Zelfstudie: Azure Active Directory-integratie met PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="3785d-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="3785d-104">In deze zelfstudie leert u hoe toointegrate PlanMyLeave met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3785d-104">In this tutorial, you learn how toointegrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3785d-105">PlanMyLeave integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="3785d-105">Integrating PlanMyLeave with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3785d-106">U kunt beheren in Azure AD die tooPlanMyLeave toegang heeft</span><span class="sxs-lookup"><span data-stu-id="3785d-106">You can control in Azure AD who has access tooPlanMyLeave</span></span>
- <span data-ttu-id="3785d-107">U kunt uw gebruikers tooautomatically get aangemelde tooPlanMyLeave (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="3785d-107">You can enable your users tooautomatically get signed-on tooPlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3785d-108">U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="3785d-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="3785d-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3785d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3785d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3785d-110">Prerequisites</span></span>

<span data-ttu-id="3785d-111">Azure AD-integratie met PlanMyLeave tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="3785d-111">tooconfigure Azure AD integration with PlanMyLeave, you need hello following items:</span></span>

- <span data-ttu-id="3785d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="3785d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3785d-113">Een PlanMyLeave eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="3785d-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="3785d-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3785d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="3785d-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="3785d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3785d-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="3785d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="3785d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3785d-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="3785d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="3785d-118">Scenario description</span></span>
<span data-ttu-id="3785d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="3785d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3785d-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="3785d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3785d-121">Het toevoegen van PlanMyLeave van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="3785d-121">Adding PlanMyLeave from hello gallery</span></span>
2. <span data-ttu-id="3785d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3785d-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-hello-gallery"></a><span data-ttu-id="3785d-123">Het toevoegen van PlanMyLeave van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="3785d-123">Adding PlanMyLeave from hello gallery</span></span>
<span data-ttu-id="3785d-124">tooconfigure hello integratie van PlanMyLeave in Azure AD, moet u tooadd PlanMyLeave uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="3785d-124">tooconfigure hello integration of PlanMyLeave into Azure AD, you need tooadd PlanMyLeave from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3785d-125">**tooadd PlanMyLeave via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3785d-125">**tooadd PlanMyLeave from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3785d-126">In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3785d-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3785d-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3785d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3785d-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3785d-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="3785d-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="3785d-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="3785d-133">Typ in het zoekvak Hallo **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="3785d-133">In hello search box, type **PlanMyLeave**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="3785d-135">Selecteer in het deelvenster resultaten hello, **PlanMyLeave**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3785d-135">In hello results panel, select **PlanMyLeave**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3785d-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3785d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3785d-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met PlanMyLeave op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="3785d-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3785d-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in PlanMyLeave is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3785d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PlanMyLeave is tooa user in Azure AD.</span></span> <span data-ttu-id="3785d-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in PlanMyLeave toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="3785d-140">In other words, a link relationship between an Azure AD user and hello related user in PlanMyLeave needs toobe established.</span></span>

<span data-ttu-id="3785d-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="3785d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="3785d-142">tooconfigure en eenmalige aanmelding Azure AD-test met PlanMyLeave, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3785d-142">tooconfigure and test Azure AD single sign-on with PlanMyLeave, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3785d-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="3785d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3785d-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3785d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3785d-145">**[Maken van een testgebruiker PlanMyLeave](#creating-a-planmyleave-test-user)**  -toohave een equivalent van Britta Simon in PlanMyLeave die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="3785d-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - toohave a counterpart of Britta Simon in PlanMyLeave that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="3785d-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3785d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3785d-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="3785d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3785d-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="3785d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3785d-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding in uw toepassing PlanMyLeave configureren.</span><span class="sxs-lookup"><span data-stu-id="3785d-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="3785d-150">**Azure AD tooconfigure eenmalige aanmelding met PlanMyLeave, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3785d-150">**tooconfigure Azure AD single sign-on with PlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="3785d-151">In hello Azure Management portal op Hallo **PlanMyLeave** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="3785d-151">In hello Azure Management portal, on hello **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="3785d-153">Op Hallo **eenmalige aanmelding** dialoogvenster pagina als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3785d-153">On hello **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="3785d-155">Op Hallo **PlanMyLeave domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3785d-155">On hello **PlanMyLeave Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="3785d-157">a.</span><span class="sxs-lookup"><span data-stu-id="3785d-157">a.</span></span> <span data-ttu-id="3785d-158">In Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen:`https://<company-name>.planmyleave.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="3785d-158">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="3785d-159">b.</span><span class="sxs-lookup"><span data-stu-id="3785d-159">b.</span></span> <span data-ttu-id="3785d-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="3785d-160">In hello **Identifer** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3785d-161">Houd er rekening mee dat deze niet Hallo echte waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="3785d-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="3785d-162">U hebt deze waarden Hello werkelijke Meld u aan bij de URL en de id tooupdate.</span><span class="sxs-lookup"><span data-stu-id="3785d-162">You have tooupdate these values with hello actual Sign On URL and Identifier.</span></span> <span data-ttu-id="3785d-163">Neem contact op met [PlanMyLeave ondersteuningsteam](mailto:support@planmyleave.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="3785d-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) tooget these values.</span></span>

4. <span data-ttu-id="3785d-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **nieuw certificaat maken**.</span><span class="sxs-lookup"><span data-stu-id="3785d-164">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="3785d-166">Op Hallo **nieuw certificaat maken** dialoogvenster, klikt u op Hallo agenda-pictogram en selecteer een **vervaldatum**.</span><span class="sxs-lookup"><span data-stu-id="3785d-166">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="3785d-167">Klik vervolgens op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="3785d-167">Then click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="3785d-169">Op Hallo **SAML-certificaat voor ondertekening van** sectie **nieuwe certificaat activeren** en klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="3785d-169">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="3785d-171">Op Hallo pop-upvenster **rollovercertificaat** venster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3785d-171">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3785d-173">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3785d-173">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="3785d-175">Op Hallo **PlanMyLeave configuratie** sectie, klikt u op **configureren PlanMyLeave** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="3785d-175">On hello **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** tooopen **Configure sign-on** window.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="3785d-178">Meld u aan bij uw tenant PlanMyLeave als een beheerder in een ander browservenster.</span><span class="sxs-lookup"><span data-stu-id="3785d-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="3785d-179">Ga te**Setup van System**.</span><span class="sxs-lookup"><span data-stu-id="3785d-179">Go too**System Setup**.</span></span> <span data-ttu-id="3785d-180">Klik op Hallo **beveiligingsbeheer** sectie Klik **bedrijf SAML-instellingen** .</span><span class="sxs-lookup"><span data-stu-id="3785d-180">Then on hello **Security Management** section click **Company SAML settings** .</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="3785d-182">Op Hallo **SAML instellingen** sectie, klikt u op het pictogram van de editor.</span><span class="sxs-lookup"><span data-stu-id="3785d-182">On hello **SAML Settings** section, click editor icon.</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="3785d-184">Op Hallo **SAML-Update-instellingen** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3785d-184">On hello **Update SAML Settings** section, perform hello following steps:</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="3785d-186">a.</span><span class="sxs-lookup"><span data-stu-id="3785d-186">a.</span></span>  <span data-ttu-id="3785d-187">In Hallo **aanmeldings-URL** textbox Hallo-waarde van **SAML Single Sign-On Service-URL** van het venster voor configuratie van Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3785d-187">In hello **Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="3785d-188">b.</span><span class="sxs-lookup"><span data-stu-id="3785d-188">b.</span></span>  <span data-ttu-id="3785d-189">Open uw gedownloade certificaat-bestand in Kladblok, alleen Hallo inhoud tussen Hallo---begint certificaat--- en---einde certificaat---ervan naar het Klembord kopiëren en plak deze toohello **certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="3785d-189">Open your downloaded certificate file in notepad, copy only hello content between hello ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>

    <span data-ttu-id="3785d-190">c.</span><span class="sxs-lookup"><span data-stu-id="3785d-190">c.</span></span> <span data-ttu-id="3785d-191">Instellen'**Is ingeschakeld**'te'**Ja**'.</span><span class="sxs-lookup"><span data-stu-id="3785d-191">Set "**Is Enable**" too"**Yes**".</span></span>

    <span data-ttu-id="3785d-192">d.</span><span class="sxs-lookup"><span data-stu-id="3785d-192">d.</span></span> <span data-ttu-id="3785d-193">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3785d-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3785d-194">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3785d-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="3785d-195">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3785d-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="3785d-197">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3785d-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3785d-198">In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3785d-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3785d-200">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="3785d-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3785d-202">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3785d-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3785d-204">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3785d-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3785d-206">a.</span><span class="sxs-lookup"><span data-stu-id="3785d-206">a.</span></span> <span data-ttu-id="3785d-207">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3785d-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3785d-208">b.</span><span class="sxs-lookup"><span data-stu-id="3785d-208">b.</span></span> <span data-ttu-id="3785d-209">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3785d-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3785d-210">c.</span><span class="sxs-lookup"><span data-stu-id="3785d-210">c.</span></span> <span data-ttu-id="3785d-211">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="3785d-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3785d-212">d.</span><span class="sxs-lookup"><span data-stu-id="3785d-212">d.</span></span> <span data-ttu-id="3785d-213">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3785d-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="3785d-214">Een testgebruiker PlanMyLeave maken</span><span class="sxs-lookup"><span data-stu-id="3785d-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="3785d-215">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in PlanMyLeave van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3785d-215">hello objective of this section is toocreate a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="3785d-216">PlanMyLeave ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3785d-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="3785d-217">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="3785d-217">There is no action item for you in this section.</span></span> <span data-ttu-id="3785d-218">Een nieuwe gebruiker wordt tijdens een poging tooaccess PlanMyLeave gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="3785d-218">A new user will be created during an attempt tooaccess PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="3785d-219">Als u een gebruiker toocreate handmatig nodig hebt, moet u toocontact [PlanMyLeave ondersteuningsteam](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="3785d-219">If you need toocreate an user manually, you need toocontact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3785d-220">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3785d-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3785d-221">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooPlanMyLeave toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="3785d-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPlanMyLeave.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="3785d-223">**tooassign Britta Simon tooPlanMyLeave, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="3785d-223">**tooassign Britta Simon tooPlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="3785d-224">Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3785d-224">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="3785d-226">Selecteer in de lijst met de toepassingen van Hallo **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="3785d-226">In hello applications list, select **PlanMyLeave**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="3785d-228">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="3785d-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="3785d-230">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="3785d-230">Click **Add** button.</span></span> <span data-ttu-id="3785d-231">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3785d-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="3785d-233">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="3785d-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3785d-234">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3785d-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3785d-235">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3785d-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="3785d-236">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3785d-236">Testing single sign-on</span></span>

<span data-ttu-id="3785d-237">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="3785d-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3785d-238">Als u op Hallo PlanMyLeave tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour PlanMyLeave toepassing.</span><span class="sxs-lookup"><span data-stu-id="3785d-238">When you click hello PlanMyLeave tile in hello Access Panel, you should get automatically signed-on tooyour PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="3785d-239">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3785d-239">Additional resources</span></span>

* [<span data-ttu-id="3785d-240">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3785d-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3785d-241">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3785d-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png