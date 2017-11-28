---
title: 'Zelfstudie: Azure Active Directory-integratie met 10.000 ft plannen | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en 10.000 ft-plannen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 9aa6fd079da4f931d4dd7277407a07e56091d7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a><span data-ttu-id="97dda-103">Zelfstudie: Azure Active Directory-integratie met 10.000 ft plannen</span><span class="sxs-lookup"><span data-stu-id="97dda-103">Tutorial: Azure Active Directory integration with 10,000ft Plans</span></span>

<span data-ttu-id="97dda-104">In deze zelfstudie leert u hoe toointegrate 10.000 ft plan met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="97dda-104">In this tutorial, you learn how toointegrate 10,000ft Plans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="97dda-105">10.000 ft plannen integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="97dda-105">Integrating 10,000ft Plans with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="97dda-106">U kunt beheren in Azure AD wie toegang tot too10, 000ft plannen heeft</span><span class="sxs-lookup"><span data-stu-id="97dda-106">You can control in Azure AD who has access too10,000ft Plans</span></span>
- <span data-ttu-id="97dda-107">U kunt uw gebruikers tooautomatically get aangemelde too10, 000ft plannen (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="97dda-107">You can enable your users tooautomatically get signed-on too10,000ft Plans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="97dda-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="97dda-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="97dda-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="97dda-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97dda-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="97dda-110">Prerequisites</span></span>

<span data-ttu-id="97dda-111">tooconfigure Azure AD-integratie met 10.000 ft plannen, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="97dda-111">tooconfigure Azure AD integration with 10,000ft Plans, you need hello following items:</span></span>

- <span data-ttu-id="97dda-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="97dda-112">An Azure AD subscription</span></span>
- <span data-ttu-id="97dda-113">Een 10.000 ft plannen voor eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="97dda-113">A 10,000ft Plans single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="97dda-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="97dda-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="97dda-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="97dda-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="97dda-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="97dda-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="97dda-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u hier een proefversie van één maand krijgen [proefabonnement](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="97dda-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="97dda-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="97dda-118">Scenario description</span></span>
<span data-ttu-id="97dda-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="97dda-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="97dda-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="97dda-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="97dda-121">Toevoegen van 10.000 ft plannen uit Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="97dda-121">Adding 10,000ft Plans from hello gallery</span></span>
2. <span data-ttu-id="97dda-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="97dda-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-10000ft-plans-from-hello-gallery"></a><span data-ttu-id="97dda-123">Toevoegen van 10.000 ft plannen uit Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="97dda-123">Adding 10,000ft Plans from hello gallery</span></span>
<span data-ttu-id="97dda-124">tooconfigure hello integratie van 10.000 ft plannen in Azure AD, moet u tooadd 10.000 ft-abonnementen van Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="97dda-124">tooconfigure hello integration of 10,000ft Plans into Azure AD, you need tooadd 10,000ft Plans from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="97dda-125">**tooadd 10.000 ft-abonnementen uit de galerie hello, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="97dda-125">**tooadd 10,000ft Plans from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="97dda-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="97dda-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="97dda-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="97dda-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="97dda-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="97dda-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="97dda-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="97dda-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="97dda-133">Typ in het zoekvak Hallo **10.000 ft plannen**.</span><span class="sxs-lookup"><span data-stu-id="97dda-133">In hello search box, type **10,000ft Plans**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_search.png)

5. <span data-ttu-id="97dda-135">Selecteer in het deelvenster resultaten hello, **10.000 ft plannen**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="97dda-135">In hello results panel, select **10,000ft Plans**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="97dda-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="97dda-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="97dda-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met 10.000 ft plannen op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="97dda-138">In this section, you configure and test Azure AD single sign-on with 10,000ft Plans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="97dda-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in 10.000 ft plannen is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97dda-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 10,000ft Plans is tooa user in Azure AD.</span></span> <span data-ttu-id="97dda-140">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in 10.000 ft moet plannen toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="97dda-140">In other words, a link relationship between an Azure AD user and hello related user in 10,000ft Plans needs toobe established.</span></span>

<span data-ttu-id="97dda-141">In 10.000 ft plannen, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="97dda-141">In 10,000ft Plans, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="97dda-142">tooconfigure en test eenmalige aanmelding Azure AD met 10.000 ft plannen, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="97dda-142">tooconfigure and test Azure AD single sign-on with 10,000ft Plans, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="97dda-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="97dda-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="97dda-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="97dda-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="97dda-145">**[Maken van een 10.000 ft plannen testgebruiker](#creating-a-10000ft-plans-test-user)**  -toohave die een exemplaar van Britta Simon in 10.000 ft-abonnementen gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="97dda-145">**[Creating a 10,000ft Plans test user](#creating-a-10000ft-plans-test-user)** - toohave a counterpart of Britta Simon in 10,000ft Plans that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="97dda-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="97dda-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="97dda-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="97dda-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="97dda-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="97dda-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="97dda-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing 10.000 ft-plannen.</span><span class="sxs-lookup"><span data-stu-id="97dda-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 10,000ft Plans application.</span></span>

<span data-ttu-id="97dda-150">**Voer tooconfigure Azure AD eenmalige aanmelding met 10.000 ft plannen, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="97dda-150">**tooconfigure Azure AD single sign-on with 10,000ft Plans, perform hello following steps:**</span></span>

1. <span data-ttu-id="97dda-151">In de Azure-portal op Hallo Hallo **10.000 ft plannen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="97dda-151">In hello Azure portal, on hello **10,000ft Plans** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="97dda-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="97dda-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_samlbase.png)

3. <span data-ttu-id="97dda-155">Op Hallo **10.000 ft domein plannen en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="97dda-155">On hello **10,000ft Plans Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_url.png)

    <span data-ttu-id="97dda-157">a.</span><span class="sxs-lookup"><span data-stu-id="97dda-157">a.</span></span> <span data-ttu-id="97dda-158">In Hallo **aanmeldings-URL** textbox type Hallo URL:`https://app.10000ft.com`</span><span class="sxs-lookup"><span data-stu-id="97dda-158">In hello **Sign-on URL** textbox, type hello URL: `https://app.10000ft.com`</span></span>

    <span data-ttu-id="97dda-159">b.</span><span class="sxs-lookup"><span data-stu-id="97dda-159">b.</span></span> <span data-ttu-id="97dda-160">In Hallo **id** textbox type Hallo URL:`https://app.10000ft.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="97dda-160">In hello **Identifier** textbox, type hello URL: `https://app.10000ft.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="97dda-161">waarde voor Hallo **id** verschilt hebt u een aangepast domein.</span><span class="sxs-lookup"><span data-stu-id="97dda-161">hello value for **Identifier** is different if you have a custom domain.</span></span> <span data-ttu-id="97dda-162">Neem contact op met [10.000 ft plannen ondersteuningsteam](https://www.10000ft.com/plans/support) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="97dda-162">Contact [10,000ft Plans support team](https://www.10000ft.com/plans/support) tooget this value.</span></span> 
 
4. <span data-ttu-id="97dda-163">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Raw)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="97dda-163">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_certificate.png) 

5. <span data-ttu-id="97dda-165">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="97dda-165">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="97dda-167">Op Hallo **10.000 ft configuratie plannen** sectie, klikt u op **10.000 ft's configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="97dda-167">On hello **10,000ft Plans Configuration** section, click **Configure 10,000ft Plans** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="97dda-168">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="97dda-168">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_configure.png) 

7. <span data-ttu-id="97dda-170">tooconfigure eenmalige aanmelding op **10.000 ft plannen** zijde, moet u toosend Hallo gedownload **Certificate(Raw), Sign-Out URL SAML entiteit-ID en SAML Single Sign-On Service-URL** te[ het ondersteuningsteam van 10.000 ft plannen](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="97dda-170">tooconfigure single sign-on on **10,000ft Plans** side, you need toosend hello downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

> [!TIP]
> <span data-ttu-id="97dda-171">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="97dda-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="97dda-172">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="97dda-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="97dda-173">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="97dda-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="97dda-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="97dda-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="97dda-175">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="97dda-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="97dda-177">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="97dda-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="97dda-178">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="97dda-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="97dda-180">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="97dda-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="97dda-182">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="97dda-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="97dda-184">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="97dda-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="97dda-186">a.</span><span class="sxs-lookup"><span data-stu-id="97dda-186">a.</span></span> <span data-ttu-id="97dda-187">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="97dda-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="97dda-188">b.</span><span class="sxs-lookup"><span data-stu-id="97dda-188">b.</span></span> <span data-ttu-id="97dda-189">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="97dda-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="97dda-190">c.</span><span class="sxs-lookup"><span data-stu-id="97dda-190">c.</span></span> <span data-ttu-id="97dda-191">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="97dda-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="97dda-192">d.</span><span class="sxs-lookup"><span data-stu-id="97dda-192">d.</span></span> <span data-ttu-id="97dda-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="97dda-193">Click **Create**.</span></span>
 
### <a name="creating-a-10000ft-plans-test-user"></a><span data-ttu-id="97dda-194">Maken van een 10.000 ft testgebruiker plannen</span><span class="sxs-lookup"><span data-stu-id="97dda-194">Creating a 10,000ft Plans test user</span></span>

<span data-ttu-id="97dda-195">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in 10.000 ft plannen van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="97dda-195">hello objective of this section is toocreate a user called Britta Simon in 10,000ft Plans.</span></span> <span data-ttu-id="97dda-196">10.000 ft plannen ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="97dda-196">10,000ft Plans supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="97dda-197">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="97dda-197">There is no action item for you in this section.</span></span> <span data-ttu-id="97dda-198">Een nieuwe gebruiker wordt tijdens een poging tooaccess 10.000 ft plannen gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="97dda-198">A new user is created during an attempt tooaccess 10,000ft Plans if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="97dda-199">Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello [10.000 ft plannen ondersteuningsteam](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="97dda-199">If you need toocreate a user manually, you need toocontact hello [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="97dda-200">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="97dda-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="97dda-201">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang too10, 000ft plannen.</span><span class="sxs-lookup"><span data-stu-id="97dda-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too10,000ft Plans.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="97dda-203">**tooassign Britta Simon too10, 000ft plannen, voert u Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="97dda-203">**tooassign Britta Simon too10,000ft Plans, perform hello following steps:**</span></span>

1. <span data-ttu-id="97dda-204">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="97dda-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="97dda-206">Selecteer in de lijst met de toepassingen van Hallo **10.000 ft plannen**.</span><span class="sxs-lookup"><span data-stu-id="97dda-206">In hello applications list, select **10,000ft Plans**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_app.png) 

3. <span data-ttu-id="97dda-208">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="97dda-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="97dda-210">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="97dda-210">Click **Add** button.</span></span> <span data-ttu-id="97dda-211">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="97dda-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="97dda-213">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="97dda-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="97dda-214">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="97dda-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="97dda-215">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="97dda-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="97dda-216">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="97dda-216">Testing single sign-on</span></span>

<span data-ttu-id="97dda-217">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="97dda-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="97dda-218">Wanneer u Hallo 10.000 ft plannen in Hallo Toegangsvenster tegel klikt, krijgt u automatisch aangemelde tooyour 10.000 ft plannen toepassing.</span><span class="sxs-lookup"><span data-stu-id="97dda-218">When you click hello 10,000ft Plans tile in hello Access Panel, you should get automatically signed-on tooyour 10,000ft Plans application.</span></span>
 
## <a name="additional-resources"></a><span data-ttu-id="97dda-219">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="97dda-219">Additional resources</span></span>

* [<span data-ttu-id="97dda-220">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97dda-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="97dda-221">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="97dda-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_203.png

