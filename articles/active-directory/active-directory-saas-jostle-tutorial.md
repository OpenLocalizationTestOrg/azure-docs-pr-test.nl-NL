---
title: 'Zelfstudie: Azure Active Directory-integratie met Jostle | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Jostle.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ca4ca1f-8f68-4225-81a6-1666b486d6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 617375d8f9e1cebcdb28450fc8d0ad8af99d7b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jostle"></a><span data-ttu-id="8afac-103">Zelfstudie: Azure Active Directory-integratie met Jostle</span><span class="sxs-lookup"><span data-stu-id="8afac-103">Tutorial: Azure Active Directory integration with Jostle</span></span>

<span data-ttu-id="8afac-104">In deze zelfstudie leert u hoe toointegrate Jostle met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8afac-104">In this tutorial, you learn how toointegrate Jostle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8afac-105">Jostle integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="8afac-105">Integrating Jostle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8afac-106">U kunt beheren in Azure AD die tooJostle toegang heeft</span><span class="sxs-lookup"><span data-stu-id="8afac-106">You can control in Azure AD who has access tooJostle</span></span>
- <span data-ttu-id="8afac-107">U kunt uw gebruikers tooautomatically get aangemelde tooJostle (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="8afac-107">You can enable your users tooautomatically get signed-on tooJostle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8afac-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="8afac-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8afac-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8afac-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8afac-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8afac-110">Prerequisites</span></span>

<span data-ttu-id="8afac-111">tooconfigure Azure AD-integratie met Jostle, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="8afac-111">tooconfigure Azure AD integration with Jostle, you need hello following items:</span></span>

- <span data-ttu-id="8afac-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="8afac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8afac-113">Een Jostle eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="8afac-113">A Jostle single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8afac-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="8afac-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8afac-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="8afac-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8afac-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="8afac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8afac-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8afac-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8afac-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="8afac-118">Scenario description</span></span>
<span data-ttu-id="8afac-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="8afac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8afac-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="8afac-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8afac-121">Het toevoegen van Jostle van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="8afac-121">Adding Jostle from hello gallery</span></span>
2. <span data-ttu-id="8afac-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8afac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jostle-from-hello-gallery"></a><span data-ttu-id="8afac-123">Het toevoegen van Jostle van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="8afac-123">Adding Jostle from hello gallery</span></span>
<span data-ttu-id="8afac-124">tooconfigure hello integratie van Jostle in Azure AD, moet u tooadd Jostle uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="8afac-124">tooconfigure hello integration of Jostle into Azure AD, you need tooadd Jostle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8afac-125">**tooadd Jostle via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8afac-125">**tooadd Jostle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8afac-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8afac-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8afac-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8afac-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8afac-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8afac-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="8afac-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8afac-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="8afac-133">Typ in het zoekvak Hallo **Jostle**.</span><span class="sxs-lookup"><span data-stu-id="8afac-133">In hello search box, type **Jostle**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_search.png)

5. <span data-ttu-id="8afac-135">Selecteer in het deelvenster resultaten hello, **Jostle**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="8afac-135">In hello results panel, select **Jostle**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8afac-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8afac-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8afac-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Jostle op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="8afac-138">In this section, you configure and test Azure AD single sign-on with Jostle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8afac-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Jostle is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8afac-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jostle is tooa user in Azure AD.</span></span> <span data-ttu-id="8afac-140">Met andere woorden, een relatie koppeling tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Jostle behoeften toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="8afac-140">In other words, a link relationship between an Azure AD user and hello related user in Jostle needs toobe established.</span></span>

<span data-ttu-id="8afac-141">Wijs in Jostle, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="8afac-141">In Jostle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8afac-142">tooconfigure en eenmalige aanmelding Azure AD-test met Jostle, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8afac-142">tooconfigure and test Azure AD single sign-on with Jostle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8afac-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="8afac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8afac-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8afac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8afac-145">**[Maken van een testgebruiker Jostle](#creating-a-jostle-test-user)**  -toohave een equivalent van Britta Simon in Jostle die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8afac-145">**[Creating a Jostle test user](#creating-a-jostle-test-user)** - toohave a counterpart of Britta Simon in Jostle that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8afac-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8afac-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8afac-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="8afac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8afac-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="8afac-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8afac-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Jostle configureren.</span><span class="sxs-lookup"><span data-stu-id="8afac-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jostle application.</span></span>

<span data-ttu-id="8afac-150">**tooconfigure eenmalige aanmelding Azure AD met Jostle, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8afac-150">**tooconfigure Azure AD single sign-on with Jostle, perform hello following steps:**</span></span>

1. <span data-ttu-id="8afac-151">In de Azure-portal op Hallo Hallo **Jostle** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="8afac-151">In hello Azure portal, on hello **Jostle** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="8afac-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8afac-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_samlbase.png)

3. <span data-ttu-id="8afac-155">Op Hallo **Jostle domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8afac-155">On hello **Jostle Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_url.png)

    <span data-ttu-id="8afac-157">a.</span><span class="sxs-lookup"><span data-stu-id="8afac-157">a.</span></span> <span data-ttu-id="8afac-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tanent name>.jostle.us/jostle-prod/`</span><span class="sxs-lookup"><span data-stu-id="8afac-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tanent name>.jostle.us/jostle-prod/`</span></span>

    <span data-ttu-id="8afac-159">b.</span><span class="sxs-lookup"><span data-stu-id="8afac-159">b.</span></span> <span data-ttu-id="8afac-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<tanent name>.jostle.us`</span><span class="sxs-lookup"><span data-stu-id="8afac-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tanent name>.jostle.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8afac-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="8afac-161">These values are not real.</span></span> <span data-ttu-id="8afac-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="8afac-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8afac-163">Neem contact op met [Jostle ondersteuningsteam](mailto:support@jostle.me) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="8afac-163">Contact [Jostle support team](mailto:support@jostle.me) tooget these values.</span></span> 
 


4. <span data-ttu-id="8afac-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="8afac-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_certificate.png) 

5. <span data-ttu-id="8afac-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="8afac-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jostle-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="8afac-168">tooconfigure eenmalige aanmelding Jostle zijde, moet u toosend Hallo gedownload XML met metagegevens te[Jostle ondersteuningsteam](mailto:support@jostle.me).</span><span class="sxs-lookup"><span data-stu-id="8afac-168">tooconfigure single sign-on on Jostle side, you need toosend hello downloaded metadata XML too[Jostle support team](mailto:support@jostle.me).</span></span> <span data-ttu-id="8afac-169">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8afac-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span> 

> [!TIP]
> <span data-ttu-id="8afac-170">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="8afac-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8afac-171">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="8afac-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8afac-172">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8afac-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8afac-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="8afac-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="8afac-174">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="8afac-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="8afac-176">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8afac-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8afac-177">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8afac-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jostle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8afac-179">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="8afac-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jostle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8afac-181">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="8afac-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jostle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8afac-183">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8afac-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jostle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8afac-185">a.</span><span class="sxs-lookup"><span data-stu-id="8afac-185">a.</span></span> <span data-ttu-id="8afac-186">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8afac-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8afac-187">b.</span><span class="sxs-lookup"><span data-stu-id="8afac-187">b.</span></span> <span data-ttu-id="8afac-188">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8afac-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8afac-189">c.</span><span class="sxs-lookup"><span data-stu-id="8afac-189">c.</span></span> <span data-ttu-id="8afac-190">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="8afac-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8afac-191">d.</span><span class="sxs-lookup"><span data-stu-id="8afac-191">d.</span></span> <span data-ttu-id="8afac-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8afac-192">Click **Create**.</span></span>
 
### <a name="creating-a-jostle-test-user"></a><span data-ttu-id="8afac-193">Een testgebruiker Jostle maken</span><span class="sxs-lookup"><span data-stu-id="8afac-193">Creating a Jostle test user</span></span>

<span data-ttu-id="8afac-194">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Jostle maken.</span><span class="sxs-lookup"><span data-stu-id="8afac-194">In this section, you create a user called Britta Simon in Jostle.</span></span> <span data-ttu-id="8afac-195">Als u niet weet hoe tooadd Britta Simon in Jostle, neem contact op met [Jostle ondersteuningsteam](mailto:support@jostle.me) tooadd testgebruiker Hallo en SSO in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="8afac-195">If you don't know how tooadd Britta Simon in Jostle, please contact with [Jostle support team](mailto:support@jostle.me) tooadd hello test user and enable SSO.</span></span>

> [!NOTE]
> <span data-ttu-id="8afac-196">Hello Azure Active Directory-accounthouder ontvangt een e-mailbericht en een koppeling tooconfirm volgt hun account voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="8afac-196">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8afac-197">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8afac-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8afac-198">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooJostle toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="8afac-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJostle.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="8afac-200">**tooassign Britta Simon tooJostle, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8afac-200">**tooassign Britta Simon tooJostle, perform hello following steps:**</span></span>

1. <span data-ttu-id="8afac-201">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8afac-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="8afac-203">Selecteer in de lijst met de toepassingen van Hallo **Jostle**.</span><span class="sxs-lookup"><span data-stu-id="8afac-203">In hello applications list, select **Jostle**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_app.png) 

3. <span data-ttu-id="8afac-205">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="8afac-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="8afac-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="8afac-207">Click **Add** button.</span></span> <span data-ttu-id="8afac-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8afac-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="8afac-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="8afac-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8afac-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8afac-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8afac-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8afac-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8afac-213">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8afac-213">Testing single sign-on</span></span>

<span data-ttu-id="8afac-214">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="8afac-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8afac-215">Wanneer u Hallo Jostle tegel in Hallo toegangsvenster klikt, moet u de aanmeldingspagina van Jostle toepassing automatisch ophalen.</span><span class="sxs-lookup"><span data-stu-id="8afac-215">When you click hello Jostle tile in hello Access Panel, you should get automatically login page of Jostle application.</span></span>
<span data-ttu-id="8afac-216">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8afac-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8afac-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8afac-217">Additional resources</span></span>

* [<span data-ttu-id="8afac-218">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8afac-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8afac-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8afac-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_203.png

