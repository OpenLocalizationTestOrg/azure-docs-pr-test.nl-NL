---
title: 'Zelfstudie: Azure Active Directory-integratie met Menlo beveiliging | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Menlo beveiliging.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 193d12eedf31f4f08e1d141936d6e918c36a2109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="98d9b-103">Zelfstudie: Azure Active Directory-integratie met Menlo beveiliging</span><span class="sxs-lookup"><span data-stu-id="98d9b-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="98d9b-104">In deze zelfstudie leert u hoe toointegrate Menlo beveiliging met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="98d9b-104">In this tutorial, you learn how toointegrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="98d9b-105">Menlo beveiliging integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="98d9b-105">Integrating Menlo Security with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="98d9b-106">U kunt beheren in Azure AD wie toegang tot tooMenlo beveiliging heeft</span><span class="sxs-lookup"><span data-stu-id="98d9b-106">You can control in Azure AD who has access tooMenlo Security</span></span>
- <span data-ttu-id="98d9b-107">U kunt uw gebruikers tooautomatically get aangemelde tooMenlo beveiliging (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="98d9b-107">You can enable your users tooautomatically get signed-on tooMenlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="98d9b-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="98d9b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="98d9b-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie.</span><span class="sxs-lookup"><span data-stu-id="98d9b-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="98d9b-110">[Wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="98d9b-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98d9b-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="98d9b-111">Prerequisites</span></span>

<span data-ttu-id="98d9b-112">Azure AD-integratie met Menlo beveiliging tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="98d9b-112">tooconfigure Azure AD integration with Menlo Security, you need hello following items:</span></span>

- <span data-ttu-id="98d9b-113">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="98d9b-113">An Azure AD subscription</span></span>
- <span data-ttu-id="98d9b-114">Een Menlo beveiliging eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="98d9b-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="98d9b-115">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="98d9b-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="98d9b-116">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="98d9b-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="98d9b-117">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="98d9b-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="98d9b-118">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="98d9b-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="98d9b-119">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="98d9b-119">Scenario description</span></span>
<span data-ttu-id="98d9b-120">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="98d9b-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="98d9b-121">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="98d9b-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="98d9b-122">Het toevoegen van Menlo beveiliging van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="98d9b-122">Adding Menlo Security from hello gallery</span></span>
2. <span data-ttu-id="98d9b-123">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="98d9b-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-hello-gallery"></a><span data-ttu-id="98d9b-124">Het toevoegen van Menlo beveiliging van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="98d9b-124">Adding Menlo Security from hello gallery</span></span>
<span data-ttu-id="98d9b-125">tooconfigure hello integratie van Menlo beveiliging met Azure AD, moet u tooadd Menlo beveiliging van Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="98d9b-125">tooconfigure hello integration of Menlo Security into Azure AD, you need tooadd Menlo Security from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="98d9b-126">**tooadd Menlo beveiliging via Hallo gallery Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="98d9b-126">**tooadd Menlo Security from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="98d9b-127">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="98d9b-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="98d9b-129">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="98d9b-130">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-130">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="98d9b-132">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="98d9b-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="98d9b-134">Typ in het zoekvak Hallo **Menlo beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-134">In hello search box, type **Menlo Security**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="98d9b-136">Selecteer in het deelvenster resultaten hello, **Menlo beveiliging**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="98d9b-136">In hello results panel, select **Menlo Security**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="98d9b-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="98d9b-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="98d9b-139">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Menlo beveiliging op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="98d9b-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="98d9b-140">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Menlo beveiliging is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98d9b-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Menlo Security is tooa user in Azure AD.</span></span> <span data-ttu-id="98d9b-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Menlo beveiliging toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="98d9b-141">In other words, a link relationship between an Azure AD user and hello related user in Menlo Security needs toobe established.</span></span>

<span data-ttu-id="98d9b-142">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Menlo beveiliging.</span><span class="sxs-lookup"><span data-stu-id="98d9b-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Menlo Security.</span></span>

<span data-ttu-id="98d9b-143">tooconfigure en test eenmalige aanmelding Azure AD met Menlo beveiliging, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="98d9b-143">tooconfigure and test Azure AD single sign-on with Menlo Security, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="98d9b-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="98d9b-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="98d9b-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="98d9b-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="98d9b-146">**[Maken van een testgebruiker Menlo beveiliging](#creating-a-menlo-security-test-user)**  -toohave een equivalent van Britta Simon in Menlo beveiliging die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="98d9b-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - toohave a counterpart of Britta Simon in Menlo Security that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="98d9b-147">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="98d9b-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="98d9b-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="98d9b-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="98d9b-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="98d9b-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="98d9b-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Menlo beveiliging configureren.</span><span class="sxs-lookup"><span data-stu-id="98d9b-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="98d9b-151">**Voer tooconfigure Azure AD eenmalige aanmelding met Menlo beveiliging Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="98d9b-151">**tooconfigure Azure AD single sign-on with Menlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="98d9b-152">In de Azure-portal op Hallo Hallo **Menlo beveiliging** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-152">In hello Azure portal, on hello **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="98d9b-154">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="98d9b-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="98d9b-156">Op Hallo **Menlo beveiligingsdomein en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="98d9b-156">On hello **Menlo Security Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="98d9b-158">a.</span><span class="sxs-lookup"><span data-stu-id="98d9b-158">a.</span></span> <span data-ttu-id="98d9b-159">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="98d9b-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="98d9b-160">b.</span><span class="sxs-lookup"><span data-stu-id="98d9b-160">b.</span></span> <span data-ttu-id="98d9b-161">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="98d9b-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="98d9b-162">Deze waarden zijn niet Hallo echte.</span><span class="sxs-lookup"><span data-stu-id="98d9b-162">These values are not hello real.</span></span> <span data-ttu-id="98d9b-163">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="98d9b-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="98d9b-164">Neem contact op met [Beveiligingsclient Menlo ondersteuningsteam](https://www.menlosecurity.com/menlo-contact) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="98d9b-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="98d9b-165">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="98d9b-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="98d9b-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="98d9b-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="98d9b-169">Op Hallo **Menlo Beveiligingsconfiguratie** sectie, klikt u op **Menlo beveiliging configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="98d9b-169">On hello **Menlo Security Configuration** section, click **Configure Menlo Security** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="98d9b-170">Kopiëren Hallo **SAML entiteit-ID**, en **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="98d9b-170">Copy hello **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="98d9b-172">tooconfigure eenmalige aanmelding op **Menlo beveiliging** side, aanmelding toohello **Menlo beveiliging** website als beheerder.</span><span class="sxs-lookup"><span data-stu-id="98d9b-172">tooconfigure single sign-on on **Menlo Security** side, login toohello **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="98d9b-173">Onder **instellingen** te gaan**verificatie** en de volgende acties uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="98d9b-173">Under **Settings** go too**Authentication** and perform following actions:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="98d9b-175">a.</span><span class="sxs-lookup"><span data-stu-id="98d9b-175">a.</span></span> <span data-ttu-id="98d9b-176">Hallo selectievakje maatstreepjes **gebruikersverificatie inschakelen via SAML**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-176">Tick hello checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="98d9b-177">b.</span><span class="sxs-lookup"><span data-stu-id="98d9b-177">b.</span></span> <span data-ttu-id="98d9b-178">Selecteer **toestaan van externe toegang** te**Ja**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-178">Select **Allow External Access** too**Yes**.</span></span>

    <span data-ttu-id="98d9b-179">c.</span><span class="sxs-lookup"><span data-stu-id="98d9b-179">c.</span></span> <span data-ttu-id="98d9b-180">Onder **SAML Provider**, selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="98d9b-181">d.</span><span class="sxs-lookup"><span data-stu-id="98d9b-181">d.</span></span> <span data-ttu-id="98d9b-182">**SAML 2.0 eindpunt** : plakken Hallo **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="98d9b-182">**SAML 2.0 Endpoint** : Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="98d9b-183">e.</span><span class="sxs-lookup"><span data-stu-id="98d9b-183">e.</span></span> <span data-ttu-id="98d9b-184">**Service-id (verlener genoemd)** : plakken Hallo **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="98d9b-184">**Service Identifier (Issuer)** : Paste hello **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="98d9b-185">f.</span><span class="sxs-lookup"><span data-stu-id="98d9b-185">f.</span></span> <span data-ttu-id="98d9b-186">**X.509-certificaat** : Open Hallo **certificaat (Base64)** gedownload van hello Azure-Portal in Kladblok en plak deze in dit vak.</span><span class="sxs-lookup"><span data-stu-id="98d9b-186">**X.509 Certificate** : Open hello **Certificate (Base64)** downloaded from hello Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="98d9b-187">g.</span><span class="sxs-lookup"><span data-stu-id="98d9b-187">g.</span></span> <span data-ttu-id="98d9b-188">Klik op **opslaan** toosave Hallo instellingen.</span><span class="sxs-lookup"><span data-stu-id="98d9b-188">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="98d9b-189">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="98d9b-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="98d9b-190">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="98d9b-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="98d9b-191">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="98d9b-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="98d9b-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="98d9b-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="98d9b-193">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="98d9b-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="98d9b-195">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="98d9b-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="98d9b-196">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="98d9b-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="98d9b-198">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="98d9b-200">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="98d9b-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="98d9b-202">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="98d9b-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="98d9b-204">a.</span><span class="sxs-lookup"><span data-stu-id="98d9b-204">a.</span></span> <span data-ttu-id="98d9b-205">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="98d9b-206">b.</span><span class="sxs-lookup"><span data-stu-id="98d9b-206">b.</span></span> <span data-ttu-id="98d9b-207">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="98d9b-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="98d9b-208">c.</span><span class="sxs-lookup"><span data-stu-id="98d9b-208">c.</span></span> <span data-ttu-id="98d9b-209">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="98d9b-210">d.</span><span class="sxs-lookup"><span data-stu-id="98d9b-210">d.</span></span> <span data-ttu-id="98d9b-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="98d9b-212">Maken van een testgebruiker Menlo beveiliging</span><span class="sxs-lookup"><span data-stu-id="98d9b-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="98d9b-213">In deze sectie maakt u Britta Simon aangeroepen in Menlo beveiliging van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="98d9b-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="98d9b-214">Werken met [Beveiligingsclient Menlo ondersteuningsteam](https://www.menlosecurity.com/menlo-contact) tooadd Hallo gebruikers in Hallo Menlo beveiliging platform.</span><span class="sxs-lookup"><span data-stu-id="98d9b-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooadd hello users in hello Menlo Security platform.</span></span> <span data-ttu-id="98d9b-215">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="98d9b-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="98d9b-216">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="98d9b-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="98d9b-217">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooMenlo beveiliging.</span><span class="sxs-lookup"><span data-stu-id="98d9b-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMenlo Security.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="98d9b-219">**tooassign Britta Simon tooMenlo beveiliging, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="98d9b-219">**tooassign Britta Simon tooMenlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="98d9b-220">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="98d9b-222">Selecteer in de lijst met de toepassingen van Hallo **Menlo beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-222">In hello applications list, select **Menlo Security**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="98d9b-224">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="98d9b-226">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="98d9b-226">Click **Add** button.</span></span> <span data-ttu-id="98d9b-227">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="98d9b-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="98d9b-229">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="98d9b-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="98d9b-230">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="98d9b-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="98d9b-231">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="98d9b-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="98d9b-232">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="98d9b-232">Testing single sign-on</span></span>

<span data-ttu-id="98d9b-233">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie testen.</span><span class="sxs-lookup"><span data-stu-id="98d9b-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="98d9b-234">Open een browservenster in een 'InPrivate' of 'Incognito' modus tootrigger een nieuwe verificatie.</span><span class="sxs-lookup"><span data-stu-id="98d9b-234">Open a browser window in an "InPrivate" or "Incognito" mode tootrigger a new authentication.</span></span>  <span data-ttu-id="98d9b-235">Gebruik Ctrl + Shift + P in Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="98d9b-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="98d9b-236">Gebruik Ctrl + Shift + N in Chrome.</span><span class="sxs-lookup"><span data-stu-id="98d9b-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="98d9b-237">In Hallo persoonlijke Browse venster Bladeren tooa beveiligde resource en uitvoeren van een Azure AD-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="98d9b-237">In hello private browsing window, browse tooa protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="98d9b-238">Bij geslaagde aanmelding zult u genomen toohello gevraagde website in een sessie isolatie.</span><span class="sxs-lookup"><span data-stu-id="98d9b-238">Upon successful login, you will be taken toohello requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="98d9b-239">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="98d9b-239">Additional resources</span></span>

* [<span data-ttu-id="98d9b-240">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="98d9b-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="98d9b-241">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="98d9b-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

