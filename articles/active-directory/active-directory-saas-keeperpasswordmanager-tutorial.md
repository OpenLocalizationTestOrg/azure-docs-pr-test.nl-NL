---
title: 'Zelfstudie: Azure Active Directory-integratie met wachtwoordbeheer houder & digitale kluis | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en houder wachtwoordbeheer & digitale kluis.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1a98f6a-2dae-4734-bdbf-4fba742a61d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 01e59004e6bdccfca08094f9da6f82270d5028d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-keeper-password-manager--digital-vault"></a><span data-ttu-id="d9cd7-103">Zelfstudie: Azure Active Directory-integratie met wachtwoordbeheer houder & digitale kluis</span><span class="sxs-lookup"><span data-stu-id="d9cd7-103">Tutorial: Azure Active Directory integration with Keeper Password Manager & Digital Vault</span></span>

<span data-ttu-id="d9cd7-104">In deze zelfstudie leert u hoe toointegrate houder wachtwoordbeheer & digitale kluis met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d9cd7-104">In this tutorial, you learn how toointegrate Keeper Password Manager & Digital Vault with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d9cd7-105">Wachtwoordbeheer houder & digitale kluis integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d9cd7-105">Integrating Keeper Password Manager & Digital Vault with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d9cd7-106">U kunt beheren in Azure AD wie heeft toegang tot tooKeeper wachtwoordbeheer & digitale kluis</span><span class="sxs-lookup"><span data-stu-id="d9cd7-106">You can control in Azure AD who has access tooKeeper Password Manager & Digital Vault</span></span>
- <span data-ttu-id="d9cd7-107">U kunt uw gebruikers tooautomatically get aangemelde tooKeeper wachtwoordbeheer & digitale kluis (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="d9cd7-107">You can enable your users tooautomatically get signed-on tooKeeper Password Manager & Digital Vault (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d9cd7-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="d9cd7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d9cd7-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d9cd7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9cd7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d9cd7-110">Prerequisites</span></span>

<span data-ttu-id="d9cd7-111">Azure AD-integratie met wachtwoordbeheer houder & digitale kluis tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="d9cd7-111">tooconfigure Azure AD integration with Keeper Password Manager & Digital Vault, you need hello following items:</span></span>

- <span data-ttu-id="d9cd7-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="d9cd7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d9cd7-113">Een houder wachtwoordbeheer & digitale kluis eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="d9cd7-113">A Keeper Password Manager & Digital Vault single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d9cd7-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d9cd7-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="d9cd7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d9cd7-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d9cd7-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d9cd7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d9cd7-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d9cd7-118">Scenario description</span></span>
<span data-ttu-id="d9cd7-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d9cd7-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d9cd7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d9cd7-121">Het toevoegen van houder wachtwoordbeheer & digitale kluis van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="d9cd7-121">Adding Keeper Password Manager & Digital Vault from hello gallery</span></span>
2. <span data-ttu-id="d9cd7-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d9cd7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-keeper-password-manager--digital-vault-from-hello-gallery"></a><span data-ttu-id="d9cd7-123">Het toevoegen van houder wachtwoordbeheer & digitale kluis van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="d9cd7-123">Adding Keeper Password Manager & Digital Vault from hello gallery</span></span>
<span data-ttu-id="d9cd7-124">tooconfigure hello integratie van houder wachtwoordbeheer & digitale kluis in Azure AD, moet u tooadd houder wachtwoordbeheer & digitale kluis in Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-124">tooconfigure hello integration of Keeper Password Manager & Digital Vault into Azure AD, you need tooadd Keeper Password Manager & Digital Vault from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d9cd7-125">**tooadd houder wachtwoordbeheer & digitale kluis uit de galerie hello, voert Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d9cd7-125">**tooadd Keeper Password Manager & Digital Vault from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9cd7-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d9cd7-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d9cd7-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d9cd7-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d9cd7-133">Typ in het zoekvak Hallo **houder wachtwoordbeheer & digitale kluis**.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-133">In hello search box, type **Keeper Password Manager & Digital Vault**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_search.png)

5. <span data-ttu-id="d9cd7-135">Selecteer in het deelvenster resultaten hello, **houder wachtwoordbeheer & digitale kluis**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-135">In hello results panel, select **Keeper Password Manager & Digital Vault**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d9cd7-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d9cd7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d9cd7-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met wachtwoordbeheer houder & digitale kluis op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="d9cd7-138">In this section, you configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d9cd7-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de houder wachtwoordbeheer & digitale kluis is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Keeper Password Manager & Digital Vault is tooa user in Azure AD.</span></span> <span data-ttu-id="d9cd7-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in houder wachtwoordbeheer & digitale kluis toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-140">In other words, a link relationship between an Azure AD user and hello related user in Keeper Password Manager & Digital Vault needs toobe established.</span></span>

<span data-ttu-id="d9cd7-141">In de houder wachtwoordbeheer & digitale kluis Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-141">In Keeper Password Manager & Digital Vault, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d9cd7-142">tooconfigure en test eenmalige aanmelding Azure AD met wachtwoordbeheer houder & digitale kluis, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d9cd7-142">tooconfigure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d9cd7-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d9cd7-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d9cd7-145">**[Maken van een testgebruiker houder wachtwoordbeheer & digitale kluis](#creating-a-keeperpasswordmanager-test-user)**  -toohave een equivalent van Britta Simon in houder wachtwoordbeheer & digitale kluis die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-145">**[Creating a Keeper Password Manager & Digital Vault test user](#creating-a-keeperpasswordmanager-test-user)** - toohave a counterpart of Britta Simon in Keeper Password Manager & Digital Vault that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d9cd7-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d9cd7-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d9cd7-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d9cd7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d9cd7-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing houder wachtwoordbeheer & digitale kluis.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Keeper Password Manager & Digital Vault application.</span></span>

<span data-ttu-id="d9cd7-150">**tooconfigure eenmalige aanmelding Azure AD met wachtwoordbeheer houder & digitale kluis Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d9cd7-150">**tooconfigure Azure AD single sign-on with Keeper Password Manager & Digital Vault, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9cd7-151">In Azure-portal op Hallo Hallo **houder wachtwoordbeheer & digitale kluis** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-151">In hello Azure portal, on hello **Keeper Password Manager & Digital Vault** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d9cd7-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_samlbase.png)

3. <span data-ttu-id="d9cd7-155">Op Hallo **houder wachtwoordbeheer & digitale kluis domein en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d9cd7-155">On hello **Keeper Password Manager & Digital Vault Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_url.png)

    <span data-ttu-id="d9cd7-157">a.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-157">a.</span></span> <span data-ttu-id="d9cd7-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span><span class="sxs-lookup"><span data-stu-id="d9cd7-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span></span>

    <span data-ttu-id="d9cd7-159">b.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-159">b.</span></span> <span data-ttu-id="d9cd7-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="d9cd7-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span></span>

    <span data-ttu-id="d9cd7-161">c.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-161">c.</span></span> <span data-ttu-id="d9cd7-162">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://{SSO CONNECT SERVER}/sso-connect`</span><span class="sxs-lookup"><span data-stu-id="d9cd7-162">In hello **Identifier** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d9cd7-163">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-163">These values are not real.</span></span> <span data-ttu-id="d9cd7-164">Deze waarden bijwerken met Hallo werkelijke antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-164">Update these values with hello actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="d9cd7-165">Neem contact op met [houder wachtwoordbeheer & digitale kluis Client ondersteuningsteam](https://keepersecurity.com/contact.html) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-165">Contact [Keeper Password Manager & Digital Vault Client support team](https://keepersecurity.com/contact.html) tooget these values.</span></span> 

4. <span data-ttu-id="d9cd7-166">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_certificate.png) 

5. <span data-ttu-id="d9cd7-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="d9cd7-170">Op Hallo **houder wachtwoordbeheer & digitale kluis configuratie** sectie, klikt u op **houder wachtwoordbeheer configureren & digitale kluis** tooopen **configureren aanmelding**venster.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-170">On hello **Keeper Password Manager & Digital Vault Configuration** section, click **Configure Keeper Password Manager & Digital Vault** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d9cd7-171">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="d9cd7-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_configure.png) 

7. <span data-ttu-id="d9cd7-173">tooconfigure eenmalige aanmelding op **houder wachtwoordbeheer & digitale kluis configuratie** zijde, Hallo richtlijnen gegeven op [houder Support Guide](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span><span class="sxs-lookup"><span data-stu-id="d9cd7-173">tooconfigure single sign-on on **Keeper Password Manager & Digital Vault Configuration** side, follow hello guidelines given at [Keeper Support Guide](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span></span>

> [!TIP]
> <span data-ttu-id="d9cd7-174">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d9cd7-175">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d9cd7-176">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d9cd7-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d9cd7-177">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d9cd7-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="d9cd7-178">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d9cd7-180">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d9cd7-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9cd7-181">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d9cd7-183">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d9cd7-185">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d9cd7-187">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d9cd7-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d9cd7-189">a.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-189">a.</span></span> <span data-ttu-id="d9cd7-190">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d9cd7-191">b.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-191">b.</span></span> <span data-ttu-id="d9cd7-192">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d9cd7-193">c.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-193">c.</span></span> <span data-ttu-id="d9cd7-194">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d9cd7-195">d.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-195">d.</span></span> <span data-ttu-id="d9cd7-196">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-196">Click **Create**.</span></span>
 
### <a name="creating-a-keeper-password-manager--digital-vault-test-user"></a><span data-ttu-id="d9cd7-197">Een testgebruiker houder wachtwoordbeheer & digitale kluis maken</span><span class="sxs-lookup"><span data-stu-id="d9cd7-197">Creating a Keeper Password Manager & Digital Vault test user</span></span>

<span data-ttu-id="d9cd7-198">Azure AD tooenable gebruikers toolog in tooKeeper wachtwoordbeheer & digitale kluis, moeten ze ingericht in houder wachtwoordbeheer & digitale kluis.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-198">tooenable Azure AD users toolog in tooKeeper Password Manager & Digital Vault, they must be provisioned into Keeper Password Manager & Digital Vault.</span></span> <span data-ttu-id="d9cd7-199">Toepassing ondersteunt Just in tijd gebruikers inrichten en na verificatie gebruikers wordt in de toepassing hello automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-199">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="d9cd7-200">U kunt contact opnemen met [houder ondersteuning](https://keepersecurity.com/contact.html), als u wilt dat gebruikers van toosetup handmatig.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-200">You can contact [Keeper Support](https://keepersecurity.com/contact.html), if you want toosetup users manually.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d9cd7-201">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9cd7-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d9cd7-202">In deze sectie u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tot tooKeeper wachtwoordbeheer & digitale kluis.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKeeper Password Manager & Digital Vault.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d9cd7-204">**tooassign Britta Simon tooKeeper wachtwoordbeheer & digitale kluis, voert Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="d9cd7-204">**tooassign Britta Simon tooKeeper Password Manager & Digital Vault, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9cd7-205">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d9cd7-207">Selecteer in de lijst met de toepassingen van Hallo **houder wachtwoordbeheer & digitale kluis**.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-207">In hello applications list, select **Keeper Password Manager & Digital Vault**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_app.png) 

3. <span data-ttu-id="d9cd7-209">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d9cd7-211">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-211">Click **Add** button.</span></span> <span data-ttu-id="d9cd7-212">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d9cd7-214">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d9cd7-215">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d9cd7-216">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d9cd7-217">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d9cd7-217">Testing single sign-on</span></span>

<span data-ttu-id="d9cd7-218">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d9cd7-219">Als u op Hallo houder wachtwoordbeheer & digitale kluis tegel in Hallo Toegangsvenster, krijgt u de aanmeldingspagina van houder wachtwoordbeheer & digitale kluis toepassing.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-219">When you click hello Keeper Password Manager & Digital Vault tile in hello Access Panel, you should get login page of Keeper Password Manager & Digital Vault application.</span></span> <span data-ttu-id="d9cd7-220">Na een geslaagde verificatie moet u in de toepassing hello ophalen.</span><span class="sxs-lookup"><span data-stu-id="d9cd7-220">Upon successful authentication, you should get into hello application.</span></span> <span data-ttu-id="d9cd7-221">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d9cd7-221">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d9cd7-222">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d9cd7-222">Additional resources</span></span>

* [<span data-ttu-id="d9cd7-223">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9cd7-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9cd7-224">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d9cd7-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_203.png

