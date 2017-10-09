---
title: 'Zelfstudie: Azure Active Directory-integratie met PagerDuty | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en PagerDuty.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c3cfbedac3bf075e2d8cd833d5de7ca0bc9468b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="b0ac6-103">Zelfstudie: Azure Active Directory-integratie met PagerDuty</span><span class="sxs-lookup"><span data-stu-id="b0ac6-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="b0ac6-104">In deze zelfstudie leert u hoe toointegrate PagerDuty met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b0ac6-104">In this tutorial, you learn how toointegrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b0ac6-105">PagerDuty integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b0ac6-105">Integrating PagerDuty with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b0ac6-106">U kunt beheren in Azure AD die tooPagerDuty toegang heeft</span><span class="sxs-lookup"><span data-stu-id="b0ac6-106">You can control in Azure AD who has access tooPagerDuty</span></span>
- <span data-ttu-id="b0ac6-107">U kunt uw gebruikers tooautomatically get aangemelde tooPagerDuty (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="b0ac6-107">You can enable your users tooautomatically get signed-on tooPagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b0ac6-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b0ac6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b0ac6-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b0ac6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0ac6-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b0ac6-110">Prerequisites</span></span>

<span data-ttu-id="b0ac6-111">Azure AD-integratie met PagerDuty tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="b0ac6-111">tooconfigure Azure AD integration with PagerDuty, you need hello following items:</span></span>

- <span data-ttu-id="b0ac6-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b0ac6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b0ac6-113">Een PagerDuty eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b0ac6-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b0ac6-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b0ac6-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b0ac6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b0ac6-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b0ac6-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b0ac6-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b0ac6-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b0ac6-118">Scenario description</span></span>
<span data-ttu-id="b0ac6-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b0ac6-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b0ac6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b0ac6-121">Het toevoegen van PagerDuty van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="b0ac6-121">Adding PagerDuty from hello gallery</span></span>
2. <span data-ttu-id="b0ac6-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b0ac6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-hello-gallery"></a><span data-ttu-id="b0ac6-123">Het toevoegen van PagerDuty van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="b0ac6-123">Adding PagerDuty from hello gallery</span></span>
<span data-ttu-id="b0ac6-124">tooconfigure hello integratie van PagerDuty in Azure AD, moet u tooadd PagerDuty uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-124">tooconfigure hello integration of PagerDuty into Azure AD, you need tooadd PagerDuty from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b0ac6-125">**tooadd PagerDuty via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b0ac6-125">**tooadd PagerDuty from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0ac6-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="b0ac6-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b0ac6-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="b0ac6-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="b0ac6-133">Typ in het zoekvak Hallo **PagerDuty**, selecteer **PagerDuty** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-133">In hello search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b0ac6-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0ac6-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b0ac6-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met PagerDuty op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b0ac6-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in PagerDuty is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PagerDuty is tooa user in Azure AD.</span></span> <span data-ttu-id="b0ac6-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in PagerDuty toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-138">In other words, a link relationship between an Azure AD user and hello related user in PagerDuty needs toobe established.</span></span>

<span data-ttu-id="b0ac6-139">Wijs in PagerDuty, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-139">In PagerDuty, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b0ac6-140">tooconfigure en eenmalige aanmelding Azure AD-test met PagerDuty, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b0ac6-140">tooconfigure and test Azure AD single sign-on with PagerDuty, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b0ac6-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b0ac6-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b0ac6-143">**[Maak een testgebruiker PagerDuty](#create-a-pagerduty-test-user)**  -toohave een equivalent van Britta Simon in PagerDuty die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - toohave a counterpart of Britta Simon in PagerDuty that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b0ac6-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b0ac6-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b0ac6-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b0ac6-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b0ac6-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing PagerDuty configureren.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="b0ac6-148">**Azure AD tooconfigure eenmalige aanmelding met PagerDuty, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b0ac6-148">**tooconfigure Azure AD single sign-on with PagerDuty, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0ac6-149">In de Azure-portal op Hallo Hallo **PagerDuty** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-149">In hello Azure portal, on hello **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b0ac6-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. <span data-ttu-id="b0ac6-153">Op Hallo **PagerDuty domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b0ac6-153">On hello **PagerDuty Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en PagerDuty domein eenmalige aanmelding informatie](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="b0ac6-155">a.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-155">a.</span></span> <span data-ttu-id="b0ac6-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="b0ac6-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="b0ac6-157">b.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-157">b.</span></span> <span data-ttu-id="b0ac6-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="b0ac6-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b0ac6-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-159">These values are not real.</span></span> <span data-ttu-id="b0ac6-160">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b0ac6-161">Neem contact op met [PagerDuty Client ondersteuningsteam](https://www.pagerduty.com/support/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) tooget these values.</span></span> 

4. <span data-ttu-id="b0ac6-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. <span data-ttu-id="b0ac6-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b0ac6-166">Op Hallo **PagerDuty configuratie** sectie, klikt u op **configureren PagerDuty** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-166">On hello **PagerDuty Configuration** section, click **Configure PagerDuty** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b0ac6-167">Kopiëren Hallo **Sign-Out URL's en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="b0ac6-167">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![PagerDuty configuratie](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. <span data-ttu-id="b0ac6-169">In een ander browservenster, meld u bij uw bedrijf Pagerduty site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

8. <span data-ttu-id="b0ac6-170">Klik in het menu bovenaan Hallo Hallo **Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-170">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="b0ac6-171">![Instellingen account](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Accountinstellingen")</span><span class="sxs-lookup"><span data-stu-id="b0ac6-171">![Account Settings](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

9. <span data-ttu-id="b0ac6-172">Klik op **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-172">Click **Single Sign-on**.</span></span>
   
    <span data-ttu-id="b0ac6-173">![Eenmalige aanmelding](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="b0ac6-173">![Single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

10. <span data-ttu-id="b0ac6-174">Op Hallo **Schakel eenmalige aanmelding (SSO)** pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b0ac6-174">On hello **Enable Single Sign-on (SSO)** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="b0ac6-175">![Eenmalige aanmelding inschakelen](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "eenmalige aanmelding inschakelen")</span><span class="sxs-lookup"><span data-stu-id="b0ac6-175">![Enable single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>
   
    <span data-ttu-id="b0ac6-176">a.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-176">a.</span></span> <span data-ttu-id="b0ac6-177">Open uw base-64 gecodeerde certificaat gedownload vanuit Azure-portal in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **X.509-certificaat** tekstvak</span><span class="sxs-lookup"><span data-stu-id="b0ac6-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="b0ac6-178">b.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-178">b.</span></span> <span data-ttu-id="b0ac6-179">In Hallo **aanmeldings-URL** textbox plakken **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-179">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="b0ac6-180">c.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-180">c.</span></span> <span data-ttu-id="b0ac6-181">In Hallo **afmelding URL** textbox plakken **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-181">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="b0ac6-182">d.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-182">d.</span></span> <span data-ttu-id="b0ac6-183">Selecteer **Single Sign-on inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-183">Select **Turn on Single Sign-on**.</span></span>
 
    <span data-ttu-id="b0ac6-184">e.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-184">e.</span></span> <span data-ttu-id="b0ac6-185">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-185">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="b0ac6-186">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b0ac6-187">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b0ac6-188">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b0ac6-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b0ac6-189">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b0ac6-189">Create an Azure AD test user</span></span>

<span data-ttu-id="b0ac6-190">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="b0ac6-192">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b0ac6-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0ac6-193">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b0ac6-195">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b0ac6-197">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b0ac6-199">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b0ac6-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b0ac6-201">a.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-201">a.</span></span> <span data-ttu-id="b0ac6-202">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b0ac6-203">b.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-203">b.</span></span> <span data-ttu-id="b0ac6-204">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b0ac6-205">c.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-205">c.</span></span> <span data-ttu-id="b0ac6-206">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b0ac6-207">d.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-207">d.</span></span> <span data-ttu-id="b0ac6-208">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-208">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="b0ac6-209">Een testgebruiker PagerDuty maken</span><span class="sxs-lookup"><span data-stu-id="b0ac6-209">Create a PagerDuty test user</span></span>

<span data-ttu-id="b0ac6-210">Azure AD tooenable gebruikers toolog in tooPagerDuty, ze in PagerDuty moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-210">tooenable Azure AD users toolog in tooPagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="b0ac6-211">In geval van PagerDuty Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-211">In hello case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="b0ac6-212">U kunt andere Pagerduty gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Pagerduty tooprovision Azure Active Directory-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-212">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty tooprovision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="b0ac6-213">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b0ac6-213">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0ac6-214">Meld u bij tooyour **Pagerduty** tenant.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-214">Log in tooyour **Pagerduty** tenant.</span></span>

2. <span data-ttu-id="b0ac6-215">Klik in het menu bovenaan Hallo Hallo **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-215">In hello menu on hello top, click **Users**.</span></span>

3. <span data-ttu-id="b0ac6-216">Klik op **gebruikers toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-216">Click **Add Users**.</span></span>
   
    <span data-ttu-id="b0ac6-217">![Gebruikers toevoegen](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "gebruikers toevoegen")</span><span class="sxs-lookup"><span data-stu-id="b0ac6-217">![Add Users](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Add Users")</span></span>

4.  <span data-ttu-id="b0ac6-218">Op Hallo **uitnodigen van uw team** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="b0ac6-218">On hello **Invite your team** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="b0ac6-219">![Uw team uitnodigen](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "uitnodigen van uw team")</span><span class="sxs-lookup"><span data-stu-id="b0ac6-219">![Invite your team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="b0ac6-220">a.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-220">a.</span></span> <span data-ttu-id="b0ac6-221">Type Hallo **eerste en laatste naam** van gebruiker zoals **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-221">Type hello **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="b0ac6-222">b.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-222">b.</span></span> <span data-ttu-id="b0ac6-223">Voer **e** adres van de gebruiker, zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="b0ac6-223">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="b0ac6-224">c.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-224">c.</span></span> <span data-ttu-id="b0ac6-225">Klik op **toevoegen**, en klik vervolgens op **verzenden nodigt**.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-225">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="b0ac6-226">Alle toegevoegde gebruikers ontvangen een uitnodiging toocreate een PagerDuty-account.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-226">All added users will receive an invite toocreate a PagerDuty account.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b0ac6-227">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0ac6-227">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b0ac6-228">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooPagerDuty toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPagerDuty.</span></span>

![Hallo-gebruikersrollen toewijzen][200]

<span data-ttu-id="b0ac6-230">**tooassign Britta Simon tooPagerDuty, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b0ac6-230">**tooassign Britta Simon tooPagerDuty, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0ac6-231">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b0ac6-233">Selecteer in de lijst met de toepassingen van Hallo **PagerDuty**.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-233">In hello applications list, select **PagerDuty**.</span></span>

    ![Hallo PagerDuty koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. <span data-ttu-id="b0ac6-235">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="b0ac6-237">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-237">Click **Add** button.</span></span> <span data-ttu-id="b0ac6-238">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="b0ac6-240">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b0ac6-241">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b0ac6-242">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b0ac6-243">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b0ac6-243">Test single sign-on</span></span>

<span data-ttu-id="b0ac6-244">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b0ac6-245">Wanneer u klikt op deze Hallo PagerDuty tegel in Hallo Panelyou toegang krijgt automatisch aangemelde tooyour PagerDuty toepassing.</span><span class="sxs-lookup"><span data-stu-id="b0ac6-245">When you click hello PagerDuty tile in hello Access Panelyou should get automatically signed-on tooyour PagerDuty application.</span></span>

<span data-ttu-id="b0ac6-246">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b0ac6-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b0ac6-247">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b0ac6-247">Additional resources</span></span>

* [<span data-ttu-id="b0ac6-248">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0ac6-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b0ac6-249">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b0ac6-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

