---
title: 'Zelfstudie: Azure Active Directory-integratie met TOPdesk - openbare | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en TOPdesk - openbaar.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ef0dd06157ecc3b33814590039f5cbae64e8c916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="672df-103">Zelfstudie: Azure Active Directory-integratie met TOPdesk - openbare</span><span class="sxs-lookup"><span data-stu-id="672df-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="672df-104">In deze zelfstudie leert u hoe toointegrate TOPdesk - openbare met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="672df-104">In this tutorial, you learn how toointegrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="672df-105">Integratie van TOPdesk - openbare met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="672df-105">Integrating TOPdesk - Public with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="672df-106">U kunt beheren in Azure AD die toegang tooTOPdesk - openbaar is.</span><span class="sxs-lookup"><span data-stu-id="672df-106">You can control in Azure AD who has access tooTOPdesk - Public.</span></span>
- <span data-ttu-id="672df-107">U kunt uw gebruikers tooautomatically get aangemelde tooTOPdesk - openbare (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="672df-107">You can enable your users tooautomatically get signed-on tooTOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="672df-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="672df-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="672df-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="672df-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="672df-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="672df-110">Prerequisites</span></span>

<span data-ttu-id="672df-111">Azure AD-integratie met TOPdesk - tooconfigure openbaar, moet u de volgende items Hallo:</span><span class="sxs-lookup"><span data-stu-id="672df-111">tooconfigure Azure AD integration with TOPdesk - Public, you need hello following items:</span></span>

- <span data-ttu-id="672df-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="672df-112">An Azure AD subscription</span></span>
- <span data-ttu-id="672df-113">Een TOPdesk - openbare eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="672df-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="672df-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="672df-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="672df-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="672df-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="672df-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="672df-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="672df-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="672df-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="672df-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="672df-118">Scenario description</span></span>
<span data-ttu-id="672df-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="672df-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="672df-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="672df-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="672df-121">TOPdesk - openbare uit Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="672df-121">Adding TOPdesk - Public from hello gallery</span></span>
2. <span data-ttu-id="672df-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="672df-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-hello-gallery"></a><span data-ttu-id="672df-123">TOPdesk - openbare uit Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="672df-123">Adding TOPdesk - Public from hello gallery</span></span>
<span data-ttu-id="672df-124">tooconfigure hello integratie van TOPdesk - openbare in Azure AD, moet u tooadd TOPdesk - openbare uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="672df-124">tooconfigure hello integration of TOPdesk - Public into Azure AD, you need tooadd TOPdesk - Public from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="672df-125">**tooadd TOPdesk - openbare via Hallo gallery Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="672df-125">**tooadd TOPdesk - Public from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="672df-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="672df-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory-knop][1]

2. <span data-ttu-id="672df-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="672df-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="672df-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="672df-129">Then go too**All applications**.</span></span>

    ![Hallo Enterprise toepassingen blade][2]
    
3. <span data-ttu-id="672df-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="672df-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![knop voor nieuwe toepassing Hello][3]

4. <span data-ttu-id="672df-133">Typ in het zoekvak Hallo **TOPdesk - openbare**, selecteer **TOPdesk - openbare** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="672df-133">In hello search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lijst met zoekresultaten TOPdesk - openbare in Hallo](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="672df-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="672df-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="672df-136">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met TOPdesk - openbare op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="672df-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="672df-137">Azure AD moet tooknow welke gebruiker van het bijbehorende equivalent Hallo in TOPdesk voor eenmalige aanmelding toowork - openbaar is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="672df-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TOPdesk - Public is tooa user in Azure AD.</span></span> <span data-ttu-id="672df-138">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in TOPdesk - moet openbaar toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="672df-138">In other words, a link relationship between an Azure AD user and hello related user in TOPdesk - Public needs toobe established.</span></span>

<span data-ttu-id="672df-139">In TOPdesk - Public worden toegekend aanwijzen Hallo waarde Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="672df-139">In TOPdesk - Public, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="672df-140">tooconfigure en Azure AD eenmalige aanmelding met TOPdesk - openbare testen, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="672df-140">tooconfigure and test Azure AD single sign-on with TOPdesk - Public, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="672df-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="672df-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="672df-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="672df-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="672df-143">**[Maken van een TOPdesk - openbare testgebruiker](#create-a-topdesk---public-test-user)**  - toohave een equivalent van Britta Simon in TOPdesk - openbare die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="672df-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - toohave a counterpart of Britta Simon in TOPdesk - Public that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="672df-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="672df-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="672df-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="672df-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="672df-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="672df-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="672df-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw TOPdesk - openbare toepassing configureren.</span><span class="sxs-lookup"><span data-stu-id="672df-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="672df-148">**tooconfigure eenmalige aanmelding Azure AD met TOPdesk - openbaar, Hallo volgende stappen uit te voeren:**</span><span class="sxs-lookup"><span data-stu-id="672df-148">**tooconfigure Azure AD single sign-on with TOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="672df-149">In de Azure-portal op Hallo Hallo **TOPdesk - openbare** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="672df-149">In hello Azure portal, on hello **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="672df-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="672df-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. <span data-ttu-id="672df-153">Op Hallo **TOPdesk - URL's en openbare domein** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="672df-153">On hello **TOPdesk - Public Domain and URLs** section, perform hello following steps:</span></span>

    ![TOPdesk - URL's en openbare domein eenmalige aanmelding informatie](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="672df-155">a.</span><span class="sxs-lookup"><span data-stu-id="672df-155">a.</span></span> <span data-ttu-id="672df-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.topdesk.net`</span><span class="sxs-lookup"><span data-stu-id="672df-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="672df-157">b.</span><span class="sxs-lookup"><span data-stu-id="672df-157">b.</span></span> <span data-ttu-id="672df-158">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.topdesk.net/tas/public/login/verify`</span><span class="sxs-lookup"><span data-stu-id="672df-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="672df-159">c.</span><span class="sxs-lookup"><span data-stu-id="672df-159">c.</span></span> <span data-ttu-id="672df-160">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.topdesk.net/tas/public/login/saml`</span><span class="sxs-lookup"><span data-stu-id="672df-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="672df-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="672df-161">These values are not real.</span></span> <span data-ttu-id="672df-162">Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="672df-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="672df-163">Antwoord-URL is explaned verderop in de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="672df-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="672df-164">Neem contact op met [TOPdesk - ondersteuningsteam openbare Client](https://help.topdesk.com/saas/enterprise/user/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="672df-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) tooget these values.</span></span>  

4. <span data-ttu-id="672df-165">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="672df-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. <span data-ttu-id="672df-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="672df-167">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="672df-169">Op Hallo **TOPdesk - configuratie van openbare** sectie, klikt u op **configureren TOPdesk - openbare** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="672df-169">On hello **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="672df-170">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="672df-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![TOPdesk - openbare configuratie](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. <span data-ttu-id="672df-172">Meld u aan bij tooyour **TOPdesk - openbare** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="672df-172">Sign on tooyour **TOPdesk - Public** company site as an administrator.</span></span>

8. <span data-ttu-id="672df-173">In Hallo **TOPdesk** menu, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="672df-173">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="672df-174">![Instellingen](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="672df-174">![Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="672df-175">Klik op **aanmeldingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="672df-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="672df-176">![Instellingen voor aanmelding](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "aanmeldingsinstellingen")</span><span class="sxs-lookup"><span data-stu-id="672df-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="672df-177">Vouw Hallo **aanmeldingsinstellingen** menu en klik vervolgens op **algemene**.</span><span class="sxs-lookup"><span data-stu-id="672df-177">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="672df-178">![Algemene](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "algemeen")</span><span class="sxs-lookup"><span data-stu-id="672df-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="672df-179">In Hallo **openbare** sectie Hallo **SAML aanmelding** configuratie sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="672df-179">In hello **Public** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="672df-180">![Instellingen voor technische](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "technische instellingen")</span><span class="sxs-lookup"><span data-stu-id="672df-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="672df-181">a.</span><span class="sxs-lookup"><span data-stu-id="672df-181">a.</span></span> <span data-ttu-id="672df-182">Klik op **downloaden** toodownload openbare metagegevensbestand Hallo en lokaal opslaan op uw computer.</span><span class="sxs-lookup"><span data-stu-id="672df-182">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="672df-183">b.</span><span class="sxs-lookup"><span data-stu-id="672df-183">b.</span></span> <span data-ttu-id="672df-184">Open het metagegevensbestand Hallo gedownload, en Ga naar Hallo **AssertionConsumerService** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="672df-184">Open hello downloaded metadata file, and then locate hello **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="672df-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="672df-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="672df-186">c.</span><span class="sxs-lookup"><span data-stu-id="672df-186">c.</span></span> <span data-ttu-id="672df-187">Kopiëren Hallo **AssertionConsumerService** waarde, plakt u deze waarde in Hallo **antwoord-URL** textbox in **TOPdesk - URL's en openbare domein** sectie.</span><span class="sxs-lookup"><span data-stu-id="672df-187">Copy hello **AssertionConsumerService** value, paste this value in hello **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
12. <span data-ttu-id="672df-188">een certificaatbestand toocreate uitvoeren Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="672df-188">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="672df-189">![Certificaat](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "certificaat")</span><span class="sxs-lookup"><span data-stu-id="672df-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="672df-190">a.</span><span class="sxs-lookup"><span data-stu-id="672df-190">a.</span></span> <span data-ttu-id="672df-191">Open Hallo gedownload bestand met metagegevens vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="672df-191">Open hello downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="672df-192">b.</span><span class="sxs-lookup"><span data-stu-id="672df-192">b.</span></span> <span data-ttu-id="672df-193">Vouw Hallo **RoleDescriptor** knooppunt met een **xsi: type** van **ingevoerd: ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="672df-193">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="672df-194">c.</span><span class="sxs-lookup"><span data-stu-id="672df-194">c.</span></span> <span data-ttu-id="672df-195">Kopieer de waarde Hallo Hallo **X509Certificate** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="672df-195">Copy hello value of hello **X509Certificate** node.</span></span>
    
    <span data-ttu-id="672df-196">d.</span><span class="sxs-lookup"><span data-stu-id="672df-196">d.</span></span> <span data-ttu-id="672df-197">Opslaan Hallo gekopieerd **X509Certificate** waarde lokaal op uw computer in een bestand.</span><span class="sxs-lookup"><span data-stu-id="672df-197">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="672df-198">In Hallo **openbare** sectie, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="672df-198">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="672df-199">![SAML-aanmelding](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML-aanmelding")</span><span class="sxs-lookup"><span data-stu-id="672df-199">![SAML Login](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

14. <span data-ttu-id="672df-200">Op Hallo **SAML-configuratie-assistent** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="672df-200">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="672df-201">![SAML-configuratie-assistent](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "assistent voor SAML-configuratie")</span><span class="sxs-lookup"><span data-stu-id="672df-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="672df-202">a.</span><span class="sxs-lookup"><span data-stu-id="672df-202">a.</span></span> <span data-ttu-id="672df-203">tooupload de metagegevens van het gedownloade bestand vanuit Azure-portal onder **Federatiemetagegevens**, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="672df-203">tooupload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="672df-204">b.</span><span class="sxs-lookup"><span data-stu-id="672df-204">b.</span></span> <span data-ttu-id="672df-205">uw certificaat bestand onder tooupload **certificaat (RSA)**, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="672df-205">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="672df-206">c.</span><span class="sxs-lookup"><span data-stu-id="672df-206">c.</span></span> <span data-ttu-id="672df-207">tooupload Hallo logo-bestand die u hebt gekregen Hallo TOPdesk ondersteuningsteam, onder **Logo pictogram**, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="672df-207">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="672df-208">d.</span><span class="sxs-lookup"><span data-stu-id="672df-208">d.</span></span> <span data-ttu-id="672df-209">In Hallo **naam gebruikerskenmerk** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="672df-209">In hello **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="672df-210">e.</span><span class="sxs-lookup"><span data-stu-id="672df-210">e.</span></span> <span data-ttu-id="672df-211">In Hallo **weergavenaam** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="672df-211">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="672df-212">f.</span><span class="sxs-lookup"><span data-stu-id="672df-212">f.</span></span> <span data-ttu-id="672df-213">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="672df-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="672df-214">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="672df-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="672df-215">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="672df-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="672df-216">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="672df-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="672df-217">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="672df-217">Create an Azure AD test user</span></span>

<span data-ttu-id="672df-218">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="672df-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="672df-220">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="672df-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="672df-221">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="672df-221">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="672df-223">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="672df-223">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="672df-225">tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="672df-225">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![knop voor Hallo toevoegen](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="672df-227">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="672df-227">In hello **User** dialog box, perform hello following steps:</span></span>

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="672df-229">a.</span><span class="sxs-lookup"><span data-stu-id="672df-229">a.</span></span> <span data-ttu-id="672df-230">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="672df-230">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="672df-231">b.</span><span class="sxs-lookup"><span data-stu-id="672df-231">b.</span></span> <span data-ttu-id="672df-232">In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.</span><span class="sxs-lookup"><span data-stu-id="672df-232">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="672df-233">c.</span><span class="sxs-lookup"><span data-stu-id="672df-233">c.</span></span> <span data-ttu-id="672df-234">Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="672df-234">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="672df-235">d.</span><span class="sxs-lookup"><span data-stu-id="672df-235">d.</span></span> <span data-ttu-id="672df-236">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="672df-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="672df-237">Een TOPdesk - openbare testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="672df-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="672df-238">In de volgorde tooenable Azure AD-gebruikers toolog in TOPdesk - openbaar, ze in TOPdesk - openbare moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="672df-238">In order tooenable Azure AD users toolog into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="672df-239">In geval van TOPdesk - Hallo openbare inrichting is een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="672df-239">In hello case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="672df-240">tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="672df-240">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="672df-241">Meld u aan bij tooyour **TOPdesk - openbare** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="672df-241">Sign on tooyour **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="672df-242">Klik in het menu bovenaan Hallo Hallo **TOPdesk \> nieuw \> ondersteuningsbestanden \> persoon**.</span><span class="sxs-lookup"><span data-stu-id="672df-242">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="672df-243">![Persoon](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "persoon")</span><span class="sxs-lookup"><span data-stu-id="672df-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span></span>

3. <span data-ttu-id="672df-244">Voer in het dialoogvenster van de nieuwe persoon Hallo, Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="672df-244">On hello New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="672df-245">![Nieuwe persoon](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "nieuwe persoon")</span><span class="sxs-lookup"><span data-stu-id="672df-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="672df-246">a.</span><span class="sxs-lookup"><span data-stu-id="672df-246">a.</span></span> <span data-ttu-id="672df-247">Klik op tabblad Algemeen van Hallo.</span><span class="sxs-lookup"><span data-stu-id="672df-247">Click hello General tab.</span></span>

    <span data-ttu-id="672df-248">b.</span><span class="sxs-lookup"><span data-stu-id="672df-248">b.</span></span> <span data-ttu-id="672df-249">In Hallo **achternaam** textbox, typ de achternaam van de gebruiker Hallo zoals Simon</span><span class="sxs-lookup"><span data-stu-id="672df-249">In hello **Surname** textbox, type Surname of hello user like Simon</span></span>
 
    <span data-ttu-id="672df-250">c.</span><span class="sxs-lookup"><span data-stu-id="672df-250">c.</span></span> <span data-ttu-id="672df-251">Selecteer een **Site** voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="672df-251">Select a **Site** for hello account.</span></span>
 
    <span data-ttu-id="672df-252">d.</span><span class="sxs-lookup"><span data-stu-id="672df-252">d.</span></span> <span data-ttu-id="672df-253">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="672df-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="672df-254">U kunt geen andere TOPdesk - hulpmiddelen voor het maken van account openbaar gebruiker of geleverd door TOPdesk - gebruikersaccounts openbare tooprovision Azure AD-API's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="672df-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="672df-255">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="672df-255">Assign hello Azure AD test user</span></span>

<span data-ttu-id="672df-256">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooTOPdesk - openbaar.</span><span class="sxs-lookup"><span data-stu-id="672df-256">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTOPdesk - Public.</span></span>

![Hallo-gebruikersrollen toewijzen][200] 

<span data-ttu-id="672df-258">**tooassign Britta Simon tooTOPdesk - openbaar, Hallo volgende stappen uit te voeren:**</span><span class="sxs-lookup"><span data-stu-id="672df-258">**tooassign Britta Simon tooTOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="672df-259">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="672df-259">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="672df-261">Selecteer in de lijst met de toepassingen van Hallo **TOPdesk - openbare**.</span><span class="sxs-lookup"><span data-stu-id="672df-261">In hello applications list, select **TOPdesk - Public**.</span></span>

    ![Hallo TOPdesk - openbare koppelen in de lijst met Hallo-toepassingen](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. <span data-ttu-id="672df-263">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="672df-263">In hello menu on hello left, click **Users and groups**.</span></span>

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. <span data-ttu-id="672df-265">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="672df-265">Click **Add** button.</span></span> <span data-ttu-id="672df-266">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="672df-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Hallo toevoegen toewijzing deelvenster][203]

5. <span data-ttu-id="672df-268">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="672df-268">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="672df-269">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="672df-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="672df-270">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="672df-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="672df-271">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="672df-271">Test single sign-on</span></span>

<span data-ttu-id="672df-272">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="672df-272">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="672df-273">Wanneer u klikt op Hallo TOPdesk - openbare-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour TOPdesk - openbare toepassing.</span><span class="sxs-lookup"><span data-stu-id="672df-273">When you click hello TOPdesk - Public tile in hello Access Panel, you should get automatically signed-on tooyour TOPdesk - Public application.</span></span>
<span data-ttu-id="672df-274">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="672df-274">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="672df-275">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="672df-275">Additional resources</span></span>

* [<span data-ttu-id="672df-276">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="672df-276">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="672df-277">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="672df-277">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

