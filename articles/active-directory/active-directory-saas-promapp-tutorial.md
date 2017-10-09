---
title: 'Zelfstudie: Azure Active Directory-integratie met Promapp | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Promapp.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 02de7679b0c86d7aa8cacb41762f900dbf2ff231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="25620-103">Zelfstudie: Azure Active Directory-integratie met Promapp</span><span class="sxs-lookup"><span data-stu-id="25620-103">Tutorial: Azure Active Directory integration with Promapp</span></span>

<span data-ttu-id="25620-104">In deze zelfstudie leert u hoe toointegrate Promapp met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="25620-104">In this tutorial, you learn how toointegrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="25620-105">Promapp integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="25620-105">Integrating Promapp with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="25620-106">U kunt beheren in Azure AD die tooPromapp toegang heeft</span><span class="sxs-lookup"><span data-stu-id="25620-106">You can control in Azure AD who has access tooPromapp</span></span>
- <span data-ttu-id="25620-107">U kunt uw gebruikers tooautomatically get aangemelde tooPromapp (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="25620-107">You can enable your users tooautomatically get signed-on tooPromapp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="25620-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="25620-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="25620-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="25620-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25620-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="25620-110">Prerequisites</span></span>

<span data-ttu-id="25620-111">Azure AD-integratie met Promapp tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="25620-111">tooconfigure Azure AD integration with Promapp, you need hello following items:</span></span>

- <span data-ttu-id="25620-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="25620-112">An Azure AD subscription</span></span>
- <span data-ttu-id="25620-113">Een Promapp eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="25620-113">A Promapp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="25620-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="25620-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="25620-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="25620-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="25620-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="25620-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="25620-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="25620-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="25620-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="25620-118">Scenario description</span></span>
<span data-ttu-id="25620-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="25620-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="25620-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="25620-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="25620-121">Het toevoegen van Promapp van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="25620-121">Adding Promapp from hello gallery</span></span>
2. <span data-ttu-id="25620-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="25620-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promapp-from-hello-gallery"></a><span data-ttu-id="25620-123">Het toevoegen van Promapp van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="25620-123">Adding Promapp from hello gallery</span></span>
<span data-ttu-id="25620-124">tooconfigure hello integratie van Promapp in Azure AD, moet u tooadd Promapp uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="25620-124">tooconfigure hello integration of Promapp into Azure AD, you need tooadd Promapp from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="25620-125">**tooadd Promapp via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="25620-125">**tooadd Promapp from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="25620-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="25620-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="25620-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="25620-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="25620-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="25620-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="25620-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="25620-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="25620-133">Typ in het zoekvak Hallo **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="25620-133">In hello search box, type **Promapp**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_search.png)

5. <span data-ttu-id="25620-135">Selecteer in het deelvenster resultaten hello, **Promapp**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="25620-135">In hello results panel, select **Promapp**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="25620-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="25620-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="25620-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Promapp op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="25620-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="25620-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Promapp is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25620-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Promapp is tooa user in Azure AD.</span></span> <span data-ttu-id="25620-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Promapp toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="25620-140">In other words, a link relationship between an Azure AD user and hello related user in Promapp needs toobe established.</span></span>

<span data-ttu-id="25620-141">Wijs in Promapp, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="25620-141">In Promapp, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="25620-142">tooconfigure en eenmalige aanmelding Azure AD-test met Promapp, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="25620-142">tooconfigure and test Azure AD single sign-on with Promapp, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="25620-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="25620-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="25620-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="25620-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="25620-145">**[Maken van een testgebruiker Promapp](#creating-a-promapp-test-user)**  -toohave een equivalent van Britta Simon in Promapp die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="25620-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - toohave a counterpart of Britta Simon in Promapp that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="25620-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="25620-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="25620-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="25620-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="25620-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="25620-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="25620-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Promapp configureren.</span><span class="sxs-lookup"><span data-stu-id="25620-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Promapp application.</span></span>

<span data-ttu-id="25620-150">**Azure AD tooconfigure eenmalige aanmelding met Promapp, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="25620-150">**tooconfigure Azure AD single sign-on with Promapp, perform hello following steps:**</span></span>

1. <span data-ttu-id="25620-151">In de Azure-portal op Hallo Hallo **Promapp** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="25620-151">In hello Azure portal, on hello **Promapp** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="25620-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="25620-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_samlbase.png)

3. <span data-ttu-id="25620-155">Op Hallo **Promapp domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="25620-155">On hello **Promapp Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_url.png)

    <span data-ttu-id="25620-157">a.</span><span class="sxs-lookup"><span data-stu-id="25620-157">a.</span></span> <span data-ttu-id="25620-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span><span class="sxs-lookup"><span data-stu-id="25620-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span></span>

    <span data-ttu-id="25620-159">b.</span><span class="sxs-lookup"><span data-stu-id="25620-159">b.</span></span> <span data-ttu-id="25620-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://DOMAINNAME.promapp.com/TENANTNAME`</span><span class="sxs-lookup"><span data-stu-id="25620-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="25620-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="25620-161">These values are not real.</span></span> <span data-ttu-id="25620-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="25620-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="25620-163">Neem contact op met [Promapp Client ondersteuningsteam](https://www.promapp.com/about-us/contact-us/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="25620-163">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="25620-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="25620-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_certificate.png) 

5. <span data-ttu-id="25620-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="25620-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-promapp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="25620-168">Op Hallo **Promapp configuratie** sectie, klikt u op **configureren Promapp** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="25620-168">On hello **Promapp Configuration** section, click **Configure Promapp** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="25620-169">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="25620-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_configure.png) 

7. <span data-ttu-id="25620-171">Eenmalige aanmelding tooyour Promapp bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="25620-171">Sign-on tooyour Promapp company site as administrator.</span></span> 

8. <span data-ttu-id="25620-172">Klik in het menu bovenaan Hallo Hallo **Admin**.</span><span class="sxs-lookup"><span data-stu-id="25620-172">In hello menu on hello top, click **Admin**.</span></span> 
   
    ![Azure AD voor eenmalige aanmelding][12]

9. <span data-ttu-id="25620-174">Klik op **Configureren**</span><span class="sxs-lookup"><span data-stu-id="25620-174">Click **Configure**.</span></span> 
   
    ![Azure AD voor eenmalige aanmelding][13]

10. <span data-ttu-id="25620-176">Op Hallo **beveiliging** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="25620-176">On hello **Security** dialog, perform hello following steps:</span></span>
   
    ![Azure AD voor eenmalige aanmelding][14]
    
    <span data-ttu-id="25620-178">a.</span><span class="sxs-lookup"><span data-stu-id="25620-178">a.</span></span> <span data-ttu-id="25620-179">Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd uit hello Azure-portal in Hallo **SSO-aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="25620-179">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **SSO-Login URL** textbox.</span></span>
    
    <span data-ttu-id="25620-180">b.</span><span class="sxs-lookup"><span data-stu-id="25620-180">b.</span></span> <span data-ttu-id="25620-181">Als **SSO - modus Single Sign-on**, selecteer **optioneel**, en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="25620-181">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>

    <span data-ttu-id="25620-182">c.</span><span class="sxs-lookup"><span data-stu-id="25620-182">c.</span></span> <span data-ttu-id="25620-183">Open Hallo certificaat in Kladblok kopie Hallo certificaatinhoud gedownload zonder Hallo eerste regel (---BEGIN CERTIFICATE---) en Hallo laatste regel (---einde certificaat---), plakt u deze in Hallo **SSO x.509-certificaat** tekstvak en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="25620-183">Open hello downloaded certificate in notepad, copy hello certificate content without hello first line (-----BEGIN CERTIFICATE-----) and hello last line (-----END CERTIFICATE-----), paste it into hello **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
        
> [!TIP]
> <span data-ttu-id="25620-184">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="25620-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="25620-185">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="25620-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="25620-186">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="25620-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="25620-187">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="25620-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="25620-188">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="25620-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="25620-190">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="25620-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="25620-191">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="25620-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-promapp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="25620-193">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="25620-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-promapp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="25620-195">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="25620-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-promapp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="25620-197">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="25620-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-promapp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="25620-199">a.</span><span class="sxs-lookup"><span data-stu-id="25620-199">a.</span></span> <span data-ttu-id="25620-200">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="25620-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="25620-201">b.</span><span class="sxs-lookup"><span data-stu-id="25620-201">b.</span></span> <span data-ttu-id="25620-202">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="25620-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="25620-203">c.</span><span class="sxs-lookup"><span data-stu-id="25620-203">c.</span></span> <span data-ttu-id="25620-204">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="25620-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="25620-205">d.</span><span class="sxs-lookup"><span data-stu-id="25620-205">d.</span></span> <span data-ttu-id="25620-206">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="25620-206">Click **Create**.</span></span>
 
### <a name="creating-a-promapp-test-user"></a><span data-ttu-id="25620-207">Een testgebruiker Promapp maken</span><span class="sxs-lookup"><span data-stu-id="25620-207">Creating a Promapp test user</span></span>

<span data-ttu-id="25620-208">Hallo Promapp toepassing biedt ondersteuning voor Just-in-Time-inrichting.</span><span class="sxs-lookup"><span data-stu-id="25620-208">hello Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="25620-209">Dit betekent een gebruikersaccount wordt automatisch gemaakt indien nodig tijdens een poging tooaccess Hallo toepassing hello Toegangsvenster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="25620-209">This means, a user account is automatically created if necessary during an attempt tooaccess hello application using hello Access Panel.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="25620-210">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="25620-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="25620-211">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooPromapp toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="25620-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPromapp.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="25620-213">**tooassign Britta Simon tooPromapp, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="25620-213">**tooassign Britta Simon tooPromapp, perform hello following steps:**</span></span>

1. <span data-ttu-id="25620-214">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="25620-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="25620-216">Selecteer in de lijst met de toepassingen van Hallo **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="25620-216">In hello applications list, select **Promapp**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_app.png) 

3. <span data-ttu-id="25620-218">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="25620-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="25620-220">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="25620-220">Click **Add** button.</span></span> <span data-ttu-id="25620-221">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="25620-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="25620-223">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="25620-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="25620-224">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="25620-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="25620-225">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="25620-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="25620-226">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="25620-226">Testing single sign-on</span></span>

<span data-ttu-id="25620-227">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="25620-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="25620-228">Als u op Hallo Promapp tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Promapp toepassing.</span><span class="sxs-lookup"><span data-stu-id="25620-228">When you click hello Promapp tile in hello Access Panel, you should get automatically signed-on tooyour Promapp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="25620-229">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="25620-229">Additional resources</span></span>

* [<span data-ttu-id="25620-230">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25620-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="25620-231">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="25620-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_05.png
[13]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_06.png
[14]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_07.png

[100]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_203.png

