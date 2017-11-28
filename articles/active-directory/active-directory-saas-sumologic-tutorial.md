---
title: 'Zelfstudie: Azure Active Directory-integratie met SumoLogic | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SumoLogic.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 2ef1bd329f5db8899f0b57744e4c0f6eed1c532f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="4a891-103">Zelfstudie: Azure Active Directory-integratie met SumoLogic</span><span class="sxs-lookup"><span data-stu-id="4a891-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="4a891-104">In deze zelfstudie leert u hoe toointegrate SumoLogic met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4a891-104">In this tutorial, you learn how toointegrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4a891-105">SumoLogic integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="4a891-105">Integrating SumoLogic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4a891-106">U kunt beheren in Azure AD die tooSumoLogic toegang heeft</span><span class="sxs-lookup"><span data-stu-id="4a891-106">You can control in Azure AD who has access tooSumoLogic</span></span>
- <span data-ttu-id="4a891-107">U kunt uw gebruikers tooautomatically get aangemelde tooSumoLogic (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="4a891-107">You can enable your users tooautomatically get signed-on tooSumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4a891-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="4a891-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4a891-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4a891-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a891-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4a891-110">Prerequisites</span></span>

<span data-ttu-id="4a891-111">Azure AD-integratie met SumoLogic tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="4a891-111">tooconfigure Azure AD integration with SumoLogic, you need hello following items:</span></span>

- <span data-ttu-id="4a891-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="4a891-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4a891-113">Een SumoLogic eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="4a891-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4a891-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="4a891-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4a891-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="4a891-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4a891-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="4a891-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4a891-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4a891-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4a891-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="4a891-118">Scenario description</span></span>
<span data-ttu-id="4a891-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4a891-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4a891-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="4a891-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4a891-121">Het toevoegen van SumoLogic van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4a891-121">Adding SumoLogic from hello gallery</span></span>
2. <span data-ttu-id="4a891-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4a891-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-hello-gallery"></a><span data-ttu-id="4a891-123">Het toevoegen van SumoLogic van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4a891-123">Adding SumoLogic from hello gallery</span></span>
<span data-ttu-id="4a891-124">tooconfigure hello integratie van SumoLogic in Azure AD, moet u tooadd SumoLogic uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="4a891-124">tooconfigure hello integration of SumoLogic into Azure AD, you need tooadd SumoLogic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4a891-125">**tooadd SumoLogic via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4a891-125">**tooadd SumoLogic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a891-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4a891-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4a891-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4a891-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4a891-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4a891-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="4a891-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4a891-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="4a891-133">Typ in het zoekvak Hallo **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="4a891-133">In hello search box, type **SumoLogic**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. <span data-ttu-id="4a891-135">Selecteer in het deelvenster resultaten hello, **SumoLogic**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="4a891-135">In hello results panel, select **SumoLogic**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4a891-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4a891-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4a891-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met SumoLogic op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="4a891-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4a891-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in SumoLogic is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a891-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SumoLogic is tooa user in Azure AD.</span></span> <span data-ttu-id="4a891-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in SumoLogic toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="4a891-140">In other words, a link relationship between an Azure AD user and hello related user in SumoLogic needs toobe established.</span></span>

<span data-ttu-id="4a891-141">Wijs in SumoLogic, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="4a891-141">In SumoLogic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4a891-142">tooconfigure en eenmalige aanmelding Azure AD-test met SumoLogic, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4a891-142">tooconfigure and test Azure AD single sign-on with SumoLogic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4a891-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="4a891-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4a891-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4a891-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4a891-145">**[Maken van een testgebruiker SumoLogic](#creating-a-sumologic-test-user)**  -toohave een equivalent van Britta Simon in SumoLogic die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4a891-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - toohave a counterpart of Britta Simon in SumoLogic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4a891-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4a891-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4a891-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="4a891-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4a891-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="4a891-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4a891-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing SumoLogic configureren.</span><span class="sxs-lookup"><span data-stu-id="4a891-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="4a891-150">**Azure AD tooconfigure eenmalige aanmelding met SumoLogic, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4a891-150">**tooconfigure Azure AD single sign-on with SumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a891-151">In de Azure-portal op Hallo Hallo **SumoLogic** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="4a891-151">In hello Azure portal, on hello **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="4a891-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4a891-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. <span data-ttu-id="4a891-155">Op Hallo **SumoLogic domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4a891-155">On hello **SumoLogic Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="4a891-157">a.</span><span class="sxs-lookup"><span data-stu-id="4a891-157">a.</span></span> <span data-ttu-id="4a891-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenantname>.SumoLogic.com`</span><span class="sxs-lookup"><span data-stu-id="4a891-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="4a891-159">b.</span><span class="sxs-lookup"><span data-stu-id="4a891-159">b.</span></span> <span data-ttu-id="4a891-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="4a891-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="4a891-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="4a891-161">These values are not real.</span></span> <span data-ttu-id="4a891-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="4a891-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4a891-163">Neem contact op met [SumoLogic Client ondersteuningsteam](https://www.sumologic.com/contact-us/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="4a891-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="4a891-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="4a891-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. <span data-ttu-id="4a891-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="4a891-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4a891-168">Op Hallo **SumoLogic configuratie** sectie, klikt u op **configureren SumoLogic** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="4a891-168">On hello **SumoLogic Configuration** section, click **Configure SumoLogic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4a891-169">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="4a891-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. <span data-ttu-id="4a891-171">In een ander browservenster, meld u aan tooyour SumoLogic bedrijf site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="4a891-171">In a different web browser window, log in tooyour SumoLogic company site as an administrator.</span></span>

8. <span data-ttu-id="4a891-172">Ga te**beheren \> beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="4a891-172">Go too**Manage \> Security**.</span></span>
   
    <span data-ttu-id="4a891-173">![Beheren](./media/active-directory-saas-sumologic-tutorial/ic778556.png "beheren")</span><span class="sxs-lookup"><span data-stu-id="4a891-173">![Manage](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Manage")</span></span>

9. <span data-ttu-id="4a891-174">Klik op **SAML**.</span><span class="sxs-lookup"><span data-stu-id="4a891-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="4a891-175">![Globale beveiligingsinstellingen](./media/active-directory-saas-sumologic-tutorial/ic778557.png "globale beveiligingsinstellingen")</span><span class="sxs-lookup"><span data-stu-id="4a891-175">![Global security settings](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Global security settings")</span></span>

10. <span data-ttu-id="4a891-176">Van Hallo **selecteert u een configuratie of maak een nieuwe** Selecteer **Azure AD**, en klik vervolgens op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="4a891-176">From hello **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="4a891-177">![Configureren van SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "SAML 2.0 configureren")</span><span class="sxs-lookup"><span data-stu-id="4a891-177">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

11. <span data-ttu-id="4a891-178">Op Hallo **configureren SAML 2.0** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="4a891-178">On hello **Configure SAML 2.0** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="4a891-179">![Configureren van SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "SAML 2.0 configureren")</span><span class="sxs-lookup"><span data-stu-id="4a891-179">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="4a891-180">a.</span><span class="sxs-lookup"><span data-stu-id="4a891-180">a.</span></span> <span data-ttu-id="4a891-181">In Hallo **configuratienaam** textbox type **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="4a891-181">In hello **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="4a891-182">b.</span><span class="sxs-lookup"><span data-stu-id="4a891-182">b.</span></span> <span data-ttu-id="4a891-183">Selecteer **foutopsporingsmodus**.</span><span class="sxs-lookup"><span data-stu-id="4a891-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="4a891-184">c.</span><span class="sxs-lookup"><span data-stu-id="4a891-184">c.</span></span> <span data-ttu-id="4a891-185">In Hallo **verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4a891-185">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="4a891-186">d.</span><span class="sxs-lookup"><span data-stu-id="4a891-186">d.</span></span> <span data-ttu-id="4a891-187">In Hallo **Authn aanvragen URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4a891-187">In hello **Authn Request URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4a891-188">e.</span><span class="sxs-lookup"><span data-stu-id="4a891-188">e.</span></span> <span data-ttu-id="4a891-189">De base-64 gecodeerde certificaat openen in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak Hallo gehele certificaat in **X.509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="4a891-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="4a891-190">f.</span><span class="sxs-lookup"><span data-stu-id="4a891-190">f.</span></span> <span data-ttu-id="4a891-191">Als **e kenmerk**, selecteer **gebruik SAML onderwerp**.</span><span class="sxs-lookup"><span data-stu-id="4a891-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="4a891-192">g.</span><span class="sxs-lookup"><span data-stu-id="4a891-192">g.</span></span> <span data-ttu-id="4a891-193">Selecteer **SP geïnitieerd aanmelding configuratie**.</span><span class="sxs-lookup"><span data-stu-id="4a891-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="4a891-194">h.</span><span class="sxs-lookup"><span data-stu-id="4a891-194">h.</span></span> <span data-ttu-id="4a891-195">In Hallo **aanmelding pad** textbox type **Azure** en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4a891-195">In hello **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4a891-196">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="4a891-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4a891-197">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="4a891-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4a891-198">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4a891-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4a891-199">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="4a891-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="4a891-200">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4a891-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="4a891-202">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4a891-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a891-203">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4a891-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4a891-205">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="4a891-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4a891-207">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="4a891-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4a891-209">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4a891-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4a891-211">a.</span><span class="sxs-lookup"><span data-stu-id="4a891-211">a.</span></span> <span data-ttu-id="4a891-212">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4a891-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4a891-213">b.</span><span class="sxs-lookup"><span data-stu-id="4a891-213">b.</span></span> <span data-ttu-id="4a891-214">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4a891-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4a891-215">c.</span><span class="sxs-lookup"><span data-stu-id="4a891-215">c.</span></span> <span data-ttu-id="4a891-216">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="4a891-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4a891-217">d.</span><span class="sxs-lookup"><span data-stu-id="4a891-217">d.</span></span> <span data-ttu-id="4a891-218">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="4a891-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="4a891-219">Een testgebruiker SumoLogic maken</span><span class="sxs-lookup"><span data-stu-id="4a891-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="4a891-220">In de volgorde tooenable Azure AD gebruikers toolog in tooSumoLogic, moeten ze ingerichte tooSumoLogic zijn.</span><span class="sxs-lookup"><span data-stu-id="4a891-220">In order tooenable Azure AD users toolog in tooSumoLogic, they must be provisioned tooSumoLogic.</span></span>  

* <span data-ttu-id="4a891-221">In geval van SumoLogic Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="4a891-221">In hello case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="4a891-222">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4a891-222">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a891-223">Meld u bij tooyour **SumoLogic** tenant.</span><span class="sxs-lookup"><span data-stu-id="4a891-223">Log in tooyour **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="4a891-224">Ga te**beheren \> gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="4a891-224">Go too**Manage \> Users**.</span></span>
   
    <span data-ttu-id="4a891-225">![Gebruikers](./media/active-directory-saas-sumologic-tutorial/ic778561.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="4a891-225">![Users](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Users")</span></span>

3. <span data-ttu-id="4a891-226">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="4a891-226">Click **Add**.</span></span>
   
    <span data-ttu-id="4a891-227">![Gebruikers](./media/active-directory-saas-sumologic-tutorial/ic778562.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="4a891-227">![Users](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Users")</span></span>

4. <span data-ttu-id="4a891-228">Op Hallo **nieuwe gebruiker** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="4a891-228">On hello **New User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="4a891-229">![Nieuwe gebruiker](./media/active-directory-saas-sumologic-tutorial/ic778563.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="4a891-229">![New User](./media/active-directory-saas-sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="4a891-230">a.</span><span class="sxs-lookup"><span data-stu-id="4a891-230">a.</span></span> <span data-ttu-id="4a891-231">Type Hallo verwante informatie van hello Azure AD-account door tooprovision in Hallo **voornaam**, **achternaam**, en **e** tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="4a891-231">Type hello related information of hello Azure AD account you want tooprovision into hello **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="4a891-232">b.</span><span class="sxs-lookup"><span data-stu-id="4a891-232">b.</span></span> <span data-ttu-id="4a891-233">Selecteer een rol.</span><span class="sxs-lookup"><span data-stu-id="4a891-233">Select a role.</span></span>
  
    <span data-ttu-id="4a891-234">c.</span><span class="sxs-lookup"><span data-stu-id="4a891-234">c.</span></span> <span data-ttu-id="4a891-235">Als **Status**, selecteer **Active**.</span><span class="sxs-lookup"><span data-stu-id="4a891-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="4a891-236">d.</span><span class="sxs-lookup"><span data-stu-id="4a891-236">d.</span></span> <span data-ttu-id="4a891-237">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4a891-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="4a891-238">U kunt andere SumoLogic gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door SumoLogic tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="4a891-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4a891-239">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a891-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4a891-240">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooSumoLogic toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="4a891-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSumoLogic.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="4a891-242">**tooassign Britta Simon tooSumoLogic, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4a891-242">**tooassign Britta Simon tooSumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="4a891-243">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4a891-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="4a891-245">Selecteer in de lijst met de toepassingen van Hallo **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="4a891-245">In hello applications list, select **SumoLogic**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. <span data-ttu-id="4a891-247">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="4a891-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="4a891-249">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="4a891-249">Click **Add** button.</span></span> <span data-ttu-id="4a891-250">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4a891-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="4a891-252">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="4a891-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4a891-253">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4a891-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4a891-254">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4a891-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4a891-255">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4a891-255">Testing single sign-on</span></span>

<span data-ttu-id="4a891-256">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="4a891-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4a891-257">Als u op Hallo SumoLogic tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SumoLogic toepassing.</span><span class="sxs-lookup"><span data-stu-id="4a891-257">When you click hello SumoLogic tile in hello Access Panel, you should get automatically signed-on tooyour SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4a891-258">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="4a891-258">Additional resources</span></span>

* [<span data-ttu-id="4a891-259">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4a891-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4a891-260">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4a891-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

