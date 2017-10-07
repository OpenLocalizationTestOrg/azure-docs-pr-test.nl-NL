---
title: 'Zelfstudie: Azure Active Directory-integratie met Abintegro | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Abintegro.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 99287e1f-4189-494a-97c8-e1c03d047fd3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 54e2865860940cab0c0ef31a496f42dd55b0e907
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-abintegro"></a><span data-ttu-id="1f2f0-103">Zelfstudie: Azure Active Directory-integratie met Abintegro</span><span class="sxs-lookup"><span data-stu-id="1f2f0-103">Tutorial: Azure Active Directory integration with Abintegro</span></span>

<span data-ttu-id="1f2f0-104">In deze zelfstudie leert u hoe toointegrate Abintegro met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1f2f0-104">In this tutorial, you learn how toointegrate Abintegro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1f2f0-105">Abintegro integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1f2f0-105">Integrating Abintegro with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1f2f0-106">U kunt beheren in Azure AD die tooAbintegro toegang heeft</span><span class="sxs-lookup"><span data-stu-id="1f2f0-106">You can control in Azure AD who has access tooAbintegro</span></span>
- <span data-ttu-id="1f2f0-107">U kunt uw gebruikers tooautomatically get aangemelde tooAbintegro (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="1f2f0-107">You can enable your users tooautomatically get signed-on tooAbintegro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1f2f0-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="1f2f0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1f2f0-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1f2f0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f2f0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1f2f0-110">Prerequisites</span></span>

<span data-ttu-id="1f2f0-111">Azure AD-integratie met Abintegro tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="1f2f0-111">tooconfigure Azure AD integration with Abintegro, you need hello following items:</span></span>

- <span data-ttu-id="1f2f0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1f2f0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1f2f0-113">Een Abintegro eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="1f2f0-113">An Abintegro single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1f2f0-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1f2f0-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1f2f0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1f2f0-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1f2f0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f2f0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1f2f0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1f2f0-118">Scenario description</span></span>
<span data-ttu-id="1f2f0-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1f2f0-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1f2f0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1f2f0-121">Het toevoegen van Abintegro van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="1f2f0-121">Adding Abintegro from hello gallery</span></span>
2. <span data-ttu-id="1f2f0-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1f2f0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-abintegro-from-hello-gallery"></a><span data-ttu-id="1f2f0-123">Het toevoegen van Abintegro van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="1f2f0-123">Adding Abintegro from hello gallery</span></span>
<span data-ttu-id="1f2f0-124">tooconfigure hello integratie van Abintegro in Azure AD, moet u tooadd Abintegro uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-124">tooconfigure hello integration of Abintegro into Azure AD, you need tooadd Abintegro from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1f2f0-125">**tooadd Abintegro via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1f2f0-125">**tooadd Abintegro from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f2f0-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1f2f0-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1f2f0-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="1f2f0-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="1f2f0-133">Typ in het zoekvak Hallo **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-133">In hello search box, type **Abintegro**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_search.png)

5. <span data-ttu-id="1f2f0-135">Selecteer in het deelvenster resultaten hello, **Abintegro**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-135">In hello results panel, select **Abintegro**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1f2f0-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1f2f0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1f2f0-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Abintegro op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="1f2f0-138">In this section, you configure and test Azure AD single sign-on with Abintegro based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1f2f0-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Abintegro is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Abintegro is tooa user in Azure AD.</span></span> <span data-ttu-id="1f2f0-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Abintegro toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-140">In other words, a link relationship between an Azure AD user and hello related user in Abintegro needs toobe established.</span></span>

<span data-ttu-id="1f2f0-141">Wijs in Abintegro, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-141">In Abintegro, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1f2f0-142">tooconfigure en eenmalige aanmelding Azure AD-test met Abintegro, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1f2f0-142">tooconfigure and test Azure AD single sign-on with Abintegro, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1f2f0-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1f2f0-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1f2f0-145">**[Maken van een testgebruiker Abintegro](#creating-an-abintegro-test-user)**  -toohave een equivalent van Britta Simon in Abintegro die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-145">**[Creating an Abintegro test user](#creating-an-abintegro-test-user)** - toohave a counterpart of Britta Simon in Abintegro that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1f2f0-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1f2f0-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1f2f0-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1f2f0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1f2f0-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Abintegro configureren.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Abintegro application.</span></span>

<span data-ttu-id="1f2f0-150">**Azure AD tooconfigure eenmalige aanmelding met Abintegro, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1f2f0-150">**tooconfigure Azure AD single sign-on with Abintegro, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f2f0-151">In de Azure-portal op Hallo Hallo **Abintegro** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-151">In hello Azure portal, on hello **Abintegro** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1f2f0-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_samlbase.png)

3. <span data-ttu-id="1f2f0-155">Op Hallo **Abintegro domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1f2f0-155">On hello **Abintegro Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_url.png)

    <span data-ttu-id="1f2f0-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span><span class="sxs-lookup"><span data-stu-id="1f2f0-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1f2f0-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-158">This value is not real.</span></span> <span data-ttu-id="1f2f0-159">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="1f2f0-160">Neem contact op met [Abintegro Client ondersteuningsteam](mailto:support@abintegro.com) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-160">Contact [Abintegro Client support team](mailto:support@abintegro.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="1f2f0-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_certificate.png) 

5. <span data-ttu-id="1f2f0-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-abintegro-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1f2f0-165">tooconfigure eenmalige aanmelding op **Abintegro** zijde, moet u toosend Hallo gedownload **Metadata XML** te[Abintegro ondersteuningsteam](mailto:support@abintegro.com).</span><span class="sxs-lookup"><span data-stu-id="1f2f0-165">tooconfigure single sign-on on **Abintegro** side, you need toosend hello downloaded **Metadata XML** too[Abintegro support team](mailto:support@abintegro.com).</span></span> <span data-ttu-id="1f2f0-166">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1f2f0-167">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1f2f0-168">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1f2f0-169">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1f2f0-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1f2f0-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1f2f0-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="1f2f0-171">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="1f2f0-173">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1f2f0-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f2f0-174">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-abintegro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1f2f0-176">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-abintegro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1f2f0-178">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-abintegro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1f2f0-180">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1f2f0-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-abintegro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1f2f0-182">a.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-182">a.</span></span> <span data-ttu-id="1f2f0-183">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1f2f0-184">b.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-184">b.</span></span> <span data-ttu-id="1f2f0-185">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1f2f0-186">c.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-186">c.</span></span> <span data-ttu-id="1f2f0-187">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1f2f0-188">d.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-188">d.</span></span> <span data-ttu-id="1f2f0-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-189">Click **Create**.</span></span>
 
### <a name="creating-an-abintegro-test-user"></a><span data-ttu-id="1f2f0-190">Een testgebruiker Abintegro maken</span><span class="sxs-lookup"><span data-stu-id="1f2f0-190">Creating an Abintegro test user</span></span>

<span data-ttu-id="1f2f0-191">Er is geen actie-item voor u tooconfigure gebruikers inrichten tooAbintegro.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-191">There is no action item for you tooconfigure user provisioning tooAbintegro.</span></span> <span data-ttu-id="1f2f0-192">Wanneer een toegewezen gebruiker toolog in Abintegro met behulp van het toegangsvenster hello probeert, controleert Abintegro of Hallo gebruiker bestaat.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-192">When an assigned user tries toolog into Abintegro using hello access panel, Abintegro checks whether hello user exists.</span></span>
  
<span data-ttu-id="1f2f0-193">Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Abintegro.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-193">If there is no user account available yet, it is automatically created by Abintegro.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1f2f0-194">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f2f0-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1f2f0-195">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooAbintegro toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAbintegro.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="1f2f0-197">**tooassign Britta Simon tooAbintegro, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="1f2f0-197">**tooassign Britta Simon tooAbintegro, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f2f0-198">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1f2f0-200">Selecteer in de lijst met de toepassingen van Hallo **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-200">In hello applications list, select **Abintegro**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_app.png) 

3. <span data-ttu-id="1f2f0-202">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="1f2f0-204">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-204">Click **Add** button.</span></span> <span data-ttu-id="1f2f0-205">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="1f2f0-207">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1f2f0-208">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1f2f0-209">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1f2f0-210">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1f2f0-210">Testing single sign-on</span></span>

<span data-ttu-id="1f2f0-211">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1f2f0-212">Als u op Hallo Abintegro tegel in Hallo Toegangsvenster, krijgt u de aanmeldingspagina van Abintegro toepassing.</span><span class="sxs-lookup"><span data-stu-id="1f2f0-212">When you click hello Abintegro tile in hello Access Panel, you should get login page of Abintegro application.</span></span>
<span data-ttu-id="1f2f0-213">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1f2f0-213">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1f2f0-214">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1f2f0-214">Additional resources</span></span>

* [<span data-ttu-id="1f2f0-215">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f2f0-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1f2f0-216">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1f2f0-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_203.png

