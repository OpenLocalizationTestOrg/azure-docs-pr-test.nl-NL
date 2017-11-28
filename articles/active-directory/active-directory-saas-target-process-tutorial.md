---
title: 'Zelfstudie: Azure Active Directory-integratie met TargetProcess | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en TargetProcess.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 05c574e2c18d7f73edc6c094093a6e59d46b8e6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="9a164-103">Zelfstudie: Azure Active Directory-integratie met TargetProcess</span><span class="sxs-lookup"><span data-stu-id="9a164-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>

<span data-ttu-id="9a164-104">In deze zelfstudie leert u hoe toointegrate TargetProcess met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9a164-104">In this tutorial, you learn how toointegrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9a164-105">TargetProcess integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="9a164-105">Integrating TargetProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9a164-106">U kunt beheren in Azure AD die tooTargetProcess toegang heeft</span><span class="sxs-lookup"><span data-stu-id="9a164-106">You can control in Azure AD who has access tooTargetProcess</span></span>
- <span data-ttu-id="9a164-107">U kunt uw gebruikers tooautomatically get aangemelde tooTargetProcess (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="9a164-107">You can enable your users tooautomatically get signed-on tooTargetProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9a164-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="9a164-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9a164-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9a164-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a164-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9a164-110">Prerequisites</span></span>

<span data-ttu-id="9a164-111">Azure AD-integratie met TargetProcess tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="9a164-111">tooconfigure Azure AD integration with TargetProcess, you need hello following items:</span></span>

- <span data-ttu-id="9a164-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="9a164-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9a164-113">Een TargetProcess eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="9a164-113">A TargetProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9a164-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="9a164-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9a164-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="9a164-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9a164-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="9a164-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9a164-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a164-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9a164-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="9a164-118">Scenario description</span></span>
<span data-ttu-id="9a164-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="9a164-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9a164-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="9a164-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a164-121">TargetProcess van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9a164-121">Add TargetProcess from hello gallery</span></span>
2. <span data-ttu-id="9a164-122">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a164-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-targetprocess-from-hello-gallery"></a><span data-ttu-id="9a164-123">TargetProcess van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9a164-123">Add TargetProcess from hello gallery</span></span>
<span data-ttu-id="9a164-124">tooconfigure hello integratie van TargetProcess in Azure AD, moet u tooadd TargetProcess uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="9a164-124">tooconfigure hello integration of TargetProcess into Azure AD, you need tooadd TargetProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9a164-125">**tooadd TargetProcess via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="9a164-125">**tooadd TargetProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a164-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9a164-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9a164-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9a164-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9a164-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9a164-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="9a164-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a164-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="9a164-133">Typ in het zoekvak Hallo **TargetProcess**, selecteer **TargetProcess** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="9a164-133">In hello search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![TargetProcess vanuit galerie toevoegen](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9a164-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a164-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="9a164-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met TargetProcess op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="9a164-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9a164-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in TargetProcess is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a164-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TargetProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="9a164-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in TargetProcess toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="9a164-138">In other words, a link relationship between an Azure AD user and hello related user in TargetProcess needs toobe established.</span></span>

<span data-ttu-id="9a164-139">Wijs in TargetProcess, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="9a164-139">In TargetProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9a164-140">tooconfigure en eenmalige aanmelding Azure AD-test met TargetProcess, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9a164-140">tooconfigure and test Azure AD single sign-on with TargetProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9a164-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="9a164-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9a164-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a164-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9a164-143">**[Maak een testgebruiker TargetProcess](#create-a-targetprocess-test-user)**  -toohave een equivalent van Britta Simon in TargetProcess die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="9a164-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - toohave a counterpart of Britta Simon in TargetProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9a164-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9a164-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9a164-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="9a164-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9a164-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="9a164-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9a164-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing TargetProcess configureren.</span><span class="sxs-lookup"><span data-stu-id="9a164-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TargetProcess application.</span></span>

<span data-ttu-id="9a164-148">**Azure AD tooconfigure eenmalige aanmelding met TargetProcess, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="9a164-148">**tooconfigure Azure AD single sign-on with TargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a164-149">In de Azure-portal op Hallo Hallo **TargetProcess** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="9a164-149">In hello Azure portal, on hello **TargetProcess** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="9a164-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9a164-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Op basis van SAML eenmalige aanmelding](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. <span data-ttu-id="9a164-153">Op Hallo **TargetProcess domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9a164-153">On hello **TargetProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![Sectie TargetProcess domein en URL 's](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    <span data-ttu-id="9a164-155">a.</span><span class="sxs-lookup"><span data-stu-id="9a164-155">a.</span></span> <span data-ttu-id="9a164-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="9a164-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    <span data-ttu-id="9a164-157">b.</span><span class="sxs-lookup"><span data-stu-id="9a164-157">b.</span></span> <span data-ttu-id="9a164-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="9a164-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9a164-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="9a164-159">These values are not real.</span></span> <span data-ttu-id="9a164-160">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="9a164-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9a164-161">Neem contact op met [TargetProcess Client ondersteuningsteam](mailto:support@targetprocess.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="9a164-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="9a164-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9a164-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Certificaat voor ondertekening van SAML-sectie](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. <span data-ttu-id="9a164-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="9a164-164">Click **Save** button.</span></span>

    ![knop Opslaan](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9a164-166">Op Hallo **TargetProcess configuratie** sectie, klikt u op **configureren TargetProcess** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="9a164-166">On hello **TargetProcess Configuration** section, click **Configure TargetProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9a164-167">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="9a164-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuratiesectie TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. <span data-ttu-id="9a164-169">Eenmalige aanmelding tooyour TargetProcess toepassing als beheerder.</span><span class="sxs-lookup"><span data-stu-id="9a164-169">Sign-on tooyour TargetProcess application as an administrator.</span></span>

8. <span data-ttu-id="9a164-170">Klik in het menu bovenaan Hallo Hallo **Setup**.</span><span class="sxs-lookup"><span data-stu-id="9a164-170">In hello menu on hello top, click **Setup**.</span></span>
   
    ![Instellen](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. <span data-ttu-id="9a164-172">Klik op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="9a164-172">Click **Settings**.</span></span>
   
    ![Instellingen](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. <span data-ttu-id="9a164-174">Klik op **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9a164-174">Click **Single Sign-on**.</span></span>
   
    ![Klik op eenmalige aanmelding](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. <span data-ttu-id="9a164-176">Op Hallo Single Sign-on instellingen dialoogvenster uitvoeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9a164-176">On hello Single Sign-on settings dialog, perform hello following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    <span data-ttu-id="9a164-178">a.</span><span class="sxs-lookup"><span data-stu-id="9a164-178">a.</span></span> <span data-ttu-id="9a164-179">Klik op **eenmalige aanmelding inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="9a164-179">Click **Enable Single Sign-on**.</span></span>
    
    <span data-ttu-id="9a164-180">b.</span><span class="sxs-lookup"><span data-stu-id="9a164-180">b.</span></span> <span data-ttu-id="9a164-181">In **aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9a164-181">In **Sign-on URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9a164-182">c.</span><span class="sxs-lookup"><span data-stu-id="9a164-182">c.</span></span> <span data-ttu-id="9a164-183">Open uw gedownloade certificaat in Kladblok, kopieer Hallo inhoud, en plak deze in Hallo **certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="9a164-183">Open your downloaded certificate in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="9a164-184">d.</span><span class="sxs-lookup"><span data-stu-id="9a164-184">d.</span></span> <span data-ttu-id="9a164-185">Klik op **JIT-inrichting inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="9a164-185">click **Enable JIT Provisioning**.</span></span>

    <span data-ttu-id="9a164-186">e.</span><span class="sxs-lookup"><span data-stu-id="9a164-186">e.</span></span> <span data-ttu-id="9a164-187">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9a164-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="9a164-188">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="9a164-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9a164-189">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="9a164-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9a164-190">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9a164-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9a164-191">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="9a164-191">Create an Azure AD test user</span></span>
<span data-ttu-id="9a164-192">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9a164-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="9a164-194">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="9a164-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a164-195">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9a164-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9a164-197">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="9a164-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![toodisplay hello lijst van gebruikers](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9a164-199">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="9a164-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Knop toevoegen](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9a164-201">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9a164-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Sectie van de gebruiker](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9a164-203">a.</span><span class="sxs-lookup"><span data-stu-id="9a164-203">a.</span></span> <span data-ttu-id="9a164-204">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9a164-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9a164-205">b.</span><span class="sxs-lookup"><span data-stu-id="9a164-205">b.</span></span> <span data-ttu-id="9a164-206">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9a164-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9a164-207">c.</span><span class="sxs-lookup"><span data-stu-id="9a164-207">c.</span></span> <span data-ttu-id="9a164-208">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="9a164-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9a164-209">d.</span><span class="sxs-lookup"><span data-stu-id="9a164-209">d.</span></span> <span data-ttu-id="9a164-210">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="9a164-210">Click **Create**.</span></span>
 
### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="9a164-211">Een testgebruiker TargetProcess maken</span><span class="sxs-lookup"><span data-stu-id="9a164-211">Create a TargetProcess test user</span></span>

<span data-ttu-id="9a164-212">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in TargetProcess van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="9a164-212">hello objective of this section is toocreate a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="9a164-213">TargetProcess ondersteuning biedt voor just-in-time-inrichting.</span><span class="sxs-lookup"><span data-stu-id="9a164-213">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="9a164-214">U hebt al ingeschakeld in [eenmalige aanmelding configureren Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="9a164-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="9a164-215">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="9a164-215">There is no action item for you in this section.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9a164-216">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a164-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9a164-217">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooTargetProcess toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="9a164-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTargetProcess.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="9a164-219">**tooassign Britta Simon tooTargetProcess, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="9a164-219">**tooassign Britta Simon tooTargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a164-220">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9a164-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="9a164-222">Selecteer in de lijst met de toepassingen van Hallo **TargetProcess**.</span><span class="sxs-lookup"><span data-stu-id="9a164-222">In hello applications list, select **TargetProcess**.</span></span>

    ![TargetProcess in lijst met Apps](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. <span data-ttu-id="9a164-224">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="9a164-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="9a164-226">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="9a164-226">Click **Add** button.</span></span> <span data-ttu-id="9a164-227">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a164-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="9a164-229">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="9a164-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9a164-230">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a164-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9a164-231">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9a164-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9a164-232">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9a164-232">Test single sign-on</span></span>

<span data-ttu-id="9a164-233">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="9a164-233">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9a164-234">Als u op Hallo TargetProcess-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour TargetProcess toepassing.</span><span class="sxs-lookup"><span data-stu-id="9a164-234">When you click hello TargetProcess tile in hello Access Panel, you should get automatically signed-on tooyour TargetProcess application.</span></span> <span data-ttu-id="9a164-235">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9a164-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9a164-236">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="9a164-236">Additional resources</span></span>

* [<span data-ttu-id="9a164-237">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a164-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a164-238">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9a164-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png

