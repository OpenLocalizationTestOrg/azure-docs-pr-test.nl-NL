---
title: 'Zelfstudie: Azure Active Directory-integratie met Nexonia | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Nexonia.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/1/2017
ms.author: jeedes
ms.openlocfilehash: 3778804084a7989414260bae5654cf76e9ccca6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="42346-103">Zelfstudie: Azure Active Directory-integratie met Nexonia</span><span class="sxs-lookup"><span data-stu-id="42346-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="42346-104">In deze zelfstudie leert u hoe toointegrate Nexonia met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42346-104">In this tutorial, you learn how toointegrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42346-105">Nexonia integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="42346-105">Integrating Nexonia with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="42346-106">U kunt beheren in Azure AD die tooNexonia toegang heeft</span><span class="sxs-lookup"><span data-stu-id="42346-106">You can control in Azure AD who has access tooNexonia</span></span>
- <span data-ttu-id="42346-107">U kunt uw gebruikers tooautomatically get aangemelde tooNexonia (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="42346-107">You can enable your users tooautomatically get signed-on tooNexonia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="42346-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="42346-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="42346-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie.</span><span class="sxs-lookup"><span data-stu-id="42346-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="42346-110">[Wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="42346-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42346-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="42346-111">Prerequisites</span></span>

<span data-ttu-id="42346-112">Azure AD-integratie met Nexonia tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="42346-112">tooconfigure Azure AD integration with Nexonia, you need hello following items:</span></span>

- <span data-ttu-id="42346-113">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="42346-113">An Azure AD subscription</span></span>
- <span data-ttu-id="42346-114">Een Nexonia eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="42346-114">A Nexonia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42346-115">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="42346-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42346-116">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="42346-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42346-117">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="42346-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42346-118">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42346-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42346-119">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="42346-119">Scenario description</span></span>
<span data-ttu-id="42346-120">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="42346-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42346-121">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="42346-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42346-122">Het toevoegen van Nexonia van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="42346-122">Adding Nexonia from hello gallery</span></span>
2. <span data-ttu-id="42346-123">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="42346-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nexonia-from-hello-gallery"></a><span data-ttu-id="42346-124">Het toevoegen van Nexonia van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="42346-124">Adding Nexonia from hello gallery</span></span>
<span data-ttu-id="42346-125">tooconfigure hello integratie van Nexonia in Azure AD, moet u tooadd Nexonia uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="42346-125">tooconfigure hello integration of Nexonia into Azure AD, you need tooadd Nexonia from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="42346-126">**tooadd Nexonia via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="42346-126">**tooadd Nexonia from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="42346-127">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="42346-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="42346-129">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="42346-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="42346-130">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="42346-130">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="42346-132">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="42346-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="42346-134">Typ in het zoekvak Hallo **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="42346-134">In hello search box, type **Nexonia**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_search.png)

5. <span data-ttu-id="42346-136">Selecteer in het deelvenster resultaten hello, **Nexonia**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="42346-136">In hello results panel, select **Nexonia**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="42346-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="42346-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="42346-139">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Nexonia op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="42346-139">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="42346-140">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Nexonia is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42346-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Nexonia is tooa user in Azure AD.</span></span> <span data-ttu-id="42346-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Nexonia toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="42346-141">In other words, a link relationship between an Azure AD user and hello related user in Nexonia needs toobe established.</span></span>

<span data-ttu-id="42346-142">Wijs in Nexonia, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="42346-142">In Nexonia, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="42346-143">tooconfigure en eenmalige aanmelding Azure AD-test met Nexonia, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="42346-143">tooconfigure and test Azure AD single sign-on with Nexonia, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="42346-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="42346-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="42346-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42346-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42346-146">**[Maken van een testgebruiker Nexonia](#creating-a-nexonia-test-user)**  -toohave een equivalent van Britta Simon in Nexonia die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="42346-146">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - toohave a counterpart of Britta Simon in Nexonia that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="42346-147">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="42346-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42346-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="42346-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="42346-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="42346-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="42346-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Nexonia configureren.</span><span class="sxs-lookup"><span data-stu-id="42346-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Nexonia application.</span></span>

>[!Note]
><span data-ttu-id="42346-151">Als u problemen bij Hallo integratie hebt vervolgens dit verwijzen [koppeling](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) voor het oplossen.</span><span class="sxs-lookup"><span data-stu-id="42346-151">If you have issues in hello integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) for troubleshooting guide.</span></span> <span data-ttu-id="42346-152">Als u nog steeds niet Hallo oplossing hebt gevonden, kunt u de ondersteuningsaanvraag Hallo vanuit Azure-portal te verhogen.</span><span class="sxs-lookup"><span data-stu-id="42346-152">If you still have not found hello solution, then raise hello support request from Azure portal.</span></span>

<span data-ttu-id="42346-153">**Azure AD tooconfigure eenmalige aanmelding met Nexonia, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="42346-153">**tooconfigure Azure AD single sign-on with Nexonia, perform hello following steps:**</span></span>

1. <span data-ttu-id="42346-154">In de Azure-portal op Hallo Hallo **Nexonia** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="42346-154">In hello Azure portal, on hello **Nexonia** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="42346-156">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="42346-156">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_samlbase.png)

3. <span data-ttu-id="42346-158">Op Hallo **Nexonia domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="42346-158">On hello **Nexonia Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_url.png)

    <span data-ttu-id="42346-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span><span class="sxs-lookup"><span data-stu-id="42346-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="42346-161">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="42346-161">This value is not real.</span></span> <span data-ttu-id="42346-162">Deze waarde met de werkelijke antwoord-URL Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="42346-162">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="42346-163">Neem contact op met [Nexonia ondersteuningsteam](https://nexonia.zendesk.com/hc/requests/new) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="42346-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) tooget this value.</span></span> 


4. <span data-ttu-id="42346-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="42346-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_certificate.png) 

5. <span data-ttu-id="42346-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="42346-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-nexonia-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="42346-168">Op Hallo **Nexonia configuratie** sectie, klikt u op **configureren Nexonia** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="42346-168">On hello **Nexonia Configuration** section, click **Configure Nexonia** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="42346-169">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="42346-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_configure.png) 

7. <span data-ttu-id="42346-171">tooget SSO geconfigureerd voor uw toepassing, neem contact op met [Nexonia ondersteuningsteam](https://nexonia.zendesk.com/hc/requests/new) en voorzien Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="42346-171">tooget SSO configured for your application, contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) and provide them with hello following:</span></span>

    <span data-ttu-id="42346-172">• Hallo gedownload **certificaat**</span><span class="sxs-lookup"><span data-stu-id="42346-172">• hello downloaded **certificate**</span></span>

    <span data-ttu-id="42346-173">• Hallo **SAML entiteit-ID**</span><span class="sxs-lookup"><span data-stu-id="42346-173">• hello **SAML Entity ID**</span></span>

    <span data-ttu-id="42346-174">• Hallo **SAML Single Sign-On Service-URL**</span><span class="sxs-lookup"><span data-stu-id="42346-174">• hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="42346-175">• Hallo **Sign-Out URL**</span><span class="sxs-lookup"><span data-stu-id="42346-175">• hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="42346-176">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="42346-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="42346-177">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="42346-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="42346-178">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="42346-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="42346-179">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="42346-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="42346-180">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="42346-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="42346-182">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="42346-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="42346-183">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="42346-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-nexonia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="42346-185">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="42346-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-nexonia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="42346-187">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="42346-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-nexonia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="42346-189">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="42346-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-nexonia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="42346-191">a.</span><span class="sxs-lookup"><span data-stu-id="42346-191">a.</span></span> <span data-ttu-id="42346-192">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="42346-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42346-193">b.</span><span class="sxs-lookup"><span data-stu-id="42346-193">b.</span></span> <span data-ttu-id="42346-194">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="42346-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="42346-195">c.</span><span class="sxs-lookup"><span data-stu-id="42346-195">c.</span></span> <span data-ttu-id="42346-196">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="42346-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="42346-197">d.</span><span class="sxs-lookup"><span data-stu-id="42346-197">d.</span></span> <span data-ttu-id="42346-198">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="42346-198">Click **Create**.</span></span>
 
### <a name="creating-a-nexonia-test-user"></a><span data-ttu-id="42346-199">Een testgebruiker Nexonia maken</span><span class="sxs-lookup"><span data-stu-id="42346-199">Creating a Nexonia test user</span></span>

<span data-ttu-id="42346-200">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Nexonia maken.</span><span class="sxs-lookup"><span data-stu-id="42346-200">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="42346-201">Werken met [Nexonia ondersteuningsteam](https://nexonia.zendesk.com/hc/requests/new) tooadd Hallo gebruikers in Hallo Nexonia platform.</span><span class="sxs-lookup"><span data-stu-id="42346-201">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) tooadd hello users in hello Nexonia platform.</span></span> <span data-ttu-id="42346-202">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="42346-202">Users must be created and activated before you use single sign-on.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="42346-203">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="42346-203">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="42346-204">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooNexonia toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="42346-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNexonia.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="42346-206">**tooassign Britta Simon tooNexonia, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="42346-206">**tooassign Britta Simon tooNexonia, perform hello following steps:**</span></span>

1. <span data-ttu-id="42346-207">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="42346-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="42346-209">Selecteer in de lijst met de toepassingen van Hallo **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="42346-209">In hello applications list, select **Nexonia**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_app.png) 

3. <span data-ttu-id="42346-211">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="42346-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="42346-213">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="42346-213">Click **Add** button.</span></span> <span data-ttu-id="42346-214">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="42346-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="42346-216">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="42346-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="42346-217">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="42346-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42346-218">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="42346-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="42346-219">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="42346-219">Testing single sign-on</span></span>

<span data-ttu-id="42346-220">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="42346-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="42346-221">Als u op Hallo Nexonia tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Nexonia toepassing.</span><span class="sxs-lookup"><span data-stu-id="42346-221">When you click hello Nexonia tile in hello Access Panel, you should get automatically signed-on tooyour Nexonia application.</span></span>
<span data-ttu-id="42346-222">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="42346-222">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="42346-223">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="42346-223">Additional resources</span></span>

* [<span data-ttu-id="42346-224">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42346-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42346-225">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="42346-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_203.png

