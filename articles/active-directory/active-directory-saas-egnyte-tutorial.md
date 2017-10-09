---
title: 'Zelfstudie: Azure Active Directory-integratie met Egnyte | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Egnyte.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: d86fa28a1e7b23474cb76c08aef8539acadaf24d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="0740c-103">Zelfstudie: Azure Active Directory-integratie met Egnyte</span><span class="sxs-lookup"><span data-stu-id="0740c-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="0740c-104">In deze zelfstudie leert u hoe toointegrate Egnyte met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0740c-104">In this tutorial, you learn how toointegrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0740c-105">Egnyte integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="0740c-105">Integrating Egnyte with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0740c-106">U kunt beheren in Azure AD die tooEgnyte toegang heeft</span><span class="sxs-lookup"><span data-stu-id="0740c-106">You can control in Azure AD who has access tooEgnyte</span></span>
- <span data-ttu-id="0740c-107">U kunt uw gebruikers tooautomatically get aangemelde tooEgnyte (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="0740c-107">You can enable your users tooautomatically get signed-on tooEgnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0740c-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="0740c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0740c-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0740c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0740c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0740c-110">Prerequisites</span></span>

<span data-ttu-id="0740c-111">Azure AD-integratie met Egnyte tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="0740c-111">tooconfigure Azure AD integration with Egnyte, you need hello following items:</span></span>

- <span data-ttu-id="0740c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="0740c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0740c-113">Een Egnyte eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="0740c-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0740c-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="0740c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0740c-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="0740c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0740c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="0740c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0740c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0740c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0740c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="0740c-118">Scenario description</span></span>
<span data-ttu-id="0740c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="0740c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0740c-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="0740c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0740c-121">Het toevoegen van Egnyte van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="0740c-121">Adding Egnyte from hello gallery</span></span>
2. <span data-ttu-id="0740c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0740c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-hello-gallery"></a><span data-ttu-id="0740c-123">Het toevoegen van Egnyte van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="0740c-123">Adding Egnyte from hello gallery</span></span>
<span data-ttu-id="0740c-124">tooconfigure hello integratie van Egnyte in Azure AD, moet u tooadd Egnyte uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="0740c-124">tooconfigure hello integration of Egnyte into Azure AD, you need tooadd Egnyte from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0740c-125">**tooadd Egnyte via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0740c-125">**tooadd Egnyte from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0740c-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0740c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0740c-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0740c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0740c-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0740c-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="0740c-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0740c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="0740c-133">Typ in het zoekvak Hallo **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="0740c-133">In hello search box, type **Egnyte**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. <span data-ttu-id="0740c-135">Selecteer in het deelvenster resultaten hello, **Egnyte**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0740c-135">In hello results panel, select **Egnyte**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0740c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0740c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0740c-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Egnyte op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="0740c-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0740c-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Egnyte is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0740c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Egnyte is tooa user in Azure AD.</span></span> <span data-ttu-id="0740c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Egnyte toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="0740c-140">In other words, a link relationship between an Azure AD user and hello related user in Egnyte needs toobe established.</span></span>

<span data-ttu-id="0740c-141">Wijs in Egnyte, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="0740c-141">In Egnyte, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0740c-142">tooconfigure en eenmalige aanmelding Azure AD-test met Egnyte, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0740c-142">tooconfigure and test Azure AD single sign-on with Egnyte, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0740c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="0740c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0740c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0740c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0740c-145">**[Maken van een testgebruiker Egnyte](#creating-an-egnyte-test-user)**  -toohave een equivalent van Britta Simon in Egnyte die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="0740c-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - toohave a counterpart of Britta Simon in Egnyte that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0740c-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0740c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0740c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="0740c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0740c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="0740c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0740c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Egnyte configureren.</span><span class="sxs-lookup"><span data-stu-id="0740c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="0740c-150">**Azure AD tooconfigure eenmalige aanmelding met Egnyte, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0740c-150">**tooconfigure Azure AD single sign-on with Egnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="0740c-151">In de Azure-portal op Hallo Hallo **Egnyte** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="0740c-151">In hello Azure portal, on hello **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="0740c-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0740c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. <span data-ttu-id="0740c-155">Op Hallo **Egnyte domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0740c-155">On hello **Egnyte Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="0740c-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.egnyte.com`</span><span class="sxs-lookup"><span data-stu-id="0740c-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0740c-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="0740c-158">This value is not real.</span></span> <span data-ttu-id="0740c-159">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="0740c-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="0740c-160">Neem contact op met [Egnyte Client ondersteuningsteam](https://www.egnyte.com/corp/contact_egnyte.html) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="0740c-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="0740c-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="0740c-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. <span data-ttu-id="0740c-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="0740c-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0740c-165">Op Hallo **Egnyte configuratie** sectie, klikt u op **configureren Egnyte** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="0740c-165">On hello **Egnyte Configuration** section, click **Configure Egnyte** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0740c-166">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="0740c-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. <span data-ttu-id="0740c-168">In een ander browservenster, meld u aan tooyour Egnyte bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="0740c-168">In a different web browser window, log in tooyour Egnyte company site as an administrator.</span></span>

8. <span data-ttu-id="0740c-169">Klik op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="0740c-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="0740c-170">![Instellingen](./media/active-directory-saas-egnyte-tutorial/ic787819.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="0740c-170">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Settings")</span></span>

9. <span data-ttu-id="0740c-171">Hallo-menu en klik op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="0740c-171">In hello menu, click **Settings**.</span></span>

   <span data-ttu-id="0740c-172">![Instellingen](./media/active-directory-saas-egnyte-tutorial/ic787820.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="0740c-172">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Settings")</span></span>

10. <span data-ttu-id="0740c-173">Klik op Hallo **configuratie** tabblad en klik vervolgens op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="0740c-173">Click hello **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="0740c-174">![Beveiliging](./media/active-directory-saas-egnyte-tutorial/ic787821.png "beveiliging")</span><span class="sxs-lookup"><span data-stu-id="0740c-174">![Security](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Security")</span></span>

11. <span data-ttu-id="0740c-175">In Hallo **eenmalige aanmelding verificatie** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0740c-175">In hello **Single Sign-On Authentication** section, perform hello following steps:</span></span>

    <span data-ttu-id="0740c-176">![Eenmalige verificatie](./media/active-directory-saas-egnyte-tutorial/ic787822.png "eenmalige-verificatie")</span><span class="sxs-lookup"><span data-stu-id="0740c-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="0740c-177">a.</span><span class="sxs-lookup"><span data-stu-id="0740c-177">a.</span></span> <span data-ttu-id="0740c-178">Als **eenmalige aanmelding verificatie**, selecteer **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="0740c-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="0740c-179">b.</span><span class="sxs-lookup"><span data-stu-id="0740c-179">b.</span></span> <span data-ttu-id="0740c-180">Als **identiteitsprovider**, selecteer **AzureAD**.</span><span class="sxs-lookup"><span data-stu-id="0740c-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="0740c-181">c.</span><span class="sxs-lookup"><span data-stu-id="0740c-181">c.</span></span> <span data-ttu-id="0740c-182">Plakken **SAML Single Sign-On Service-URL** gekopieerd vanuit Azure-portal naar Hallo **identiteit provider aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="0740c-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into hello **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="0740c-183">d.</span><span class="sxs-lookup"><span data-stu-id="0740c-183">d.</span></span> <span data-ttu-id="0740c-184">Plakken **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal in Hallo **identiteit provider entiteit-ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="0740c-184">Paste **SAML Entity ID** which you have copied from Azure portal into hello **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="0740c-185">e.</span><span class="sxs-lookup"><span data-stu-id="0740c-185">e.</span></span> <span data-ttu-id="0740c-186">De base-64 gecodeerde certificaat openen in Kladblok gedownload vanuit Azure-portal kopie Hallo inhoud ervan naar het Klembord en plak deze toohello **provider identiteitscertificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="0740c-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="0740c-187">f.</span><span class="sxs-lookup"><span data-stu-id="0740c-187">f.</span></span> <span data-ttu-id="0740c-188">Als **standaard Gebruikerskoppeling**, selecteer **e-mailadres**.</span><span class="sxs-lookup"><span data-stu-id="0740c-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="0740c-189">g.</span><span class="sxs-lookup"><span data-stu-id="0740c-189">g.</span></span> <span data-ttu-id="0740c-190">Als **domeinspecifieke verlener waarde**, selecteer **uitgeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="0740c-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="0740c-191">h.</span><span class="sxs-lookup"><span data-stu-id="0740c-191">h.</span></span> <span data-ttu-id="0740c-192">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="0740c-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0740c-193">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="0740c-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0740c-194">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="0740c-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0740c-195">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0740c-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0740c-196">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="0740c-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="0740c-197">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0740c-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="0740c-199">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0740c-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0740c-200">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0740c-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0740c-202">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="0740c-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0740c-204">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="0740c-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0740c-206">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0740c-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0740c-208">a.</span><span class="sxs-lookup"><span data-stu-id="0740c-208">a.</span></span> <span data-ttu-id="0740c-209">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0740c-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0740c-210">b.</span><span class="sxs-lookup"><span data-stu-id="0740c-210">b.</span></span> <span data-ttu-id="0740c-211">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0740c-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0740c-212">c.</span><span class="sxs-lookup"><span data-stu-id="0740c-212">c.</span></span> <span data-ttu-id="0740c-213">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="0740c-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0740c-214">d.</span><span class="sxs-lookup"><span data-stu-id="0740c-214">d.</span></span> <span data-ttu-id="0740c-215">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0740c-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="0740c-216">Een testgebruiker Egnyte maken</span><span class="sxs-lookup"><span data-stu-id="0740c-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="0740c-217">Azure AD tooenable gebruikers toolog in tooEgnyte, ze in Egnyte moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="0740c-217">tooenable Azure AD users toolog in tooEgnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="0740c-218">In geval van Egnyte Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="0740c-218">In hello case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="0740c-219">**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**</span><span class="sxs-lookup"><span data-stu-id="0740c-219">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="0740c-220">Meld u bij tooyour **Egnyte** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="0740c-220">Log in tooyour **Egnyte** company site as administrator.</span></span>

2. <span data-ttu-id="0740c-221">Ga te**instellingen \> gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="0740c-221">Go too**Settings \> Users & Groups**.</span></span>

3. <span data-ttu-id="0740c-222">Klik op **nieuwe gebruiker toevoegen**, en selecteer vervolgens Hallo-type van de gebruiker gewenste tooadd.</span><span class="sxs-lookup"><span data-stu-id="0740c-222">Click **Add New User**, and then select hello type of user you want tooadd.</span></span>
   
   <span data-ttu-id="0740c-223">![Gebruikers](./media/active-directory-saas-egnyte-tutorial/ic787824.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="0740c-223">![Users](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Users")</span></span>

4. <span data-ttu-id="0740c-224">In Hallo **nieuwe standaardgebruiker** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0740c-224">In hello **New Standard User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="0740c-225">![Nieuwe standaardgebruiker](./media/active-directory-saas-egnyte-tutorial/ic787825.png "nieuwe standaardgebruiker")</span><span class="sxs-lookup"><span data-stu-id="0740c-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="0740c-226">a.</span><span class="sxs-lookup"><span data-stu-id="0740c-226">a.</span></span> <span data-ttu-id="0740c-227">Type Hallo **e**, **gebruikersnaam**, en andere details van een geldige Azure Active Directory-account dat u wilt dat tooprovision.</span><span class="sxs-lookup"><span data-stu-id="0740c-227">Type hello **Email**, **Username**, and other details of a valid Azure Active Directory account you want tooprovision.</span></span>
   
   <span data-ttu-id="0740c-228">b.</span><span class="sxs-lookup"><span data-stu-id="0740c-228">b.</span></span> <span data-ttu-id="0740c-229">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="0740c-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="0740c-230">Hello Azure Active Directory-accounthouder ontvangt een melding per e-mail.</span><span class="sxs-lookup"><span data-stu-id="0740c-230">hello Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="0740c-231">U kunt andere Egnyte gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Egnyte tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="0740c-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0740c-232">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0740c-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0740c-233">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooEgnyte toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="0740c-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEgnyte.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="0740c-235">**tooassign Britta Simon tooEgnyte, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="0740c-235">**tooassign Britta Simon tooEgnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="0740c-236">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0740c-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="0740c-238">Selecteer in de lijst met de toepassingen van Hallo **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="0740c-238">In hello applications list, select **Egnyte**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. <span data-ttu-id="0740c-240">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="0740c-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="0740c-242">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="0740c-242">Click **Add** button.</span></span> <span data-ttu-id="0740c-243">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0740c-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="0740c-245">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="0740c-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0740c-246">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0740c-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0740c-247">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0740c-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0740c-248">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0740c-248">Testing single sign-on</span></span>

<span data-ttu-id="0740c-249">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="0740c-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0740c-250">Als u op Hallo Egnyte tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Egnyte toepassing.</span><span class="sxs-lookup"><span data-stu-id="0740c-250">When you click hello Egnyte tile in hello Access Panel, you should get automatically signed-on tooyour Egnyte application.</span></span>
<span data-ttu-id="0740c-251">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0740c-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0740c-252">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="0740c-252">Additional resources</span></span>

* [<span data-ttu-id="0740c-253">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0740c-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0740c-254">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0740c-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

