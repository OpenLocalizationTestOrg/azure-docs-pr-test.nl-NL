---
title: 'Zelfstudie: Azure Active Directory-integratie met Atlassian Cloud | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Atlassian Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: f679e8b3306bf0efb9373d8baa0cfe095b760aaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="ee78d-103">Zelfstudie: Azure Active Directory-integratie met Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="ee78d-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="ee78d-104">In deze zelfstudie leert u hoe toointegrate Atlassian Cloud met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ee78d-104">In this tutorial, you learn how toointegrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ee78d-105">Atlassian Cloud integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ee78d-105">Integrating Atlassian Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ee78d-106">U kunt beheren in Azure AD wie toegang tot tooAtlassian Cloud heeft</span><span class="sxs-lookup"><span data-stu-id="ee78d-106">You can control in Azure AD who has access tooAtlassian Cloud</span></span>
- <span data-ttu-id="ee78d-107">U kunt uw gebruikers tooautomatically get aangemelde tooAtlassian Cloud (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="ee78d-107">You can enable your users tooautomatically get signed-on tooAtlassian Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ee78d-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ee78d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ee78d-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ee78d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee78d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ee78d-110">Prerequisites</span></span>

<span data-ttu-id="ee78d-111">Azure AD-integratie met Atlassian Cloud tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="ee78d-111">tooconfigure Azure AD integration with Atlassian Cloud, you need hello following items:</span></span>

- <span data-ttu-id="ee78d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ee78d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ee78d-113">Een Atlassian Cloud eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ee78d-113">An Atlassian Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ee78d-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ee78d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ee78d-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ee78d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ee78d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ee78d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ee78d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ee78d-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ee78d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ee78d-118">Scenario description</span></span>
<span data-ttu-id="ee78d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ee78d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ee78d-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ee78d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ee78d-121">Het toevoegen van Atlassian Cloud van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ee78d-121">Adding Atlassian Cloud from hello gallery</span></span>
2. <span data-ttu-id="ee78d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ee78d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atlassian-cloud-from-hello-gallery"></a><span data-ttu-id="ee78d-123">Het toevoegen van Atlassian Cloud van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="ee78d-123">Adding Atlassian Cloud from hello gallery</span></span>
<span data-ttu-id="ee78d-124">tooconfigure hello integratie van Atlassian Cloud met Azure AD, moet u tooadd Atlassian Cloud uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ee78d-124">tooconfigure hello integration of Atlassian Cloud into Azure AD, you need tooadd Atlassian Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ee78d-125">**tooadd Atlassian Cloud via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ee78d-125">**tooadd Atlassian Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee78d-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ee78d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ee78d-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ee78d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ee78d-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ee78d-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ee78d-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ee78d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ee78d-133">Typ in het zoekvak Hallo **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="ee78d-133">In hello search box, type **Atlassian Cloud**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. <span data-ttu-id="ee78d-135">Selecteer in het deelvenster resultaten hello, **Atlassian Cloud**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ee78d-135">In hello results panel, select **Atlassian Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ee78d-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ee78d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ee78d-138">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met Atlassian Cloud op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="ee78d-138">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ee78d-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de Atlassian Cloud is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ee78d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Atlassian Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="ee78d-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in de Atlassian Cloud hello toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="ee78d-140">In other words, a link relationship between an Azure AD user and hello related user in Atlassian Cloud needs toobe established.</span></span>

<span data-ttu-id="ee78d-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="ee78d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Atlassian Cloud.</span></span>

<span data-ttu-id="ee78d-142">tooconfigure en eenmalige aanmelding Azure AD-test met Atlassian Cloud, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ee78d-142">tooconfigure and test Azure AD single sign-on with Atlassian Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ee78d-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="ee78d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ee78d-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ee78d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ee78d-145">**[Maken van een testgebruiker Atlassian Cloud](#creating-an-atlassian-cloud-test-user)**  -toohave een equivalent van Britta Simon in Atlassian Cloud die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ee78d-145">**[Creating an Atlassian Cloud test user](#creating-an-atlassian-cloud-test-user)** - toohave a counterpart of Britta Simon in Atlassian Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ee78d-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ee78d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ee78d-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ee78d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ee78d-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ee78d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ee78d-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="ee78d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Atlassian Cloud application.</span></span>

<span data-ttu-id="ee78d-150">**Voer tooconfigure Azure AD eenmalige aanmelding met Atlassian Cloud, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ee78d-150">**tooconfigure Azure AD single sign-on with Atlassian Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee78d-151">In de Azure-portal op Hallo Hallo **Atlassian Cloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ee78d-151">In hello Azure portal, on hello **Atlassian Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ee78d-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ee78d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. <span data-ttu-id="ee78d-155">Op Hallo **Atlassian Cloud-domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wilt dat tooconfigure Hallo toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="ee78d-155">On hello **Atlassian Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    <span data-ttu-id="ee78d-157">a.</span><span class="sxs-lookup"><span data-stu-id="ee78d-157">a.</span></span> <span data-ttu-id="ee78d-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<instancename>.atlassian.net/admin/saml/edit`</span><span class="sxs-lookup"><span data-stu-id="ee78d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.atlassian.net/admin/saml/edit`</span></span>

    <span data-ttu-id="ee78d-159">b.</span><span class="sxs-lookup"><span data-stu-id="ee78d-159">b.</span></span> <span data-ttu-id="ee78d-160">In Hallo **antwoord-URL** textbox, typ een URL als:`https://id.atlassian.com/login/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="ee78d-160">In hello **Reply URL** textbox, type a URL as: `https://id.atlassian.com/login/saml/acs`</span></span>

4. <span data-ttu-id="ee78d-161">Controleer **weergeven geavanceerde instellingen voor URL** en uitvoeren van de volgende stap als u wilt dat tooconfigure Hallo toepassing in Hallo **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="ee78d-161">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    <span data-ttu-id="ee78d-163">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<instancename>.atlassian.net`</span><span class="sxs-lookup"><span data-stu-id="ee78d-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.atlassian.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ee78d-164">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="ee78d-164">These values are not real.</span></span> <span data-ttu-id="ee78d-165">Bijwerken van deze waarden met de werkelijke Hallo-id en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="ee78d-165">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="ee78d-166">Hallo exacte waarden kunt u krijgen via Cloud SAML-configuratie van Atlassian scherm.</span><span class="sxs-lookup"><span data-stu-id="ee78d-166">You can get hello exact values from Atlassian Cloud SAML Configuration screen.</span></span>
 
5. <span data-ttu-id="ee78d-167">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ee78d-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. <span data-ttu-id="ee78d-169">Op Hallo **Atlassian Cloudconfiguratie** sectie, klikt u op **Atlassian Cloud configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="ee78d-169">On hello **Atlassian Cloud Configuration** section, click **Configure Atlassian Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ee78d-170">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="ee78d-170">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. <span data-ttu-id="ee78d-172">tooget SSO is geconfigureerd voor uw toepassing, aanmelding toohello Atlassian Portal met behulp van Hallo administrator-rechten.</span><span class="sxs-lookup"><span data-stu-id="ee78d-172">tooget SSO configured for your application, login toohello Atlassian Portal using hello administrator rights.</span></span>

8. <span data-ttu-id="ee78d-173">Klik in het Hallo-verificatiesectie van Hallo linkernavigatiebalk op **domeinen**.</span><span class="sxs-lookup"><span data-stu-id="ee78d-173">In hello Authentication section of hello left navigation click **Domains**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    <span data-ttu-id="ee78d-175">a.</span><span class="sxs-lookup"><span data-stu-id="ee78d-175">a.</span></span> <span data-ttu-id="ee78d-176">Typ de naam van uw domein in Hallo tekstvak en klik vervolgens op **domein toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ee78d-176">In hello textbox, type your domain name, and then click **Add domain**.</span></span>
        
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    <span data-ttu-id="ee78d-178">b.</span><span class="sxs-lookup"><span data-stu-id="ee78d-178">b.</span></span> <span data-ttu-id="ee78d-179">tooverify hello domein, klikt u op **controleren**.</span><span class="sxs-lookup"><span data-stu-id="ee78d-179">tooverify hello domain, click **Verify**.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    <span data-ttu-id="ee78d-181">c.</span><span class="sxs-lookup"><span data-stu-id="ee78d-181">c.</span></span> <span data-ttu-id="ee78d-182">Hallo-domein verificatie HTML-bestand downloaden, toohello hoofdmap van de website van uw domein te uploaden en klik vervolgens op **domein controleren**.</span><span class="sxs-lookup"><span data-stu-id="ee78d-182">Download hello domain verification html file, upload it toohello root folder of your domain's website, and then click **Verify domain**.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    <span data-ttu-id="ee78d-184">d.</span><span class="sxs-lookup"><span data-stu-id="ee78d-184">d.</span></span> <span data-ttu-id="ee78d-185">Zodra het Hallo-domein is geverifieerd, waarde van Hallo Hallo **Status** veld is **geverifieerde**.</span><span class="sxs-lookup"><span data-stu-id="ee78d-185">Once hello domain is verified, hello value of hello **Status** field is **Verified**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. <span data-ttu-id="ee78d-187">Klik in het Hallo linkernavigatiebalk op **SAML**.</span><span class="sxs-lookup"><span data-stu-id="ee78d-187">In hello left navigation bar, click **SAML**.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. <span data-ttu-id="ee78d-189">Maken van een SAML-configuratie en Hallo identiteit providerconfiguratie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ee78d-189">Create a SAML Configuration and add hello Identity provider configuration.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    <span data-ttu-id="ee78d-191">a.</span><span class="sxs-lookup"><span data-stu-id="ee78d-191">a.</span></span> <span data-ttu-id="ee78d-192">In Hallo **identiteitsprovider entiteit-ID** tekstvak plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ee78d-192">In hello **Identity provider Entity ID** text box, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ee78d-193">b.</span><span class="sxs-lookup"><span data-stu-id="ee78d-193">b.</span></span> <span data-ttu-id="ee78d-194">In Hallo **identiteitsprovider URL SSO** tekstvak plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ee78d-194">In hello **Identity provider SSO URL** text box, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ee78d-195">c.</span><span class="sxs-lookup"><span data-stu-id="ee78d-195">c.</span></span> <span data-ttu-id="ee78d-196">Open Hallo gedownload certificaat van de Azure portal en Hallo waarden kopiëren zonder Hallo Begin en einde regels en plak deze in Hallo **openbare X509 certificaat** vak.</span><span class="sxs-lookup"><span data-stu-id="ee78d-196">Open hello downloaded certificate from Azure portal and copy hello values without hello Begin and End lines and paste it in hello **Public X509 certificate** box.</span></span>
    
    <span data-ttu-id="ee78d-197">d.</span><span class="sxs-lookup"><span data-stu-id="ee78d-197">d.</span></span> <span data-ttu-id="ee78d-198">Klik op **configuratie opslaan** tooSave Hallo instellingen.</span><span class="sxs-lookup"><span data-stu-id="ee78d-198">Click **Save Configuration**  tooSave hello settings.</span></span>
     
11. <span data-ttu-id="ee78d-199">Werk hello Azure AD-instellingen toomake ervoor dat u setup Hallo identificatie-URL te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="ee78d-199">Update hello Azure AD settings toomake sure that you have setup hello correct Identifier URL.</span></span>
  
    <span data-ttu-id="ee78d-200">a.</span><span class="sxs-lookup"><span data-stu-id="ee78d-200">a.</span></span> <span data-ttu-id="ee78d-201">Kopiëren Hallo **SP identiteit ID** van Hallo SAML scherm en plak deze in Azure AD als Hallo **id** waarde.</span><span class="sxs-lookup"><span data-stu-id="ee78d-201">Copy hello **SP Identity ID** from hello SAML screen and paste it in Azure AD as hello **Identifier** value.</span></span>

    <span data-ttu-id="ee78d-202">b.</span><span class="sxs-lookup"><span data-stu-id="ee78d-202">b.</span></span> <span data-ttu-id="ee78d-203">Meld u op de URL is Hallo tenant-URL van uw Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="ee78d-203">Sign On URL is hello tenant URL of your Atlassian Cloud.</span></span>     

     ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. <span data-ttu-id="ee78d-205">Klik in hello Azure-portal, op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ee78d-205">In hello Azure portal, Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="ee78d-207">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="ee78d-207">You can now read a concise version of these instructions inside hello [Azure  portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ee78d-208">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="ee78d-208">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ee78d-209">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ee78d-209">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ee78d-210">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ee78d-210">Creating an Azure AD test user</span></span>
<span data-ttu-id="ee78d-211">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ee78d-211">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ee78d-213">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ee78d-213">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee78d-214">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ee78d-214">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ee78d-216">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ee78d-216">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ee78d-218">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="ee78d-218">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ee78d-220">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ee78d-220">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ee78d-222">a.</span><span class="sxs-lookup"><span data-stu-id="ee78d-222">a.</span></span> <span data-ttu-id="ee78d-223">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ee78d-223">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ee78d-224">b.</span><span class="sxs-lookup"><span data-stu-id="ee78d-224">b.</span></span> <span data-ttu-id="ee78d-225">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ee78d-225">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ee78d-226">c.</span><span class="sxs-lookup"><span data-stu-id="ee78d-226">c.</span></span> <span data-ttu-id="ee78d-227">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ee78d-227">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ee78d-228">d.</span><span class="sxs-lookup"><span data-stu-id="ee78d-228">d.</span></span> <span data-ttu-id="ee78d-229">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ee78d-229">Click **Create**.</span></span>
 
### <a name="creating-an-atlassian-cloud-test-user"></a><span data-ttu-id="ee78d-230">Een testgebruiker Atlassian Cloud maken</span><span class="sxs-lookup"><span data-stu-id="ee78d-230">Creating an Atlassian Cloud test user</span></span>

<span data-ttu-id="ee78d-231">Azure AD tooenable gebruikers toolog in tooAtlassian Cloud, ze in de Atlassian Cloud moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="ee78d-231">tooenable Azure AD users toolog in tooAtlassian Cloud, they must be provisioned into Atlassian Cloud.</span></span>  
<span data-ttu-id="ee78d-232">In geval van een Atlassian Cloud is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="ee78d-232">In case of Atlassian Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="ee78d-233">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ee78d-233">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee78d-234">Klik in de beheersectie van de Site Hallo, op Hallo **gebruikers** knop</span><span class="sxs-lookup"><span data-stu-id="ee78d-234">In hello Site administration section, click hello **Users** button</span></span>

    ![Atlassian Cloud-gebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. <span data-ttu-id="ee78d-236">Klik op Hallo **gebruiker maken** knop toocreate een gebruiker in Hallo Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="ee78d-236">Click hello **Create User** button toocreate a user in hello Atlassian Cloud</span></span>

    ![Atlassian Cloud-gebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. <span data-ttu-id="ee78d-238">Voer van Hallo gebruiker **e-mailadres**, **gebruikersnaam**, en **volledige naam** en toegang tot de toepassing hello toewijzen.</span><span class="sxs-lookup"><span data-stu-id="ee78d-238">Enter hello user's **Email address**, **Username**, and **Full Name** and assign hello application access.</span></span> 

    ![Atlassian Cloud-gebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. <span data-ttu-id="ee78d-240">Klik op **gebruiker maken** knop, stuurt deze Hallo e-mailadres uitnodiging toohello gebruikersnaam en na het accepteren van Hallo uitnodiging Hallo gebruiker worden actief in Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="ee78d-240">Click **Create user** button, it will send hello email invitation toohello user and after accepting hello invitation hello user will be active in hello system.</span></span> 

>[!NOTE] 
><span data-ttu-id="ee78d-241">U kunt ook maken Hallo bulksgewijs gebruikers door te klikken op Hallo **bulksgewijs maken** knop in Hallo sectie gebruikers.</span><span class="sxs-lookup"><span data-stu-id="ee78d-241">You can also create hello bulk users by clicking hello **Bulk Create** button in hello Users section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ee78d-242">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee78d-242">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ee78d-243">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooAtlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="ee78d-243">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAtlassian Cloud.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ee78d-245">**tooassign Britta Simon tooAtlassian Cloud, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="ee78d-245">**tooassign Britta Simon tooAtlassian Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee78d-246">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ee78d-246">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ee78d-248">Selecteer in de lijst met de toepassingen van Hallo **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="ee78d-248">In hello applications list, select **Atlassian Cloud**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. <span data-ttu-id="ee78d-250">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ee78d-250">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ee78d-252">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ee78d-252">Click **Add** button.</span></span> <span data-ttu-id="ee78d-253">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ee78d-253">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ee78d-255">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee78d-255">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ee78d-256">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ee78d-256">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ee78d-257">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ee78d-257">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ee78d-258">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ee78d-258">Testing single sign-on</span></span>

<span data-ttu-id="ee78d-259">In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ee78d-259">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="ee78d-260">Als u op Hallo Atlassian Cloud-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Atlassian Cloud-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ee78d-260">When you click hello Atlassian Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Atlassian Cloud application.</span></span> <span data-ttu-id="ee78d-261">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ee78d-261">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ee78d-262">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ee78d-262">Additional resources</span></span>

* [<span data-ttu-id="ee78d-263">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee78d-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ee78d-264">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ee78d-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

