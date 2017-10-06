---
title: 'Zelfstudie: Azure Active Directory-integratie met InTime | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en InTime.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d4e2c6e1-ae5d-4d2c-8ffc-1b24534d376a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jeedes
ms.openlocfilehash: 63652f0f098aeac95e89a2500b46a18440e34698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intime"></a><span data-ttu-id="b102c-103">Zelfstudie: Azure Active Directory-integratie met InTime</span><span class="sxs-lookup"><span data-stu-id="b102c-103">Tutorial: Azure Active Directory integration with InTime</span></span>

<span data-ttu-id="b102c-104">In deze zelfstudie leert u hoe toointegrate InTime met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b102c-104">In this tutorial, you learn how toointegrate InTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b102c-105">InTime integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b102c-105">Integrating InTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b102c-106">U kunt beheren in Azure AD die tooInTime toegang heeft.</span><span class="sxs-lookup"><span data-stu-id="b102c-106">You can control in Azure AD who has access tooInTime.</span></span>
- <span data-ttu-id="b102c-107">U kunt uw gebruikers tooautomatically get aangemelde tooInTime (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b102c-107">You can enable your users tooautomatically get signed-on tooInTime (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b102c-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="b102c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="b102c-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b102c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b102c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b102c-110">Prerequisites</span></span>

<span data-ttu-id="b102c-111">Azure AD-integratie met InTime tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="b102c-111">tooconfigure Azure AD integration with InTime, you need hello following items:</span></span>

- <span data-ttu-id="b102c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b102c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b102c-113">Een InTime eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b102c-113">A InTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b102c-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b102c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b102c-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b102c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b102c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b102c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b102c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b102c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b102c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b102c-118">Scenario description</span></span>
<span data-ttu-id="b102c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b102c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b102c-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b102c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b102c-121">Het toevoegen van InTime van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="b102c-121">Adding InTime from hello gallery</span></span>
2. <span data-ttu-id="b102c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b102c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intime-from-hello-gallery"></a><span data-ttu-id="b102c-123">Het toevoegen van InTime van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="b102c-123">Adding InTime from hello gallery</span></span>
<span data-ttu-id="b102c-124">tooconfigure hello integratie van InTime in Azure AD, moet u tooadd InTime uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b102c-124">tooconfigure hello integration of InTime into Azure AD, you need tooadd InTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b102c-125">**tooadd InTime via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b102c-125">**tooadd InTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b102c-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b102c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="b102c-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b102c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b102c-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b102c-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="b102c-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b102c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="b102c-133">Typ in het zoekvak Hallo **InTime**, selecteer **InTime** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b102c-133">In hello search box, type **InTime**, select **InTime** from result panel then click **Add** button tooadd hello application.</span></span>

    ![In de lijst met resultaten Hallo inTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b102c-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="b102c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b102c-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met InTime op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b102c-136">In this section, you configure and test Azure AD single sign-on with InTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b102c-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in InTime is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b102c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in InTime is tooa user in Azure AD.</span></span> <span data-ttu-id="b102c-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in InTime toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="b102c-138">In other words, a link relationship between an Azure AD user and hello related user in InTime needs toobe established.</span></span>

<span data-ttu-id="b102c-139">Wijs in InTime, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="b102c-139">In InTime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b102c-140">tooconfigure en eenmalige aanmelding Azure AD-test met InTime, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b102c-140">tooconfigure and test Azure AD single sign-on with InTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b102c-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="b102c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b102c-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b102c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b102c-143">**[Maak een InTime testgebruiker](#create-a-intime-test-user)**  -toohave een equivalent van Britta Simon in InTime die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b102c-143">**[Create a InTime test user](#create-a-intime-test-user)** - toohave a counterpart of Britta Simon in InTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b102c-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b102c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b102c-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b102c-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b102c-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b102c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b102c-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing InTime configureren.</span><span class="sxs-lookup"><span data-stu-id="b102c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your InTime application.</span></span>

<span data-ttu-id="b102c-148">**Azure AD tooconfigure eenmalige aanmelding met InTime, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b102c-148">**tooconfigure Azure AD single sign-on with InTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="b102c-149">In de Azure-portal op Hallo Hallo **InTime** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b102c-149">In hello Azure portal, on hello **InTime** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b102c-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b102c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-intime-tutorial/tutorial_intime_samlbase.png)

3. <span data-ttu-id="b102c-153">Op Hallo **InTime domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b102c-153">On hello **InTime Domain and URLs** section, perform hello following steps:</span></span>

    ![InTime domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-intime-tutorial/tutorial_intime_url.png)

    <span data-ttu-id="b102c-155">a.</span><span class="sxs-lookup"><span data-stu-id="b102c-155">a.</span></span> <span data-ttu-id="b102c-156">In Hallo **aanmeldings-URL** textbox type Hallo URL:`https://intime6.intimesoft.com/mytime/login/login.xhtml`</span><span class="sxs-lookup"><span data-stu-id="b102c-156">In hello **Sign-on URL** textbox, type hello URL: `https://intime6.intimesoft.com/mytime/login/login.xhtml`</span></span>

    <span data-ttu-id="b102c-157">b.</span><span class="sxs-lookup"><span data-stu-id="b102c-157">b.</span></span> <span data-ttu-id="b102c-158">In Hallo **id** textbox type Hallo URL:`https://auth.intimesoft.com/auth/realms/master`</span><span class="sxs-lookup"><span data-stu-id="b102c-158">In hello **Identifier** textbox, type hello URL: `https://auth.intimesoft.com/auth/realms/master`</span></span>

4. <span data-ttu-id="b102c-159">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b102c-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-intime-tutorial/tutorial_intime_certificate.png) 

5. <span data-ttu-id="b102c-161">Uw toepassing InTime verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist.</span><span class="sxs-lookup"><span data-stu-id="b102c-161">Your InTime application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="b102c-162">Hallo volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="b102c-162">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="b102c-163">Hallo standaardwaarde van **gebruikers-id** is **user.userprincipalname** maar InTime deze toobe toegewezen met e-mailadres van de gebruiker Hallo verwacht.</span><span class="sxs-lookup"><span data-stu-id="b102c-163">hello default value of **User Identifier** is **user.userprincipalname** but InTime expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="b102c-164">Die u kunt **user.mail** kenmerk uit de lijst Hallo of Hallo juiste kenmerkwaarde op basis van de organisatieconfiguratie van uw gebruiken</span><span class="sxs-lookup"><span data-stu-id="b102c-164">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration</span></span> 

    ![Kenmerk configureren](./media/active-directory-saas-intime-tutorial/tutorial_intime_attribute.png)

6. <span data-ttu-id="b102c-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b102c-166">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-intime-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="b102c-168">Op Hallo **InTime configuratie** sectie, klikt u op **InTime configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="b102c-168">On hello **InTime Configuration** section, click **Configure InTime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b102c-169">Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="b102c-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![InTime configuratie](./media/active-directory-saas-intime-tutorial/tutorial_intime_configure.png) 

8. <span data-ttu-id="b102c-171">tooconfigure eenmalige aanmelding op **InTime** zijde, moet u toosend Hallo gedownload **Metadata XML**, **Sign-Out URL's, en SAML Single Sign-On Service** te[InTime ondersteuningsteam](mailto:hdollard@intimesoft.com).</span><span class="sxs-lookup"><span data-stu-id="b102c-171">tooconfigure single sign-on on **InTime** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, and SAML Single Sign-On Service URL** too[InTime support team](mailto:hdollard@intimesoft.com).</span></span> <span data-ttu-id="b102c-172">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b102c-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b102c-173">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="b102c-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b102c-174">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="b102c-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b102c-175">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b102c-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b102c-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b102c-176">Create an Azure AD test user</span></span>

<span data-ttu-id="b102c-177">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b102c-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="b102c-179">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b102c-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b102c-180">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="b102c-180">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-intime-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b102c-182">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b102c-182">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-intime-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b102c-184">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b102c-184">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-intime-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b102c-186">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b102c-186">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-intime-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b102c-188">a.</span><span class="sxs-lookup"><span data-stu-id="b102c-188">a.</span></span> <span data-ttu-id="b102c-189">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b102c-189">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b102c-190">b.</span><span class="sxs-lookup"><span data-stu-id="b102c-190">b.</span></span> <span data-ttu-id="b102c-191">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="b102c-191">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="b102c-192">c.</span><span class="sxs-lookup"><span data-stu-id="b102c-192">c.</span></span> <span data-ttu-id="b102c-193">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="b102c-193">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="b102c-194">d.</span><span class="sxs-lookup"><span data-stu-id="b102c-194">d.</span></span> <span data-ttu-id="b102c-195">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b102c-195">Click **Create**.</span></span>
 
### <a name="create-a-intime-test-user"></a><span data-ttu-id="b102c-196">Een InTime testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b102c-196">Create a InTime test user</span></span>

<span data-ttu-id="b102c-197">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in InTime maken.</span><span class="sxs-lookup"><span data-stu-id="b102c-197">In this section, you create a user called Britta Simon in InTime.</span></span> <span data-ttu-id="b102c-198">Werken met [InTime ondersteuningsteam](mailto:hdollard@intimesoft.com) tooadd Hallo gebruikers in InTime Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="b102c-198">Work with [InTime support team](mailto:hdollard@intimesoft.com) tooadd hello users in hello InTime platform.</span></span> <span data-ttu-id="b102c-199">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b102c-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b102c-200">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b102c-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b102c-201">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooInTime toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="b102c-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInTime.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="b102c-203">**tooassign Britta Simon tooInTime, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="b102c-203">**tooassign Britta Simon tooInTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="b102c-204">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b102c-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b102c-206">Selecteer in de lijst met de toepassingen van Hallo **InTime**.</span><span class="sxs-lookup"><span data-stu-id="b102c-206">In hello applications list, select **InTime**.</span></span>

    ![Hallo InTime koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-intime-tutorial/tutorial_intime_app.png)  

3. <span data-ttu-id="b102c-208">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b102c-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="b102c-210">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b102c-210">Click **Add** button.</span></span> <span data-ttu-id="b102c-211">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b102c-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="b102c-213">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="b102c-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b102c-214">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b102c-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b102c-215">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b102c-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b102c-216">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b102c-216">Test single sign-on</span></span>

<span data-ttu-id="b102c-217">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b102c-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b102c-218">Wanneer u klikt op Hallo InTime tegel in Hallo Toegangsvenster, krijgt u de aanmeldingspagina Hallo van uw toepassing InTime.</span><span class="sxs-lookup"><span data-stu-id="b102c-218">When you click hello InTime tile in hello Access Panel, you should get hello login page of your InTime application.</span></span> <span data-ttu-id="b102c-219">Klik op Hallo **aanmelding** knop, en vervolgens een reeks IdPs wordt weergegeven op een lijst met knoppen.</span><span class="sxs-lookup"><span data-stu-id="b102c-219">Click hello **Login** button, then a series of IdPs will be displayed on a list of buttons.</span></span> <span data-ttu-id="b102c-220">Klik op **IDP naam** gegeven door [InTime ondersteuningsteam](mailto:hdollard@intimesoft.com) toologin in uw toepassing InTime.</span><span class="sxs-lookup"><span data-stu-id="b102c-220">click **IDP name** given by [InTime support team](mailto:hdollard@intimesoft.com) toologin into your InTime application.</span></span> <span data-ttu-id="b102c-221">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b102c-221">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b102c-222">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b102c-222">Additional resources</span></span>

* [<span data-ttu-id="b102c-223">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b102c-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b102c-224">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b102c-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-intime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intime-tutorial/tutorial_general_203.png

