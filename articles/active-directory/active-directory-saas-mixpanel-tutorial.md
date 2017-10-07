---
title: 'Zelfstudie: Azure Active Directory-integratie met Mixpanel | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Mixpanel.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2df26ef-d441-44ac-a9f3-b37bf9709bcb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 8da8aaefee3558c37babe3e10aeba4224ceffa16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mixpanel"></a><span data-ttu-id="7b429-103">Zelfstudie: Azure Active Directory-integratie met Mixpanel</span><span class="sxs-lookup"><span data-stu-id="7b429-103">Tutorial: Azure Active Directory integration with Mixpanel</span></span>

<span data-ttu-id="7b429-104">In deze zelfstudie leert u hoe toointegrate Mixpanel met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7b429-104">In this tutorial, you learn how toointegrate Mixpanel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7b429-105">Mixpanel integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7b429-105">Integrating Mixpanel with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7b429-106">U kunt beheren in Azure AD die tooMixpanel toegang heeft</span><span class="sxs-lookup"><span data-stu-id="7b429-106">You can control in Azure AD who has access tooMixpanel</span></span>
- <span data-ttu-id="7b429-107">U kunt uw gebruikers tooautomatically get aangemelde tooMixpanel (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="7b429-107">You can enable your users tooautomatically get signed-on tooMixpanel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7b429-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="7b429-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7b429-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7b429-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b429-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7b429-110">Prerequisites</span></span>

<span data-ttu-id="7b429-111">Azure AD-integratie met Mixpanel tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="7b429-111">tooconfigure Azure AD integration with Mixpanel, you need hello following items:</span></span>

- <span data-ttu-id="7b429-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="7b429-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7b429-113">Een Mixpanel eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="7b429-113">A Mixpanel single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7b429-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="7b429-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7b429-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="7b429-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7b429-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="7b429-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7b429-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b429-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7b429-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="7b429-118">Scenario description</span></span>
<span data-ttu-id="7b429-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="7b429-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7b429-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="7b429-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7b429-121">Het toevoegen van Mixpanel van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="7b429-121">Adding Mixpanel from hello gallery</span></span>
2. <span data-ttu-id="7b429-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7b429-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mixpanel-from-hello-gallery"></a><span data-ttu-id="7b429-123">Het toevoegen van Mixpanel van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="7b429-123">Adding Mixpanel from hello gallery</span></span>
<span data-ttu-id="7b429-124">tooconfigure hello integratie van Mixpanel in Azure AD, moet u tooadd Mixpanel uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="7b429-124">tooconfigure hello integration of Mixpanel into Azure AD, you need tooadd Mixpanel from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7b429-125">**tooadd Mixpanel via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7b429-125">**tooadd Mixpanel from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b429-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7b429-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7b429-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7b429-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7b429-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7b429-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="7b429-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7b429-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="7b429-133">Typ in het zoekvak Hallo **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="7b429-133">In hello search box, type **Mixpanel**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_search.png)

5. <span data-ttu-id="7b429-135">Selecteer in het deelvenster resultaten hello, **Mixpanel**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b429-135">In hello results panel, select **Mixpanel**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7b429-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7b429-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7b429-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Mixpanel op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="7b429-138">In this section, you configure and test Azure AD single sign-on with Mixpanel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7b429-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Mixpanel is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b429-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mixpanel is tooa user in Azure AD.</span></span> <span data-ttu-id="7b429-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Mixpanel toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="7b429-140">In other words, a link relationship between an Azure AD user and hello related user in Mixpanel needs toobe established.</span></span>

<span data-ttu-id="7b429-141">Wijs in Mixpanel, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="7b429-141">In Mixpanel, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7b429-142">tooconfigure en eenmalige aanmelding Azure AD-test met Mixpanel, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b429-142">tooconfigure and test Azure AD single sign-on with Mixpanel, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7b429-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="7b429-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7b429-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7b429-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7b429-145">**[Maken van een testgebruiker Mixpanel](#creating-a-mixpanel-test-user)**  -toohave een equivalent van Britta Simon in Mixpanel die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7b429-145">**[Creating a Mixpanel test user](#creating-a-mixpanel-test-user)** - toohave a counterpart of Britta Simon in Mixpanel that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7b429-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7b429-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7b429-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="7b429-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7b429-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="7b429-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7b429-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Mixpanel configureren.</span><span class="sxs-lookup"><span data-stu-id="7b429-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mixpanel application.</span></span>

<span data-ttu-id="7b429-150">**Azure AD tooconfigure eenmalige aanmelding met Mixpanel, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7b429-150">**tooconfigure Azure AD single sign-on with Mixpanel, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b429-151">In de Azure-portal op Hallo Hallo **Mixpanel** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7b429-151">In hello Azure portal, on hello **Mixpanel** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="7b429-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="7b429-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_samlbase.png)

3. <span data-ttu-id="7b429-155">Op Hallo **Mixpanel domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b429-155">On hello **Mixpanel Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_url.png)

     <span data-ttu-id="7b429-157">In Hallo **aanmeldings-URL** textbox, typ een URL als:`https://mixpanel.com/login/`</span><span class="sxs-lookup"><span data-stu-id="7b429-157">In hello **Sign-on URL** textbox, type a URL as: `https://mixpanel.com/login/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7b429-158">Registreer op [https://mixpanel.com/register/](https://mixpanel.com/register/) tooset van uw aanmeldingsreferenties en neem contact op met Hallo [Mixpanel ondersteuningsteam](mailto:support@mixpanel.com) tooenable SSO-instellingen voor uw tenant.</span><span class="sxs-lookup"><span data-stu-id="7b429-158">Please register at [https://mixpanel.com/register/](https://mixpanel.com/register/) tooset up your login credentials and  contact hello [Mixpanel support team](mailto:support@mixpanel.com) tooenable SSO settings for your tenant.</span></span> <span data-ttu-id="7b429-159">Ook kunt u uw aanmelding op URL-waarde indien nodig ophalen uit het ondersteuningsteam Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="7b429-159">You can also get your Sign On URL value if necessary from your Mixpanel support team.</span></span> 
 
4. <span data-ttu-id="7b429-160">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="7b429-160">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_certificate.png) 

5. <span data-ttu-id="7b429-162">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="7b429-162">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mixpanel-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7b429-164">Op Hallo **Mixpanel configuratie** sectie, klikt u op **configureren Mixpanel** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="7b429-164">On hello **Mixpanel Configuration** section, click **Configure Mixpanel** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7b429-165">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="7b429-165">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_configure.png) 

7. <span data-ttu-id="7b429-167">In een ander browservenster, aanmelding tooyour Mixpanel toepassing als beheerder.</span><span class="sxs-lookup"><span data-stu-id="7b429-167">In a different browser window, sign-on tooyour Mixpanel application as an administrator.</span></span>

8. <span data-ttu-id="7b429-168">Klik op onder aan de pagina Hallo Hallo enigszins **stemmen** pictogram in de linkerhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b429-168">On bottom of hello page, click hello little **gear** icon in hello left corner.</span></span> 
   
    ![Mixpanel voor eenmalige aanmelding](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_06.png) 

9. <span data-ttu-id="7b429-170">Klik op Hallo **toegangsbeveiliging** tabblad en klik vervolgens op **instellingen wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="7b429-170">Click hello **Access security** tab, and then click **Change settings**.</span></span>
   
    ![Mixpanel instellingen](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_08.png) 

10. <span data-ttu-id="7b429-172">Op Hallo **wijzigen van uw certificaat** dialoogvenster pagina, klikt u op **bestand kiezen** tooupload uw gedownloade certificaat en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="7b429-172">On hello **Change your certificate** dialog page, click **Choose file** tooupload your downloaded certificate, and then click **NEXT**.</span></span>
   
    ![Mixpanel instellingen](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_09.png) 

11.  <span data-ttu-id="7b429-174">In Hallo verificatie URL textbox op Hallo **wijzigen van de URL voor webverificatie** dialoogvenster Pagina plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal en klik vervolgens op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="7b429-174">In hello authentication URL textbox on hello **Change your authentication  URL** dialog page, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal, and then click **NEXT**.</span></span>
   
   ![Mixpanel instellingen](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_10.png) 

12. <span data-ttu-id="7b429-176">Klik op **Gereed**.</span><span class="sxs-lookup"><span data-stu-id="7b429-176">Click **Done**.</span></span>

> [!TIP]
> <span data-ttu-id="7b429-177">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="7b429-177">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7b429-178">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="7b429-178">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7b429-179">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7b429-179">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7b429-180">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="7b429-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="7b429-181">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="7b429-181">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="7b429-183">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7b429-183">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b429-184">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7b429-184">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7b429-186">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="7b429-186">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7b429-188">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="7b429-188">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7b429-190">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b429-190">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7b429-192">a.</span><span class="sxs-lookup"><span data-stu-id="7b429-192">a.</span></span> <span data-ttu-id="7b429-193">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7b429-193">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7b429-194">b.</span><span class="sxs-lookup"><span data-stu-id="7b429-194">b.</span></span> <span data-ttu-id="7b429-195">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7b429-195">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7b429-196">c.</span><span class="sxs-lookup"><span data-stu-id="7b429-196">c.</span></span> <span data-ttu-id="7b429-197">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="7b429-197">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7b429-198">d.</span><span class="sxs-lookup"><span data-stu-id="7b429-198">d.</span></span> <span data-ttu-id="7b429-199">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7b429-199">Click **Create**.</span></span>
 
### <a name="creating-a-mixpanel-test-user"></a><span data-ttu-id="7b429-200">Een testgebruiker Mixpanel maken</span><span class="sxs-lookup"><span data-stu-id="7b429-200">Creating a Mixpanel test user</span></span>

<span data-ttu-id="7b429-201">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Mixpanel van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7b429-201">hello objective of this section is toocreate a user called Britta Simon in Mixpanel.</span></span> 

1. <span data-ttu-id="7b429-202">Meld u op tooyour Mixpanel bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="7b429-202">Sign on tooyour Mixpanel company site as an administrator.</span></span>

2. <span data-ttu-id="7b429-203">Klik op Hallo onderaan pagina Hallo Hallo weinig tandwielpictogram knop op Hallo linkerhoek tooopen hello **instellingen** venster.</span><span class="sxs-lookup"><span data-stu-id="7b429-203">On hello bottom of hello page, click hello little gear button on hello left corner tooopen hello **Settings** window.</span></span>

3. <span data-ttu-id="7b429-204">Klik op Hallo **Team** tabblad.</span><span class="sxs-lookup"><span data-stu-id="7b429-204">Click hello **Team** tab.</span></span>

4. <span data-ttu-id="7b429-205">In Hallo **teamlid** textbox Britta van e-mailadres typt in hello Azure.</span><span class="sxs-lookup"><span data-stu-id="7b429-205">In hello **team member** textbox, type Britta's email address in hello Azure.</span></span>
   
    ![Mixpanel instellingen](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_11.png) 

5. <span data-ttu-id="7b429-207">Klik op **uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="7b429-207">Click **Invite**.</span></span> 

> [!Note]
> <span data-ttu-id="7b429-208">Hallo gebruiker ontvangt een e-tooset van Hallo-profiel.</span><span class="sxs-lookup"><span data-stu-id="7b429-208">hello user will get an email tooset up hello profile.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7b429-209">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b429-209">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7b429-210">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooMixpanel toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="7b429-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMixpanel.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="7b429-212">**tooassign Britta Simon tooMixpanel, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="7b429-212">**tooassign Britta Simon tooMixpanel, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b429-213">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7b429-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="7b429-215">Selecteer in de lijst met de toepassingen van Hallo **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="7b429-215">In hello applications list, select **Mixpanel**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_app.png) 

3. <span data-ttu-id="7b429-217">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="7b429-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="7b429-219">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="7b429-219">Click **Add** button.</span></span> <span data-ttu-id="7b429-220">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7b429-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="7b429-222">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b429-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7b429-223">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7b429-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7b429-224">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7b429-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7b429-225">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7b429-225">Testing single sign-on</span></span>

<span data-ttu-id="7b429-226">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="7b429-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7b429-227">Als u op Hallo Mixpanel tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Mixpanel toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b429-227">When you click hello Mixpanel tile in hello Access Panel, you should get automatically signed-on tooyour Mixpanel application.</span></span>
<span data-ttu-id="7b429-228">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7b429-228">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7b429-229">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7b429-229">Additional resources</span></span>

* [<span data-ttu-id="7b429-230">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b429-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b429-231">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7b429-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_203.png

