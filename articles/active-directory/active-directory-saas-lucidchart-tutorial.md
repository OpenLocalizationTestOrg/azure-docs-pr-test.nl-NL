---
title: 'Zelfstudie: Azure Active Directory-integratie met Lucidchart | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Lucidchart.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 774e5f423097650a3cae8e8ca13b2c65b8470736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="f721b-103">Zelfstudie: Azure Active Directory-integratie met Lucidchart</span><span class="sxs-lookup"><span data-stu-id="f721b-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>

<span data-ttu-id="f721b-104">In deze zelfstudie leert u hoe toointegrate Lucidchart met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f721b-104">In this tutorial, you learn how toointegrate Lucidchart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f721b-105">Lucidchart integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f721b-105">Integrating Lucidchart with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f721b-106">U kunt beheren in Azure AD die tooLucidchart toegang heeft</span><span class="sxs-lookup"><span data-stu-id="f721b-106">You can control in Azure AD who has access tooLucidchart</span></span>
- <span data-ttu-id="f721b-107">U kunt uw gebruikers tooautomatically get aangemelde tooLucidchart (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="f721b-107">You can enable your users tooautomatically get signed-on tooLucidchart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f721b-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f721b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f721b-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f721b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f721b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f721b-110">Prerequisites</span></span>

<span data-ttu-id="f721b-111">Azure AD-integratie met Lucidchart tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="f721b-111">tooconfigure Azure AD integration with Lucidchart, you need hello following items:</span></span>

- <span data-ttu-id="f721b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f721b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f721b-113">Een Lucidchart eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f721b-113">A Lucidchart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f721b-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f721b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f721b-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f721b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f721b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f721b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f721b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f721b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f721b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f721b-118">Scenario description</span></span>
<span data-ttu-id="f721b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f721b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f721b-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f721b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f721b-121">Het toevoegen van Lucidchart van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f721b-121">Adding Lucidchart from hello gallery</span></span>
2. <span data-ttu-id="f721b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f721b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lucidchart-from-hello-gallery"></a><span data-ttu-id="f721b-123">Het toevoegen van Lucidchart van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f721b-123">Adding Lucidchart from hello gallery</span></span>
<span data-ttu-id="f721b-124">tooconfigure hello integratie van Lucidchart in Azure AD, moet u tooadd Lucidchart uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f721b-124">tooconfigure hello integration of Lucidchart into Azure AD, you need tooadd Lucidchart from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f721b-125">**tooadd Lucidchart via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f721b-125">**tooadd Lucidchart from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f721b-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f721b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f721b-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f721b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f721b-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f721b-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f721b-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f721b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f721b-133">Typ in het zoekvak Hallo **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="f721b-133">In hello search box, type **Lucidchart**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. <span data-ttu-id="f721b-135">Selecteer in het deelvenster resultaten hello, **Lucidchart**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f721b-135">In hello results panel, select **Lucidchart**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f721b-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f721b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f721b-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Lucidchart op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f721b-138">In this section, you configure and test Azure AD single sign-on with Lucidchart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f721b-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Lucidchart is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f721b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lucidchart is tooa user in Azure AD.</span></span> <span data-ttu-id="f721b-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Lucidchart toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="f721b-140">In other words, a link relationship between an Azure AD user and hello related user in Lucidchart needs toobe established.</span></span>

<span data-ttu-id="f721b-141">Wijs in Lucidchart, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="f721b-141">In Lucidchart, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f721b-142">tooconfigure en eenmalige aanmelding Azure AD-test met Lucidchart, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f721b-142">tooconfigure and test Azure AD single sign-on with Lucidchart, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f721b-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="f721b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f721b-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f721b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f721b-145">**[Maken van een testgebruiker Lucidchart](#creating-a-lucidchart-test-user)**  -toohave een equivalent van Britta Simon in Lucidchart die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f721b-145">**[Creating a Lucidchart test user](#creating-a-lucidchart-test-user)** - toohave a counterpart of Britta Simon in Lucidchart that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f721b-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f721b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f721b-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f721b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f721b-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f721b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f721b-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Lucidchart configureren.</span><span class="sxs-lookup"><span data-stu-id="f721b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lucidchart application.</span></span>

<span data-ttu-id="f721b-150">**Azure AD tooconfigure eenmalige aanmelding met Lucidchart, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f721b-150">**tooconfigure Azure AD single sign-on with Lucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="f721b-151">In de Azure-portal op Hallo Hallo **Lucidchart** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f721b-151">In hello Azure portal, on hello **Lucidchart** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f721b-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f721b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. <span data-ttu-id="f721b-155">Op Hallo **Lucidchart domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f721b-155">On hello **Lucidchart Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    <span data-ttu-id="f721b-157">In Hallo **aanmeldings-URL** textbox, typ een URL als:`https://chart2.office.lucidchart.com/saml/sso/azure`</span><span class="sxs-lookup"><span data-stu-id="f721b-157">In hello **Sign-on URL** textbox, type a URL as: `https://chart2.office.lucidchart.com/saml/sso/azure`</span></span>

4. <span data-ttu-id="f721b-158">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f721b-158">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. <span data-ttu-id="f721b-160">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f721b-160">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f721b-162">In een ander browservenster, meld u bij uw bedrijf Lucidchart site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f721b-162">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>

7. <span data-ttu-id="f721b-163">Klik in het menu bovenaan Hallo Hallo **Team**.</span><span class="sxs-lookup"><span data-stu-id="f721b-163">In hello menu on hello top, click **Team**.</span></span>
   
    <span data-ttu-id="f721b-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span><span class="sxs-lookup"><span data-stu-id="f721b-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span></span>

8. <span data-ttu-id="f721b-165">Klik op **toepassingen \> SAML beheren**.</span><span class="sxs-lookup"><span data-stu-id="f721b-165">Click **Applications \> Manage SAML**.</span></span>
   
    <span data-ttu-id="f721b-166">![Beheren van SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "SAML beheren")</span><span class="sxs-lookup"><span data-stu-id="f721b-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML")</span></span>

9. <span data-ttu-id="f721b-167">Op Hallo **SAML-verificatie-instellingen** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f721b-167">On hello **SAML Authentication Settings** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="f721b-168">a.</span><span class="sxs-lookup"><span data-stu-id="f721b-168">a.</span></span> <span data-ttu-id="f721b-169">Selecteer **SAML-verificatie inschakelen**, en klik vervolgens op **optioneel**.</span><span class="sxs-lookup"><span data-stu-id="f721b-169">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

    <span data-ttu-id="f721b-170">![Verificatie-instellingen van SAML](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML-verificatie-instellingen")</span><span class="sxs-lookup"><span data-stu-id="f721b-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings")</span></span>
 
    <span data-ttu-id="f721b-171">b.</span><span class="sxs-lookup"><span data-stu-id="f721b-171">b.</span></span> <span data-ttu-id="f721b-172">In Hallo **domein** textbox, typt u uw domein en klik vervolgens op **wijziging certificaat**.</span><span class="sxs-lookup"><span data-stu-id="f721b-172">In hello **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

    <span data-ttu-id="f721b-173">![Certificaat wijzigen](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "-certificaat wijzigen")</span><span class="sxs-lookup"><span data-stu-id="f721b-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate")</span></span>
 
    <span data-ttu-id="f721b-174">c.</span><span class="sxs-lookup"><span data-stu-id="f721b-174">c.</span></span> <span data-ttu-id="f721b-175">Open uw gedownloade metagegevensbestand, kopie Hallo inhoud en plak deze in Hallo **metagegevens uploaden** textbox.</span><span class="sxs-lookup"><span data-stu-id="f721b-175">Open your downloaded metadata file, copy hello content, and then paste it into hello **Upload Metadata** textbox.</span></span>

    <span data-ttu-id="f721b-176">![Uploaden van metagegevens](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "metagegevens uploaden")</span><span class="sxs-lookup"><span data-stu-id="f721b-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata")</span></span>
 
    <span data-ttu-id="f721b-177">d.</span><span class="sxs-lookup"><span data-stu-id="f721b-177">d.</span></span> <span data-ttu-id="f721b-178">Selecteer **automatisch toevoegen van nieuwe gebruikers toohello team**, en klik vervolgens op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f721b-178">Select **Automatically Add new users toohello team**, and then click **Save changes**.</span></span>

    <span data-ttu-id="f721b-179">![Wijzigingen opslaan](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "wijzigingen opslaan")</span><span class="sxs-lookup"><span data-stu-id="f721b-179">![Save Changes](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Save Changes")</span></span>

> [!TIP]
> <span data-ttu-id="f721b-180">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="f721b-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f721b-181">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="f721b-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f721b-182">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f721b-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f721b-183">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f721b-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="f721b-184">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f721b-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f721b-186">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f721b-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f721b-187">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f721b-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f721b-189">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f721b-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f721b-191">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="f721b-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f721b-193">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f721b-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f721b-195">a.</span><span class="sxs-lookup"><span data-stu-id="f721b-195">a.</span></span> <span data-ttu-id="f721b-196">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f721b-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f721b-197">b.</span><span class="sxs-lookup"><span data-stu-id="f721b-197">b.</span></span> <span data-ttu-id="f721b-198">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f721b-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f721b-199">c.</span><span class="sxs-lookup"><span data-stu-id="f721b-199">c.</span></span> <span data-ttu-id="f721b-200">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f721b-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f721b-201">d.</span><span class="sxs-lookup"><span data-stu-id="f721b-201">d.</span></span> <span data-ttu-id="f721b-202">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f721b-202">Click **Create**.</span></span>
 
### <a name="creating-a-lucidchart-test-user"></a><span data-ttu-id="f721b-203">Een testgebruiker Lucidchart maken</span><span class="sxs-lookup"><span data-stu-id="f721b-203">Creating a Lucidchart test user</span></span>

<span data-ttu-id="f721b-204">Er is geen actie-item voor u tooconfigure gebruikers inrichten tooLucidchart.</span><span class="sxs-lookup"><span data-stu-id="f721b-204">There is no action item for you tooconfigure user provisioning tooLucidchart.</span></span>  <span data-ttu-id="f721b-205">Wanneer een toegewezen gebruiker toolog in Lucidchart met behulp van het toegangsvenster hello probeert, controleert Lucidchart of Hallo gebruiker bestaat.</span><span class="sxs-lookup"><span data-stu-id="f721b-205">When an assigned user tries toolog into Lucidchart using hello access panel, Lucidchart checks whether hello user exists.</span></span>  

<span data-ttu-id="f721b-206">Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="f721b-206">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f721b-207">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f721b-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f721b-208">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooLucidchart toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="f721b-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLucidchart.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f721b-210">**tooassign Britta Simon tooLucidchart, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f721b-210">**tooassign Britta Simon tooLucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="f721b-211">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f721b-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f721b-213">Selecteer in de lijst met de toepassingen van Hallo **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="f721b-213">In hello applications list, select **Lucidchart**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. <span data-ttu-id="f721b-215">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f721b-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f721b-217">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f721b-217">Click **Add** button.</span></span> <span data-ttu-id="f721b-218">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f721b-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f721b-220">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="f721b-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f721b-221">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f721b-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f721b-222">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f721b-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f721b-223">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f721b-223">Testing single sign-on</span></span>

<span data-ttu-id="f721b-224">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="f721b-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f721b-225">Als u op Hallo Lucidchart tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Lucidchart toepassing.</span><span class="sxs-lookup"><span data-stu-id="f721b-225">When you click hello Lucidchart tile in hello Access Panel, you should get automatically signed-on tooyour Lucidchart application.</span></span>
<span data-ttu-id="f721b-226">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f721b-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f721b-227">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f721b-227">Additional resources</span></span>

* [<span data-ttu-id="f721b-228">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f721b-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f721b-229">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f721b-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png

