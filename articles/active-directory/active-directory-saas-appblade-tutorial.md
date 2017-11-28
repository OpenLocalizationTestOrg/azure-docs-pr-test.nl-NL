---
title: 'Zelfstudie: Azure Active Directory-integratie met AppBlade | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en AppBlade.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3360d7aa-6518-4f99-88bd-b7f7258183e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 06f3d8fcee97945c867bca6f3aebe15ecef04617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appblade"></a><span data-ttu-id="f4ed5-103">Zelfstudie: Azure Active Directory-integratie met AppBlade</span><span class="sxs-lookup"><span data-stu-id="f4ed5-103">Tutorial: Azure Active Directory integration with AppBlade</span></span>

<span data-ttu-id="f4ed5-104">In deze zelfstudie leert u hoe toointegrate AppBlade met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f4ed5-104">In this tutorial, you learn how toointegrate AppBlade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f4ed5-105">AppBlade integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f4ed5-105">Integrating AppBlade with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f4ed5-106">U kunt beheren in Azure AD die tooAppBlade toegang heeft</span><span class="sxs-lookup"><span data-stu-id="f4ed5-106">You can control in Azure AD who has access tooAppBlade</span></span>
- <span data-ttu-id="f4ed5-107">U kunt uw gebruikers tooautomatically get aangemelde tooAppBlade (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="f4ed5-107">You can enable your users tooautomatically get signed-on tooAppBlade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f4ed5-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f4ed5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f4ed5-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f4ed5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4ed5-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f4ed5-110">Prerequisites</span></span>

<span data-ttu-id="f4ed5-111">Azure AD-integratie met AppBlade tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="f4ed5-111">tooconfigure Azure AD integration with AppBlade, you need hello following items:</span></span>

- <span data-ttu-id="f4ed5-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f4ed5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f4ed5-113">Een AppBlade eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f4ed5-113">An AppBlade single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f4ed5-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f4ed5-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f4ed5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f4ed5-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f4ed5-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f4ed5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f4ed5-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f4ed5-118">Scenario description</span></span>
<span data-ttu-id="f4ed5-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f4ed5-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f4ed5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f4ed5-121">Het toevoegen van AppBlade van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f4ed5-121">Adding AppBlade from hello gallery</span></span>
2. <span data-ttu-id="f4ed5-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f4ed5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appblade-from-hello-gallery"></a><span data-ttu-id="f4ed5-123">Het toevoegen van AppBlade van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f4ed5-123">Adding AppBlade from hello gallery</span></span>
<span data-ttu-id="f4ed5-124">tooconfigure hello integratie van AppBlade in Azure AD, moet u tooadd AppBlade uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-124">tooconfigure hello integration of AppBlade into Azure AD, you need tooadd AppBlade from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f4ed5-125">**tooadd AppBlade via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f4ed5-125">**tooadd AppBlade from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4ed5-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f4ed5-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f4ed5-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f4ed5-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f4ed5-133">Typ in het zoekvak Hallo **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-133">In hello search box, type **AppBlade**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_search.png)

5. <span data-ttu-id="f4ed5-135">Selecteer in het deelvenster resultaten hello, **AppBlade**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-135">In hello results panel, select **AppBlade**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f4ed5-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f4ed5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f4ed5-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met AppBlade op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="f4ed5-138">In this section, you configure and test Azure AD single sign-on with AppBlade based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f4ed5-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in AppBlade is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AppBlade is tooa user in Azure AD.</span></span> <span data-ttu-id="f4ed5-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in AppBlade toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-140">In other words, a link relationship between an Azure AD user and hello related user in AppBlade needs toobe established.</span></span>

<span data-ttu-id="f4ed5-141">Wijs in AppBlade, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-141">In AppBlade, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f4ed5-142">tooconfigure en eenmalige aanmelding Azure AD-test met AppBlade, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f4ed5-142">tooconfigure and test Azure AD single sign-on with AppBlade, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f4ed5-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f4ed5-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f4ed5-145">**[Maken van een testgebruiker AppBlade](#creating-an-appblade-test-user)**  -toohave een equivalent van Britta Simon in AppBlade die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-145">**[Creating an AppBlade test user](#creating-an-appblade-test-user)** - toohave a counterpart of Britta Simon in AppBlade that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f4ed5-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f4ed5-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f4ed5-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f4ed5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f4ed5-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing AppBlade configureren.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AppBlade application.</span></span>

<span data-ttu-id="f4ed5-150">**Azure AD tooconfigure eenmalige aanmelding met AppBlade, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f4ed5-150">**tooconfigure Azure AD single sign-on with AppBlade, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4ed5-151">In de Azure-portal op Hallo Hallo **AppBlade** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-151">In hello Azure portal, on hello **AppBlade** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f4ed5-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_samlbase.png)

3. <span data-ttu-id="f4ed5-155">Op Hallo **AppBlade domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f4ed5-155">On hello **AppBlade Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_url.png)

    <span data-ttu-id="f4ed5-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.appblade.com/saml/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="f4ed5-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.appblade.com/saml/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f4ed5-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-158">This value is not real.</span></span> <span data-ttu-id="f4ed5-159">Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="f4ed5-160">Neem contact op met [AppBlade Client ondersteuningsteam](mailto:support@appblade.com) tooget Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-160">Contact [AppBlade Client support team](mailto:support@appblade.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="f4ed5-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_certificate.png) 

5. <span data-ttu-id="f4ed5-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appblade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f4ed5-165">tooconfigure eenmalige aanmelding op **AppBlade** zijde, moet u toosend Hallo gedownload **Metadata XML** te[AppBlade ondersteuningsteam](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="f4ed5-165">tooconfigure single sign-on on **AppBlade** side, you need toosend hello downloaded **Metadata XML** too[AppBlade support team](mailto:support@appblade.com).</span></span> <span data-ttu-id="f4ed5-166">Bovendien kunt u verwijzen tooconfigure Hallo **URL SSO-verlener** als `https://appblade.com/saml`.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-166">Also, please ask them tooconfigure hello **SSO Issuer URL** as `https://appblade.com/saml`.</span></span> <span data-ttu-id="f4ed5-167">Deze instelling is vereist voor één aanmelding toowork.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-167">This setting is required for single sign-on toowork.</span></span>


> [!TIP]
> <span data-ttu-id="f4ed5-168">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-168">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f4ed5-169">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-169">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f4ed5-170">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f4ed5-170">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f4ed5-171">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f4ed5-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="f4ed5-172">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-172">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f4ed5-174">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f4ed5-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4ed5-175">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-175">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appblade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f4ed5-177">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-177">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appblade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f4ed5-179">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-179">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appblade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f4ed5-181">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f4ed5-181">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appblade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f4ed5-183">a.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-183">a.</span></span> <span data-ttu-id="f4ed5-184">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-184">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f4ed5-185">b.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-185">b.</span></span> <span data-ttu-id="f4ed5-186">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-186">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f4ed5-187">c.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-187">c.</span></span> <span data-ttu-id="f4ed5-188">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-188">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f4ed5-189">d.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-189">d.</span></span> <span data-ttu-id="f4ed5-190">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-190">Click **Create**.</span></span>
 
### <a name="creating-an-appblade-test-user"></a><span data-ttu-id="f4ed5-191">Een testgebruiker AppBlade maken</span><span class="sxs-lookup"><span data-stu-id="f4ed5-191">Creating an AppBlade test user</span></span>

<span data-ttu-id="f4ed5-192">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in AppBlade van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-192">hello objective of this section is toocreate a user called Britta Simon in AppBlade.</span></span> <span data-ttu-id="f4ed5-193">AppBlade ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-193">AppBlade supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="f4ed5-194">**Zorg ervoor dat de domeinnaam van uw is geconfigureerd met AppBlade voor gebruikers inrichten. Na die alleen Hallo just in time gebruikers inrichten werkt.**</span><span class="sxs-lookup"><span data-stu-id="f4ed5-194">**Make sure that your domain name is configured with AppBlade for user provisioning. After that only hello just-in-time user provisioning works.**</span></span>

<span data-ttu-id="f4ed5-195">Als Hallo gebruiker een e-mailadres dat eindigt op Hallo domein geconfigureerd door AppBlade voor uw account en vervolgens Hallo gebruiker automatisch Hallo-account wordt toegevoegd als een lid met de Hallo-machtigingsniveau die u opgeeft heeft, is dit een van de 'Basic' (een basisgebruiker die alleen kan worden geïnstalleerd toepassingen), 'Teamlid' (een gebruiker die u kunt nieuwe versies van de app uploaden en beheren van de projecten) of 'Administrator' (volledig Administrator-bevoegdheden toohello account).</span><span class="sxs-lookup"><span data-stu-id="f4ed5-195">If hello user has an email address ending with hello domain configured by AppBlade for your account, then hello user will automatically join hello account as a member with hello permission level you specify, which is one of "Basic" (a basic user who can only install applications), "Team Member" (a user who can upload new app versions and manage projects), or "Administrator" (full admin privileges toohello account).</span></span> <span data-ttu-id="f4ed5-196">Normaal gesproken één zou Basic kiezen en vervolgens gebruikers handmatig via een aanmeldgegevens van serverbeheerder promoveren (AppBlade moet een op basis van e-beheerderaanmelding tooconfigure van tevoren of promoveren van een gebruiker namens de klant Hallo na aanmelding).</span><span class="sxs-lookup"><span data-stu-id="f4ed5-196">Normally one would choose Basic and then promote users manually via an Admin login (AppBlade needs tooconfigure either an email-based admin login in advance or promote a user on behalf of hello customer after login).</span></span>

<span data-ttu-id="f4ed5-197">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-197">There is no action item for you in this section.</span></span> <span data-ttu-id="f4ed5-198">Een nieuwe gebruiker wordt tijdens een poging tooaccess AppBlade gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-198">A new user is created during an attempt tooaccess AppBlade if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="f4ed5-199">Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello [AppBlade ondersteuningsteam](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="f4ed5-199">If you need toocreate a user manually, you need toocontact hello [AppBlade support team](mailto:support@appblade.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f4ed5-200">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4ed5-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f4ed5-201">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooAppBlade toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAppBlade.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f4ed5-203">**tooassign Britta Simon tooAppBlade, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f4ed5-203">**tooassign Britta Simon tooAppBlade, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4ed5-204">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f4ed5-206">Selecteer in de lijst met de toepassingen van Hallo **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-206">In hello applications list, select **AppBlade**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_app.png) 

3. <span data-ttu-id="f4ed5-208">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f4ed5-210">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-210">Click **Add** button.</span></span> <span data-ttu-id="f4ed5-211">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f4ed5-213">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f4ed5-214">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f4ed5-215">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f4ed5-216">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f4ed5-216">Testing single sign-on</span></span>

<span data-ttu-id="f4ed5-217">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="f4ed5-218">Als u op Hallo AppBlade tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour AppBlade toepassing.</span><span class="sxs-lookup"><span data-stu-id="f4ed5-218">When you click hello AppBlade tile in hello Access Panel, you should get automatically signed-on tooyour AppBlade application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f4ed5-219">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f4ed5-219">Additional resources</span></span>

* [<span data-ttu-id="f4ed5-220">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4ed5-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f4ed5-221">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f4ed5-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_203.png

