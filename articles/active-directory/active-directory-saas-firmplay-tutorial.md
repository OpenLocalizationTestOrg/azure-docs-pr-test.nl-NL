---
title: 'Zelfstudie: Azure Active Directory-integratie met FirmPlay - werknemer Advocacy voor werving | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en FirmPlay - werknemer Advocacy voor werving.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f143e0bb8f2a42de880d77e5f033694ce3f09cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="de4e1-103">Zelfstudie: Azure Active Directory-integratie met FirmPlay - werknemer Advocacy voor werving</span><span class="sxs-lookup"><span data-stu-id="de4e1-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="de4e1-104">In deze zelfstudie leert u hoe toointegrate FirmPlay - werknemer Advocacy voor werving met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="de4e1-104">In this tutorial, you learn how toointegrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="de4e1-105">Integratie van FirmPlay - werknemer Advocacy voor werving met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="de4e1-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="de4e1-106">U kunt beheren in Azure AD wie toegang tot tooFirmPlay - werknemer Advocacy voor werving heeft</span><span class="sxs-lookup"><span data-stu-id="de4e1-106">You can control in Azure AD who has access tooFirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="de4e1-107">U kunt uw gebruikers tooautomatically get aangemelde tooFirmPlay - werknemer Advocacy voor werving (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="de4e1-107">You can enable your users tooautomatically get signed-on tooFirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="de4e1-108">U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="de4e1-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="de4e1-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="de4e1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de4e1-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="de4e1-110">Prerequisites</span></span>

<span data-ttu-id="de4e1-111">tooconfigure Azure AD-integratie met FirmPlay - werknemer Advocacy voor werving, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="de4e1-111">tooconfigure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need hello following items:</span></span>

- <span data-ttu-id="de4e1-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="de4e1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="de4e1-113">Een FirmPlay - werknemer Advocacy voor het werven van eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="de4e1-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="de4e1-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="de4e1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="de4e1-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="de4e1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="de4e1-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="de4e1-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="de4e1-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="de4e1-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="de4e1-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="de4e1-118">Scenario description</span></span>
<span data-ttu-id="de4e1-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="de4e1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="de4e1-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="de4e1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="de4e1-121">FirmPlay - werknemer Advocacy voor werving uit Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="de4e1-121">Adding FirmPlay - Employee Advocacy for Recruiting from hello gallery</span></span>
2. <span data-ttu-id="de4e1-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="de4e1-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-hello-gallery"></a><span data-ttu-id="de4e1-123">FirmPlay - werknemer Advocacy voor werving uit Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="de4e1-123">Adding FirmPlay - Employee Advocacy for Recruiting from hello gallery</span></span>
<span data-ttu-id="de4e1-124">tooconfigure hello integratie van FirmPlay - werknemer Advocacy voor werving in Azure AD, moet u tooadd FirmPlay - werknemer Advocacy voor werving uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="de4e1-124">tooconfigure hello integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need tooadd FirmPlay - Employee Advocacy for Recruiting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="de4e1-125">**tooadd FirmPlay - werknemer Advocacy voor werving via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="de4e1-125">**tooadd FirmPlay - Employee Advocacy for Recruiting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="de4e1-126">In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="de4e1-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="de4e1-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="de4e1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="de4e1-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="de4e1-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="de4e1-131">Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="de4e1-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="de4e1-133">Typ in het zoekvak Hallo **FirmPlay - werknemer Advocacy voor werving**.</span><span class="sxs-lookup"><span data-stu-id="de4e1-133">In hello search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="de4e1-135">Selecteer in het deelvenster resultaten hello, **FirmPlay - werknemer Advocacy voor werving**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="de4e1-135">In hello results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="de4e1-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="de4e1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="de4e1-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met FirmPlay - werknemer Advocacy voor werving op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="de4e1-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="de4e1-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in FirmPlay - werknemer Advocacy voor werving is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de4e1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FirmPlay - Employee Advocacy for Recruiting is tooa user in Azure AD.</span></span> <span data-ttu-id="de4e1-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in FirmPlay - werknemer Advocacy voor werving toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="de4e1-140">In other words, a link relationship between an Azure AD user and hello related user in FirmPlay - Employee Advocacy for Recruiting needs toobe established.</span></span>

<span data-ttu-id="de4e1-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in FirmPlay - werknemer Advocacy voor werving.</span><span class="sxs-lookup"><span data-stu-id="de4e1-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="de4e1-142">tooconfigure en eenmalige aanmelding Azure AD-test met FirmPlay - werknemer Advocacy voor werving, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="de4e1-142">tooconfigure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="de4e1-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="de4e1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="de4e1-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="de4e1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="de4e1-145">**[Maken van een FirmPlay - werknemer Advocacy voor de testgebruiker werving](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**  -toohave een equivalent van Britta Simon in FirmPlay: werknemer Advocacy voor het werven van die toohello Azure AD-weergave van haar gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="de4e1-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - toohave a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="de4e1-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="de4e1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="de4e1-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="de4e1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="de4e1-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="de4e1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="de4e1-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding in uw FirmPlay - werknemer Advocacy voor werving toepassing configureren.</span><span class="sxs-lookup"><span data-stu-id="de4e1-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="de4e1-150">**tooconfigure eenmalige aanmelding Azure AD met FirmPlay - werknemer Advocacy voor werving, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="de4e1-150">**tooconfigure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform hello following steps:**</span></span>

1. <span data-ttu-id="de4e1-151">In hello Azure Management portal op Hallo **FirmPlay - werknemer Advocacy voor werving** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="de4e1-151">In hello Azure Management portal, on hello **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="de4e1-153">Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="de4e1-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="de4e1-155">Op Hallo **FirmPlay - werknemer Advocacy voor het werven van domein en de URL's** sectie in Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen:`https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="de4e1-155">On hello **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="de4e1-157">Houd er rekening mee dat dit geen Hallo echte waarde is.</span><span class="sxs-lookup"><span data-stu-id="de4e1-157">Please note that this is not hello real value.</span></span> <span data-ttu-id="de4e1-158">U hebt deze waarde Hello werkelijke aanmelden URL tooupdate.</span><span class="sxs-lookup"><span data-stu-id="de4e1-158">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="de4e1-159">Neem contact op met [FirmPlay - werknemer Advocacy voor werving ondersteuningsteam](mailto:engineering@firmplay.com) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="de4e1-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) tooget this value.</span></span> 

4. <span data-ttu-id="de4e1-160">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **nieuw certificaat maken**.</span><span class="sxs-lookup"><span data-stu-id="de4e1-160">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="de4e1-162">Op Hallo **nieuw certificaat maken** dialoogvenster, klikt u op Hallo agenda-pictogram en selecteer een **vervaldatum**.</span><span class="sxs-lookup"><span data-stu-id="de4e1-162">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="de4e1-163">Klik vervolgens op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="de4e1-163">Then click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="de4e1-165">Op Hallo **SAML-certificaat voor ondertekening van** sectie **nieuwe certificaat activeren** en klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="de4e1-165">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="de4e1-167">Op Hallo pop-upvenster **rollovercertificaat** venster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="de4e1-167">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="de4e1-169">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="de4e1-169">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="de4e1-171">Op Hallo **FirmPlay - werknemer Advocacy voor configuratie werven** sectie, klikt u op **configureren FirmPlay - werknemer Advocacy voor werving** tooopen **configureren aanmelding**dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="de4e1-171">On hello **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** tooopen **Configure sign-on** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="de4e1-174">tooget SSO geconfigureerd voor uw toepassing, neem contact op met [FirmPlay - werknemer Advocacy voor werving ondersteuningsteam](mailto:engineering@firmplay.com) en voorzien Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="de4e1-174">tooget SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with hello following:</span></span> 

    <span data-ttu-id="de4e1-175">• Hallo gedownload **certificaatbestand**</span><span class="sxs-lookup"><span data-stu-id="de4e1-175">•  hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="de4e1-176">• Hallo **SAML Single Sign-On Service-URL**</span><span class="sxs-lookup"><span data-stu-id="de4e1-176">•  hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="de4e1-177">• Hallo **SAML entiteit-ID**</span><span class="sxs-lookup"><span data-stu-id="de4e1-177">•  hello **SAML Entity ID**</span></span>

    <span data-ttu-id="de4e1-178">• Hallo **Sign-Out URL**</span><span class="sxs-lookup"><span data-stu-id="de4e1-178">•  hello **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="de4e1-179">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="de4e1-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="de4e1-180">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="de4e1-180">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="de4e1-182">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="de4e1-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="de4e1-183">In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="de4e1-183">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="de4e1-185">Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="de4e1-185">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="de4e1-187">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="de4e1-187">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="de4e1-189">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="de4e1-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="de4e1-191">a.</span><span class="sxs-lookup"><span data-stu-id="de4e1-191">a.</span></span> <span data-ttu-id="de4e1-192">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="de4e1-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="de4e1-193">b.</span><span class="sxs-lookup"><span data-stu-id="de4e1-193">b.</span></span> <span data-ttu-id="de4e1-194">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="de4e1-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="de4e1-195">c.</span><span class="sxs-lookup"><span data-stu-id="de4e1-195">c.</span></span> <span data-ttu-id="de4e1-196">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="de4e1-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="de4e1-197">d.</span><span class="sxs-lookup"><span data-stu-id="de4e1-197">d.</span></span> <span data-ttu-id="de4e1-198">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="de4e1-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="de4e1-199">Maken van een FirmPlay - werknemer Advocacy voor werving testgebruiker</span><span class="sxs-lookup"><span data-stu-id="de4e1-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="de4e1-200">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in FirmPlay - werknemer Advocacy voor werving maken.</span><span class="sxs-lookup"><span data-stu-id="de4e1-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="de4e1-201">Neem contact op met [FirmPlay - werknemer Advocacy voor werving ondersteuningsteam](mailto:engineering@firmplay.com) tooadd Hallo gebruikers in Hallo FirmPlay - werknemer Advocacy voor werving platform.</span><span class="sxs-lookup"><span data-stu-id="de4e1-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) tooadd hello users in hello FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="de4e1-202">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="de4e1-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="de4e1-203">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar toegang tooFirmPlay - werknemer Advocacy voor werving verlenen.</span><span class="sxs-lookup"><span data-stu-id="de4e1-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFirmPlay - Employee Advocacy for Recruiting.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="de4e1-205">**tooassign Britta Simon tooFirmPlay - werknemer Advocacy voor werving, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="de4e1-205">**tooassign Britta Simon tooFirmPlay - Employee Advocacy for Recruiting, perform hello following steps:**</span></span>

1. <span data-ttu-id="de4e1-206">Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="de4e1-206">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="de4e1-208">Selecteer in de lijst met de toepassingen van Hallo **FirmPlay - werknemer Advocacy voor werving**.</span><span class="sxs-lookup"><span data-stu-id="de4e1-208">In hello applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="de4e1-210">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="de4e1-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="de4e1-212">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="de4e1-212">Click **Add** button.</span></span> <span data-ttu-id="de4e1-213">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="de4e1-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="de4e1-215">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="de4e1-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="de4e1-216">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="de4e1-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="de4e1-217">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="de4e1-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="de4e1-218">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="de4e1-218">Testing single sign-on</span></span>

<span data-ttu-id="de4e1-219">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="de4e1-219">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="de4e1-220">Wanneer u klikt op Hallo FirmPlay - werknemer Advocacy werving tegel in Hallo paneel voor Apptoegang, krijgt u automatisch aangemelde tooyour FirmPlay - werknemer Advocacy voor werving toepassing.</span><span class="sxs-lookup"><span data-stu-id="de4e1-220">When you click hello FirmPlay - Employee Advocacy for Recruiting tile in hello Access Panel, you should get automatically signed-on tooyour FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="de4e1-221">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="de4e1-221">Additional resources</span></span>

* [<span data-ttu-id="de4e1-222">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="de4e1-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="de4e1-223">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="de4e1-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png