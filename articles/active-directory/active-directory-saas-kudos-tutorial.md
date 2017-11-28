---
title: 'Zelfstudie: Azure Active Directory-integratie met kudo | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en kudo.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: c1b481463574461f9948db2b83843fefa5d74e99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="11d6c-103">Zelfstudie: Azure Active Directory-integratie met kudo</span><span class="sxs-lookup"><span data-stu-id="11d6c-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="11d6c-104">In deze zelfstudie leert u hoe toointegrate kudo met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="11d6c-104">In this tutorial, you learn how toointegrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="11d6c-105">Kudo integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="11d6c-105">Integrating Kudos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="11d6c-106">U kunt beheren in Azure AD die tooKudos toegang heeft</span><span class="sxs-lookup"><span data-stu-id="11d6c-106">You can control in Azure AD who has access tooKudos</span></span>
- <span data-ttu-id="11d6c-107">U kunt uw gebruikers tooautomatically get aangemelde tooKudos (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="11d6c-107">You can enable your users tooautomatically get signed-on tooKudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="11d6c-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="11d6c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="11d6c-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="11d6c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11d6c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="11d6c-110">Prerequisites</span></span>

<span data-ttu-id="11d6c-111">Azure AD-integratie met kudo tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="11d6c-111">tooconfigure Azure AD integration with Kudos, you need hello following items:</span></span>

- <span data-ttu-id="11d6c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="11d6c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="11d6c-113">Een kudo eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="11d6c-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="11d6c-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="11d6c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="11d6c-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="11d6c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="11d6c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="11d6c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="11d6c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="11d6c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="11d6c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="11d6c-118">Scenario description</span></span>
<span data-ttu-id="11d6c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="11d6c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="11d6c-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="11d6c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="11d6c-121">Het toevoegen van kudo van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="11d6c-121">Adding Kudos from hello gallery</span></span>
2. <span data-ttu-id="11d6c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="11d6c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-hello-gallery"></a><span data-ttu-id="11d6c-123">Het toevoegen van kudo van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="11d6c-123">Adding Kudos from hello gallery</span></span>
<span data-ttu-id="11d6c-124">tooconfigure hello integratie van kudo in Azure AD, moet u tooadd kudo uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="11d6c-124">tooconfigure hello integration of Kudos into Azure AD, you need tooadd Kudos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="11d6c-125">**tooadd kudo via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="11d6c-125">**tooadd Kudos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="11d6c-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="11d6c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="11d6c-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="11d6c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="11d6c-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="11d6c-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="11d6c-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="11d6c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="11d6c-133">Typ in het zoekvak Hallo **kudo**.</span><span class="sxs-lookup"><span data-stu-id="11d6c-133">In hello search box, type **Kudos**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. <span data-ttu-id="11d6c-135">Selecteer in het deelvenster resultaten hello, **kudo**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="11d6c-135">In hello results panel, select **Kudos**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="11d6c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="11d6c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="11d6c-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met kudo op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="11d6c-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="11d6c-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in kudo is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11d6c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kudos is tooa user in Azure AD.</span></span> <span data-ttu-id="11d6c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in kudo toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="11d6c-140">In other words, a link relationship between an Azure AD user and hello related user in Kudos needs toobe established.</span></span>

<span data-ttu-id="11d6c-141">Wijs in kudo, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="11d6c-141">In Kudos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="11d6c-142">tooconfigure en eenmalige aanmelding Azure AD-test met kudo, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="11d6c-142">tooconfigure and test Azure AD single sign-on with Kudos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="11d6c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="11d6c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="11d6c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11d6c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="11d6c-145">**[Maken van een testgebruiker kudo](#creating-a-kudos-test-user)**  -toohave een equivalent van Britta Simon in kudo die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="11d6c-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - toohave a counterpart of Britta Simon in Kudos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="11d6c-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="11d6c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="11d6c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="11d6c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="11d6c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="11d6c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="11d6c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing kudo configureren.</span><span class="sxs-lookup"><span data-stu-id="11d6c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="11d6c-150">**Azure AD tooconfigure eenmalige aanmelding met kudo, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="11d6c-150">**tooconfigure Azure AD single sign-on with Kudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="11d6c-151">In de Azure-portal op Hallo Hallo **kudo** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="11d6c-151">In hello Azure portal, on hello **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="11d6c-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="11d6c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. <span data-ttu-id="11d6c-155">Op Hallo **kudo domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="11d6c-155">On hello **Kudos Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="11d6c-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company>.kudosnow.com`</span><span class="sxs-lookup"><span data-stu-id="11d6c-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="11d6c-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="11d6c-158">This value is not real.</span></span> <span data-ttu-id="11d6c-159">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="11d6c-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="11d6c-160">Neem contact op met [kudo Client ondersteuningsteam](http://success.kudosnow.com/home) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="11d6c-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) tooget this value.</span></span> 
 
4. <span data-ttu-id="11d6c-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="11d6c-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. <span data-ttu-id="11d6c-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="11d6c-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="11d6c-165">Op Hallo **kudo configuratie** sectie, klikt u op **kudo configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="11d6c-165">On hello **Kudos Configuration** section, click **Configure Kudos** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="11d6c-166">Kopiëren Hallo **Sign-Out URL's en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="11d6c-166">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. <span data-ttu-id="11d6c-168">In een ander browservenster, meld u bij uw bedrijf kudo site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="11d6c-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

8. <span data-ttu-id="11d6c-169">Klik in het menu bovenaan Hallo Hallo **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="11d6c-169">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="11d6c-170">![Instellingen](./media/active-directory-saas-kudos-tutorial/ic787806.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="11d6c-170">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

9. <span data-ttu-id="11d6c-171">Klik op **integraties \> SSO**.</span><span class="sxs-lookup"><span data-stu-id="11d6c-171">Click **Integrations \> SSO**.</span></span>

10. <span data-ttu-id="11d6c-172">In Hallo **SSO** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="11d6c-172">In hello **SSO** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="11d6c-173">![EENMALIGE AANMELDING](./media/active-directory-saas-kudos-tutorial/ic787807.png "EENMALIGE AANMELDING")</span><span class="sxs-lookup"><span data-stu-id="11d6c-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="11d6c-174">a.</span><span class="sxs-lookup"><span data-stu-id="11d6c-174">a.</span></span> <span data-ttu-id="11d6c-175">In **aanmelden URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="11d6c-175">In **Sign on URL** textbox, paste hello value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="11d6c-176">b.</span><span class="sxs-lookup"><span data-stu-id="11d6c-176">b.</span></span> <span data-ttu-id="11d6c-177">De base-64 gecodeerde certificaat openen in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **X.509-certificaat** tekstvak</span><span class="sxs-lookup"><span data-stu-id="11d6c-177">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="11d6c-178">c.</span><span class="sxs-lookup"><span data-stu-id="11d6c-178">c.</span></span> <span data-ttu-id="11d6c-179">In **afmelding tooURL**, plak Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="11d6c-179">In **Logout tooURL**, paste hello value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="11d6c-180">d.</span><span class="sxs-lookup"><span data-stu-id="11d6c-180">d.</span></span> <span data-ttu-id="11d6c-181">In Hallo **de kudo URL** textbox, typ de naam van uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="11d6c-181">In hello **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="11d6c-182">e.</span><span class="sxs-lookup"><span data-stu-id="11d6c-182">e.</span></span> <span data-ttu-id="11d6c-183">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="11d6c-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="11d6c-184">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="11d6c-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="11d6c-185">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="11d6c-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="11d6c-186">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="11d6c-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="11d6c-187">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="11d6c-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="11d6c-188">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="11d6c-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="11d6c-190">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="11d6c-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="11d6c-191">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="11d6c-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="11d6c-193">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="11d6c-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="11d6c-195">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="11d6c-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="11d6c-197">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="11d6c-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="11d6c-199">a.</span><span class="sxs-lookup"><span data-stu-id="11d6c-199">a.</span></span> <span data-ttu-id="11d6c-200">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="11d6c-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="11d6c-201">b.</span><span class="sxs-lookup"><span data-stu-id="11d6c-201">b.</span></span> <span data-ttu-id="11d6c-202">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="11d6c-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="11d6c-203">c.</span><span class="sxs-lookup"><span data-stu-id="11d6c-203">c.</span></span> <span data-ttu-id="11d6c-204">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="11d6c-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="11d6c-205">d.</span><span class="sxs-lookup"><span data-stu-id="11d6c-205">d.</span></span> <span data-ttu-id="11d6c-206">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="11d6c-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="11d6c-207">Een testgebruiker kudo maken</span><span class="sxs-lookup"><span data-stu-id="11d6c-207">Creating a Kudos test user</span></span>

<span data-ttu-id="11d6c-208">In volgorde tooenable Azure AD gebruikers toolog in kudo, moeten ze worden ingericht in kudo.</span><span class="sxs-lookup"><span data-stu-id="11d6c-208">In order tooenable Azure AD users toolog into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="11d6c-209">In geval van kudo Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="11d6c-209">In hello case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="11d6c-210">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="11d6c-210">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="11d6c-211">Meld u bij tooyour **kudo** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="11d6c-211">Log in tooyour **Kudos** company site as administrator.</span></span>

2. <span data-ttu-id="11d6c-212">Klik in het menu bovenaan Hallo Hallo **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="11d6c-212">In hello menu on hello top, click **Settings**.</span></span>
   
   <span data-ttu-id="11d6c-213">![Instellingen](./media/active-directory-saas-kudos-tutorial/ic787806.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="11d6c-213">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

3. <span data-ttu-id="11d6c-214">Klik op **Gebruikerbeheerder**.</span><span class="sxs-lookup"><span data-stu-id="11d6c-214">Click **User Admin**.</span></span>

4. <span data-ttu-id="11d6c-215">Klik op Hallo **gebruikers** tabblad en klik vervolgens op **toevoegen van een gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="11d6c-215">Click hello **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="11d6c-216">![Gebruikerbeheerder](./media/active-directory-saas-kudos-tutorial/ic787809.png "Gebruikerbeheerder")</span><span class="sxs-lookup"><span data-stu-id="11d6c-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span></span>

5. <span data-ttu-id="11d6c-217">In Hallo **toevoegen van een gebruiker** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="11d6c-217">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="11d6c-218">![Een gebruiker toevoegen](./media/active-directory-saas-kudos-tutorial/ic787810.png "een gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="11d6c-218">![Add a User](./media/active-directory-saas-kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="11d6c-219">a.</span><span class="sxs-lookup"><span data-stu-id="11d6c-219">a.</span></span> <span data-ttu-id="11d6c-220">Type Hallo **voornaam**, **achternaam**, **e** en andere details van een geldige Azure Active Directory-account dat u wilt dat tooprovision in Hallo gerelateerde tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="11d6c-220">Type hello **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="11d6c-221">b.</span><span class="sxs-lookup"><span data-stu-id="11d6c-221">b.</span></span> <span data-ttu-id="11d6c-222">Klik op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="11d6c-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="11d6c-223">U kunt andere kudo gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door kudo tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="11d6c-223">You can use any other Kudos user account creation tools or APIs provided by Kudos tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="11d6c-224">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="11d6c-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="11d6c-225">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooKudos toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="11d6c-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKudos.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="11d6c-227">**tooassign Britta Simon tooKudos, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="11d6c-227">**tooassign Britta Simon tooKudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="11d6c-228">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="11d6c-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="11d6c-230">Selecteer in de lijst met de toepassingen van Hallo **kudo**.</span><span class="sxs-lookup"><span data-stu-id="11d6c-230">In hello applications list, select **Kudos**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. <span data-ttu-id="11d6c-232">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="11d6c-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="11d6c-234">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="11d6c-234">Click **Add** button.</span></span> <span data-ttu-id="11d6c-235">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="11d6c-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="11d6c-237">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="11d6c-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="11d6c-238">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="11d6c-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="11d6c-239">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="11d6c-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="11d6c-240">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="11d6c-240">Testing single sign-on</span></span>

<span data-ttu-id="11d6c-241">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="11d6c-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="11d6c-242">Als u op Hallo kudo tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour kudo toepassing.</span><span class="sxs-lookup"><span data-stu-id="11d6c-242">When you click hello Kudos tile in hello Access Panel, you should get automatically signed-on tooyour Kudos application.</span></span> <span data-ttu-id="11d6c-243">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="11d6c-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="11d6c-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="11d6c-244">Additional resources</span></span>

* [<span data-ttu-id="11d6c-245">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11d6c-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="11d6c-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="11d6c-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png

