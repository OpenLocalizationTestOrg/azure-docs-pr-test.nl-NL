---
title: 'Zelfstudie: Azure Active Directory-integratie met kruipen dicht | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en kruipen dicht.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 0b2f6c4d839943cdd07699a1ff95dc8f90505699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="245bf-103">Zelfstudie: Azure Active Directory-integratie met kruipen dicht</span><span class="sxs-lookup"><span data-stu-id="245bf-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="245bf-104">In deze zelfstudie leert u hoe toointegrate kruipen dicht bij Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="245bf-104">In this tutorial, you learn how toointegrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="245bf-105">Kruipen dicht integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="245bf-105">Integrating Huddle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="245bf-106">U kunt beheren in Azure AD die tooHuddle toegang heeft</span><span class="sxs-lookup"><span data-stu-id="245bf-106">You can control in Azure AD who has access tooHuddle</span></span>
- <span data-ttu-id="245bf-107">U kunt uw gebruikers tooautomatically get aangemelde tooHuddle (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="245bf-107">You can enable your users tooautomatically get signed-on tooHuddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="245bf-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="245bf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="245bf-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="245bf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="245bf-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="245bf-110">Prerequisites</span></span>

<span data-ttu-id="245bf-111">tooconfigure Azure AD-integratie met kruipen dicht, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="245bf-111">tooconfigure Azure AD integration with Huddle, you need hello following items:</span></span>

- <span data-ttu-id="245bf-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="245bf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="245bf-113">Een kruipen dicht eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="245bf-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="245bf-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="245bf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="245bf-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="245bf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="245bf-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="245bf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="245bf-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="245bf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="245bf-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="245bf-118">Scenario description</span></span>

<span data-ttu-id="245bf-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="245bf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="245bf-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="245bf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="245bf-121">Het toevoegen van kruipen dicht van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="245bf-121">Adding Huddle from hello gallery</span></span>
2. <span data-ttu-id="245bf-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="245bf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-hello-gallery"></a><span data-ttu-id="245bf-123">Het toevoegen van kruipen dicht van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="245bf-123">Adding Huddle from hello gallery</span></span>
<span data-ttu-id="245bf-124">tooconfigure hello integratie van kruipen dicht in Azure AD, moet u tooadd kruipen dicht in Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="245bf-124">tooconfigure hello integration of Huddle into Azure AD, you need tooadd Huddle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="245bf-125">**tooadd kruipen dicht in de galerie Hallo, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="245bf-125">**tooadd Huddle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="245bf-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="245bf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="245bf-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="245bf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="245bf-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="245bf-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="245bf-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="245bf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="245bf-133">Typ in het zoekvak Hallo **kruipen dicht**.</span><span class="sxs-lookup"><span data-stu-id="245bf-133">In hello search box, type **Huddle**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="245bf-135">Selecteer in het deelvenster resultaten hello, **kruipen dicht**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="245bf-135">In hello results panel, select **Huddle**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="245bf-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="245bf-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="245bf-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met kruipen dicht op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="245bf-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="245bf-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in kruipen dicht is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="245bf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Huddle is tooa user in Azure AD.</span></span> <span data-ttu-id="245bf-140">Met andere woorden, een relatie koppeling tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in kruipen dicht behoeften toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="245bf-140">In other words, a link relationship between an Azure AD user and hello related user in Huddle needs toobe established.</span></span>

<span data-ttu-id="245bf-141">Wijs in het kruipen dicht, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="245bf-141">In Huddle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="245bf-142">tooconfigure en eenmalige aanmelding Azure AD-test met kruipen dicht, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="245bf-142">tooconfigure and test Azure AD single sign-on with Huddle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="245bf-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="245bf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>

2. <span data-ttu-id="245bf-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="245bf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="245bf-145">**[Maken van een testgebruiker kruipen dicht](#creating-a-huddle-test-user)**  -toohave een equivalent van Britta Simon in kruipen dicht die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="245bf-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - toohave a counterpart of Britta Simon in Huddle that is linked toohello Azure AD representation of user.</span></span>

4. <span data-ttu-id="245bf-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="245bf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>

5. <span data-ttu-id="245bf-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="245bf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="245bf-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="245bf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="245bf-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing kruipen dicht configureren.</span><span class="sxs-lookup"><span data-stu-id="245bf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="245bf-150">**tooconfigure eenmalige aanmelding Azure AD met kruipen dicht, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="245bf-150">**tooconfigure Azure AD single sign-on with Huddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="245bf-151">In de Azure-portal op Hallo Hallo **kruipen dicht** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="245bf-151">In hello Azure portal, on hello **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="245bf-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="245bf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="245bf-155">Op Hallo **kruipen dicht domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="245bf-155">On hello **Huddle Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="245bf-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`http://<company name>.huddle.com`</span><span class="sxs-lookup"><span data-stu-id="245bf-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="245bf-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="245bf-158">This value is not real.</span></span> <span data-ttu-id="245bf-159">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="245bf-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="245bf-160">Neem contact op met [Client kruipen dicht ondersteuningsteam](https://huddle.zendesk.com) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="245bf-160">Contact [Huddle Client support team](https://huddle.zendesk.com) tooget this value.</span></span> 

4. <span data-ttu-id="245bf-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="245bf-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="245bf-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="245bf-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="245bf-165">Op Hallo **kruipen dicht configuratie** sectie, klikt u op **configureren kruipen dicht** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="245bf-165">On hello **Huddle Configuration** section, click **Configure Huddle** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="245bf-166">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="245bf-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="245bf-168">tooconfigure eenmalige aanmelding kruipen dicht zijde, moet u toosend Hallo gedownload **certificaat**, **SAML Single Sign-On Service-URL**, en **SAML entiteit-ID** te[Client kruipen dicht ondersteuningsteam](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="245bf-168">tooconfigure single sign-on on Huddle side, you need toosend hello downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="245bf-169">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="245bf-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="245bf-170">Eenmalige aanmelding moet toobe ingeschakeld door Hallo kruipen dicht ondersteuningsteam.</span><span class="sxs-lookup"><span data-stu-id="245bf-170">Single sign-on needs toobe enabled by hello Huddle support team.</span></span> <span data-ttu-id="245bf-171">U krijgt een melding wanneer het Hallo-configuratie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="245bf-171">You get a notification when hello configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="245bf-172">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="245bf-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="245bf-173">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="245bf-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="245bf-174">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="245bf-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="245bf-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="245bf-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="245bf-176">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="245bf-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="245bf-178">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="245bf-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="245bf-179">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="245bf-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="245bf-181">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="245bf-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="245bf-183">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="245bf-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="245bf-185">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="245bf-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="245bf-187">a.</span><span class="sxs-lookup"><span data-stu-id="245bf-187">a.</span></span> <span data-ttu-id="245bf-188">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="245bf-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="245bf-189">b.</span><span class="sxs-lookup"><span data-stu-id="245bf-189">b.</span></span> <span data-ttu-id="245bf-190">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="245bf-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="245bf-191">c.</span><span class="sxs-lookup"><span data-stu-id="245bf-191">c.</span></span> <span data-ttu-id="245bf-192">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="245bf-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="245bf-193">d.</span><span class="sxs-lookup"><span data-stu-id="245bf-193">d.</span></span> <span data-ttu-id="245bf-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="245bf-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="245bf-195">Een testgebruiker kruipen dicht maken</span><span class="sxs-lookup"><span data-stu-id="245bf-195">Creating a Huddle test user</span></span>

<span data-ttu-id="245bf-196">Azure AD tooenable gebruikers toolog in tooHuddle, ze in kruipen dicht moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="245bf-196">tooenable Azure AD users toolog in tooHuddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="245bf-197">In geval van kruipen dicht Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="245bf-197">In hello case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="245bf-198">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="245bf-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="245bf-199">Meld u bij tooyour **kruipen dicht** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="245bf-199">Log in tooyour **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="245bf-200">Klik op **werkruimte**.</span><span class="sxs-lookup"><span data-stu-id="245bf-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="245bf-201">Klik op **mensen \> personen uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="245bf-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="245bf-202">![Mensen](./media/active-directory-saas-huddle-tutorial/IC787838.png "personen")</span><span class="sxs-lookup"><span data-stu-id="245bf-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="245bf-203">In Hallo **maken van een nieuwe uitnodiging** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="245bf-203">In hello **Create a new invitation** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="245bf-204">![Nieuwe uitnodiging](./media/active-directory-saas-huddle-tutorial/IC787839.png "nieuwe uitnodiging")</span><span class="sxs-lookup"><span data-stu-id="245bf-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="245bf-205">a.</span><span class="sxs-lookup"><span data-stu-id="245bf-205">a.</span></span> <span data-ttu-id="245bf-206">In Hallo **Kies een team tooinvite mensen toojoin** selecteert **team**.</span><span class="sxs-lookup"><span data-stu-id="245bf-206">In hello **Choose a team tooinvite people toojoin** list, select **team**.</span></span>

   <span data-ttu-id="245bf-207">b.</span><span class="sxs-lookup"><span data-stu-id="245bf-207">b.</span></span> <span data-ttu-id="245bf-208">Type Hallo **e-mailadres** van een geldige Azure AD-account in de gewenste tooprovision te**Enter e-mailadres voor mensen gewenst tooinvite** textbox.</span><span class="sxs-lookup"><span data-stu-id="245bf-208">Type hello **Email Address** of a valid Azure AD account you want tooprovision in too**Enter email address for people you'd like tooinvite** textbox.</span></span>

   <span data-ttu-id="245bf-209">c.</span><span class="sxs-lookup"><span data-stu-id="245bf-209">c.</span></span> <span data-ttu-id="245bf-210">Klik op **uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="245bf-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="245bf-211">Hello Azure AD-account houder ontvangt een e-mail met inbegrip van een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="245bf-211">hello Azure AD account holder will receive an email including a link tooconfirm hello account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="245bf-212">U kunt andere kruipen dicht gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door tooprovision kruipen dicht Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="245bf-212">You can use any other Huddle user account creation tools or APIs provided by Huddle tooprovision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="245bf-213">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="245bf-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="245bf-214">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooHuddle toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="245bf-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHuddle.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="245bf-216">**tooassign Britta Simon tooHuddle, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="245bf-216">**tooassign Britta Simon tooHuddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="245bf-217">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="245bf-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="245bf-219">Selecteer in de lijst met de toepassingen van Hallo **kruipen dicht**.</span><span class="sxs-lookup"><span data-stu-id="245bf-219">In hello applications list, select **Huddle**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="245bf-221">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="245bf-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="245bf-223">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="245bf-223">Click **Add** button.</span></span> <span data-ttu-id="245bf-224">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="245bf-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="245bf-226">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="245bf-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="245bf-227">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="245bf-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="245bf-228">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="245bf-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="245bf-229">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="245bf-229">Testing single sign-on</span></span>

<span data-ttu-id="245bf-230">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="245bf-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="245bf-231">Wanneer u Hallo kruipen dicht tegel in Hallo toegangsvenster klikt, moet u de aanmeldingspagina van toepassing kruipen dicht automatisch ophalen.</span><span class="sxs-lookup"><span data-stu-id="245bf-231">When you click hello Huddle tile in hello Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="245bf-232">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="245bf-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="245bf-233">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="245bf-233">Additional resources</span></span>

* [<span data-ttu-id="245bf-234">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="245bf-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="245bf-235">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="245bf-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
