---
title: 'Zelfstudie: Azure Active Directory-integratie met RunMyProcess | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en RunMyProcess.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f02acda015aeb8d131d8e3ef88bf50c4e8e94750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="c3664-103">Zelfstudie: Azure Active Directory-integratie met RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="c3664-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="c3664-104">In deze zelfstudie leert u hoe toointegrate RunMyProcess met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3664-104">In this tutorial, you learn how toointegrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c3664-105">RunMyProcess integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c3664-105">Integrating RunMyProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c3664-106">U kunt beheren in Azure AD die tooRunMyProcess toegang heeft</span><span class="sxs-lookup"><span data-stu-id="c3664-106">You can control in Azure AD who has access tooRunMyProcess</span></span>
- <span data-ttu-id="c3664-107">U kunt uw gebruikers tooautomatically get aangemelde tooRunMyProcess (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="c3664-107">You can enable your users tooautomatically get signed-on tooRunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c3664-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c3664-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c3664-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c3664-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3664-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c3664-110">Prerequisites</span></span>

<span data-ttu-id="c3664-111">Azure AD-integratie met RunMyProcess tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="c3664-111">tooconfigure Azure AD integration with RunMyProcess, you need hello following items:</span></span>

- <span data-ttu-id="c3664-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c3664-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c3664-113">Een RunMyProcess eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c3664-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c3664-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c3664-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c3664-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c3664-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c3664-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c3664-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c3664-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden:[proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c3664-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c3664-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c3664-118">Scenario description</span></span>
<span data-ttu-id="c3664-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c3664-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c3664-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c3664-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c3664-121">Het toevoegen van RunMyProcess van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="c3664-121">Adding RunMyProcess from hello gallery</span></span>
2. <span data-ttu-id="c3664-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c3664-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-hello-gallery"></a><span data-ttu-id="c3664-123">Het toevoegen van RunMyProcess van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="c3664-123">Adding RunMyProcess from hello gallery</span></span>
<span data-ttu-id="c3664-124">tooconfigure hello integratie van RunMyProcess in Azure AD, moet u tooadd RunMyProcess uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c3664-124">tooconfigure hello integration of RunMyProcess into Azure AD, you need tooadd RunMyProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c3664-125">**tooadd RunMyProcess via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c3664-125">**tooadd RunMyProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3664-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c3664-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c3664-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c3664-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c3664-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c3664-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c3664-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c3664-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c3664-133">Typ in het zoekvak Hallo **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="c3664-133">In hello search box, type **RunMyProcess**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. <span data-ttu-id="c3664-135">Selecteer in het deelvenster resultaten hello, **RunMyProcess**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c3664-135">In hello results panel, select **RunMyProcess**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c3664-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c3664-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c3664-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met RunMyProcess op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="c3664-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c3664-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in RunMyProcess is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3664-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RunMyProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="c3664-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in RunMyProcess toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="c3664-140">In other words, a link relationship between an Azure AD user and hello related user in RunMyProcess needs toobe established.</span></span>

<span data-ttu-id="c3664-141">Wijs in RunMyProcess, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="c3664-141">In RunMyProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c3664-142">tooconfigure en eenmalige aanmelding Azure AD-test met RunMyProcess, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c3664-142">tooconfigure and test Azure AD single sign-on with RunMyProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c3664-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="c3664-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c3664-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3664-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c3664-145">**[Maken van een testgebruiker RunMyProcess](#creating-a-runmyprocess-test-user)**  -toohave een equivalent van Britta Simon in RunMyProcess die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c3664-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - toohave a counterpart of Britta Simon in RunMyProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c3664-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c3664-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c3664-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c3664-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c3664-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c3664-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c3664-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing RunMyProcess configureren.</span><span class="sxs-lookup"><span data-stu-id="c3664-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="c3664-150">**Azure AD tooconfigure eenmalige aanmelding met RunMyProcess, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c3664-150">**tooconfigure Azure AD single sign-on with RunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3664-151">In de Azure-portal op Hallo Hallo **RunMyProcess** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c3664-151">In hello Azure portal, on hello **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c3664-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c3664-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. <span data-ttu-id="c3664-155">Op Hallo **RunMyProcess domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c3664-155">On hello **RunMyProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="c3664-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://live.runmyprocess.com/live/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="c3664-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c3664-158">Hallo-waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="c3664-158">hello value is not real.</span></span> <span data-ttu-id="c3664-159">Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="c3664-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="c3664-160">Neem contact op met [RunMyProcess Client ondersteuningsteam](mailto:support@runmyprocess.com) tooget Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="c3664-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) tooget hello value.</span></span> 

4. <span data-ttu-id="c3664-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c3664-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. <span data-ttu-id="c3664-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c3664-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c3664-165">Op Hallo **RunMyProcess configuratie** sectie, klikt u op **configureren RunMyProcess** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="c3664-165">On hello **RunMyProcess Configuration** section, click **Configure RunMyProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c3664-166">Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="c3664-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. <span data-ttu-id="c3664-168">In een ander browservenster, aanmelding tooyour RunMyProcess tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c3664-168">In a different web browser window, sign-on tooyour RunMyProcess tenant as an administrator.</span></span>

8. <span data-ttu-id="c3664-169">Klik in het linkernavigatievenster, **Account** en selecteer **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="c3664-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. <span data-ttu-id="c3664-171">Ga te**verificatiemethode** sectie en Voer onderstaande stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c3664-171">Go too**Authentication method** section and perform below steps:</span></span>
   
    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="c3664-173">a.</span><span class="sxs-lookup"><span data-stu-id="c3664-173">a.</span></span> <span data-ttu-id="c3664-174">Als **methode**, selecteer **-SSO met Samlv2**.</span><span class="sxs-lookup"><span data-stu-id="c3664-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="c3664-175">b.</span><span class="sxs-lookup"><span data-stu-id="c3664-175">b.</span></span> <span data-ttu-id="c3664-176">In Hallo **SSO omleiding** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c3664-176">In hello **SSO redirect** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c3664-177">c.</span><span class="sxs-lookup"><span data-stu-id="c3664-177">c.</span></span> <span data-ttu-id="c3664-178">In Hallo **afmelding omleiding** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c3664-178">In hello **Logout redirect** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c3664-179">d.</span><span class="sxs-lookup"><span data-stu-id="c3664-179">d.</span></span> <span data-ttu-id="c3664-180">In Hallo **indeling naam-Id** textbox Hallo typewaarde van **indeling van de id** als **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="c3664-180">In hello **Name Id Format** textbox, type hello value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="c3664-181">e.</span><span class="sxs-lookup"><span data-stu-id="c3664-181">e.</span></span> <span data-ttu-id="c3664-182">Hallo-inhoud van het gedownloade bestand Hallo Kopieer en plak deze in Hallo **certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="c3664-182">Copy hello content of hello downloaded certificate file and then paste it into hello **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="c3664-183">f.</span><span class="sxs-lookup"><span data-stu-id="c3664-183">f.</span></span> <span data-ttu-id="c3664-184">Klik op **opslaan** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c3664-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="c3664-185">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="c3664-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c3664-186">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="c3664-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c3664-187">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c3664-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c3664-188">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c3664-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="c3664-189">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c3664-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c3664-191">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c3664-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3664-192">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c3664-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c3664-194">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c3664-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c3664-196">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="c3664-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c3664-198">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c3664-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c3664-200">a.</span><span class="sxs-lookup"><span data-stu-id="c3664-200">a.</span></span> <span data-ttu-id="c3664-201">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c3664-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c3664-202">b.</span><span class="sxs-lookup"><span data-stu-id="c3664-202">b.</span></span> <span data-ttu-id="c3664-203">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c3664-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c3664-204">c.</span><span class="sxs-lookup"><span data-stu-id="c3664-204">c.</span></span> <span data-ttu-id="c3664-205">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c3664-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c3664-206">d.</span><span class="sxs-lookup"><span data-stu-id="c3664-206">d.</span></span> <span data-ttu-id="c3664-207">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c3664-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="c3664-208">Een testgebruiker RunMyProcess maken</span><span class="sxs-lookup"><span data-stu-id="c3664-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="c3664-209">In de volgorde tooenable Azure AD gebruikers toolog in tooRunMyProcess, moeten ze worden ingericht in RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="c3664-209">In order tooenable Azure AD users toolog in tooRunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="c3664-210">In geval van RunMyProcess Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="c3664-210">In hello case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="c3664-211">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c3664-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3664-212">Aanmelden tooyour RunMyProcess bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c3664-212">Log in tooyour RunMyProcess company site as an administrator.</span></span>

2. <span data-ttu-id="c3664-213">Klik op **Account** en selecteer **gebruikers** in het linkernavigatievenster, klik vervolgens op **nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="c3664-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="c3664-214">![Nieuwe gebruiker](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="c3664-214">![New User](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

3. <span data-ttu-id="c3664-215">In Hallo **gebruikersinstellingen** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c3664-215">In hello **User Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c3664-216">![Profiel](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "profiel")</span><span class="sxs-lookup"><span data-stu-id="c3664-216">![Profile](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="c3664-217">a.</span><span class="sxs-lookup"><span data-stu-id="c3664-217">a.</span></span> <span data-ttu-id="c3664-218">Type Hallo **naam** en **e** van een geldig Azure tekstvakken met betrekking tot AD-account u wilt dat tooprovision in Hallo.</span><span class="sxs-lookup"><span data-stu-id="c3664-218">Type hello **Name** and **E-mail** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="c3664-219">b.</span><span class="sxs-lookup"><span data-stu-id="c3664-219">b.</span></span> <span data-ttu-id="c3664-220">Selecteer een **IDE taal**, **taal**, en **profiel**.</span><span class="sxs-lookup"><span data-stu-id="c3664-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="c3664-221">c.</span><span class="sxs-lookup"><span data-stu-id="c3664-221">c.</span></span> <span data-ttu-id="c3664-222">Selecteer **verzenden account maken van het e-toome**.</span><span class="sxs-lookup"><span data-stu-id="c3664-222">Select **Send account creation e-mail toome**.</span></span> 

    <span data-ttu-id="c3664-223">d.</span><span class="sxs-lookup"><span data-stu-id="c3664-223">d.</span></span> <span data-ttu-id="c3664-224">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c3664-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="c3664-225">U kunt andere RunMyProcess gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door RunMyProcess tooprovision Azure Active Directory-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="c3664-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess tooprovision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c3664-226">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3664-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c3664-227">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooRunMyProcess toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="c3664-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRunMyProcess.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c3664-229">**tooassign Britta Simon tooRunMyProcess, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c3664-229">**tooassign Britta Simon tooRunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3664-230">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c3664-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c3664-232">Selecteer in de lijst met de toepassingen van Hallo **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="c3664-232">In hello applications list, select **RunMyProcess**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. <span data-ttu-id="c3664-234">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c3664-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c3664-236">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c3664-236">Click **Add** button.</span></span> <span data-ttu-id="c3664-237">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c3664-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c3664-239">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="c3664-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c3664-240">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c3664-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c3664-241">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c3664-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c3664-242">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c3664-242">Testing single sign-on</span></span>

<span data-ttu-id="c3664-243">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="c3664-243">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="c3664-244">Als u op Hallo RunMyProcess-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour RunMyProcess toepassing.</span><span class="sxs-lookup"><span data-stu-id="c3664-244">When you click hello RunMyProcess tile in hello Access Panel, you should get automatically signed-on tooyour RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c3664-245">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c3664-245">Additional resources</span></span>

* [<span data-ttu-id="c3664-246">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3664-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c3664-247">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c3664-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

