---
title: 'Zelfstudie: Azure Active Directory-integratie met Kontiki | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Kontiki.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8d5e5413-da4c-40d8-b1d0-f03ecfef030b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: bfbc3c4f23494f7e3cf9498817fb8948bb300470
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kontiki"></a><span data-ttu-id="62890-103">Zelfstudie: Azure Active Directory-integratie met Kontiki</span><span class="sxs-lookup"><span data-stu-id="62890-103">Tutorial: Azure Active Directory integration with Kontiki</span></span>

<span data-ttu-id="62890-104">In deze zelfstudie leert u hoe toointegrate Kontiki met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="62890-104">In this tutorial, you learn how toointegrate Kontiki with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="62890-105">Kontiki integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="62890-105">Integrating Kontiki with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="62890-106">U kunt beheren in Azure AD die tooKontiki toegang heeft</span><span class="sxs-lookup"><span data-stu-id="62890-106">You can control in Azure AD who has access tooKontiki</span></span>
- <span data-ttu-id="62890-107">U kunt uw gebruikers tooautomatically get aangemelde tooKontiki (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="62890-107">You can enable your users tooautomatically get signed-on tooKontiki (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="62890-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="62890-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="62890-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="62890-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62890-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="62890-110">Prerequisites</span></span>

<span data-ttu-id="62890-111">Azure AD-integratie met Kontiki tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="62890-111">tooconfigure Azure AD integration with Kontiki, you need hello following items:</span></span>

- <span data-ttu-id="62890-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="62890-112">An Azure AD subscription</span></span>
- <span data-ttu-id="62890-113">Een Kontiki eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="62890-113">A Kontiki single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="62890-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="62890-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="62890-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="62890-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="62890-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="62890-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="62890-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="62890-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="62890-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="62890-118">Scenario description</span></span>
<span data-ttu-id="62890-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="62890-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="62890-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="62890-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="62890-121">Het toevoegen van Kontiki van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="62890-121">Adding Kontiki from hello gallery</span></span>
2. <span data-ttu-id="62890-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="62890-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kontiki-from-hello-gallery"></a><span data-ttu-id="62890-123">Het toevoegen van Kontiki van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="62890-123">Adding Kontiki from hello gallery</span></span>
<span data-ttu-id="62890-124">tooconfigure hello integratie van Kontiki in Azure AD, moet u tooadd Kontiki uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="62890-124">tooconfigure hello integration of Kontiki into Azure AD, you need tooadd Kontiki from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="62890-125">**tooadd Kontiki via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="62890-125">**tooadd Kontiki from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="62890-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="62890-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="62890-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="62890-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="62890-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="62890-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="62890-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="62890-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="62890-133">Typ in het zoekvak Hallo **Kontiki**.</span><span class="sxs-lookup"><span data-stu-id="62890-133">In hello search box, type **Kontiki**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kontiki-tutorial/tutorial_kontiki_search.png)

5. <span data-ttu-id="62890-135">Selecteer in het deelvenster resultaten hello, **Kontiki**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="62890-135">In hello results panel, select **Kontiki**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kontiki-tutorial/tutorial_kontiki_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="62890-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="62890-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="62890-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Kontiki op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="62890-138">In this section, you configure and test Azure AD single sign-on with Kontiki based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="62890-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Kontiki is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62890-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kontiki is tooa user in Azure AD.</span></span> <span data-ttu-id="62890-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Kontiki toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="62890-140">In other words, a link relationship between an Azure AD user and hello related user in Kontiki needs toobe established.</span></span>

<span data-ttu-id="62890-141">Wijs in Kontiki, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="62890-141">In Kontiki, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="62890-142">tooconfigure en eenmalige aanmelding Azure AD-test met Kontiki, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="62890-142">tooconfigure and test Azure AD single sign-on with Kontiki, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="62890-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="62890-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="62890-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62890-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="62890-145">**[Maken van een testgebruiker Kontiki](#creating-a-kontiki-test-user)**  -toohave een equivalent van Britta Simon in Kontiki die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="62890-145">**[Creating a Kontiki test user](#creating-a-kontiki-test-user)** - toohave a counterpart of Britta Simon in Kontiki that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="62890-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="62890-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="62890-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="62890-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="62890-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="62890-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="62890-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Kontiki configureren.</span><span class="sxs-lookup"><span data-stu-id="62890-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kontiki application.</span></span>

<span data-ttu-id="62890-150">**Azure AD tooconfigure eenmalige aanmelding met Kontiki, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="62890-150">**tooconfigure Azure AD single sign-on with Kontiki, perform hello following steps:**</span></span>

1. <span data-ttu-id="62890-151">In de Azure-portal op Hallo Hallo **Kontiki** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="62890-151">In hello Azure portal, on hello **Kontiki** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="62890-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="62890-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kontiki-tutorial/tutorial_kontiki_samlbase.png)

3. <span data-ttu-id="62890-155">Op Hallo **Kontiki domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="62890-155">On hello **Kontiki Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kontiki-tutorial/tutorial_kontiki_url.png)

     <span data-ttu-id="62890-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.mc.eval.kontiki.com`</span><span class="sxs-lookup"><span data-stu-id="62890-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.mc.eval.kontiki.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="62890-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="62890-158">This value is not real.</span></span> <span data-ttu-id="62890-159">Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="62890-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="62890-160">Neem contact op met [Kontiki Client ondersteuningsteam](http://customersupport.kontiki.com/enterprise/contactsupport.html) tooget Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="62890-160">Contact [Kontiki Client support team](http://customersupport.kontiki.com/enterprise/contactsupport.html) tooget hello value.</span></span> 
 
4. <span data-ttu-id="62890-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="62890-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kontiki-tutorial/tutorial_kontiki_certificate.png) 

5. <span data-ttu-id="62890-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="62890-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kontiki-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="62890-165">tooconfigure eenmalige aanmelding op **Kontiki** zijde, moet u toosend Hallo gedownload **Metadata XML** te[Kontiki ondersteuningsteam](http://customersupport.kontiki.com/enterprise/contactsupport.html).</span><span class="sxs-lookup"><span data-stu-id="62890-165">tooconfigure single sign-on on **Kontiki** side, you need toosend hello downloaded **Metadata XML** too[Kontiki support team](http://customersupport.kontiki.com/enterprise/contactsupport.html).</span></span> <span data-ttu-id="62890-166">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="62890-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="62890-167">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="62890-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="62890-168">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="62890-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="62890-169">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="62890-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="62890-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="62890-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="62890-171">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="62890-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="62890-173">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="62890-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="62890-174">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="62890-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kontiki-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="62890-176">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="62890-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kontiki-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="62890-178">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="62890-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kontiki-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="62890-180">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="62890-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kontiki-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="62890-182">a.</span><span class="sxs-lookup"><span data-stu-id="62890-182">a.</span></span> <span data-ttu-id="62890-183">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="62890-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="62890-184">b.</span><span class="sxs-lookup"><span data-stu-id="62890-184">b.</span></span> <span data-ttu-id="62890-185">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="62890-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="62890-186">c.</span><span class="sxs-lookup"><span data-stu-id="62890-186">c.</span></span> <span data-ttu-id="62890-187">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="62890-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="62890-188">d.</span><span class="sxs-lookup"><span data-stu-id="62890-188">d.</span></span> <span data-ttu-id="62890-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="62890-189">Click **Create**.</span></span>
 
### <a name="creating-a-kontiki-test-user"></a><span data-ttu-id="62890-190">Een testgebruiker Kontiki maken</span><span class="sxs-lookup"><span data-stu-id="62890-190">Creating a Kontiki test user</span></span>

<span data-ttu-id="62890-191">Er is geen actie-item voor u tooconfigure gebruikers inrichten tooKontiki.</span><span class="sxs-lookup"><span data-stu-id="62890-191">There is no action item for you tooconfigure user provisioning tooKontiki.</span></span> <span data-ttu-id="62890-192">Wanneer een toegewezen gebruiker toolog in tooKontiki met behulp van het toegangsvenster hello probeert, controleert Kontiki of Hallo gebruiker bestaat.</span><span class="sxs-lookup"><span data-stu-id="62890-192">When an assigned user tries toolog in tooKontiki using hello access panel, Kontiki checks whether hello user exists.</span></span>  

>[!NOTE]
><span data-ttu-id="62890-193">Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Kontiki.</span><span class="sxs-lookup"><span data-stu-id="62890-193">If there is no user account available yet, it is automatically created by Kontiki.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="62890-194">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="62890-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="62890-195">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooKontiki toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="62890-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKontiki.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="62890-197">**tooassign Britta Simon tooKontiki, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="62890-197">**tooassign Britta Simon tooKontiki, perform hello following steps:**</span></span>

1. <span data-ttu-id="62890-198">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="62890-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="62890-200">Selecteer in de lijst met de toepassingen van Hallo **Kontiki**.</span><span class="sxs-lookup"><span data-stu-id="62890-200">In hello applications list, select **Kontiki**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kontiki-tutorial/tutorial_kontiki_app.png) 

3. <span data-ttu-id="62890-202">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="62890-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="62890-204">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="62890-204">Click **Add** button.</span></span> <span data-ttu-id="62890-205">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="62890-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="62890-207">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="62890-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="62890-208">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="62890-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="62890-209">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="62890-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="62890-210">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="62890-210">Testing single sign-on</span></span>

<span data-ttu-id="62890-211">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="62890-211">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="62890-212">Als u op Hallo Kontiki tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Kontiki toepassing.</span><span class="sxs-lookup"><span data-stu-id="62890-212">When you click hello Kontiki tile in hello Access Panel, you should get automatically signed-on tooyour Kontiki application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="62890-213">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="62890-213">Additional resources</span></span>

* [<span data-ttu-id="62890-214">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="62890-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62890-215">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="62890-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_203.png

