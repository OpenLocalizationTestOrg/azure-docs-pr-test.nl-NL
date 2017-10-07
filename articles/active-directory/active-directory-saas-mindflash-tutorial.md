---
title: 'Zelfstudie: Azure Active Directory-integratie met Mindflash | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Mindflash.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdf91993-aaaa-4598-89b7-77ef8ca065d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a1bc327ea3867287103acbb64d30f0a8d7d4c5e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mindflash"></a><span data-ttu-id="d72c7-103">Zelfstudie: Azure Active Directory-integratie met Mindflash</span><span class="sxs-lookup"><span data-stu-id="d72c7-103">Tutorial: Azure Active Directory integration with Mindflash</span></span>

<span data-ttu-id="d72c7-104">In deze zelfstudie leert u hoe toointegrate Mindflash met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d72c7-104">In this tutorial, you learn how toointegrate Mindflash with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d72c7-105">Mindflash integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d72c7-105">Integrating Mindflash with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d72c7-106">U kunt beheren in Azure AD die tooMindflash toegang heeft</span><span class="sxs-lookup"><span data-stu-id="d72c7-106">You can control in Azure AD who has access tooMindflash</span></span>
- <span data-ttu-id="d72c7-107">U kunt uw gebruikers tooautomatically get aangemelde tooMindflash (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="d72c7-107">You can enable your users tooautomatically get signed-on tooMindflash (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d72c7-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="d72c7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d72c7-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d72c7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d72c7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d72c7-110">Prerequisites</span></span>

<span data-ttu-id="d72c7-111">Azure AD-integratie met Mindflash tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="d72c7-111">tooconfigure Azure AD integration with Mindflash, you need hello following items:</span></span>

- <span data-ttu-id="d72c7-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="d72c7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d72c7-113">Een Mindflash eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="d72c7-113">A Mindflash single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d72c7-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d72c7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d72c7-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="d72c7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d72c7-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d72c7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d72c7-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d72c7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d72c7-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d72c7-118">Scenario description</span></span>
<span data-ttu-id="d72c7-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d72c7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d72c7-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d72c7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d72c7-121">Het toevoegen van Mindflash van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="d72c7-121">Adding Mindflash from hello gallery</span></span>
2. <span data-ttu-id="d72c7-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d72c7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mindflash-from-hello-gallery"></a><span data-ttu-id="d72c7-123">Het toevoegen van Mindflash van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="d72c7-123">Adding Mindflash from hello gallery</span></span>
<span data-ttu-id="d72c7-124">tooconfigure hello integratie van Mindflash in Azure AD, moet u tooadd Mindflash uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d72c7-124">tooconfigure hello integration of Mindflash into Azure AD, you need tooadd Mindflash from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d72c7-125">**tooadd Mindflash via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d72c7-125">**tooadd Mindflash from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d72c7-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d72c7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d72c7-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d72c7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d72c7-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d72c7-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d72c7-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d72c7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d72c7-133">Typ in het zoekvak Hallo **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="d72c7-133">In hello search box, type **Mindflash**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_search.png)

5. <span data-ttu-id="d72c7-135">Selecteer in het deelvenster resultaten hello, **Mindflash**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d72c7-135">In hello results panel, select **Mindflash**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d72c7-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d72c7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d72c7-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Mindflash op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="d72c7-138">In this section, you configure and test Azure AD single sign-on with Mindflash based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d72c7-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Mindflash is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d72c7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mindflash is tooa user in Azure AD.</span></span> <span data-ttu-id="d72c7-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Mindflash toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="d72c7-140">In other words, a link relationship between an Azure AD user and hello related user in Mindflash needs toobe established.</span></span>

<span data-ttu-id="d72c7-141">Wijs in Mindflash, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="d72c7-141">In Mindflash, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d72c7-142">tooconfigure en eenmalige aanmelding Azure AD-test met Mindflash, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d72c7-142">tooconfigure and test Azure AD single sign-on with Mindflash, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d72c7-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="d72c7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d72c7-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d72c7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d72c7-145">**[Maken van een testgebruiker Mindflash](#creating-a-mindflash-test-user)**  -toohave een equivalent van Britta Simon in Mindflash die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d72c7-145">**[Creating a Mindflash test user](#creating-a-mindflash-test-user)** - toohave a counterpart of Britta Simon in Mindflash that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d72c7-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d72c7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d72c7-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d72c7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d72c7-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d72c7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d72c7-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Mindflash configureren.</span><span class="sxs-lookup"><span data-stu-id="d72c7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mindflash application.</span></span>

<span data-ttu-id="d72c7-150">**Azure AD tooconfigure eenmalige aanmelding met Mindflash, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d72c7-150">**tooconfigure Azure AD single sign-on with Mindflash, perform hello following steps:**</span></span>

1. <span data-ttu-id="d72c7-151">In de Azure-portal op Hallo Hallo **Mindflash** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d72c7-151">In hello Azure portal, on hello **Mindflash** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d72c7-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d72c7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_samlbase.png)

3. <span data-ttu-id="d72c7-155">Op Hallo **Mindflash domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d72c7-155">On hello **Mindflash Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_url.png)

    <span data-ttu-id="d72c7-157">a.</span><span class="sxs-lookup"><span data-stu-id="d72c7-157">a.</span></span> <span data-ttu-id="d72c7-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="d72c7-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.mindflash.com`</span></span>

    <span data-ttu-id="d72c7-159">b.</span><span class="sxs-lookup"><span data-stu-id="d72c7-159">b.</span></span> <span data-ttu-id="d72c7-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="d72c7-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.mindflash.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d72c7-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="d72c7-161">These values are not real.</span></span> <span data-ttu-id="d72c7-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="d72c7-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d72c7-163">Neem contact op met [Mindflash Client ondersteuningsteam](https://www.mindflash.com/contact/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="d72c7-163">Contact [Mindflash Client support team](https://www.mindflash.com/contact/) tooget these values.</span></span> 
 


4. <span data-ttu-id="d72c7-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d72c7-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_certificate.png) 

5. <span data-ttu-id="d72c7-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d72c7-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mindflash-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d72c7-168">tooconfigure eenmalige aanmelding op **Mindflash** zijde, moet u toosend Hallo gedownload **Metadata XML** te[Mindflash ondersteuningsteam](https://www.mindflash.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="d72c7-168">tooconfigure single sign-on on **Mindflash** side, you need toosend hello downloaded **Metadata XML** too[Mindflash support team](https://www.mindflash.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="d72c7-169">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="d72c7-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d72c7-170">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="d72c7-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d72c7-171">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d72c7-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d72c7-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d72c7-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="d72c7-173">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d72c7-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d72c7-175">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d72c7-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d72c7-176">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d72c7-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mindflash-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d72c7-178">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="d72c7-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mindflash-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d72c7-180">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="d72c7-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mindflash-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d72c7-182">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d72c7-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mindflash-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d72c7-184">a.</span><span class="sxs-lookup"><span data-stu-id="d72c7-184">a.</span></span> <span data-ttu-id="d72c7-185">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d72c7-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d72c7-186">b.</span><span class="sxs-lookup"><span data-stu-id="d72c7-186">b.</span></span> <span data-ttu-id="d72c7-187">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d72c7-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d72c7-188">c.</span><span class="sxs-lookup"><span data-stu-id="d72c7-188">c.</span></span> <span data-ttu-id="d72c7-189">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d72c7-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d72c7-190">d.</span><span class="sxs-lookup"><span data-stu-id="d72c7-190">d.</span></span> <span data-ttu-id="d72c7-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d72c7-191">Click **Create**.</span></span>
 
### <a name="creating-a-mindflash-test-user"></a><span data-ttu-id="d72c7-192">Een testgebruiker Mindflash maken</span><span class="sxs-lookup"><span data-stu-id="d72c7-192">Creating a Mindflash test user</span></span>

<span data-ttu-id="d72c7-193">In de volgorde tooenable Azure AD gebruikers toolog in Mindflash, moeten ze worden ingericht in Mindflash.</span><span class="sxs-lookup"><span data-stu-id="d72c7-193">In order tooenable Azure AD users toolog into Mindflash, they must be provisioned into Mindflash.</span></span> <span data-ttu-id="d72c7-194">In geval van Mindflash Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="d72c7-194">In hello case of Mindflash, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="d72c7-195">tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="d72c7-195">tooprovision a user accounts, perform hello following steps:</span></span>

1. <span data-ttu-id="d72c7-196">Meld u bij tooyour **Mindflash** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="d72c7-196">Log in tooyour **Mindflash** company site as an administrator.</span></span>

2. <span data-ttu-id="d72c7-197">Ga te**gebruikers beheren**.</span><span class="sxs-lookup"><span data-stu-id="d72c7-197">Go too**Manage Users**.</span></span>
   
    <span data-ttu-id="d72c7-198">![Gebruikers beheren](./media/active-directory-saas-mindflash-tutorial/ic787140.png "gebruikers beheren")</span><span class="sxs-lookup"><span data-stu-id="d72c7-198">![Manage Users](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Manage Users")</span></span>

3. <span data-ttu-id="d72c7-199">Klik op Hallo **gebruikers toevoegen**, en klik vervolgens op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="d72c7-199">Click hello **Add Users**, and then click **New**.</span></span>

4. <span data-ttu-id="d72c7-200">In Hallo **nieuwe gebruikers toevoegen** sectie, voert u Hallo stappen uit te voeren van een geldig Azure AD-account die u wilt dat tooprovision:</span><span class="sxs-lookup"><span data-stu-id="d72c7-200">In hello **Add New Users** section, perform hello following steps of a valid Azure AD account you want tooprovision:</span></span>
   
    <span data-ttu-id="d72c7-201">![Nieuwe gebruikers toevoegen](./media/active-directory-saas-mindflash-tutorial/ic787141.png "nieuwe gebruikers toevoegen")</span><span class="sxs-lookup"><span data-stu-id="d72c7-201">![Add New Users](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Add New Users")</span></span>
   
    <span data-ttu-id="d72c7-202">a.</span><span class="sxs-lookup"><span data-stu-id="d72c7-202">a.</span></span> <span data-ttu-id="d72c7-203">In Hallo **voornaam** textbox type **voornaam** van Hallo gebruiker als **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d72c7-203">In hello **First name** textbox, type **First name** of hello user as **Britta**.</span></span>

    <span data-ttu-id="d72c7-204">b.</span><span class="sxs-lookup"><span data-stu-id="d72c7-204">b.</span></span> <span data-ttu-id="d72c7-205">In Hallo **achternaam** textbox type **achternaam** van Hallo gebruiker als **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d72c7-205">In hello **Last name** textbox, type **Last name** of hello user as **Simon**.</span></span>
    
    <span data-ttu-id="d72c7-206">c.</span><span class="sxs-lookup"><span data-stu-id="d72c7-206">c.</span></span> <span data-ttu-id="d72c7-207">In Hallo **e** textbox type **e-mailadres** van Hallo gebruiker als  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="d72c7-207">In hello **Email** textbox, type **Email Address** of hello user as **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="d72c7-208">b.</span><span class="sxs-lookup"><span data-stu-id="d72c7-208">b.</span></span> <span data-ttu-id="d72c7-209">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="d72c7-209">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="d72c7-210">U kunt andere Mindflash gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Mindflash tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="d72c7-210">You can use any other Mindflash user account creation tools or APIs provided by Mindflash tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d72c7-211">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d72c7-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d72c7-212">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooMindflash toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="d72c7-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMindflash.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d72c7-214">**tooassign Britta Simon tooMindflash, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d72c7-214">**tooassign Britta Simon tooMindflash, perform hello following steps:**</span></span>

1. <span data-ttu-id="d72c7-215">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d72c7-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d72c7-217">Selecteer in de lijst met de toepassingen van Hallo **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="d72c7-217">In hello applications list, select **Mindflash**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_app.png) 

3. <span data-ttu-id="d72c7-219">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d72c7-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d72c7-221">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d72c7-221">Click **Add** button.</span></span> <span data-ttu-id="d72c7-222">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d72c7-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d72c7-224">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="d72c7-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d72c7-225">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d72c7-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d72c7-226">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d72c7-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d72c7-227">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d72c7-227">Testing single sign-on</span></span>

<span data-ttu-id="d72c7-228">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="d72c7-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d72c7-229">Als u op Hallo Mindflash tegel in Hallo Toegangsvenster, krijgt u de aanmeldingspagina van Mindflash toepassing.</span><span class="sxs-lookup"><span data-stu-id="d72c7-229">When you click hello Mindflash tile in hello Access Panel, you should get login page of Mindflash application.</span></span>
<span data-ttu-id="d72c7-230">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d72c7-230">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d72c7-231">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d72c7-231">Additional resources</span></span>

* [<span data-ttu-id="d72c7-232">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d72c7-232">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d72c7-233">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d72c7-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_203.png

