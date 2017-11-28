---
title: 'Zelfstudie: Azure Active Directory-integratie met MOVEit overdracht - Azure AD-integratie | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en MOVEit overdracht - Azure AD-integratie.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="f7498-103">Zelfstudie: Azure Active Directory-integratie met MOVEit overdracht - Azure AD-integratie</span><span class="sxs-lookup"><span data-stu-id="f7498-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="f7498-104">In deze zelfstudie leert u hoe toointegrate MOVEit overdracht - Azure AD-integratie met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f7498-104">In this tutorial, you learn how toointegrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f7498-105">Integratie van MOVEit overdracht - Azure AD-integratie met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f7498-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f7498-106">U kunt beheren in Azure AD wie toegang tot tooMOVEit overdracht - Azure AD-integratie heeft.</span><span class="sxs-lookup"><span data-stu-id="f7498-106">You can control in Azure AD who has access tooMOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="f7498-107">U kunt uw gebruikers tooautomatically get aangemelde tooMOVEit overdracht - Azure AD-integratie met hun Azure AD-accounts (Single Sign-On) inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f7498-107">You can enable your users tooautomatically get signed-on tooMOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f7498-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="f7498-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="f7498-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f7498-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7498-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f7498-110">Prerequisites</span></span>

<span data-ttu-id="f7498-111">tooconfigure Azure AD-integratie met MOVEit overdracht - integratie van Azure AD, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="f7498-111">tooconfigure Azure AD integration with MOVEit Transfer - Azure AD integration, you need hello following items:</span></span>

- <span data-ttu-id="f7498-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f7498-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f7498-113">De overdracht van een MOVEit - Azure AD-integratie eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f7498-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f7498-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f7498-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f7498-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f7498-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f7498-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f7498-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f7498-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f7498-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f7498-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f7498-118">Scenario description</span></span>
<span data-ttu-id="f7498-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f7498-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f7498-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f7498-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f7498-121">MOVEit overdracht - Azure AD-integratie uit Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f7498-121">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
2. <span data-ttu-id="f7498-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f7498-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a><span data-ttu-id="f7498-123">MOVEit overdracht - Azure AD-integratie uit Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f7498-123">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
<span data-ttu-id="f7498-124">tooconfigure hello integratie van MOVEit overdracht - Azure AD-integratie met Azure AD, moet u tooadd MOVEit overdracht - Azure AD-integratie in Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f7498-124">tooconfigure hello integration of MOVEit Transfer - Azure AD integration into Azure AD, you need tooadd MOVEit Transfer - Azure AD integration from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f7498-125">**tooadd MOVEit overdracht - Azure AD-integratie uit de galerie hello, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f7498-125">**tooadd MOVEit Transfer - Azure AD integration from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7498-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f7498-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="f7498-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f7498-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f7498-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f7498-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="f7498-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f7498-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="f7498-133">Typ in het zoekvak Hallo **MOVEit overdracht - Azure AD-integratie**, selecteer **MOVEit overdracht - Azure AD-integratie** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f7498-133">In hello search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Overdracht van MOVEit - Azure AD-integratie in de lijst met resultaten Hallo](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f7498-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7498-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f7498-136">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met MOVEit overdracht - Azure AD-integratie op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f7498-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f7498-137">Azure AD moet tooknow welke gebruiker Hallo equivalent in overdrachts-MOVEit voor eenmalige aanmelding toowork - Azure AD-integratie is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f7498-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MOVEit Transfer - Azure AD integration is tooa user in Azure AD.</span></span> <span data-ttu-id="f7498-138">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in overdrachts-MOVEit - moet Azure AD-integratie toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="f7498-138">In other words, a link relationship between an Azure AD user and hello related user in MOVEit Transfer - Azure AD integration needs toobe established.</span></span>

<span data-ttu-id="f7498-139">In MOVEit overdrachts - Azure AD-integratie Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="f7498-139">In MOVEit Transfer - Azure AD integration, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f7498-140">tooconfigure en eenmalige aanmelding Azure AD-test met MOVEit overdracht - integratie van Azure AD, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f7498-140">tooconfigure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f7498-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="f7498-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f7498-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f7498-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f7498-143">**[Maken van een overdracht MOVEit - Azure AD-integratie testgebruiker](#create-a-moveit-transfer---azure-ad-integration-test-user)**  - toohave een equivalent van Britta Simon in overdrachts-MOVEit - Azure AD-integratie die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f7498-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - toohave a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f7498-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f7498-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f7498-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f7498-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f7498-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f7498-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f7498-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in de overdracht van uw MOVEit - toepassing voor Azure AD-integratie.</span><span class="sxs-lookup"><span data-stu-id="f7498-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="f7498-148">**Voer tooconfigure Azure AD eenmalige aanmelding met MOVEit overdracht - Azure AD-integratie Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f7498-148">**tooconfigure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7498-149">In Azure-portal op Hallo Hallo **MOVEit overdracht - Azure AD-integratie** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f7498-149">In hello Azure portal, on hello **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f7498-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f7498-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="f7498-153">Op Hallo **MOVEit overdracht - URL's en Azure AD-integratie domein** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f7498-153">On hello **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="f7498-155">a.</span><span class="sxs-lookup"><span data-stu-id="f7498-155">a.</span></span> <span data-ttu-id="f7498-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://contoso.com`</span><span class="sxs-lookup"><span data-stu-id="f7498-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="f7498-157">b.</span><span class="sxs-lookup"><span data-stu-id="f7498-157">b.</span></span> <span data-ttu-id="f7498-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="f7498-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="f7498-159">c.</span><span class="sxs-lookup"><span data-stu-id="f7498-159">c.</span></span> <span data-ttu-id="f7498-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="f7498-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="f7498-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="f7498-161">These values are not real.</span></span> <span data-ttu-id="f7498-162">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="f7498-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="f7498-163">U kunt deze waarden later in verwijzen **metagegevens-URL voor Service Provider** sectie of neem contact op met [MOVEit overdracht - ondersteuningsteam van Azure AD-integratie Client](https://community.ipswitch.com/s/support) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="f7498-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) tooget these values.</span></span>

4. <span data-ttu-id="f7498-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f7498-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="f7498-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f7498-166">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="f7498-168">Meld u aan op tooyour MOVEit overdracht tenant als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f7498-168">Sign on tooyour MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="f7498-169">Klik op Hallo navigatiedeelvenster links **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="f7498-169">On hello left navigation pane, click **Settings**.</span></span>

    ![Instellingen sectie op App aan clientzijde](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="f7498-171">Klik op **eenmalige aanmelding** koppeling, die zich onder **beveiligingsbeleid-gebruikersverificatie >**.</span><span class="sxs-lookup"><span data-stu-id="f7498-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![Security-beleid op App aan clientzijde](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="f7498-173">Klik op Hallo metagegevens-URL koppeling toodownload hello metagegevensdocument.</span><span class="sxs-lookup"><span data-stu-id="f7498-173">Click hello Metadata URL link toodownload hello metadata document.</span></span>

    ![Serviceprovider metagegevens-URL](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="f7498-175">Controleer of **id van de entiteit** overeenkomt met **id** in Hallo **MOVEit overdracht - URL's en Azure AD-integratie domein** sectie.</span><span class="sxs-lookup"><span data-stu-id="f7498-175">Verify **entityID** matches **Identifier** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="f7498-176">Controleer of **AssertionConsumerService** locatie-URL overeenkomt met **antwoord-URL** in Hallo **MOVEit overdracht - URL's en Azure AD-integratie domein** sectie.</span><span class="sxs-lookup"><span data-stu-id="f7498-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="f7498-178">Klik op **identiteitsprovider toevoegen** tooadd knop een nieuwe federatieve id-Provider.</span><span class="sxs-lookup"><span data-stu-id="f7498-178">Click **Add Identity Provider** button tooadd a new Federated Identity Provider.</span></span>

    ![ID-Provider toevoegen](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="f7498-180">Klik op **bladeren...**  tooselect Hallo metagegevensbestand dat u hebt gedownload van Azure-portal en klik vervolgens op **identiteitsprovider toevoegen** tooupload Hallo bestand hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="f7498-180">Click **Browse...** tooselect hello metadata file which you downloaded from Azure portal, then click **Add Identity Provider** tooupload hello downloaded file.</span></span>

    ![SAML-identiteitsprovider](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="f7498-182">Selecteer "**Ja**' als **ingeschakeld** in Hallo **federatieve identiteit Providerinstellingen bewerken...**  pagina en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f7498-182">Select "**Yes**" as **Enabled** in hello **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![Federatieve identiteiten Providerinstellingen](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="f7498-184">In Hallo **bewerken federatieve identiteit Provider gebruikersinstellingen** pagina, voert u Hallo van de volgende activiteiten:</span><span class="sxs-lookup"><span data-stu-id="f7498-184">In hello **Edit Federated Identity Provider User Settings** page, perform hello following actions:</span></span>
    
    ![Federatieve identiteiten Providerinstellingen bewerken](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="f7498-186">a.</span><span class="sxs-lookup"><span data-stu-id="f7498-186">a.</span></span> <span data-ttu-id="f7498-187">Selecteer **SAML NameID** als **aanmeldingsnaam**.</span><span class="sxs-lookup"><span data-stu-id="f7498-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="f7498-188">b.</span><span class="sxs-lookup"><span data-stu-id="f7498-188">b.</span></span> <span data-ttu-id="f7498-189">Selecteer **andere** als **volledige naam** en in Hallo **kenmerknaam** textbox plaatsen Hallo-waarde: `http://schemas.microsoft.com/identity/claims/displayname`.</span><span class="sxs-lookup"><span data-stu-id="f7498-189">Select **Other** as **Full name** and in hello **Attribute name** textbox put hello value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="f7498-190">c.</span><span class="sxs-lookup"><span data-stu-id="f7498-190">c.</span></span> <span data-ttu-id="f7498-191">Selecteer **andere** als **e** en in Hallo **kenmerknaam** textbox plaatsen Hallo-waarde: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="f7498-191">Select **Other** as **Email** and in hello **Attribute name** textbox put hello value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="f7498-192">d.</span><span class="sxs-lookup"><span data-stu-id="f7498-192">d.</span></span> <span data-ttu-id="f7498-193">Selecteer **Ja** als **automatisch maken van account aanmeldt**.</span><span class="sxs-lookup"><span data-stu-id="f7498-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="f7498-194">e.</span><span class="sxs-lookup"><span data-stu-id="f7498-194">e.</span></span> <span data-ttu-id="f7498-195">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f7498-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="f7498-196">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="f7498-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f7498-197">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="f7498-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f7498-198">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f7498-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f7498-199">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f7498-199">Create an Azure AD test user</span></span>

<span data-ttu-id="f7498-200">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f7498-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="f7498-202">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="f7498-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7498-203">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="f7498-203">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f7498-205">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f7498-205">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f7498-207">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f7498-207">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f7498-209">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f7498-209">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f7498-211">a.</span><span class="sxs-lookup"><span data-stu-id="f7498-211">a.</span></span> <span data-ttu-id="f7498-212">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f7498-212">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f7498-213">b.</span><span class="sxs-lookup"><span data-stu-id="f7498-213">b.</span></span> <span data-ttu-id="f7498-214">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="f7498-214">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="f7498-215">c.</span><span class="sxs-lookup"><span data-stu-id="f7498-215">c.</span></span> <span data-ttu-id="f7498-216">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="f7498-216">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="f7498-217">d.</span><span class="sxs-lookup"><span data-stu-id="f7498-217">d.</span></span> <span data-ttu-id="f7498-218">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f7498-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="f7498-219">Een MOVEit Transfer - Azure AD-integratie testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f7498-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="f7498-220">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in MOVEit overdracht - Azure AD-integratie van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f7498-220">hello objective of this section is toocreate a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="f7498-221">Overdracht van MOVEit - Azure AD-integratie ondersteunt just-in-time-inrichting, die u hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f7498-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="f7498-222">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="f7498-222">There is no action item for you in this section.</span></span> <span data-ttu-id="f7498-223">Een nieuwe gebruiker is gemaakt tijdens een poging tooaccess MOVEit overdracht - Azure AD-integratie als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="f7498-223">A new user is created during an attempt tooaccess MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="f7498-224">Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello [MOVEit overdracht - ondersteuningsteam van Azure AD-integratie Client](https://community.ipswitch.com/s/support).</span><span class="sxs-lookup"><span data-stu-id="f7498-224">If you need toocreate a user manually, you need toocontact hello [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="f7498-225">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7498-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="f7498-226">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooMOVEit overdracht - Azure AD-integratie.</span><span class="sxs-lookup"><span data-stu-id="f7498-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMOVEit Transfer - Azure AD integration.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="f7498-228">**tooassign Britta Simon tooMOVEit overdracht - Azure AD-integratie Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f7498-228">**tooassign Britta Simon tooMOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7498-229">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f7498-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f7498-231">Selecteer in de lijst met de toepassingen van Hallo **MOVEit overdracht - Azure AD-integratie**.</span><span class="sxs-lookup"><span data-stu-id="f7498-231">In hello applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![Hallo MOVEit overdracht - Azure AD-integratie koppelen in de lijst met Hallo-toepassingen](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="f7498-233">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f7498-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="f7498-235">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f7498-235">Click **Add** button.</span></span> <span data-ttu-id="f7498-236">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f7498-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="f7498-238">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="f7498-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f7498-239">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f7498-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f7498-240">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f7498-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f7498-241">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f7498-241">Test single sign-on</span></span>

<span data-ttu-id="f7498-242">Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="f7498-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="f7498-243">Wanneer u klikt op Hallo MOVEit overdracht - tegel van Azure AD-integratie in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour MOVEit overdracht - toepassing voor Azure AD-integratie.</span><span class="sxs-lookup"><span data-stu-id="f7498-243">When you click hello MOVEit Transfer - Azure AD integration tile in hello Access Panel, you should get automatically signed-on tooyour MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f7498-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f7498-244">Additional resources</span></span>

* [<span data-ttu-id="f7498-245">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f7498-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f7498-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f7498-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

