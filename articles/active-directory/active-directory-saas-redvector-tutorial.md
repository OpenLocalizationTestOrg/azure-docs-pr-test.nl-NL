---
title: 'Zelfstudie: Azure Active Directory-integratie met RedVector | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en RedVector.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 99042f39-0ab2-475b-8df8-3016d7f875e9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 4b866911769dcd1a5e6fe978f2c42e680215b4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-redvector"></a><span data-ttu-id="da663-103">Zelfstudie: Azure Active Directory-integratie met RedVector</span><span class="sxs-lookup"><span data-stu-id="da663-103">Tutorial: Azure Active Directory integration with RedVector</span></span>

<span data-ttu-id="da663-104">In deze zelfstudie leert u hoe toointegrate RedVector met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="da663-104">In this tutorial, you learn how toointegrate RedVector with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="da663-105">RedVector integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="da663-105">Integrating RedVector with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="da663-106">U kunt beheren in Azure AD die tooRedVector toegang heeft</span><span class="sxs-lookup"><span data-stu-id="da663-106">You can control in Azure AD who has access tooRedVector</span></span>
- <span data-ttu-id="da663-107">U kunt uw gebruikers tooautomatically get aangemelde tooRedVector (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="da663-107">You can enable your users tooautomatically get signed-on tooRedVector (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="da663-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="da663-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="da663-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="da663-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da663-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="da663-110">Prerequisites</span></span>

<span data-ttu-id="da663-111">Azure AD-integratie met RedVector tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="da663-111">tooconfigure Azure AD integration with RedVector, you need hello following items:</span></span>

- <span data-ttu-id="da663-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="da663-112">An Azure AD subscription</span></span>
- <span data-ttu-id="da663-113">Een RedVector eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="da663-113">A RedVector single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="da663-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="da663-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="da663-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="da663-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="da663-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="da663-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="da663-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="da663-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="da663-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="da663-118">Scenario description</span></span>
<span data-ttu-id="da663-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="da663-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="da663-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="da663-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="da663-121">Het toevoegen van RedVector van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="da663-121">Adding RedVector from hello gallery</span></span>
2. <span data-ttu-id="da663-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="da663-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-redvector-from-hello-gallery"></a><span data-ttu-id="da663-123">Het toevoegen van RedVector van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="da663-123">Adding RedVector from hello gallery</span></span>
<span data-ttu-id="da663-124">tooconfigure hello integratie van RedVector in Azure AD, moet u tooadd RedVector uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="da663-124">tooconfigure hello integration of RedVector into Azure AD, you need tooadd RedVector from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="da663-125">**tooadd RedVector via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="da663-125">**tooadd RedVector from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="da663-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="da663-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="da663-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="da663-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="da663-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="da663-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="da663-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="da663-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="da663-133">Typ in het zoekvak Hallo **RedVector**.</span><span class="sxs-lookup"><span data-stu-id="da663-133">In hello search box, type **RedVector**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_search.png)

5. <span data-ttu-id="da663-135">Selecteer in het deelvenster resultaten hello, **RedVector**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="da663-135">In hello results panel, select **RedVector**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="da663-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="da663-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="da663-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met RedVector op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="da663-138">In this section, you configure and test Azure AD single sign-on with RedVector based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="da663-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in RedVector is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da663-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RedVector is tooa user in Azure AD.</span></span> <span data-ttu-id="da663-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in RedVector toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="da663-140">In other words, a link relationship between an Azure AD user and hello related user in RedVector needs toobe established.</span></span>

<span data-ttu-id="da663-141">Wijs in RedVector, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="da663-141">In RedVector, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="da663-142">tooconfigure en eenmalige aanmelding Azure AD-test met RedVector, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="da663-142">tooconfigure and test Azure AD single sign-on with RedVector, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="da663-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="da663-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="da663-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="da663-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="da663-145">**[Maken van een testgebruiker RedVector](#creating-a-redvector-test-user)**  -toohave een equivalent van Britta Simon in RedVector die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="da663-145">**[Creating a RedVector test user](#creating-a-redvector-test-user)** - toohave a counterpart of Britta Simon in RedVector that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="da663-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="da663-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="da663-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="da663-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="da663-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="da663-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="da663-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing RedVector configureren.</span><span class="sxs-lookup"><span data-stu-id="da663-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RedVector application.</span></span>

<span data-ttu-id="da663-150">**Azure AD tooconfigure eenmalige aanmelding met RedVector, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="da663-150">**tooconfigure Azure AD single sign-on with RedVector, perform hello following steps:**</span></span>

1. <span data-ttu-id="da663-151">In de Azure-portal op Hallo Hallo **RedVector** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="da663-151">In hello Azure portal, on hello **RedVector** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="da663-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="da663-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_samlbase.png)

3. <span data-ttu-id="da663-155">Op Hallo **RedVector domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="da663-155">On hello **RedVector Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_url.png)

    <span data-ttu-id="da663-157">a.</span><span class="sxs-lookup"><span data-stu-id="da663-157">a.</span></span> <span data-ttu-id="da663-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://sso2.redvector.com/adfs/<Companyname>`</span><span class="sxs-lookup"><span data-stu-id="da663-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso2.redvector.com/adfs/<Companyname>`</span></span>

    <span data-ttu-id="da663-159">b.</span><span class="sxs-lookup"><span data-stu-id="da663-159">b.</span></span> <span data-ttu-id="da663-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<Companyname>.redvector.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="da663-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<Companyname>.redvector.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="da663-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="da663-161">These values are not real.</span></span> <span data-ttu-id="da663-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="da663-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="da663-163">Neem contact op met [RedVector Client ondersteuningsteam](mailto:sso@redvector.com) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="da663-163">Contact [RedVector Client support team](mailto:sso@redvector.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="da663-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="da663-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_certificate.png) 

5. <span data-ttu-id="da663-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="da663-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-redvector-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="da663-168">Op Hallo **RedVector configuratie** sectie, klikt u op **configureren RedVector** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="da663-168">On hello **RedVector Configuration** section, click **Configure RedVector** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="da663-169">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="da663-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_configure.png) 

7. <span data-ttu-id="da663-171">tooconfigure eenmalige aanmelding op **RedVector** zijde, moet u toosend Hallo gedownload **certificaat (Base64)** en **SAML Single Sign-On Service-URL** te[RedVector ondersteuningsteam](mailto:sso@redvector.com).</span><span class="sxs-lookup"><span data-stu-id="da663-171">tooconfigure single sign-on on **RedVector** side, you need toosend hello downloaded **Certificate (Base64)** and **SAML Single Sign-On Service URL** too[RedVector support team](mailto:sso@redvector.com).</span></span> <span data-ttu-id="da663-172">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="da663-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="da663-173">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="da663-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="da663-174">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="da663-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="da663-175">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="da663-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="da663-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="da663-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="da663-177">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="da663-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="da663-179">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="da663-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="da663-180">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="da663-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-redvector-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="da663-182">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="da663-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-redvector-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="da663-184">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="da663-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-redvector-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="da663-186">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="da663-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-redvector-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="da663-188">a.</span><span class="sxs-lookup"><span data-stu-id="da663-188">a.</span></span> <span data-ttu-id="da663-189">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="da663-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="da663-190">b.</span><span class="sxs-lookup"><span data-stu-id="da663-190">b.</span></span> <span data-ttu-id="da663-191">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="da663-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="da663-192">c.</span><span class="sxs-lookup"><span data-stu-id="da663-192">c.</span></span> <span data-ttu-id="da663-193">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="da663-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="da663-194">d.</span><span class="sxs-lookup"><span data-stu-id="da663-194">d.</span></span> <span data-ttu-id="da663-195">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="da663-195">Click **Create**.</span></span>
 
### <a name="creating-a-redvector-test-user"></a><span data-ttu-id="da663-196">Een testgebruiker RedVector maken</span><span class="sxs-lookup"><span data-stu-id="da663-196">Creating a RedVector test user</span></span>

<span data-ttu-id="da663-197">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in RedVector maken.</span><span class="sxs-lookup"><span data-stu-id="da663-197">In this section, you create a user called Britta Simon in RedVector.</span></span> <span data-ttu-id="da663-198">Als u niet weet hoe tooadd Britta Simon in RedVector, werken met [RedVector ondersteuningsteam](mailto:sso@redvector.com) tooadd testgebruiker Hallo en SSO in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="da663-198">If you don't know how tooadd Britta Simon in RedVector, Work with [RedVector support team](mailto:sso@redvector.com) tooadd hello test user and enable SSO.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="da663-199">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="da663-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="da663-200">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooRedVector toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="da663-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRedVector.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="da663-202">**tooassign Britta Simon tooRedVector, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="da663-202">**tooassign Britta Simon tooRedVector, perform hello following steps:**</span></span>

1. <span data-ttu-id="da663-203">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="da663-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="da663-205">Selecteer in de lijst met de toepassingen van Hallo **RedVector**.</span><span class="sxs-lookup"><span data-stu-id="da663-205">In hello applications list, select **RedVector**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-redvector-tutorial/tutorial_redvector_app.png) 

3. <span data-ttu-id="da663-207">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="da663-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="da663-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="da663-209">Click **Add** button.</span></span> <span data-ttu-id="da663-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="da663-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="da663-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="da663-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="da663-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="da663-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="da663-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="da663-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="da663-215">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="da663-215">Testing single sign-on</span></span>

<span data-ttu-id="da663-216">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="da663-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="da663-217">Als u op Hallo RedVector tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour RedVector toepassing...</span><span class="sxs-lookup"><span data-stu-id="da663-217">When you click hello RedVector tile in hello Access Panel, you should get automatically signed-on tooyour RedVector application..</span></span>

## <a name="additional-resources"></a><span data-ttu-id="da663-218">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="da663-218">Additional resources</span></span>

* [<span data-ttu-id="da663-219">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="da663-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="da663-220">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="da663-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_203.png

