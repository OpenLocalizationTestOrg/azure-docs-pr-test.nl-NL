---
title: 'Zelfstudie: Azure Active Directory-integratie met de Jitbit Helpdesk | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Jitbit Helpdesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f6c837bbb910c1e84f7ed9da676c5ab40f75338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="cc2c2-103">Zelfstudie: Azure Active Directory-integratie met Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="cc2c2-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="cc2c2-104">In deze zelfstudie leert u hoe toointegrate Jitbit Helpdesk met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc2c2-104">In this tutorial, you learn how toointegrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc2c2-105">Jitbit Helpdesk integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="cc2c2-105">Integrating Jitbit Helpdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cc2c2-106">U kunt beheren in Azure AD wie toegang tot tooJitbit Helpdesk heeft</span><span class="sxs-lookup"><span data-stu-id="cc2c2-106">You can control in Azure AD who has access tooJitbit Helpdesk</span></span>
- <span data-ttu-id="cc2c2-107">U kunt uw gebruikers tooautomatically get aangemelde tooJitbit Helpdesk (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="cc2c2-107">You can enable your users tooautomatically get signed-on tooJitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cc2c2-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="cc2c2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cc2c2-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cc2c2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc2c2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cc2c2-110">Prerequisites</span></span>

<span data-ttu-id="cc2c2-111">Azure AD-integratie met de Jitbit Helpdesk tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="cc2c2-111">tooconfigure Azure AD integration with Jitbit Helpdesk, you need hello following items:</span></span>

- <span data-ttu-id="cc2c2-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="cc2c2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc2c2-113">Een Jitbit Helpdesk eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="cc2c2-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc2c2-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc2c2-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="cc2c2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc2c2-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc2c2-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc2c2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc2c2-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="cc2c2-118">Scenario description</span></span>
<span data-ttu-id="cc2c2-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc2c2-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="cc2c2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc2c2-121">Het toevoegen van Jitbit Helpdesk van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="cc2c2-121">Adding Jitbit Helpdesk from hello gallery</span></span>
2. <span data-ttu-id="cc2c2-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cc2c2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-hello-gallery"></a><span data-ttu-id="cc2c2-123">Het toevoegen van Jitbit Helpdesk van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="cc2c2-123">Adding Jitbit Helpdesk from hello gallery</span></span>
<span data-ttu-id="cc2c2-124">tooconfigure hello integratie van Jitbit Helpdesk in Azure AD, moet u tooadd Jitbit Helpdesk uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-124">tooconfigure hello integration of Jitbit Helpdesk into Azure AD, you need tooadd Jitbit Helpdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cc2c2-125">**tooadd Jitbit Helpdesk via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cc2c2-125">**tooadd Jitbit Helpdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc2c2-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cc2c2-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cc2c2-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="cc2c2-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="cc2c2-133">Typ in het zoekvak Hallo **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-133">In hello search box, type **Jitbit Helpdesk**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="cc2c2-135">Selecteer in het deelvenster resultaten hello, **Jitbit Helpdesk**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-135">In hello results panel, select **Jitbit Helpdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cc2c2-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cc2c2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cc2c2-138">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Jitbit Helpdesk op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cc2c2-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Jitbit Helpdesk is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jitbit Helpdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="cc2c2-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Jitbit Helpdesk toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-140">In other words, a link relationship between an Azure AD user and hello related user in Jitbit Helpdesk needs toobe established.</span></span>

<span data-ttu-id="cc2c2-141">In Jitbit Helpdesk, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-141">In Jitbit Helpdesk, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cc2c2-142">tooconfigure en eenmalige aanmelding Azure AD-test met Jitbit Helpdesk, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc2c2-142">tooconfigure and test Azure AD single sign-on with Jitbit Helpdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cc2c2-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cc2c2-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cc2c2-145">**[Maken van een testgebruiker Jitbit Helpdesk](#creating-a-jitbit-helpdesk-test-user)**  -toohave een equivalent van Britta Simon in Jitbit Helpdesk die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - toohave a counterpart of Britta Simon in Jitbit Helpdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cc2c2-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cc2c2-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cc2c2-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="cc2c2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cc2c2-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="cc2c2-150">**Voer tooconfigure Azure AD eenmalige aanmelding met de Jitbit Helpdesk, Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cc2c2-150">**tooconfigure Azure AD single sign-on with Jitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc2c2-151">In de Azure-portal op Hallo Hallo **Jitbit Helpdesk** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-151">In hello Azure portal, on hello **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="cc2c2-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="cc2c2-155">Op Hallo **Jitbit Helpdesk domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc2c2-155">On hello **Jitbit Helpdesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="cc2c2-157">a.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-157">a.</span></span> <span data-ttu-id="cc2c2-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="cc2c2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="cc2c2-159">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-159">This value is not real.</span></span> <span data-ttu-id="cc2c2-160">Deze waarde bijwerken Hello werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-160">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="cc2c2-161">Neem contact op met [Jitbit Helpdesk Client ondersteuningsteam](https://www.jitbit.com/support/) tooget deze waarde.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) tooget this value.</span></span> 
    
    <span data-ttu-id="cc2c2-162">b.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-162">b.</span></span>  <span data-ttu-id="cc2c2-163">In Hallo **id** textbox, typ een URL als volgt:`https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="cc2c2-163">In hello **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="cc2c2-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="cc2c2-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cc2c2-168">Op Hallo **Jitbit Helpdesk configuratie** sectie, klikt u op **configureren Jitbit Helpdesk** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-168">On hello **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cc2c2-169">Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="cc2c2-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="cc2c2-171">In een ander browservenster, meld u bij uw bedrijf Jitbit Helpdesk site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="cc2c2-172">Klik in de werkbalk bovenaan Hallo Hallo op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-172">In hello toolbar on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="cc2c2-173">![Beheer](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="cc2c2-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="cc2c2-174">Klik op **algemene instellingen**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="cc2c2-175">![Gebruikers, bedrijven en machtigingen](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "gebruikers, bedrijven en machtigingen")</span><span class="sxs-lookup"><span data-stu-id="cc2c2-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="cc2c2-176">In Hallo **verificatie-instellingen** configuratie sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc2c2-176">In hello **Authentication settings** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="cc2c2-177">![Verificatie-instellingen](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "verificatie-instellingen")</span><span class="sxs-lookup"><span data-stu-id="cc2c2-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="cc2c2-178">a.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-178">a.</span></span> <span data-ttu-id="cc2c2-179">Selecteer **inschakelen-SAML één 2.0 aanmelden**, toosign in het gebruik van eenmalige aanmelding (SSO), met **OneLogin**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-179">Select **Enable SAML 2.0 single sign on**, toosign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="cc2c2-180">b.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-180">b.</span></span> <span data-ttu-id="cc2c2-181">In Hallo **eindpunt-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-181">In hello **EndPoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cc2c2-182">c.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-182">c.</span></span> <span data-ttu-id="cc2c2-183">Open uw **base 64-** gecodeerd certificaat in Kladblok en kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **X.509-certificaat** tekstvak</span><span class="sxs-lookup"><span data-stu-id="cc2c2-183">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="cc2c2-184">d.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-184">d.</span></span> <span data-ttu-id="cc2c2-185">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="cc2c2-186">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cc2c2-187">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cc2c2-188">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cc2c2-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cc2c2-189">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="cc2c2-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="cc2c2-190">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="cc2c2-192">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cc2c2-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc2c2-193">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cc2c2-195">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cc2c2-197">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cc2c2-199">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="cc2c2-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cc2c2-201">a.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-201">a.</span></span> <span data-ttu-id="cc2c2-202">In Hallo **naam** textbox typenaam als **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-202">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="cc2c2-203">b.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-203">b.</span></span> <span data-ttu-id="cc2c2-204">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cc2c2-205">c.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-205">c.</span></span> <span data-ttu-id="cc2c2-206">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cc2c2-207">d.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-207">d.</span></span> <span data-ttu-id="cc2c2-208">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="cc2c2-209">Maken van een testgebruiker Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="cc2c2-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="cc2c2-210">In de volgorde tooenable Azure AD gebruikers toolog in Jitbit Helpdesk, moeten ze worden ingericht in Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-210">In order tooenable Azure AD users toolog into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="cc2c2-211">In geval van Jitbit Helpdesk Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-211">In hello case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="cc2c2-212">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cc2c2-212">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc2c2-213">Meld u bij tooyour **Jitbit Helpdesk** tenant.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-213">Log in tooyour **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="cc2c2-214">Klik in het menu bovenaan Hallo Hallo **beheer**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-214">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="cc2c2-215">![Beheer](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="cc2c2-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="cc2c2-216">Klik op **gebruikers, bedrijven en machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="cc2c2-217">![Gebruikers, bedrijven en machtigingen](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "gebruikers, bedrijven en machtigingen")</span><span class="sxs-lookup"><span data-stu-id="cc2c2-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="cc2c2-218">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="cc2c2-219">![Gebruiker toevoegen](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="cc2c2-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="cc2c2-220">Typ in de sectie maken Hallo, Hallo-gegevens van hello Azure AD-account dat u wilt dat tooprovision als volgt:</span><span class="sxs-lookup"><span data-stu-id="cc2c2-220">In hello Create section, type hello data of hello Azure AD account you want tooprovision as follows:</span></span>

    <span data-ttu-id="cc2c2-221">![Maak](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "maken")</span><span class="sxs-lookup"><span data-stu-id="cc2c2-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="cc2c2-222">a.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-222">a.</span></span> <span data-ttu-id="cc2c2-223">In Hallo **gebruikersnaam** textbox type **BrittaSimon**, de gebruikersnaam Hallo zoals hello Azure-portal in.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-223">In hello **Username** textbox, type **BrittaSimon**, hello user name as in hello Azure portal.</span></span>

   <span data-ttu-id="cc2c2-224">b.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-224">b.</span></span> <span data-ttu-id="cc2c2-225">In Hallo **e** textbox type e-mailadres van de gebruiker hello, zoals  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="cc2c2-225">In hello **Email** textbox, type email of hello user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="cc2c2-226">c.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-226">c.</span></span> <span data-ttu-id="cc2c2-227">In Hallo **voornaam** textbox type voornaam van de gebruiker Hallo zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-227">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>

   <span data-ttu-id="cc2c2-228">d.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-228">d.</span></span> <span data-ttu-id="cc2c2-229">In Hallo **achternaam** textbox type achternaam van de gebruiker Hallo zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-229">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span>
   
   <span data-ttu-id="cc2c2-230">e.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-230">e.</span></span> <span data-ttu-id="cc2c2-231">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="cc2c2-232">U kunt andere Jitbit Helpdesk gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Jitbit Helpdesk tooprovision Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk tooprovision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cc2c2-233">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc2c2-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cc2c2-234">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooJitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJitbit Helpdesk.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="cc2c2-236">**tooassign Britta Simon tooJitbit Helpdesk, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="cc2c2-236">**tooassign Britta Simon tooJitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc2c2-237">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="cc2c2-239">Selecteer in de lijst met de toepassingen van Hallo **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-239">In hello applications list, select **Jitbit Helpdesk**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="cc2c2-241">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="cc2c2-243">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-243">Click **Add** button.</span></span> <span data-ttu-id="cc2c2-244">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="cc2c2-246">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cc2c2-247">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cc2c2-248">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cc2c2-249">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="cc2c2-249">Testing single sign-on</span></span>

<span data-ttu-id="cc2c2-250">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cc2c2-251">Als u op Hallo Jitbit Helpdesk-tegel in Hallo Toegangsvenster, krijgt u de aanmeldingspagina van Jitbit Helpdesk-toepassing.</span><span class="sxs-lookup"><span data-stu-id="cc2c2-251">When you click hello Jitbit Helpdesk tile in hello Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="cc2c2-252">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cc2c2-252">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cc2c2-253">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="cc2c2-253">Additional resources</span></span>

* [<span data-ttu-id="cc2c2-254">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc2c2-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc2c2-255">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cc2c2-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

