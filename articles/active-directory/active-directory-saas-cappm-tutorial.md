---
title: 'Zelfstudie: Azure Active Directory-integratie met CA PPM | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en CA-pagina's per minuut.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca9d5e71-e429-4891-8d10-3498e7210e89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 571130f3be0529c986aa0d8a08e4172015cd0b40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ca-ppm"></a><span data-ttu-id="61ca2-103">Zelfstudie: Azure Active Directory-integratie met CA PPM</span><span class="sxs-lookup"><span data-stu-id="61ca2-103">Tutorial: Azure Active Directory integration with CA PPM</span></span>

<span data-ttu-id="61ca2-104">In deze zelfstudie leert u hoe toointegrate CA PPM met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="61ca2-104">In this tutorial, you learn how toointegrate CA PPM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="61ca2-105">CA PPM integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="61ca2-105">Integrating CA PPM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="61ca2-106">U kunt beheren in Azure AD wie toegang tot tooCA pagina's per minuut heeft</span><span class="sxs-lookup"><span data-stu-id="61ca2-106">You can control in Azure AD who has access tooCA PPM</span></span>
- <span data-ttu-id="61ca2-107">U kunt uw gebruikers tooautomatically get aangemelde tooCA PPM (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="61ca2-107">You can enable your users tooautomatically get signed-on tooCA PPM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="61ca2-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="61ca2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="61ca2-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="61ca2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61ca2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="61ca2-110">Prerequisites</span></span>

<span data-ttu-id="61ca2-111">Azure AD-integratie met CA PPM tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="61ca2-111">tooconfigure Azure AD integration with CA PPM, you need hello following items:</span></span>

- <span data-ttu-id="61ca2-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="61ca2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="61ca2-113">Een CA PPM eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="61ca2-113">A CA PPM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="61ca2-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="61ca2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="61ca2-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="61ca2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="61ca2-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="61ca2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="61ca2-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="61ca2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="61ca2-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="61ca2-118">Scenario description</span></span>
<span data-ttu-id="61ca2-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="61ca2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="61ca2-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="61ca2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="61ca2-121">Het toevoegen van CA PPM van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="61ca2-121">Adding CA PPM from hello gallery</span></span>
2. <span data-ttu-id="61ca2-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="61ca2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ca-ppm-from-hello-gallery"></a><span data-ttu-id="61ca2-123">Het toevoegen van CA PPM van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="61ca2-123">Adding CA PPM from hello gallery</span></span>
<span data-ttu-id="61ca2-124">tooconfigure hello integratie van CA-pagina's per minuut in Azure AD, moet u tooadd CA PPM uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="61ca2-124">tooconfigure hello integration of CA PPM into Azure AD, you need tooadd CA PPM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="61ca2-125">**tooadd CA PPM via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="61ca2-125">**tooadd CA PPM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="61ca2-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="61ca2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="61ca2-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="61ca2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="61ca2-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="61ca2-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="61ca2-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="61ca2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="61ca2-133">Typ in het zoekvak Hallo **CA PPM**.</span><span class="sxs-lookup"><span data-stu-id="61ca2-133">In hello search box, type **CA PPM**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_search.png)

5. <span data-ttu-id="61ca2-135">Selecteer in het deelvenster resultaten hello, **CA PPM**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="61ca2-135">In hello results panel, select **CA PPM**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="61ca2-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="61ca2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="61ca2-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met CA PPM op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="61ca2-138">In this section, you configure and test Azure AD single sign-on with CA PPM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="61ca2-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent CA ppm is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61ca2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CA PPM is tooa user in Azure AD.</span></span> <span data-ttu-id="61ca2-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo CA ppm toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="61ca2-140">In other words, a link relationship between an Azure AD user and hello related user in CA PPM needs toobe established.</span></span>

<span data-ttu-id="61ca2-141">CA-ppm Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="61ca2-141">In CA PPM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="61ca2-142">tooconfigure en test eenmalige aanmelding Azure AD met CA PPM, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="61ca2-142">tooconfigure and test Azure AD single sign-on with CA PPM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="61ca2-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="61ca2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="61ca2-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61ca2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="61ca2-145">**[Maken van een CA PPM testgebruiker](#creating-a-ca-ppm-test-user)**  -toohave een equivalent van Britta Simon CA ppm die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="61ca2-145">**[Creating a CA PPM test user](#creating-a-ca-ppm-test-user)** - toohave a counterpart of Britta Simon in CA PPM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="61ca2-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="61ca2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="61ca2-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="61ca2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="61ca2-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="61ca2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="61ca2-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw CA PPM-toepassing.</span><span class="sxs-lookup"><span data-stu-id="61ca2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CA PPM application.</span></span>

<span data-ttu-id="61ca2-150">**Voer tooconfigure Azure AD eenmalige aanmelding met CA-PPM Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="61ca2-150">**tooconfigure Azure AD single sign-on with CA PPM, perform hello following steps:**</span></span>

1. <span data-ttu-id="61ca2-151">In Azure-portal op Hallo Hallo **CA PPM** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="61ca2-151">In hello Azure portal, on hello **CA PPM** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="61ca2-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="61ca2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_samlbase.png)

3. <span data-ttu-id="61ca2-155">Op Hallo **CA PPM domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="61ca2-155">On hello **CA PPM Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_url.png)

    <span data-ttu-id="61ca2-157">a.</span><span class="sxs-lookup"><span data-stu-id="61ca2-157">a.</span></span> <span data-ttu-id="61ca2-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://ca.ondemand.saml.20.post.<companyname>`</span><span class="sxs-lookup"><span data-stu-id="61ca2-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://ca.ondemand.saml.20.post.<companyname>`</span></span>
    
    <span data-ttu-id="61ca2-159">b.</span><span class="sxs-lookup"><span data-stu-id="61ca2-159">b.</span></span> <span data-ttu-id="61ca2-160">In Hallo **antwoord-URL** textbox type als:`https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="61ca2-160">In hello **Reply URL** textbox, type as: `https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="61ca2-161">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="61ca2-161">This value is not real.</span></span> <span data-ttu-id="61ca2-162">Deze waarde bijwerken Hello werkelijke id.</span><span class="sxs-lookup"><span data-stu-id="61ca2-162">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="61ca2-163">Neem contact op met [CA PPM-ondersteuningsteam](mailto:catechnicalsupport@ca.com) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="61ca2-163">Contact [CA PPM support team](mailto:catechnicalsupport@ca.com) tooget this value.</span></span>
 
4. <span data-ttu-id="61ca2-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="61ca2-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_certificate.png) 

5. <span data-ttu-id="61ca2-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="61ca2-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cappm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="61ca2-168">Op Hallo **CA PPM-configuratie** sectie, klikt u op **configureren CA PPM** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="61ca2-168">On hello **CA PPM Configuration** section, click **Configure CA PPM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="61ca2-169">Kopiëren Hallo **SAML entiteit-ID** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="61ca2-169">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_configure.png) 

7. <span data-ttu-id="61ca2-171">tooconfigure eenmalige aanmelding op **CA PPM** zijde, moet u toosend Hallo gedownload **Certificate(Base64)** en **SAML entiteit-ID** te[ondersteuningsteam CA pagina's per minuut ](mailto:catechnicalsupport@ca.com).</span><span class="sxs-lookup"><span data-stu-id="61ca2-171">tooconfigure single sign-on on **CA PPM** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Entity ID** too[CA PPM support team](mailto:catechnicalsupport@ca.com).</span></span>

> [!TIP]
> <span data-ttu-id="61ca2-172">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="61ca2-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="61ca2-173">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="61ca2-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="61ca2-174">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="61ca2-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="61ca2-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="61ca2-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="61ca2-176">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="61ca2-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="61ca2-178">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="61ca2-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="61ca2-179">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="61ca2-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cappm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="61ca2-181">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="61ca2-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cappm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="61ca2-183">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="61ca2-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cappm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="61ca2-185">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="61ca2-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cappm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="61ca2-187">a.</span><span class="sxs-lookup"><span data-stu-id="61ca2-187">a.</span></span> <span data-ttu-id="61ca2-188">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="61ca2-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="61ca2-189">b.</span><span class="sxs-lookup"><span data-stu-id="61ca2-189">b.</span></span> <span data-ttu-id="61ca2-190">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="61ca2-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="61ca2-191">c.</span><span class="sxs-lookup"><span data-stu-id="61ca2-191">c.</span></span> <span data-ttu-id="61ca2-192">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="61ca2-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="61ca2-193">d.</span><span class="sxs-lookup"><span data-stu-id="61ca2-193">d.</span></span> <span data-ttu-id="61ca2-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="61ca2-194">Click **Create**.</span></span>
 
### <a name="creating-a-ca-ppm-test-user"></a><span data-ttu-id="61ca2-195">Maken van een CA PPM testgebruiker</span><span class="sxs-lookup"><span data-stu-id="61ca2-195">Creating a CA PPM test user</span></span>

<span data-ttu-id="61ca2-196">In deze sectie maakt maken u een gebruiker met de naam van Britta Simon CA ppm.</span><span class="sxs-lookup"><span data-stu-id="61ca2-196">In this section, you create a user called Britta Simon in CA PPM.</span></span> <span data-ttu-id="61ca2-197">Werken met [CA PPM-ondersteuningsteam](mailto:catechnicalsupport@ca.com) tooadd Hallo gebruikers in Hallo CA PPM-platform.</span><span class="sxs-lookup"><span data-stu-id="61ca2-197">Work with [CA PPM support team](mailto:catechnicalsupport@ca.com) tooadd hello users in hello CA PPM platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="61ca2-198">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="61ca2-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="61ca2-199">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooCA pagina's per minuut.</span><span class="sxs-lookup"><span data-stu-id="61ca2-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCA PPM.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="61ca2-201">**tooassign Britta Simon tooCA PPM, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="61ca2-201">**tooassign Britta Simon tooCA PPM, perform hello following steps:**</span></span>

1. <span data-ttu-id="61ca2-202">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="61ca2-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="61ca2-204">Selecteer in de lijst met de toepassingen van Hallo **CA PPM**.</span><span class="sxs-lookup"><span data-stu-id="61ca2-204">In hello applications list, select **CA PPM**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_app.png) 

3. <span data-ttu-id="61ca2-206">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="61ca2-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="61ca2-208">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="61ca2-208">Click **Add** button.</span></span> <span data-ttu-id="61ca2-209">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="61ca2-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="61ca2-211">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="61ca2-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="61ca2-212">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="61ca2-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="61ca2-213">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="61ca2-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="61ca2-214">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="61ca2-214">Testing single sign-on</span></span>

<span data-ttu-id="61ca2-215">In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="61ca2-215">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="61ca2-216">Als u op Hallo CA PPM-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour CA PPM-toepassing.</span><span class="sxs-lookup"><span data-stu-id="61ca2-216">When you click hello CA PPM tile in hello Access Panel, you should get automatically signed-on tooyour CA PPM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="61ca2-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="61ca2-217">Additional resources</span></span>

* [<span data-ttu-id="61ca2-218">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61ca2-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="61ca2-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="61ca2-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_203.png

