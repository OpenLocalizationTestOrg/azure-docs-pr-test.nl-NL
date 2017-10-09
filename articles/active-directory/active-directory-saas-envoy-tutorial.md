---
title: 'Zelfstudie: Azure Active Directory-integratie met Envoy | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Envoy.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 93add7c1f3cf1fc163acc505f11e34bd696c571c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="e99c2-103">Zelfstudie: Azure Active Directory-integratie met Envoy</span><span class="sxs-lookup"><span data-stu-id="e99c2-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="e99c2-104">In deze zelfstudie leert u hoe toointegrate Envoy met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e99c2-104">In this tutorial, you learn how toointegrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e99c2-105">Envoy integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e99c2-105">Integrating Envoy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e99c2-106">U kunt beheren in Azure AD die tooEnvoy toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="e99c2-106">You can control in Azure AD who has access tooEnvoy.</span></span>
- <span data-ttu-id="e99c2-107">U kunt uw gebruikers tooautomatically get aangemelde tooEnvoy (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e99c2-107">You can enable your users tooautomatically get signed-on tooEnvoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e99c2-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="e99c2-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="e99c2-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e99c2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e99c2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e99c2-110">Prerequisites</span></span>

<span data-ttu-id="e99c2-111">Azure AD-integratie met Envoy tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="e99c2-111">tooconfigure Azure AD integration with Envoy, you need hello following items:</span></span>

- <span data-ttu-id="e99c2-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e99c2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e99c2-113">Een Envoy eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e99c2-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e99c2-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e99c2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e99c2-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e99c2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e99c2-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e99c2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e99c2-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e99c2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e99c2-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e99c2-118">Scenario description</span></span>
<span data-ttu-id="e99c2-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e99c2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e99c2-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e99c2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e99c2-121">Het toevoegen van Envoy van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="e99c2-121">Adding Envoy from hello gallery</span></span>
2. <span data-ttu-id="e99c2-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e99c2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-hello-gallery"></a><span data-ttu-id="e99c2-123">Het toevoegen van Envoy van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="e99c2-123">Adding Envoy from hello gallery</span></span>
<span data-ttu-id="e99c2-124">tooconfigure hello integratie van Envoy in Azure AD, moet u tooadd Envoy uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e99c2-124">tooconfigure hello integration of Envoy into Azure AD, you need tooadd Envoy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e99c2-125">**tooadd Envoy via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e99c2-125">**tooadd Envoy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e99c2-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e99c2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="e99c2-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e99c2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e99c2-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e99c2-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="e99c2-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e99c2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="e99c2-133">Typ in het zoekvak Hallo **Envoy**, selecteer **Envoy** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e99c2-133">In hello search box, type **Envoy**, select **Envoy** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lijst met zoekresultaten Envoy in Hallo](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e99c2-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="e99c2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e99c2-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Envoy op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="e99c2-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e99c2-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Envoy is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e99c2-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Envoy is tooa user in Azure AD.</span></span> <span data-ttu-id="e99c2-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Envoy toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="e99c2-138">In other words, a link relationship between an Azure AD user and hello related user in Envoy needs toobe established.</span></span>

<span data-ttu-id="e99c2-139">Wijs in Envoy, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="e99c2-139">In Envoy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e99c2-140">tooconfigure en eenmalige aanmelding Azure AD-test met Envoy, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e99c2-140">tooconfigure and test Azure AD single sign-on with Envoy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e99c2-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="e99c2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e99c2-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e99c2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e99c2-143">**[Maken van een testgebruiker Envoy](#create-an-envoy-test-user)**  -toohave een equivalent van Britta Simon in Envoy die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e99c2-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - toohave a counterpart of Britta Simon in Envoy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e99c2-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e99c2-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e99c2-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e99c2-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e99c2-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e99c2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e99c2-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Envoy configureren.</span><span class="sxs-lookup"><span data-stu-id="e99c2-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="e99c2-148">**Azure AD tooconfigure eenmalige aanmelding met Envoy, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e99c2-148">**tooconfigure Azure AD single sign-on with Envoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="e99c2-149">In de Azure-portal op Hallo Hallo **Envoy** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e99c2-149">In hello Azure portal, on hello **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e99c2-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e99c2-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="e99c2-153">Op Hallo **Envoy-domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e99c2-153">On hello **Envoy Domain and URLs** section, perform hello following steps:</span></span>

    ![Envoy-domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="e99c2-155">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.Envoy.com`</span><span class="sxs-lookup"><span data-stu-id="e99c2-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="e99c2-156">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="e99c2-156">This value is not real.</span></span> <span data-ttu-id="e99c2-157">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="e99c2-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="e99c2-158">Neem contact op met [Envoy Client ondersteuningsteam](https://envoy.com/contact/) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="e99c2-158">Contact [Envoy Client support team](https://envoy.com/contact/) tooget this value.</span></span>

4. <span data-ttu-id="e99c2-159">Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van het certificaat...</span><span class="sxs-lookup"><span data-stu-id="e99c2-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate..</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="e99c2-161">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e99c2-161">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e99c2-163">Op Hallo **Envoy configuratie** sectie, klikt u op **Envoy configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="e99c2-163">On hello **Envoy Configuration** section, click **Configure Envoy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e99c2-164">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="e99c2-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Envoy-configuratie](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="e99c2-166">In een ander browservenster, meld u bij uw bedrijf Envoy site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e99c2-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="e99c2-167">Klik in de werkbalk bovenaan Hallo Hallo op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="e99c2-167">In hello toolbar on hello top, click **Settings**.</span></span>

    <span data-ttu-id="e99c2-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span><span class="sxs-lookup"><span data-stu-id="e99c2-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="e99c2-169">Klik op **bedrijf**.</span><span class="sxs-lookup"><span data-stu-id="e99c2-169">Click **Company**.</span></span>

    <span data-ttu-id="e99c2-170">![Bedrijf](./media/active-directory-saas-envoy-tutorial/ic776783.png "bedrijf")</span><span class="sxs-lookup"><span data-stu-id="e99c2-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="e99c2-171">Klik op **SAML**.</span><span class="sxs-lookup"><span data-stu-id="e99c2-171">Click **SAML**.</span></span>

    <span data-ttu-id="e99c2-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="e99c2-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="e99c2-173">In Hallo **SAML-verificatie** configuratie sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e99c2-173">In hello **SAML Authentication** configuration section, perform hello following steps:</span></span>

    <span data-ttu-id="e99c2-174">![SAML-verificatie](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML-verificatie")</span><span class="sxs-lookup"><span data-stu-id="e99c2-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="e99c2-175">Hallo-waarde voor Hallo hoofdkantoor locatie-ID is automatisch gegenereerd door de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="e99c2-175">hello value for hello HQ location ID is auto generated by hello application.</span></span>
    
    <span data-ttu-id="e99c2-176">a.</span><span class="sxs-lookup"><span data-stu-id="e99c2-176">a.</span></span> <span data-ttu-id="e99c2-177">In **vingerafdruk** textbox plakken Hallo **vingerafdruk** waarde van het certificaat dat u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e99c2-177">In **Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="e99c2-178">b.</span><span class="sxs-lookup"><span data-stu-id="e99c2-178">b.</span></span> <span data-ttu-id="e99c2-179">Plakken **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd formulier hello Azure portal naar Hallo **identiteit PROVIDER HTTP-URL voor SAML** textbox.</span><span class="sxs-lookup"><span data-stu-id="e99c2-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form hello Azure portal into hello **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="e99c2-180">c.</span><span class="sxs-lookup"><span data-stu-id="e99c2-180">c.</span></span> <span data-ttu-id="e99c2-181">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e99c2-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="e99c2-182">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="e99c2-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e99c2-183">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="e99c2-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e99c2-184">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e99c2-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e99c2-185">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e99c2-185">Create an Azure AD test user</span></span>

<span data-ttu-id="e99c2-186">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e99c2-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="e99c2-188">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e99c2-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e99c2-189">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="e99c2-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e99c2-191">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e99c2-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e99c2-193">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e99c2-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e99c2-195">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e99c2-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e99c2-197">a.</span><span class="sxs-lookup"><span data-stu-id="e99c2-197">a.</span></span> <span data-ttu-id="e99c2-198">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e99c2-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e99c2-199">b.</span><span class="sxs-lookup"><span data-stu-id="e99c2-199">b.</span></span> <span data-ttu-id="e99c2-200">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="e99c2-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="e99c2-201">c.</span><span class="sxs-lookup"><span data-stu-id="e99c2-201">c.</span></span> <span data-ttu-id="e99c2-202">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="e99c2-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="e99c2-203">d.</span><span class="sxs-lookup"><span data-stu-id="e99c2-203">d.</span></span> <span data-ttu-id="e99c2-204">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e99c2-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="e99c2-205">Een testgebruiker Envoy maken</span><span class="sxs-lookup"><span data-stu-id="e99c2-205">Create an Envoy test user</span></span>

<span data-ttu-id="e99c2-206">Er is geen actie-item voor u tooconfigure gebruikers inrichten tooEnvoy.</span><span class="sxs-lookup"><span data-stu-id="e99c2-206">There is no action item for you tooconfigure user provisioning tooEnvoy.</span></span> <span data-ttu-id="e99c2-207">Wanneer een toegewezen gebruiker toolog in Envoy met behulp van het toegangsvenster hello probeert, controleert Envoy of Hallo gebruiker bestaat.</span><span class="sxs-lookup"><span data-stu-id="e99c2-207">When an assigned user tries toolog into Envoy using hello access panel, Envoy checks whether hello user exists.</span></span> <span data-ttu-id="e99c2-208">Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Envoy.</span><span class="sxs-lookup"><span data-stu-id="e99c2-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e99c2-209">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e99c2-209">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e99c2-210">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooEnvoy toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="e99c2-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEnvoy.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="e99c2-212">**tooassign Britta Simon tooEnvoy, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="e99c2-212">**tooassign Britta Simon tooEnvoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="e99c2-213">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e99c2-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e99c2-215">Selecteer in de lijst met de toepassingen van Hallo **Envoy**.</span><span class="sxs-lookup"><span data-stu-id="e99c2-215">In hello applications list, select **Envoy**.</span></span>

    ![Hallo Envoy-koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="e99c2-217">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e99c2-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="e99c2-219">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e99c2-219">Click **Add** button.</span></span> <span data-ttu-id="e99c2-220">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e99c2-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="e99c2-222">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="e99c2-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e99c2-223">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e99c2-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e99c2-224">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e99c2-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e99c2-225">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e99c2-225">Test single sign-on</span></span>

<span data-ttu-id="e99c2-226">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="e99c2-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e99c2-227">Als u op Hallo Envoy-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Envoy-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e99c2-227">When you click hello Envoy tile in hello Access Panel, you should get automatically signed-on tooyour Envoy application.</span></span>
<span data-ttu-id="e99c2-228">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e99c2-228">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e99c2-229">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e99c2-229">Additional resources</span></span>

* [<span data-ttu-id="e99c2-230">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e99c2-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e99c2-231">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e99c2-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

