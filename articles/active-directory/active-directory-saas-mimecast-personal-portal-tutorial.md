---
title: 'Zelfstudie: Azure Active Directory-integratie met de persoonlijke Portal Mimecast | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en persoonlijke Mimecast-Portal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ee2a8edcab36f295732ac1ebe641ed7fcfc1f2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="fbbb8-103">Zelfstudie: Azure Active Directory-integratie met Mimecast persoonlijke Portal</span><span class="sxs-lookup"><span data-stu-id="fbbb8-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="fbbb8-104">In deze zelfstudie leert u hoe toointegrate Mimecast persoonlijke Portal met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fbbb8-104">In this tutorial, you learn how toointegrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fbbb8-105">Mimecast persoonlijke Portal integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="fbbb8-105">Integrating Mimecast Personal Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fbbb8-106">U kunt beheren in Azure AD wie toegang tot tooMimecast persoonlijke Portal heeft</span><span class="sxs-lookup"><span data-stu-id="fbbb8-106">You can control in Azure AD who has access tooMimecast Personal Portal</span></span>
- <span data-ttu-id="fbbb8-107">U kunt uw gebruikers tooautomatically get aangemelde tooMimecast persoonlijke Portal (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="fbbb8-107">You can enable your users tooautomatically get signed-on tooMimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fbbb8-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="fbbb8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fbbb8-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fbbb8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbbb8-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fbbb8-110">Prerequisites</span></span>

<span data-ttu-id="fbbb8-111">Azure AD-integratie met de persoonlijke Portal Mimecast tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="fbbb8-111">tooconfigure Azure AD integration with Mimecast Personal Portal, you need hello following items:</span></span>

- <span data-ttu-id="fbbb8-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="fbbb8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fbbb8-113">Een persoonlijke Portal Mimecast eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="fbbb8-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fbbb8-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fbbb8-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="fbbb8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fbbb8-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fbbb8-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbbb8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fbbb8-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="fbbb8-118">Scenario description</span></span>
<span data-ttu-id="fbbb8-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fbbb8-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="fbbb8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fbbb8-121">Het toevoegen van persoonlijke Portal Mimecast van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="fbbb8-121">Adding Mimecast Personal Portal from hello gallery</span></span>
2. <span data-ttu-id="fbbb8-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fbbb8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-hello-gallery"></a><span data-ttu-id="fbbb8-123">Het toevoegen van persoonlijke Portal Mimecast van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="fbbb8-123">Adding Mimecast Personal Portal from hello gallery</span></span>
<span data-ttu-id="fbbb8-124">tooconfigure hello integratie van persoonlijke Portal Mimecast in Azure AD, moet u tooadd Mimecast persoonlijke Portal uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-124">tooconfigure hello integration of Mimecast Personal Portal into Azure AD, you need tooadd Mimecast Personal Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fbbb8-125">**tooadd Mimecast persoonlijke Portal via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fbbb8-125">**tooadd Mimecast Personal Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbbb8-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fbbb8-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fbbb8-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="fbbb8-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="fbbb8-133">Typ in het zoekvak Hallo **Mimecast persoonlijke Portal**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-133">In hello search box, type **Mimecast Personal Portal**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="fbbb8-135">Selecteer in het deelvenster resultaten hello, **Mimecast persoonlijke Portal**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-135">In hello results panel, select **Mimecast Personal Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fbbb8-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fbbb8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fbbb8-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Mimecast persoonlijke Portal op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fbbb8-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Mimecast persoonlijke Portal is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Personal Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="fbbb8-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Mimecast persoonlijke Portal toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-140">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Personal Portal needs toobe established.</span></span>

<span data-ttu-id="fbbb8-141">In Mimecast persoonlijke Portal Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-141">In Mimecast Personal Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fbbb8-142">tooconfigure en test eenmalige aanmelding Azure AD met Mimecast persoonlijke Portal, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fbbb8-142">tooconfigure and test Azure AD single sign-on with Mimecast Personal Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fbbb8-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fbbb8-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fbbb8-145">**[Maken van een testgebruiker Mimecast persoonlijke Portal](#creating-a-mimecast-personal-portal-test-user)**  -toohave een equivalent van Britta Simon in Mimecast persoonlijke Portal die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - toohave a counterpart of Britta Simon in Mimecast Personal Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fbbb8-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fbbb8-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fbbb8-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="fbbb8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fbbb8-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Mimecast persoonlijke Portal configureren.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="fbbb8-150">**tooconfigure eenmalige aanmelding Azure AD met Mimecast persoonlijke Portal, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fbbb8-150">**tooconfigure Azure AD single sign-on with Mimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbbb8-151">In de Azure-portal op Hallo Hallo **Mimecast persoonlijke Portal** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-151">In hello Azure portal, on hello **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="fbbb8-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="fbbb8-155">Op Hallo **Mimecast persoonlijke Portal domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fbbb8-155">On hello **Mimecast Personal Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="fbbb8-157">a.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-157">a.</span></span> <span data-ttu-id="fbbb8-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="fbbb8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="fbbb8-159">b.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-159">b.</span></span> <span data-ttu-id="fbbb8-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="fbbb8-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="fbbb8-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-161">These values are not real.</span></span> <span data-ttu-id="fbbb8-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fbbb8-163">Neem contact op met [Mimecast persoonlijke Portal Client ondersteuningsteam](https://www.mimecast.com/customer-success/technical-support/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) tooget these values.</span></span> 
 


4. <span data-ttu-id="fbbb8-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="fbbb8-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fbbb8-168">Op Hallo **Mimecast persoonlijke Portal-configuratie** sectie, klikt u op **Mimecast persoonlijke Portal configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-168">On hello **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fbbb8-169">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="fbbb8-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="fbbb8-171">In een ander browservenster, meld u bij uw persoonlijke Mimecast-Portal als beheerder.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="fbbb8-172">Ga te**Services \> toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-172">Go too**Services \> Applications**.</span></span>
   
    <span data-ttu-id="fbbb8-173">![Toepassingen](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="fbbb8-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="fbbb8-174">Klik op **verificatie profielen**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="fbbb8-175">![Verificatie profielen](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "verificatie-profielen")</span><span class="sxs-lookup"><span data-stu-id="fbbb8-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="fbbb8-176">Klik op **nieuwe Authentication profiel**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="fbbb8-177">![Nieuwe Authentication profiel](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "nieuwe profiel voor verificatie")</span><span class="sxs-lookup"><span data-stu-id="fbbb8-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="fbbb8-178">In Hallo **Authentication profiel** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fbbb8-178">In hello **Authentication Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="fbbb8-179">![Authentication profiel](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication profiel")</span><span class="sxs-lookup"><span data-stu-id="fbbb8-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="fbbb8-180">a.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-180">a.</span></span> <span data-ttu-id="fbbb8-181">In Hallo **beschrijving** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-181">In hello **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="fbbb8-182">b.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-182">b.</span></span> <span data-ttu-id="fbbb8-183">Selecteer **afdwingen van SAML-verificatie voor Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="fbbb8-184">c.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-184">c.</span></span> <span data-ttu-id="fbbb8-185">Als **Provider**, selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="fbbb8-186">d.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-186">d.</span></span> <span data-ttu-id="fbbb8-187">In **URL-verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-187">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="fbbb8-188">e.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-188">e.</span></span> <span data-ttu-id="fbbb8-189">In **aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-189">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="fbbb8-190">f.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-190">f.</span></span> <span data-ttu-id="fbbb8-191">In **afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-191">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="fbbb8-192">g.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-192">g.</span></span> <span data-ttu-id="fbbb8-193">Open uw **base 64-** gecodeerd certificaat in Kladblok gedownload vanuit Azure-portal kopie Hallo inhoud ervan naar het Klembord en plak deze toohello **Provider identiteitscertificaat (metagegevens)** tekstvak.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="fbbb8-194">h.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-194">h.</span></span> <span data-ttu-id="fbbb8-195">Selecteer **toestaan voor eenmalige op**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="fbbb8-196">ik.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-196">i.</span></span> <span data-ttu-id="fbbb8-197">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="fbbb8-198">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fbbb8-199">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fbbb8-200">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fbbb8-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fbbb8-201">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="fbbb8-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="fbbb8-202">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="fbbb8-204">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fbbb8-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbbb8-205">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fbbb8-207">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fbbb8-209">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fbbb8-211">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fbbb8-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fbbb8-213">a.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-213">a.</span></span> <span data-ttu-id="fbbb8-214">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fbbb8-215">b.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-215">b.</span></span> <span data-ttu-id="fbbb8-216">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fbbb8-217">c.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-217">c.</span></span> <span data-ttu-id="fbbb8-218">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fbbb8-219">d.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-219">d.</span></span> <span data-ttu-id="fbbb8-220">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="fbbb8-221">Een testgebruiker Mimecast persoonlijke Portal maken</span><span class="sxs-lookup"><span data-stu-id="fbbb8-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="fbbb8-222">In volgorde tooenable Azure AD gebruikers toolog bij Mimecast persoonlijke Portal, moeten ze worden ingericht bij Mimecast persoonlijke Portal.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-222">In order tooenable Azure AD users toolog into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="fbbb8-223">In geval van persoonlijke Portal Mimecast Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-223">In hello case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="fbbb8-224">Tooregister een domein moet u voordat u gebruikers kunt maken.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-224">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="fbbb8-225">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fbbb8-225">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbbb8-226">Meld u aan bij tooyour **Mimecast persoonlijke Portal** als administrator.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-226">Sign on tooyour **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="fbbb8-227">Ga te**mappen \> intern**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-227">Go too**Directories \> Internal**.</span></span>
   
    <span data-ttu-id="fbbb8-228">![Mappen](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "mappen")</span><span class="sxs-lookup"><span data-stu-id="fbbb8-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="fbbb8-229">Klik op **nieuwe domein registreren**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="fbbb8-230">![Nieuwe domein registreren](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "nieuwe domein registreren")</span><span class="sxs-lookup"><span data-stu-id="fbbb8-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="fbbb8-231">Nadat het nieuwe domein is gemaakt, klikt u op **nieuw adres**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="fbbb8-232">![Nieuw adres](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "nieuw adres")</span><span class="sxs-lookup"><span data-stu-id="fbbb8-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="fbbb8-233">Uitvoeren in het nieuwe adres dialoogvenster Hallo Hallo stappen uit te voeren van een geldig Azure AD-account die u wilt dat tooprovision:</span><span class="sxs-lookup"><span data-stu-id="fbbb8-233">In hello new address dialog, perform hello following steps of a valid Azure AD account you want tooprovision:</span></span>
   
    <span data-ttu-id="fbbb8-234">![Sla](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "opslaan")</span><span class="sxs-lookup"><span data-stu-id="fbbb8-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="fbbb8-235">a.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-235">a.</span></span> <span data-ttu-id="fbbb8-236">In Hallo **e-mailadres** textbox type **e-mailadres** van Hallo gebruiker als  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="fbbb8-236">In hello **Email Address** textbox, type **Email Address** of hello user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="fbbb8-237">b.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-237">b.</span></span> <span data-ttu-id="fbbb8-238">In Hallo **globale naam** textbox type Hallo **gebruikersnaam** als **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-238">In hello **Global Name** textbox, type hello **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="fbbb8-239">c.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-239">c.</span></span> <span data-ttu-id="fbbb8-240">In Hallo **wachtwoord**, en **wachtwoord bevestigen** tekstvakken, type Hallo **wachtwoord** van Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-240">In hello **Password**, and **Confirm Password** textboxes, type hello **Password** of hello user.</span></span>
   
    <span data-ttu-id="fbbb8-241">b.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-241">b.</span></span> <span data-ttu-id="fbbb8-242">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="fbbb8-243">U kunt geen andere hulpprogramma's voor persoonlijke Portal Mimecast gebruiker-account maken of API's die worden geleverd door Mimecast persoonlijke Portal tooprovision Azure AD-gebruikersaccounts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fbbb8-244">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbbb8-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fbbb8-245">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooMimecast persoonlijke Portal.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Personal Portal.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="fbbb8-247">**tooassign Britta Simon tooMimecast persoonlijke Portal uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fbbb8-247">**tooassign Britta Simon tooMimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbbb8-248">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="fbbb8-250">Selecteer in de lijst met de toepassingen van Hallo **Mimecast persoonlijke Portal**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-250">In hello applications list, select **Mimecast Personal Portal**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="fbbb8-252">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="fbbb8-254">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-254">Click **Add** button.</span></span> <span data-ttu-id="fbbb8-255">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="fbbb8-257">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fbbb8-258">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fbbb8-259">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fbbb8-260">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fbbb8-260">Testing single sign-on</span></span>
<span data-ttu-id="fbbb8-261">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fbbb8-262">Als u op Hallo Mimecast persoonlijke Portal-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Mimecast persoonlijke Portal-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fbbb8-262">When you click hello Mimecast Personal Portal tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Personal Portal application.</span></span> <span data-ttu-id="fbbb8-263">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fbbb8-263">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fbbb8-264">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="fbbb8-264">Additional resources</span></span>

* [<span data-ttu-id="fbbb8-265">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbbb8-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fbbb8-266">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fbbb8-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

