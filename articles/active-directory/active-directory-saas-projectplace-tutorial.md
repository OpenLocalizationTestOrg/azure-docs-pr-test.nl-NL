---
title: 'Zelfstudie: Azure Active Directory-integratie met Projectplace | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Projectplace.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 298059ca-b652-4577-916a-c31393d53d7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 95d109052096161f995ff26a18f8d64f0c4a3dc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-projectplace"></a><span data-ttu-id="f3789-103">Zelfstudie: Azure Active Directory-integratie met Projectplace</span><span class="sxs-lookup"><span data-stu-id="f3789-103">Tutorial: Azure Active Directory integration with Projectplace</span></span>

<span data-ttu-id="f3789-104">In deze zelfstudie leert u hoe toointegrate Projectplace met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f3789-104">In this tutorial, you learn how toointegrate Projectplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f3789-105">Projectplace integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f3789-105">Integrating Projectplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f3789-106">U kunt beheren in Azure AD die tooProjectplace toegang heeft</span><span class="sxs-lookup"><span data-stu-id="f3789-106">You can control in Azure AD who has access tooProjectplace</span></span>
- <span data-ttu-id="f3789-107">U kunt uw gebruikers tooautomatically get aangemelde tooProjectplace (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="f3789-107">You can enable your users tooautomatically get signed-on tooProjectplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f3789-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f3789-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f3789-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f3789-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3789-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f3789-110">Prerequisites</span></span>

<span data-ttu-id="f3789-111">Azure AD-integratie met Projectplace tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="f3789-111">tooconfigure Azure AD integration with Projectplace, you need hello following items:</span></span>

- <span data-ttu-id="f3789-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f3789-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f3789-113">Een Projectplace eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f3789-113">A Projectplace single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f3789-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f3789-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f3789-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f3789-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f3789-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f3789-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f3789-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f3789-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f3789-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f3789-118">Scenario description</span></span>
<span data-ttu-id="f3789-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f3789-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f3789-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f3789-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f3789-121">Het toevoegen van Projectplace van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f3789-121">Adding Projectplace from hello gallery</span></span>
2. <span data-ttu-id="f3789-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f3789-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-projectplace-from-hello-gallery"></a><span data-ttu-id="f3789-123">Het toevoegen van Projectplace van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="f3789-123">Adding Projectplace from hello gallery</span></span>
<span data-ttu-id="f3789-124">tooconfigure hello integratie van Projectplace in Azure AD, moet u tooadd Projectplace uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f3789-124">tooconfigure hello integration of Projectplace into Azure AD, you need tooadd Projectplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f3789-125">**tooadd Projectplace via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f3789-125">**tooadd Projectplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f3789-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f3789-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f3789-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f3789-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f3789-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f3789-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f3789-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f3789-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f3789-133">Typ in het zoekvak Hallo **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="f3789-133">In hello search box, type **Projectplace**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_search.png)

5. <span data-ttu-id="f3789-135">Selecteer in het deelvenster resultaten hello, **Projectplace**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f3789-135">In hello results panel, select **Projectplace**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f3789-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f3789-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f3789-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Projectplace op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f3789-138">In this section, you configure and test Azure AD single sign-on with Projectplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f3789-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Projectplace is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3789-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Projectplace is tooa user in Azure AD.</span></span> <span data-ttu-id="f3789-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Projectplace toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="f3789-140">In other words, a link relationship between an Azure AD user and hello related user in Projectplace needs toobe established.</span></span>

<span data-ttu-id="f3789-141">Wijs in Projectplace, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="f3789-141">In Projectplace, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f3789-142">tooconfigure en eenmalige aanmelding Azure AD-test met Projectplace, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f3789-142">tooconfigure and test Azure AD single sign-on with Projectplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f3789-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="f3789-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f3789-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f3789-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f3789-145">**[Maken van een testgebruiker Projectplace](#creating-a-projectplace-test-user)**  -toohave een equivalent van Britta Simon in Projectplace die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f3789-145">**[Creating a Projectplace test user](#creating-a-projectplace-test-user)** - toohave a counterpart of Britta Simon in Projectplace that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f3789-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f3789-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f3789-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f3789-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f3789-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f3789-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f3789-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw Projectplace-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f3789-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Projectplace application.</span></span>

<span data-ttu-id="f3789-150">**Azure AD tooconfigure eenmalige aanmelding met Projectplace, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f3789-150">**tooconfigure Azure AD single sign-on with Projectplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="f3789-151">In de Azure-portal op Hallo Hallo **Projectplace** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f3789-151">In hello Azure portal, on hello **Projectplace** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f3789-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f3789-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_samlbase.png)

3. <span data-ttu-id="f3789-155">Op Hallo **Projectplace-domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f3789-155">On hello **Projectplace Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_url.png)

    <span data-ttu-id="f3789-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company>.projectplace.com`</span><span class="sxs-lookup"><span data-stu-id="f3789-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.projectplace.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f3789-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="f3789-158">This value is not real.</span></span> <span data-ttu-id="f3789-159">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="f3789-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="f3789-160">Neem contact op met [Projectplace-Client-ondersteuningsteam](https://success.planview.com/Projectplace/Support) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="f3789-160">Contact [Projectplace Client support team](https://success.planview.com/Projectplace/Support) tooget this value.</span></span> 
 
4. <span data-ttu-id="f3789-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f3789-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_certificate.png) 

5. <span data-ttu-id="f3789-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f3789-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-projectplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f3789-165">tooconfigure eenmalige aanmelding op **Projectplace** zijde, moet u toosend Hallo gedownload **Metadata XML** te[Projectplace-ondersteuningsteam](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="f3789-165">tooconfigure single sign-on on **Projectplace** side, you need toosend hello downloaded **Metadata XML** too[Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="f3789-166">Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f3789-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="f3789-167">Hallo aanmelding configuratie voor één is uitgevoerd door Hallo toobe [Projectplace-ondersteuningsteam](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="f3789-167">hello single sign-on configuration has toobe performed by hello [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="f3789-168">U ontvangt een melding zodra het Hallo-configuratie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f3789-168">You will get a notification as soon as hello configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="f3789-169">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="f3789-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f3789-170">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="f3789-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f3789-171">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f3789-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f3789-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f3789-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="f3789-173">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f3789-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f3789-175">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f3789-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f3789-176">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f3789-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-projectplace-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f3789-178">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f3789-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-projectplace-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f3789-180">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="f3789-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-projectplace-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f3789-182">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f3789-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-projectplace-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f3789-184">a.</span><span class="sxs-lookup"><span data-stu-id="f3789-184">a.</span></span> <span data-ttu-id="f3789-185">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f3789-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f3789-186">b.</span><span class="sxs-lookup"><span data-stu-id="f3789-186">b.</span></span> <span data-ttu-id="f3789-187">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f3789-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f3789-188">c.</span><span class="sxs-lookup"><span data-stu-id="f3789-188">c.</span></span> <span data-ttu-id="f3789-189">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f3789-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f3789-190">d.</span><span class="sxs-lookup"><span data-stu-id="f3789-190">d.</span></span> <span data-ttu-id="f3789-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f3789-191">Click **Create**.</span></span>
 
### <a name="creating-a-projectplace-test-user"></a><span data-ttu-id="f3789-192">Een testgebruiker Projectplace maken</span><span class="sxs-lookup"><span data-stu-id="f3789-192">Creating a Projectplace test user</span></span>

<span data-ttu-id="f3789-193">In volgorde tooenable Azure AD gebruikers toolog in Projectplace, moeten ze worden ingericht in Projectplace.</span><span class="sxs-lookup"><span data-stu-id="f3789-193">In order tooenable Azure AD users toolog into Projectplace, they must be provisioned into Projectplace.</span></span> <span data-ttu-id="f3789-194">In geval van Projectplace Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="f3789-194">In hello case of Projectplace, provisioning is a manual task.</span></span>

<span data-ttu-id="f3789-195">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f3789-195">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="f3789-196">Meld u bij tooyour **Projectplace** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f3789-196">Log in tooyour **Projectplace** company site as an administrator.</span></span>

2. <span data-ttu-id="f3789-197">Ga te**mensen**, en klik vervolgens op **leden**.</span><span class="sxs-lookup"><span data-stu-id="f3789-197">Go too**People**, and then click **Members**.</span></span>
   
    <span data-ttu-id="f3789-198">![Mensen](./media/active-directory-saas-projectplace-tutorial/ic790228.png "personen")</span><span class="sxs-lookup"><span data-stu-id="f3789-198">![People](./media/active-directory-saas-projectplace-tutorial/ic790228.png "People")</span></span>

3. <span data-ttu-id="f3789-199">Klik op **lid toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f3789-199">Click **Add Member**.</span></span>
   
    <span data-ttu-id="f3789-200">![Toevoegen van leden](./media/active-directory-saas-projectplace-tutorial/ic790232.png "leden toevoegen")</span><span class="sxs-lookup"><span data-stu-id="f3789-200">![Add Members](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Add Members")</span></span>

4. <span data-ttu-id="f3789-201">In Hallo **lid toevoegen** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f3789-201">In hello **Add Member** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f3789-202">![Nieuwe leden](./media/active-directory-saas-projectplace-tutorial/ic790233.png "nieuwe leden")</span><span class="sxs-lookup"><span data-stu-id="f3789-202">![New Members](./media/active-directory-saas-projectplace-tutorial/ic790233.png "New Members")</span></span>
   
    <span data-ttu-id="f3789-203">a.</span><span class="sxs-lookup"><span data-stu-id="f3789-203">a.</span></span> <span data-ttu-id="f3789-204">In Hallo **nieuwe leden** textbox type Hallo e-mailadres van een geldige AAD-account u wilt dat tooprovision in Hallo gerelateerde tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="f3789-204">In hello **New Members** textbox, type hello email address of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="f3789-205">b.</span><span class="sxs-lookup"><span data-stu-id="f3789-205">b.</span></span> <span data-ttu-id="f3789-206">Klik op **verzenden**.</span><span class="sxs-lookup"><span data-stu-id="f3789-206">Click **Send**.</span></span>

   <span data-ttu-id="f3789-207">Een e-mailbericht met inbegrip van een account koppelen tooconfirm Hallo voordat deze actief is Azure Active Directory-accounthouder toohello verzonden.</span><span class="sxs-lookup"><span data-stu-id="f3789-207">An email including a link tooconfirm hello account before it becomes active is sent toohello Azure Active Directory account holder.</span></span>

>[!NOTE]
><span data-ttu-id="f3789-208">U kunt andere Projectplace gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Projectplace tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="f3789-208">You can use any other Projectplace user account creation tools or APIs provided by Projectplace tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f3789-209">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3789-209">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f3789-210">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooProjectplace toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="f3789-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooProjectplace.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f3789-212">**tooassign Britta Simon tooProjectplace, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f3789-212">**tooassign Britta Simon tooProjectplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="f3789-213">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f3789-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f3789-215">Selecteer in de lijst met de toepassingen van Hallo **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="f3789-215">In hello applications list, select **Projectplace**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_app.png) 

3. <span data-ttu-id="f3789-217">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f3789-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f3789-219">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f3789-219">Click **Add** button.</span></span> <span data-ttu-id="f3789-220">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f3789-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f3789-222">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="f3789-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f3789-223">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f3789-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f3789-224">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f3789-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f3789-225">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f3789-225">Testing single sign-on</span></span>

<span data-ttu-id="f3789-226">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="f3789-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f3789-227">Als u op Hallo Projectplace-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Projectplace-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f3789-227">When you click hello Projectplace tile in hello Access Panel, you should get automatically signed-on tooyour Projectplace application.</span></span>
<span data-ttu-id="f3789-228">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f3789-228">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f3789-229">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f3789-229">Additional resources</span></span>

* [<span data-ttu-id="f3789-230">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3789-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f3789-231">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f3789-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_203.png

