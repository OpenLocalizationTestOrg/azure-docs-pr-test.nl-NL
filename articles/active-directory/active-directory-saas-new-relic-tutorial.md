---
title: 'Zelfstudie: Azure Active Directory-integratie met New Relic | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en de New Relic.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: dc8f0df3b18a32bde155e8911a581fc5f91af217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="0a187-103">Zelfstudie: Azure Active Directory-integratie met New Relic</span><span class="sxs-lookup"><span data-stu-id="0a187-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="0a187-104">In deze zelfstudie leert u hoe toointegrate New Relic met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a187-104">In this tutorial, you learn how toointegrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a187-105">New Relic integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="0a187-105">Integrating New Relic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0a187-106">U kunt beheren in Azure AD wie toegang tot tooNew Relic heeft</span><span class="sxs-lookup"><span data-stu-id="0a187-106">You can control in Azure AD who has access tooNew Relic</span></span>
- <span data-ttu-id="0a187-107">U kunt uw gebruikers tooautomatically get aangemelde tooNew Relic (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="0a187-107">You can enable your users tooautomatically get signed-on tooNew Relic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0a187-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="0a187-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0a187-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0a187-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a187-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0a187-110">Prerequisites</span></span>

<span data-ttu-id="0a187-111">Azure AD-integratie met New Relic tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="0a187-111">tooconfigure Azure AD integration with New Relic, you need hello following items:</span></span>

- <span data-ttu-id="0a187-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="0a187-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a187-113">Een New Relic eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="0a187-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a187-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="0a187-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a187-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="0a187-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a187-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="0a187-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a187-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a187-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a187-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="0a187-118">Scenario description</span></span>
<span data-ttu-id="0a187-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="0a187-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a187-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="0a187-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a187-121">Het toevoegen van New Relic van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="0a187-121">Adding New Relic from hello gallery</span></span>
2. <span data-ttu-id="0a187-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0a187-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-hello-gallery"></a><span data-ttu-id="0a187-123">Het toevoegen van New Relic van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="0a187-123">Adding New Relic from hello gallery</span></span>
<span data-ttu-id="0a187-124">tooconfigure hello integratie van New Relic in Azure AD, moet u tooadd New Relic in Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="0a187-124">tooconfigure hello integration of New Relic into Azure AD, you need tooadd New Relic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0a187-125">**New Relic via Hallo gallery tooadd uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0a187-125">**tooadd New Relic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a187-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0a187-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0a187-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0a187-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0a187-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0a187-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="0a187-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0a187-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="0a187-133">Typ in het zoekvak Hallo **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="0a187-133">In hello search box, type **New Relic**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. <span data-ttu-id="0a187-135">Selecteer in het deelvenster resultaten hello, **New Relic**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0a187-135">In hello results panel, select **New Relic**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0a187-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0a187-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0a187-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met New Relic op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="0a187-138">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0a187-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in New Relic is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a187-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in New Relic is tooa user in Azure AD.</span></span> <span data-ttu-id="0a187-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in New Relic toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="0a187-140">In other words, a link relationship between an Azure AD user and hello related user in New Relic needs toobe established.</span></span>

<span data-ttu-id="0a187-141">Wijs in New Relic Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="0a187-141">In New Relic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0a187-142">tooconfigure en test eenmalige aanmelding Azure AD met behulp van New Relic, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0a187-142">tooconfigure and test Azure AD single sign-on with New Relic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0a187-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="0a187-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0a187-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a187-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a187-145">**[Maken van een New Relic-testgebruiker](#creating-a-new-relic-test-user)**  -toohave een equivalent van Britta Simon in New Relic die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="0a187-145">**[Creating a New Relic test user](#creating-a-new-relic-test-user)** - toohave a counterpart of Britta Simon in New Relic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0a187-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0a187-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0a187-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="0a187-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0a187-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="0a187-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0a187-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing New Relic configureren.</span><span class="sxs-lookup"><span data-stu-id="0a187-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="0a187-150">**Voer tooconfigure Azure AD eenmalige aanmelding met New Relic Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0a187-150">**tooconfigure Azure AD single sign-on with New Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a187-151">In de Azure-portal op Hallo Hallo **New Relic** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="0a187-151">In hello Azure portal, on hello **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="0a187-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0a187-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. <span data-ttu-id="0a187-155">Op Hallo **nieuwe Relic domein en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0a187-155">On hello **New Relic Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    <span data-ttu-id="0a187-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="0a187-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.newrelic.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0a187-158">Hallo-waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="0a187-158">hello value is not real.</span></span> <span data-ttu-id="0a187-159">Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="0a187-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="0a187-160">Neem contact op met [nieuwe Relic Client ondersteuningsteam](https://support.newrelic.com/) tooget Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="0a187-160">Contact [New Relic Client support team](https://support.newrelic.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="0a187-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="0a187-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. <span data-ttu-id="0a187-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="0a187-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0a187-165">Op Hallo **nieuwe Relic configuratie** sectie, klikt u op **New Relic configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="0a187-165">On hello **New Relic Configuration** section, click **Configure New Relic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0a187-166">Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="0a187-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. <span data-ttu-id="0a187-168">Een ander browservenster, meld u aan bij tooyour **New Relic** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="0a187-168">In a different web browser window, sign on tooyour **New Relic** company site as administrator.</span></span>

8. <span data-ttu-id="0a187-169">Klik in het menu bovenaan Hallo Hallo **Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="0a187-169">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="0a187-170">![Instellingen account](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Accountinstellingen")</span><span class="sxs-lookup"><span data-stu-id="0a187-170">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Account Settings")</span></span>

9. <span data-ttu-id="0a187-171">Klik op Hallo **beveiligings- en** tabblad en klik vervolgens op Hallo **eenmalige aanmelding** tabblad.</span><span class="sxs-lookup"><span data-stu-id="0a187-171">Click hello **Security and authentication** tab, and then click hello **Single sign on** tab.</span></span>
   
    <span data-ttu-id="0a187-172">![Eenmalige aanmelding](./media/active-directory-saas-new-relic-tutorial/ic797037.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="0a187-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

10. <span data-ttu-id="0a187-173">Voer op Hallo SAML dialoogvenster pagina Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0a187-173">On hello SAML dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="0a187-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="0a187-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="0a187-175">a.</span><span class="sxs-lookup"><span data-stu-id="0a187-175">a.</span></span> <span data-ttu-id="0a187-176">Klik op **bestand kiezen** tooupload uw gedownloade Azure Active Directory-certificaat.</span><span class="sxs-lookup"><span data-stu-id="0a187-176">Click **Choose File** tooupload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="0a187-177">b.</span><span class="sxs-lookup"><span data-stu-id="0a187-177">b.</span></span> <span data-ttu-id="0a187-178">In Hallo **externe aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0a187-178">In hello **Remote login URL** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="0a187-179">c.</span><span class="sxs-lookup"><span data-stu-id="0a187-179">c.</span></span> <span data-ttu-id="0a187-180">In Hallo **afmelding aanvoer URL** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0a187-180">In hello **Logout landing URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="0a187-181">d.</span><span class="sxs-lookup"><span data-stu-id="0a187-181">d.</span></span> <span data-ttu-id="0a187-182">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="0a187-182">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="0a187-183">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="0a187-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0a187-184">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="0a187-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0a187-185">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0a187-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0a187-186">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="0a187-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="0a187-187">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0a187-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="0a187-189">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0a187-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a187-190">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0a187-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0a187-192">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="0a187-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0a187-194">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="0a187-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0a187-196">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0a187-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0a187-198">a.</span><span class="sxs-lookup"><span data-stu-id="0a187-198">a.</span></span> <span data-ttu-id="0a187-199">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a187-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a187-200">b.</span><span class="sxs-lookup"><span data-stu-id="0a187-200">b.</span></span> <span data-ttu-id="0a187-201">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0a187-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0a187-202">c.</span><span class="sxs-lookup"><span data-stu-id="0a187-202">c.</span></span> <span data-ttu-id="0a187-203">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="0a187-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0a187-204">d.</span><span class="sxs-lookup"><span data-stu-id="0a187-204">d.</span></span> <span data-ttu-id="0a187-205">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0a187-205">Click **Create**.</span></span>
 
### <a name="creating-a-new-relic-test-user"></a><span data-ttu-id="0a187-206">De gebruiker van een New Relic-test maken</span><span class="sxs-lookup"><span data-stu-id="0a187-206">Creating a New Relic test user</span></span>

<span data-ttu-id="0a187-207">In de volgorde tooenable Azure Active Directory gebruikers toolog in tooNew Relic, moeten ze worden ingericht in New Relic.</span><span class="sxs-lookup"><span data-stu-id="0a187-207">In order tooenable Azure Active Directory users toolog in tooNew Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="0a187-208">In geval van New Relic Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="0a187-208">In hello case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="0a187-209">**een gebruiker account tooNew Relic, tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0a187-209">**tooprovision a user account tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a187-210">Meld u bij tooyour **New Relic** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="0a187-210">Log in tooyour **New Relic** company site as administrator.</span></span>

2. <span data-ttu-id="0a187-211">Klik in het menu bovenaan Hallo Hallo **Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="0a187-211">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="0a187-212">![Instellingen account](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Accountinstellingen")</span><span class="sxs-lookup"><span data-stu-id="0a187-212">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Account Settings")</span></span>

3. <span data-ttu-id="0a187-213">In Hallo **Account** deelvenster op Hallo linkerkant, klikt u op **samenvatting**, en klik vervolgens op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="0a187-213">In hello **Account** pane on hello left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="0a187-214">![Instellingen account](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Accountinstellingen")</span><span class="sxs-lookup"><span data-stu-id="0a187-214">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Account Settings")</span></span>

4. <span data-ttu-id="0a187-215">Op Hallo **actieve gebruikers** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="0a187-215">On hello **Active users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="0a187-216">![Actieve gebruikers](./media/active-directory-saas-new-relic-tutorial/ic797042.png "actieve gebruikers")</span><span class="sxs-lookup"><span data-stu-id="0a187-216">![Active Users](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="0a187-217">a.</span><span class="sxs-lookup"><span data-stu-id="0a187-217">a.</span></span> <span data-ttu-id="0a187-218">In Hallo **e** textbox Hallo type e-mailadres van een geldige Azure Active Directory-gebruiker gewenste tooprovision.</span><span class="sxs-lookup"><span data-stu-id="0a187-218">In hello **Email** textbox, type hello email address of a valid Azure Active Directory user you want tooprovision.</span></span>

    <span data-ttu-id="0a187-219">b.</span><span class="sxs-lookup"><span data-stu-id="0a187-219">b.</span></span> <span data-ttu-id="0a187-220">Als **rol** Selecteer **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="0a187-220">As **Role** select **User**.</span></span>

    <span data-ttu-id="0a187-221">c.</span><span class="sxs-lookup"><span data-stu-id="0a187-221">c.</span></span> <span data-ttu-id="0a187-222">Klik op **deze gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="0a187-222">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="0a187-223">U kunt andere New Relic gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door New Relic tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="0a187-223">You can use any other New Relic user account creation tools or APIs provided by New Relic tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0a187-224">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a187-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0a187-225">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooNew Relic.</span><span class="sxs-lookup"><span data-stu-id="0a187-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNew Relic.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="0a187-227">**tooassign Britta Simon tooNew Relic, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0a187-227">**tooassign Britta Simon tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a187-228">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0a187-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="0a187-230">Selecteer in de lijst met de toepassingen van Hallo **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="0a187-230">In hello applications list, select **New Relic**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. <span data-ttu-id="0a187-232">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="0a187-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="0a187-234">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="0a187-234">Click **Add** button.</span></span> <span data-ttu-id="0a187-235">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0a187-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="0a187-237">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="0a187-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0a187-238">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0a187-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a187-239">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0a187-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0a187-240">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0a187-240">Testing single sign-on</span></span>

<span data-ttu-id="0a187-241">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="0a187-241">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0a187-242">Als u op Hallo New Relic-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour New Relic-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0a187-242">When you click hello New Relic tile in hello Access Panel, you should get automatically signed-on tooyour New Relic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0a187-243">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="0a187-243">Additional resources</span></span>

* [<span data-ttu-id="0a187-244">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a187-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a187-245">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0a187-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

