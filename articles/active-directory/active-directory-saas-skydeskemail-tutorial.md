---
title: 'Zelfstudie: Azure Active Directory-integratie met e-mailadres SkyDesk | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SkyDesk e-mailbericht.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 19c670a60f581a2be55b74eacdb5393a36e38be3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a><span data-ttu-id="15aec-103">Zelfstudie: Azure Active Directory-integratie met SkyDesk e-mailadres</span><span class="sxs-lookup"><span data-stu-id="15aec-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span></span>

<span data-ttu-id="15aec-104">In deze zelfstudie leert u hoe het e-toointegrate SkyDesk met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="15aec-104">In this tutorial, you learn how toointegrate SkyDesk Email with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="15aec-105">E-mailadres SkyDesk integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="15aec-105">Integrating SkyDesk Email with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="15aec-106">U kunt beheren in Azure AD wie toegang tot tooSkyDesk e heeft</span><span class="sxs-lookup"><span data-stu-id="15aec-106">You can control in Azure AD who has access tooSkyDesk Email</span></span>
- <span data-ttu-id="15aec-107">U kunt uw gebruikers tooautomatically get aangemelde tooSkyDesk e (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="15aec-107">You can enable your users tooautomatically get signed-on tooSkyDesk Email (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="15aec-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="15aec-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="15aec-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="15aec-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15aec-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="15aec-110">Prerequisites</span></span>

<span data-ttu-id="15aec-111">Azure AD-integratie met e-mailadres SkyDesk tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="15aec-111">tooconfigure Azure AD integration with SkyDesk Email, you need hello following items:</span></span>

- <span data-ttu-id="15aec-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="15aec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="15aec-113">Een e-mailadres SkyDesk eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="15aec-113">A SkyDesk Email single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="15aec-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="15aec-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="15aec-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="15aec-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="15aec-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="15aec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="15aec-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u hier een proefversie van één maand krijgen [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="15aec-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="15aec-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="15aec-118">Scenario description</span></span>
<span data-ttu-id="15aec-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="15aec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="15aec-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="15aec-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="15aec-121">Het toevoegen van SkyDesk e van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="15aec-121">Adding SkyDesk Email from hello gallery</span></span>
2. <span data-ttu-id="15aec-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="15aec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skydesk-email-from-hello-gallery"></a><span data-ttu-id="15aec-123">Het toevoegen van SkyDesk e van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="15aec-123">Adding SkyDesk Email from hello gallery</span></span>
<span data-ttu-id="15aec-124">tooconfigure hello integratie van SkyDesk E-mail in Azure AD, moet u tooadd SkyDesk e uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="15aec-124">tooconfigure hello integration of SkyDesk Email into Azure AD, you need tooadd SkyDesk Email from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="15aec-125">**tooadd SkyDesk E-mail via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="15aec-125">**tooadd SkyDesk Email from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="15aec-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="15aec-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="15aec-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="15aec-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="15aec-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="15aec-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="15aec-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="15aec-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="15aec-133">Typ in het zoekvak Hallo **SkyDesk e**.</span><span class="sxs-lookup"><span data-stu-id="15aec-133">In hello search box, type **SkyDesk Email**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. <span data-ttu-id="15aec-135">Selecteer in het deelvenster resultaten hello, **SkyDesk e**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="15aec-135">In hello results panel, select **SkyDesk Email**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="15aec-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="15aec-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="15aec-138">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met SkyDesk e-mailadres op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="15aec-138">In this section, you configure and test Azure AD single sign-on with SkyDesk Email based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="15aec-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in SkyDesk e-mailbericht is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15aec-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SkyDesk Email is tooa user in Azure AD.</span></span> <span data-ttu-id="15aec-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in SkyDesk e-mailbericht toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="15aec-140">In other words, a link relationship between an Azure AD user and hello related user in SkyDesk Email needs toobe established.</span></span>

<span data-ttu-id="15aec-141">In het e-mailadres SkyDesk Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="15aec-141">In SkyDesk Email, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="15aec-142">tooconfigure en test eenmalige aanmelding Azure AD met SkyDesk e-mailadres, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="15aec-142">tooconfigure and test Azure AD single sign-on with SkyDesk Email, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="15aec-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="15aec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="15aec-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="15aec-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="15aec-145">**[Maken van een testgebruiker SkyDesk e](#creating-a-skydesk-email-test-user)**  -toohave een equivalent van Britta Simon in SkyDesk e-mailbericht is gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="15aec-145">**[Creating a SkyDesk Email test user](#creating-a-skydesk-email-test-user)** - toohave a counterpart of Britta Simon in SkyDesk Email that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="15aec-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="15aec-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="15aec-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="15aec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="15aec-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="15aec-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="15aec-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw SkyDesk e-mailtoepassing configureren.</span><span class="sxs-lookup"><span data-stu-id="15aec-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SkyDesk Email application.</span></span>

<span data-ttu-id="15aec-150">**Voer tooconfigure Azure AD eenmalige aanmelding met e-mailadres SkyDesk Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="15aec-150">**tooconfigure Azure AD single sign-on with SkyDesk Email, perform hello following steps:**</span></span>

1. <span data-ttu-id="15aec-151">In Azure-portal op Hallo Hallo **SkyDesk e** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="15aec-151">In hello Azure portal, on hello **SkyDesk Email** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="15aec-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="15aec-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. <span data-ttu-id="15aec-155">Op Hallo **SkyDesk e-maildomein en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="15aec-155">On hello **SkyDesk Email Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    <span data-ttu-id="15aec-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://mail.skydesk.jp/portal/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="15aec-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.skydesk.jp/portal/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="15aec-158">Hallo-waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="15aec-158">hello value is not real.</span></span> <span data-ttu-id="15aec-159">Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="15aec-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="15aec-160">Neem contact op met [SkyDesk e-mailclient ondersteuningsteam](https://www.skydesk.sg/support/) tooget Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="15aec-160">Contact [SkyDesk Email Client support team](https://www.skydesk.sg/support/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="15aec-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="15aec-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. <span data-ttu-id="15aec-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="15aec-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="15aec-165">Op Hallo **SkyDesk e-mailconfiguratie** sectie, klikt u op **configureren SkyDesk e** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="15aec-165">On hello **SkyDesk Email Configuration** section, click **Configure SkyDesk Email** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="15aec-166">Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="15aec-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. <span data-ttu-id="15aec-168">tooenable SSO in **SkyDesk e**, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="15aec-168">tooenable SSO in **SkyDesk Email**, perform hello following steps:</span></span>

    <span data-ttu-id="15aec-169">a.</span><span class="sxs-lookup"><span data-stu-id="15aec-169">a.</span></span> <span data-ttu-id="15aec-170">Eenmalige aanmelding tooyour SkyDesk e-mailaccount als administrator.</span><span class="sxs-lookup"><span data-stu-id="15aec-170">Sign-on tooyour SkyDesk Email account as administrator.</span></span>

    <span data-ttu-id="15aec-171">b.</span><span class="sxs-lookup"><span data-stu-id="15aec-171">b.</span></span> <span data-ttu-id="15aec-172">Klik in het menu bovenaan Hallo Hallo **Setup**, en selecteer **Org**.</span><span class="sxs-lookup"><span data-stu-id="15aec-172">In hello menu on hello top, click **Setup**, and select **Org**.</span></span> 
    
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    <span data-ttu-id="15aec-174">c.</span><span class="sxs-lookup"><span data-stu-id="15aec-174">c.</span></span> <span data-ttu-id="15aec-175">Klik op **domeinen** van het linkerpaneel Hallo.</span><span class="sxs-lookup"><span data-stu-id="15aec-175">Click on **Domains** from hello left panel.</span></span>
    
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    <span data-ttu-id="15aec-177">d.</span><span class="sxs-lookup"><span data-stu-id="15aec-177">d.</span></span> <span data-ttu-id="15aec-178">Klik op **domein toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="15aec-178">Click on **Add Domain**.</span></span>
    
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    <span data-ttu-id="15aec-180">e.</span><span class="sxs-lookup"><span data-stu-id="15aec-180">e.</span></span> <span data-ttu-id="15aec-181">Voer uw domeinnaam en controleer vervolgens Hallo domein.</span><span class="sxs-lookup"><span data-stu-id="15aec-181">Enter your Domain name, and then verify hello Domain.</span></span>
    
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    <span data-ttu-id="15aec-183">f.</span><span class="sxs-lookup"><span data-stu-id="15aec-183">f.</span></span> <span data-ttu-id="15aec-184">Klik op **SAML-verificatie** van het linkerpaneel Hallo.</span><span class="sxs-lookup"><span data-stu-id="15aec-184">Click on **SAML Authentication** from hello left panel.</span></span>
    
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. <span data-ttu-id="15aec-186">Op Hallo **SAML-verificatie** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="15aec-186">On hello **SAML Authentication** dialog page, perform hello following steps:</span></span>
   
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    ><span data-ttu-id="15aec-188">toouse SAML gebaseerde verificatie, hebt u ofwel **gecontroleerde domein** of **portal URL** setup.</span><span class="sxs-lookup"><span data-stu-id="15aec-188">toouse SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span></span> <span data-ttu-id="15aec-189">U kunt instellen Hallo portal URL met Hallo unieke naam.</span><span class="sxs-lookup"><span data-stu-id="15aec-189">You can set hello portal URL with hello unique name.</span></span>
    > 
    > 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    <span data-ttu-id="15aec-191">a.</span><span class="sxs-lookup"><span data-stu-id="15aec-191">a.</span></span> <span data-ttu-id="15aec-192">In Hallo **aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="15aec-192">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="15aec-193">b.</span><span class="sxs-lookup"><span data-stu-id="15aec-193">b.</span></span> <span data-ttu-id="15aec-194">In Hallo **afmelding** tekstvak URL plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="15aec-194">In hello **Logout** URL textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="15aec-195">c.</span><span class="sxs-lookup"><span data-stu-id="15aec-195">c.</span></span> <span data-ttu-id="15aec-196">**De URL van het wachtwoord wijzigen** is optioneel dus laat dit veld leeg.</span><span class="sxs-lookup"><span data-stu-id="15aec-196">**Change Password URL** is optional so leave it blank.</span></span>

    <span data-ttu-id="15aec-197">d.</span><span class="sxs-lookup"><span data-stu-id="15aec-197">d.</span></span> <span data-ttu-id="15aec-198">Klik op **sleutelbestand ophalen** tooselect uw gedownloade certificaat van de Azure-portal en klik vervolgens op **Open** tooupload Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="15aec-198">Click on **Get Key From File** tooselect your downloaded certificate from Azure portal, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="15aec-199">e.</span><span class="sxs-lookup"><span data-stu-id="15aec-199">e.</span></span> <span data-ttu-id="15aec-200">Als **algoritme**, selecteer **RSA**.</span><span class="sxs-lookup"><span data-stu-id="15aec-200">As **Algorithm**, select **RSA**.</span></span>

    <span data-ttu-id="15aec-201">f.</span><span class="sxs-lookup"><span data-stu-id="15aec-201">f.</span></span> <span data-ttu-id="15aec-202">Klik op **Ok** toosave Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="15aec-202">Click **Ok** toosave hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="15aec-203">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="15aec-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="15aec-204">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="15aec-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="15aec-205">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="15aec-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="15aec-206">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="15aec-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="15aec-207">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="15aec-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="15aec-209">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="15aec-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="15aec-210">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="15aec-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="15aec-212">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="15aec-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="15aec-214">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="15aec-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="15aec-216">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="15aec-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="15aec-218">a.</span><span class="sxs-lookup"><span data-stu-id="15aec-218">a.</span></span> <span data-ttu-id="15aec-219">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="15aec-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="15aec-220">b.</span><span class="sxs-lookup"><span data-stu-id="15aec-220">b.</span></span> <span data-ttu-id="15aec-221">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="15aec-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="15aec-222">c.</span><span class="sxs-lookup"><span data-stu-id="15aec-222">c.</span></span> <span data-ttu-id="15aec-223">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="15aec-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="15aec-224">d.</span><span class="sxs-lookup"><span data-stu-id="15aec-224">d.</span></span> <span data-ttu-id="15aec-225">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="15aec-225">Click **Create**.</span></span>
 
### <a name="creating-a-skydesk-email-test-user"></a><span data-ttu-id="15aec-226">Maken van een testgebruiker SkyDesk e</span><span class="sxs-lookup"><span data-stu-id="15aec-226">Creating a SkyDesk Email test user</span></span>

<span data-ttu-id="15aec-227">In deze sectie kunt u een gebruiker met de naam van Britta Simon in SkyDesk E-mail maken.</span><span class="sxs-lookup"><span data-stu-id="15aec-227">In this section, you create a user called Britta Simon in SkyDesk Email.</span></span>

1. <span data-ttu-id="15aec-228">Klik op **gebruikerstoegang** van Hallo links van het deelvenster in SkyDesk e-mailbericht en voer uw gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="15aec-228">Click on **User Access** from hello left panel in SkyDesk Email and then enter your username.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
><span data-ttu-id="15aec-230">Als u toocreate bulksgewijs gebruikers moet, moet u toocontact hello [SkyDesk e-mailclient ondersteuningsteam](https://www.skydesk.sg/support/).</span><span class="sxs-lookup"><span data-stu-id="15aec-230">If you need toocreate bulk users, you need toocontact hello [SkyDesk Email Client support team](https://www.skydesk.sg/support/).</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="15aec-231">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="15aec-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="15aec-232">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSkyDesk e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="15aec-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSkyDesk Email.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="15aec-234">**tooassign Britta Simon tooSkyDesk e-mailadres Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="15aec-234">**tooassign Britta Simon tooSkyDesk Email, perform hello following steps:**</span></span>

1. <span data-ttu-id="15aec-235">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="15aec-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="15aec-237">Selecteer in de lijst met de toepassingen van Hallo **SkyDesk e**.</span><span class="sxs-lookup"><span data-stu-id="15aec-237">In hello applications list, select **SkyDesk Email**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. <span data-ttu-id="15aec-239">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="15aec-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="15aec-241">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="15aec-241">Click **Add** button.</span></span> <span data-ttu-id="15aec-242">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="15aec-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="15aec-244">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="15aec-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="15aec-245">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="15aec-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="15aec-246">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="15aec-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="15aec-247">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="15aec-247">Testing single sign-on</span></span>

<span data-ttu-id="15aec-248">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="15aec-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="15aec-249">Als u op Hallo SkyDesk e-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SkyDesk e-mailtoepassing.</span><span class="sxs-lookup"><span data-stu-id="15aec-249">When you click hello SkyDesk Email tile in hello Access Panel, you should get automatically signed-on tooyour SkyDesk Email application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="15aec-250">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="15aec-250">Additional resources</span></span>

* [<span data-ttu-id="15aec-251">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15aec-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="15aec-252">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="15aec-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png

