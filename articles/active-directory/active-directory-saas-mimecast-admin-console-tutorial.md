---
title: 'Zelfstudie: Azure Active Directory-integratie met Mimecast-beheerconsole | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Mimecast-beheerconsole.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 5a04a5abd9ff30d484bce0a5c97a1d3e48b69e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="fe44f-103">Zelfstudie: Azure Active Directory-integratie met Mimecast-beheerconsole</span><span class="sxs-lookup"><span data-stu-id="fe44f-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="fe44f-104">In deze zelfstudie leert u hoe toointegrate Mimecast-beheerconsole met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fe44f-104">In this tutorial, you learn how toointegrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fe44f-105">Beheerconsole Mimecast integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="fe44f-105">Integrating Mimecast Admin Console with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fe44f-106">U kunt beheren in Azure AD wie toegang tot tooMimecast-beheerconsole heeft.</span><span class="sxs-lookup"><span data-stu-id="fe44f-106">You can control in Azure AD who has access tooMimecast Admin Console.</span></span>
- <span data-ttu-id="fe44f-107">U kunt uw gebruikers tooautomatically get aangemelde tooMimecast-beheerconsole (Single Sign-On) inschakelen met hun Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="fe44f-107">You can enable your users tooautomatically get signed-on tooMimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fe44f-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="fe44f-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="fe44f-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fe44f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe44f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fe44f-110">Prerequisites</span></span>

<span data-ttu-id="fe44f-111">tooconfigure Azure AD-integratie met Mimecast-beheerconsole, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="fe44f-111">tooconfigure Azure AD integration with Mimecast Admin Console, you need hello following items:</span></span>

- <span data-ttu-id="fe44f-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="fe44f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fe44f-113">Een beheerconsole Mimecast eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="fe44f-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fe44f-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="fe44f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fe44f-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="fe44f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fe44f-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="fe44f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fe44f-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fe44f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fe44f-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="fe44f-118">Scenario description</span></span>
<span data-ttu-id="fe44f-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="fe44f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fe44f-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="fe44f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fe44f-121">Het toevoegen van Mimecast-beheerconsole van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="fe44f-121">Adding Mimecast Admin Console from hello gallery</span></span>
2. <span data-ttu-id="fe44f-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fe44f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-hello-gallery"></a><span data-ttu-id="fe44f-123">Het toevoegen van Mimecast-beheerconsole van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="fe44f-123">Adding Mimecast Admin Console from hello gallery</span></span>
<span data-ttu-id="fe44f-124">tooconfigure hello integratie van Mimecast-beheerconsole in Azure AD, moet u tooadd Mimecast-beheerconsole uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="fe44f-124">tooconfigure hello integration of Mimecast Admin Console into Azure AD, you need tooadd Mimecast Admin Console from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fe44f-125">**tooadd Mimecast-beheerconsole uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fe44f-125">**tooadd Mimecast Admin Console from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe44f-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="fe44f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="fe44f-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fe44f-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="fe44f-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fe44f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="fe44f-133">Typ in het zoekvak Hallo **Mimecast-beheerconsole**, selecteer **Mimecast-beheerconsole** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fe44f-133">In hello search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Mimecast-beheerconsole in de lijst met resultaten Hallo](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fe44f-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe44f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fe44f-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Mimecast-beheerconsole op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="fe44f-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fe44f-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de beheerconsole Mimecast is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe44f-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Admin Console is tooa user in Azure AD.</span></span> <span data-ttu-id="fe44f-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de beheerconsole Mimecast Hallo toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="fe44f-138">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Admin Console needs toobe established.</span></span>

<span data-ttu-id="fe44f-139">In de beheerconsole Mimecast, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="fe44f-139">In Mimecast Admin Console, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fe44f-140">tooconfigure en eenmalige aanmelding Azure AD-test met Mimecast-beheerconsole, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fe44f-140">tooconfigure and test Azure AD single sign-on with Mimecast Admin Console, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fe44f-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="fe44f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fe44f-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fe44f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fe44f-143">**[Maak een testgebruiker beheerconsole Mimecast](#create-a-mimecast-admin-console-test-user)**  -toohave een equivalent van Britta Simon in Mimecast-beheerconsole die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="fe44f-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - toohave a counterpart of Britta Simon in Mimecast Admin Console that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fe44f-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="fe44f-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fe44f-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="fe44f-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fe44f-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="fe44f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fe44f-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Mimecast-beheerconsole.</span><span class="sxs-lookup"><span data-stu-id="fe44f-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="fe44f-148">**tooconfigure eenmalige aanmelding Azure AD met Mimecast-beheerconsole voert Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fe44f-148">**tooconfigure Azure AD single sign-on with Mimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe44f-149">In de Azure-portal op Hallo Hallo **Mimecast-beheerconsole** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-149">In hello Azure portal, on hello **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="fe44f-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="fe44f-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="fe44f-153">Op Hallo **Mimecast Admin Consoledomein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fe44f-153">On hello **Mimecast Admin Console Domain and URLs** section, perform hello following steps:</span></span>

    ![Domein Mimecast Administrator-Console en URL's van eenmalige aanmelding informatie](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="fe44f-155">In Hallo **aanmeldings-URL** textbox type Hallo URL:</span><span class="sxs-lookup"><span data-stu-id="fe44f-155">In hello **Sign-on URL** textbox, type hello URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="fe44f-156">Hallo aanmelding URL is een specifieke regio.</span><span class="sxs-lookup"><span data-stu-id="fe44f-156">hello sign on URL is region specific.</span></span>

4. <span data-ttu-id="fe44f-157">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="fe44f-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="fe44f-159">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="fe44f-159">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fe44f-161">Op Hallo **Mimecast Console beheerdersconfiguratie** sectie, klikt u op **Mimecast beheerconsole configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="fe44f-161">On hello **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fe44f-162">Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="fe44f-162">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuratie van de Console Mimecast Admin](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="fe44f-164">In een ander browservenster, meld u bij uw Mimecast-beheerconsole als beheerder.</span><span class="sxs-lookup"><span data-stu-id="fe44f-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="fe44f-165">Ga te**Services \> toepassing**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-165">Go too**Services \> Application**.</span></span>

    <span data-ttu-id="fe44f-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span><span class="sxs-lookup"><span data-stu-id="fe44f-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="fe44f-167">Klik op **verificatie profielen**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="fe44f-168">![Verificatie profielen](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "verificatie-profielen")</span><span class="sxs-lookup"><span data-stu-id="fe44f-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="fe44f-169">Klik op **nieuwe Authentication profiel**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="fe44f-170">![Nieuwe verificatie profielen](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "nieuwe verificatie-profielen")</span><span class="sxs-lookup"><span data-stu-id="fe44f-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="fe44f-171">In Hallo **Authentication profiel** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fe44f-171">In hello **Authentication Profile** section, perform hello following steps:</span></span>

    <span data-ttu-id="fe44f-172">![Authentication profiel](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication profiel")</span><span class="sxs-lookup"><span data-stu-id="fe44f-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="fe44f-173">a.</span><span class="sxs-lookup"><span data-stu-id="fe44f-173">a.</span></span> <span data-ttu-id="fe44f-174">In Hallo **beschrijving** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="fe44f-174">In hello **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="fe44f-175">b.</span><span class="sxs-lookup"><span data-stu-id="fe44f-175">b.</span></span> <span data-ttu-id="fe44f-176">Selecteer **afdwingen van SAML-verificatie voor de beheerconsole Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="fe44f-177">c.</span><span class="sxs-lookup"><span data-stu-id="fe44f-177">c.</span></span> <span data-ttu-id="fe44f-178">Als **Provider**, selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="fe44f-179">d.</span><span class="sxs-lookup"><span data-stu-id="fe44f-179">d.</span></span> <span data-ttu-id="fe44f-180">Plakken **SAML entiteit-ID**, die u hebt gekopieerd uit hello Azure-portal in Hallo **URL-verlener** textbox.</span><span class="sxs-lookup"><span data-stu-id="fe44f-180">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="fe44f-181">e.</span><span class="sxs-lookup"><span data-stu-id="fe44f-181">e.</span></span> <span data-ttu-id="fe44f-182">Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd uit hello Azure-portal in Hallo **aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="fe44f-182">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Login URL** textbox.</span></span>

    <span data-ttu-id="fe44f-183">f.</span><span class="sxs-lookup"><span data-stu-id="fe44f-183">f.</span></span> <span data-ttu-id="fe44f-184">Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd uit hello Azure-portal in Hallo **afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="fe44f-184">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="fe44f-185">Hallo zijn aanmeldings-URL-waarde en Hallo afmelding URL-waarde voor hello Mimecast-beheerconsole Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="fe44f-185">hello Login URL value and hello Logout URL value are for hello Mimecast Admin Console hello same.</span></span>
    
    <span data-ttu-id="fe44f-186">g.</span><span class="sxs-lookup"><span data-stu-id="fe44f-186">g.</span></span> <span data-ttu-id="fe44f-187">Open uw base 64-certificaat gedownload vanuit Azure-portal in Kladblok Hallo eerste regel verwijderen ('*--*') en de laatste regel hello ('*--*'), kopie Hallo resterende inhoud van deze in het Klembord en plak deze toohello **Provider identiteitscertificaat (metagegevens)** textbox.</span><span class="sxs-lookup"><span data-stu-id="fe44f-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove hello first line (“*--*“) and hello last line (“*--*“), copy hello remaining content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="fe44f-188">h.</span><span class="sxs-lookup"><span data-stu-id="fe44f-188">h.</span></span> <span data-ttu-id="fe44f-189">Selecteer **toestaan voor eenmalige op**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="fe44f-190">ik.</span><span class="sxs-lookup"><span data-stu-id="fe44f-190">i.</span></span> <span data-ttu-id="fe44f-191">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="fe44f-192">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="fe44f-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fe44f-193">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="fe44f-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fe44f-194">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fe44f-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fe44f-195">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="fe44f-195">Create an Azure AD test user</span></span>

<span data-ttu-id="fe44f-196">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="fe44f-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="fe44f-198">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fe44f-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe44f-199">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="fe44f-199">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="fe44f-201">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-201">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="fe44f-203">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fe44f-203">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="fe44f-205">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fe44f-205">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="fe44f-207">a.</span><span class="sxs-lookup"><span data-stu-id="fe44f-207">a.</span></span> <span data-ttu-id="fe44f-208">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fe44f-209">b.</span><span class="sxs-lookup"><span data-stu-id="fe44f-209">b.</span></span> <span data-ttu-id="fe44f-210">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="fe44f-210">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="fe44f-211">c.</span><span class="sxs-lookup"><span data-stu-id="fe44f-211">c.</span></span> <span data-ttu-id="fe44f-212">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="fe44f-212">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="fe44f-213">d.</span><span class="sxs-lookup"><span data-stu-id="fe44f-213">d.</span></span> <span data-ttu-id="fe44f-214">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="fe44f-215">Maak een testgebruiker Mimecast-beheerconsole</span><span class="sxs-lookup"><span data-stu-id="fe44f-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="fe44f-216">In volgorde tooenable Azure AD gebruikers toolog in Mimecast-beheerconsole, moeten ze worden ingericht in Mimecast-beheerconsole.</span><span class="sxs-lookup"><span data-stu-id="fe44f-216">In order tooenable Azure AD users toolog into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="fe44f-217">In geval van Mimecast-beheerconsole Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="fe44f-217">In hello case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="fe44f-218">Tooregister een domein moet u voordat u gebruikers kunt maken.</span><span class="sxs-lookup"><span data-stu-id="fe44f-218">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="fe44f-219">**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fe44f-219">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe44f-220">Meld u aan bij tooyour **Mimecast-beheerconsole** als administrator.</span><span class="sxs-lookup"><span data-stu-id="fe44f-220">Sign on tooyour **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="fe44f-221">Ga te**mappen \> intern**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-221">Go too**Directories \> Internal**.</span></span>
   
   <span data-ttu-id="fe44f-222">![Mappen](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "mappen")</span><span class="sxs-lookup"><span data-stu-id="fe44f-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="fe44f-223">Klik op **nieuwe domein registreren**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="fe44f-224">![Nieuwe domein registreren](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "nieuwe domein registreren")</span><span class="sxs-lookup"><span data-stu-id="fe44f-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="fe44f-225">Nadat het nieuwe domein is gemaakt, klikt u op **nieuw adres**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="fe44f-226">![Nieuw adres](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "nieuw adres")</span><span class="sxs-lookup"><span data-stu-id="fe44f-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="fe44f-227">Uitvoeren in het nieuwe adres dialoogvenster Hallo Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fe44f-227">In hello new address dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="fe44f-228">![Sla](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "opslaan")</span><span class="sxs-lookup"><span data-stu-id="fe44f-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="fe44f-229">a.</span><span class="sxs-lookup"><span data-stu-id="fe44f-229">a.</span></span> <span data-ttu-id="fe44f-230">Type Hallo **e-mailadres**, **globale naam**, **wachtwoord**, en **wachtwoord bevestigen** kenmerken van een geldige Azure AD-account u wilt tooprovision in Hallo gerelateerd tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="fe44f-230">Type hello **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span>

   <span data-ttu-id="fe44f-231">b.</span><span class="sxs-lookup"><span data-stu-id="fe44f-231">b.</span></span> <span data-ttu-id="fe44f-232">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="fe44f-233">U kunt geen andere hulpprogramma's voor Mimecast-beheerconsole gebruiker-account maken of API's die worden geleverd door Mimecast-beheerconsole tooprovision Azure AD-gebruikersaccounts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fe44f-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console tooprovision Azure AD user accounts.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="fe44f-234">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe44f-234">Assign hello Azure AD test user</span></span>

<span data-ttu-id="fe44f-235">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooMimecast-beheerconsole.</span><span class="sxs-lookup"><span data-stu-id="fe44f-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Admin Console.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="fe44f-237">**tooassign Britta Simon tooMimecast-beheerconsole voert Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="fe44f-237">**tooassign Britta Simon tooMimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe44f-238">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="fe44f-240">Selecteer in de lijst met de toepassingen van Hallo **Mimecast-beheerconsole**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-240">In hello applications list, select **Mimecast Admin Console**.</span></span>

    ![Hallo Mimecast-beheerconsole koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="fe44f-242">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="fe44f-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="fe44f-244">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="fe44f-244">Click **Add** button.</span></span> <span data-ttu-id="fe44f-245">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fe44f-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="fe44f-247">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="fe44f-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fe44f-248">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fe44f-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fe44f-249">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fe44f-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fe44f-250">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fe44f-250">Test single sign-on</span></span>

<span data-ttu-id="fe44f-251">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="fe44f-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fe44f-252">Als u op Hallo Mimecast-beheerconsole tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Mimecast-beheerconsole toepassing.</span><span class="sxs-lookup"><span data-stu-id="fe44f-252">When you click hello Mimecast Admin Console tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Admin Console application.</span></span>
<span data-ttu-id="fe44f-253">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fe44f-253">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fe44f-254">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="fe44f-254">Additional resources</span></span>

* [<span data-ttu-id="fe44f-255">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe44f-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fe44f-256">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fe44f-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

