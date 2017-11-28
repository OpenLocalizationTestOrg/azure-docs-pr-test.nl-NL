---
title: 'Zelfstudie: Azure Active Directory-integratie met Optimizely | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Optimizely.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 868aefae27ca155d2963f3dcfcd79bbb564b48ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="2db2b-103">Zelfstudie: Azure Active Directory-integratie met Optimizely</span><span class="sxs-lookup"><span data-stu-id="2db2b-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>

<span data-ttu-id="2db2b-104">In deze zelfstudie leert u hoe toointegrate Optimizely met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2db2b-104">In this tutorial, you learn how toointegrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2db2b-105">Optimizely integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2db2b-105">Integrating Optimizely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2db2b-106">U kunt beheren in Azure AD die tooOptimizely toegang heeft</span><span class="sxs-lookup"><span data-stu-id="2db2b-106">You can control in Azure AD who has access tooOptimizely</span></span>
- <span data-ttu-id="2db2b-107">U kunt uw gebruikers tooautomatically get aangemelde tooOptimizely (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="2db2b-107">You can enable your users tooautomatically get signed-on tooOptimizely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2db2b-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="2db2b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2db2b-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2db2b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2db2b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2db2b-110">Prerequisites</span></span>

<span data-ttu-id="2db2b-111">Azure AD-integratie met Optimizely tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="2db2b-111">tooconfigure Azure AD integration with Optimizely, you need hello following items:</span></span>

- <span data-ttu-id="2db2b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2db2b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2db2b-113">Een Optimizely eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2db2b-113">An Optimizely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2db2b-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2db2b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2db2b-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2db2b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2db2b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2db2b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2db2b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2db2b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2db2b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2db2b-118">Scenario description</span></span>
<span data-ttu-id="2db2b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2db2b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2db2b-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2db2b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2db2b-121">Het toevoegen van Optimizely van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2db2b-121">Adding Optimizely from hello gallery</span></span>
2. <span data-ttu-id="2db2b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2db2b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-optimizely-from-hello-gallery"></a><span data-ttu-id="2db2b-123">Het toevoegen van Optimizely van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="2db2b-123">Adding Optimizely from hello gallery</span></span>
<span data-ttu-id="2db2b-124">tooconfigure hello integratie van Optimizely in Azure AD, moet u tooadd Optimizely uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2db2b-124">tooconfigure hello integration of Optimizely into Azure AD, you need tooadd Optimizely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2db2b-125">**tooadd Optimizely via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2db2b-125">**tooadd Optimizely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2db2b-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2db2b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2db2b-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2db2b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2db2b-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2db2b-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="2db2b-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2db2b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="2db2b-133">Typ in het zoekvak Hallo **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="2db2b-133">In hello search box, type **Optimizely**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. <span data-ttu-id="2db2b-135">Selecteer in het deelvenster resultaten hello, **Optimizely**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2db2b-135">In hello results panel, select **Optimizely**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2db2b-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2db2b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2db2b-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Optimizely op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="2db2b-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2db2b-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Optimizely is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2db2b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Optimizely is tooa user in Azure AD.</span></span> <span data-ttu-id="2db2b-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Optimizely toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="2db2b-140">In other words, a link relationship between an Azure AD user and hello related user in Optimizely needs toobe established.</span></span>

<span data-ttu-id="2db2b-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Optimizely.</span><span class="sxs-lookup"><span data-stu-id="2db2b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Optimizely.</span></span>

<span data-ttu-id="2db2b-142">tooconfigure en eenmalige aanmelding Azure AD-test met Optimizely, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2db2b-142">tooconfigure and test Azure AD single sign-on with Optimizely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2db2b-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="2db2b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2db2b-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2db2b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2db2b-145">**[Maken van een testgebruiker Optimizely](#creating-an-optimizely-test-user)**  -toohave een equivalent van Britta Simon in Optimizely die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2db2b-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - toohave a counterpart of Britta Simon in Optimizely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2db2b-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2db2b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2db2b-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2db2b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2db2b-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2db2b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2db2b-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Optimizely configureren.</span><span class="sxs-lookup"><span data-stu-id="2db2b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Optimizely application.</span></span>

<span data-ttu-id="2db2b-150">**Azure AD tooconfigure eenmalige aanmelding met Optimizely, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2db2b-150">**tooconfigure Azure AD single sign-on with Optimizely, perform hello following steps:**</span></span>

1. <span data-ttu-id="2db2b-151">In de Azure-portal op Hallo Hallo **Optimizely** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2db2b-151">In hello Azure portal, on hello **Optimizely** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2db2b-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2db2b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. <span data-ttu-id="2db2b-155">Op Hallo **Optimizely domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2db2b-155">On hello **Optimizely Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    <span data-ttu-id="2db2b-157">a.</span><span class="sxs-lookup"><span data-stu-id="2db2b-157">a.</span></span> <span data-ttu-id="2db2b-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://app.optimizely.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="2db2b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.optimizely.net/<instance name>`</span></span>

    <span data-ttu-id="2db2b-159">b.</span><span class="sxs-lookup"><span data-stu-id="2db2b-159">b.</span></span> <span data-ttu-id="2db2b-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`urn:auth0:optimizely:contoso`</span><span class="sxs-lookup"><span data-stu-id="2db2b-160">In hello **Identifier** textbox, type a URL using hello following pattern:  `urn:auth0:optimizely:contoso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2db2b-161">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="2db2b-161">These values are not hello real.</span></span> <span data-ttu-id="2db2b-162">Hallo-waarde wordt bijgewerkt met Hallo werkelijke aanmeldings-URL en de id, die verderop in Hallo zelfstudie wordt uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="2db2b-162">You will update hello value with hello actual Sign-on URL and Identifier, which is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="2db2b-163">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2db2b-163">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. <span data-ttu-id="2db2b-165">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2db2b-165">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2db2b-167">Op Hallo **Optimizely configuratie** sectie, klikt u op **configureren Optimizely** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="2db2b-167">On hello **Optimizely Configuration** section, click **Configure Optimizely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2db2b-168">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="2db2b-168">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. <span data-ttu-id="2db2b-170">tooconfigure eenmalige aanmelding op **Optimizely** zijde, neem contact op met uw accountmanager Optimizely en bieden Hallo gedownload **certificaat (Base64)**, en **SAML Single Sign-On Service-URL** .</span><span class="sxs-lookup"><span data-stu-id="2db2b-170">tooconfigure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide hello downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span></span> 

8. <span data-ttu-id="2db2b-171">In het antwoord tooyour e-mail biedt Optimizely u Hallo aanmelding op URL (Serviceprovider geïnitieerde SSO) en Hallo identificatiewaarden (Service Provider entiteit-ID).</span><span class="sxs-lookup"><span data-stu-id="2db2b-171">In response tooyour email, Optimizely provides you with hello Sign On URL (SP-initiated SSO) and hello Identifier (Service Provider Entity ID) values.</span></span>

    <span data-ttu-id="2db2b-172">a.</span><span class="sxs-lookup"><span data-stu-id="2db2b-172">a.</span></span> <span data-ttu-id="2db2b-173">Kopiëren Hallo **Serviceprovider geïnitieerde eenmalige aanmelding URL** opgegeven door Optimizely en plakken in Hallo **aanmelding op URL** textbox in **Optimizely domein en de URL's** sectie in Azure portal</span><span class="sxs-lookup"><span data-stu-id="2db2b-173">Copy hello **SP-initiated SSO URL** provided by Optimizely, and paste into hello **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

    <span data-ttu-id="2db2b-174">b.</span><span class="sxs-lookup"><span data-stu-id="2db2b-174">b.</span></span> <span data-ttu-id="2db2b-175">Kopiëren Hallo **Service Provider entiteit-ID** opgegeven door Optimizely en plakken in Hallo **id** textbox in **Optimizely domein en de URL's** sectie in Azure portal</span><span class="sxs-lookup"><span data-stu-id="2db2b-175">Copy hello **Service Provider Entity ID** provided by Optimizely, and paste into hello **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

9. <span data-ttu-id="2db2b-176">In een ander browservenster, aanmelding tooyour Optimizely toepassing.</span><span class="sxs-lookup"><span data-stu-id="2db2b-176">In a different browser window, sign-on tooyour Optimizely application.</span></span>

10. <span data-ttu-id="2db2b-177">Klikt u op dat u de accountnaam in de bovenste Hallo rechterbovenhoek en vervolgens **Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="2db2b-177">Click you account name in hello top right corner and then **Account Settings**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. <span data-ttu-id="2db2b-179">In het tabblad Account Hallo selectievakje Hallo **eenmalige aanmelding inschakelen** onder eenmalige aanmelding in Hallo **overzicht** sectie.</span><span class="sxs-lookup"><span data-stu-id="2db2b-179">In hello Account tab, check hello box **Enable SSO** under Single Sign On in hello **Overview** section.</span></span>
   
    ![Azure AD voor eenmalige aanmelding](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. <span data-ttu-id="2db2b-181">Klik op **opslaan**</span><span class="sxs-lookup"><span data-stu-id="2db2b-181">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="2db2b-182">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="2db2b-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2db2b-183">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="2db2b-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2db2b-184">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2db2b-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2db2b-185">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2db2b-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="2db2b-186">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2db2b-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="2db2b-188">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2db2b-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2db2b-189">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2db2b-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2db2b-191">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2db2b-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2db2b-193">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="2db2b-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2db2b-195">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2db2b-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2db2b-197">a.</span><span class="sxs-lookup"><span data-stu-id="2db2b-197">a.</span></span> <span data-ttu-id="2db2b-198">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2db2b-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2db2b-199">b.</span><span class="sxs-lookup"><span data-stu-id="2db2b-199">b.</span></span> <span data-ttu-id="2db2b-200">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2db2b-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="2db2b-201">c.</span><span class="sxs-lookup"><span data-stu-id="2db2b-201">c.</span></span> <span data-ttu-id="2db2b-202">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2db2b-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2db2b-203">d.</span><span class="sxs-lookup"><span data-stu-id="2db2b-203">d.</span></span> <span data-ttu-id="2db2b-204">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2db2b-204">Click **Create**.</span></span>
 
### <a name="creating-an-optimizely-test-user"></a><span data-ttu-id="2db2b-205">Een testgebruiker Optimizely maken</span><span class="sxs-lookup"><span data-stu-id="2db2b-205">Creating an Optimizely test user</span></span>

<span data-ttu-id="2db2b-206">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Optimizely maken.</span><span class="sxs-lookup"><span data-stu-id="2db2b-206">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="2db2b-207">Selecteer op de startpagina van Hallo **deelnemers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="2db2b-207">On hello home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="2db2b-208">tooadd nieuwe medewerker toohello project, klik op **nieuwe medewerker**.</span><span class="sxs-lookup"><span data-stu-id="2db2b-208">tooadd new collaborator toohello project, click **New Collaborator**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="2db2b-210">Vul Hallo e-mailadres en een rol toewijzen.</span><span class="sxs-lookup"><span data-stu-id="2db2b-210">Fill in hello email address and assign them a role.</span></span> <span data-ttu-id="2db2b-211">Klik op **uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="2db2b-211">Click **Invite**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. <span data-ttu-id="2db2b-213">Ze ontvangen een e-uitnodiging.</span><span class="sxs-lookup"><span data-stu-id="2db2b-213">They receive an email invite.</span></span> <span data-ttu-id="2db2b-214">Hallo e-mailadres hebben ze toolog in tooOptimizely.</span><span class="sxs-lookup"><span data-stu-id="2db2b-214">Using hello email address, they have toolog in tooOptimizely.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2db2b-215">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2db2b-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2db2b-216">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooOptimizely toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="2db2b-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOptimizely.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="2db2b-218">**tooassign Britta Simon tooOptimizely, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="2db2b-218">**tooassign Britta Simon tooOptimizely, perform hello following steps:**</span></span>

1. <span data-ttu-id="2db2b-219">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2db2b-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2db2b-221">Selecteer in de lijst met de toepassingen van Hallo **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="2db2b-221">In hello applications list, select **Optimizely**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. <span data-ttu-id="2db2b-223">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2db2b-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="2db2b-225">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2db2b-225">Click **Add** button.</span></span> <span data-ttu-id="2db2b-226">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2db2b-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="2db2b-228">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="2db2b-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2db2b-229">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2db2b-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2db2b-230">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2db2b-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2db2b-231">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2db2b-231">Testing single sign-on</span></span>

<span data-ttu-id="2db2b-232">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="2db2b-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2db2b-233">Als u op Hallo Optimizely tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Optimizely toepassing.</span><span class="sxs-lookup"><span data-stu-id="2db2b-233">When you click hello Optimizely tile in hello Access Panel, you should get automatically signed-on tooyour Optimizely application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2db2b-234">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2db2b-234">Additional resources</span></span>

* [<span data-ttu-id="2db2b-235">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2db2b-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2db2b-236">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2db2b-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

