---
title: 'Zelfstudie: Azure Active Directory-integratie met Tangoe opdracht Premium Mobile | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Tangoe opdracht Premium Mobile.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 7bd1cd6afade58a4a47a173b249f92eb84e42112
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="8e56c-103">Zelfstudie: Azure Active Directory-integratie met Tangoe opdracht Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="8e56c-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="8e56c-104">In deze zelfstudie leert u hoe toointegrate Tangoe opdracht Premium mobiel met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8e56c-104">In this tutorial, you learn how toointegrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8e56c-105">Tangoe opdracht Premium Mobile integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="8e56c-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8e56c-106">U kunt beheren in Azure AD wie toegang tot tooTangoe opdracht Premium Mobile heeft</span><span class="sxs-lookup"><span data-stu-id="8e56c-106">You can control in Azure AD who has access tooTangoe Command Premium Mobile</span></span>
- <span data-ttu-id="8e56c-107">U kunt uw gebruikers tooautomatically get aangemelde tooTangoe opdracht Premium Mobile (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="8e56c-107">You can enable your users tooautomatically get signed-on tooTangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8e56c-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="8e56c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8e56c-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8e56c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e56c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8e56c-110">Prerequisites</span></span>

<span data-ttu-id="8e56c-111">Azure AD-integratie met Tangoe opdracht Premium Mobile tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="8e56c-111">tooconfigure Azure AD integration with Tangoe Command Premium Mobile, you need hello following items:</span></span>

- <span data-ttu-id="8e56c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="8e56c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8e56c-113">Een Tangoe opdracht Premium Mobile eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="8e56c-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8e56c-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="8e56c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8e56c-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="8e56c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8e56c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="8e56c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8e56c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8e56c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8e56c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="8e56c-118">Scenario description</span></span>
<span data-ttu-id="8e56c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="8e56c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8e56c-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="8e56c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8e56c-121">Tangoe opdracht Premium Mobile van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="8e56c-121">Add Tangoe Command Premium Mobile from hello gallery</span></span>
2. <span data-ttu-id="8e56c-122">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e56c-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tangoe-command-premium-mobile-from-hello-gallery"></a><span data-ttu-id="8e56c-123">Tangoe opdracht Premium Mobile van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="8e56c-123">Add Tangoe Command Premium Mobile from hello gallery</span></span>
<span data-ttu-id="8e56c-124">tooconfigure hello integratie van Tangoe opdracht Premium Mobile in Azure AD, moet u tooadd Tangoe opdracht Premium Mobile uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="8e56c-124">tooconfigure hello integration of Tangoe Command Premium Mobile into Azure AD, you need tooadd Tangoe Command Premium Mobile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8e56c-125">**tooadd Tangoe opdracht Premium Mobile via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8e56c-125">**tooadd Tangoe Command Premium Mobile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e56c-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8e56c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8e56c-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8e56c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8e56c-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8e56c-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="8e56c-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8e56c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="8e56c-133">Typ in het zoekvak Hallo **Tangoe opdracht Premium Mobile**, selecteer **Tangoe opdracht Premium Mobile** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="8e56c-133">In hello search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![<span data-ttu-id="8e56c-134">Tangoe opdracht Premium Mobile uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="8e56c-134">Add Tangoe Command Premium Mobile from gallery</span></span> ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8e56c-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e56c-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="8e56c-136">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Tangoe opdracht Premium Mobile op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="8e56c-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8e56c-137">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Tangoe opdracht Premium Mobile is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e56c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tangoe Command Premium Mobile is tooa user in Azure AD.</span></span> <span data-ttu-id="8e56c-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Tangoe opdracht Premium Mobile toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="8e56c-138">In other words, a link relationship between an Azure AD user and hello related user in Tangoe Command Premium Mobile needs toobe established.</span></span>

<span data-ttu-id="8e56c-139">Wijs in Tangoe opdracht Premium Mobile Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="8e56c-139">In Tangoe Command Premium Mobile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8e56c-140">tooconfigure en test eenmalige aanmelding Azure AD met Tangoe opdracht Premium Mobile, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8e56c-140">tooconfigure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8e56c-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="8e56c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8e56c-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e56c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8e56c-143">**[Maak een testgebruiker Tangoe opdracht Premium Mobile](#create-a-tangoe-command-premium-mobile-test-user)**  -toohave een equivalent van Britta Simon in Tangoe opdracht Premium Mobile gekoppelde toohello Azure AD-weergave van de gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="8e56c-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - toohave a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8e56c-144">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8e56c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8e56c-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="8e56c-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8e56c-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="8e56c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8e56c-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Tangoe opdracht Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="8e56c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="8e56c-148">**tooconfigure eenmalige aanmelding Azure AD met Tangoe opdracht Premium Mobile Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8e56c-148">**tooconfigure Azure AD single sign-on with Tangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e56c-149">In de Azure-portal op Hallo Hallo **Tangoe opdracht Premium Mobile** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="8e56c-149">In hello Azure portal, on hello **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="8e56c-151">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8e56c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Op basis van SAML eenmalige aanmelding](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. <span data-ttu-id="8e56c-153">Op Hallo **Tangoe opdracht Premium Mobile domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8e56c-153">On hello **Tangoe Command Premium Mobile Domain and URLs** section, perform hello following steps:</span></span>

    ![URL's en mobiele Tangoe opdracht Premium-domein](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    <span data-ttu-id="8e56c-155">a.</span><span class="sxs-lookup"><span data-stu-id="8e56c-155">a.</span></span> <span data-ttu-id="8e56c-156">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span><span class="sxs-lookup"><span data-stu-id="8e56c-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span></span>

    <span data-ttu-id="8e56c-157">b.</span><span class="sxs-lookup"><span data-stu-id="8e56c-157">b.</span></span> <span data-ttu-id="8e56c-158">In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://sso.tangoe.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="8e56c-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8e56c-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="8e56c-159">These values are not real.</span></span> <span data-ttu-id="8e56c-160">Deze waarden bijwerken met Hallo werkelijke antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="8e56c-160">Update these values with hello actual  Reply URL and Sign-On URL.</span></span> <span data-ttu-id="8e56c-161">Neem contact op met [Tangoe opdracht Premium Mobile Client ondersteuningsteam](https://www.tangoe.com/contact-2/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="8e56c-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooget these values.</span></span> 

4. <span data-ttu-id="8e56c-162">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="8e56c-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Certificaat voor ondertekening van SAML-sectie](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. <span data-ttu-id="8e56c-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="8e56c-164">Click **Save** button.</span></span>

    ![knop Opslaan](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="8e56c-166">Op Hallo **Tangoe Premium mobiele configuratie** sectie, klikt u op **configureren Tangoe opdracht Premium Mobile** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="8e56c-166">On hello **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8e56c-167">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="8e56c-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuratiesectie Tangoe opdracht Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. <span data-ttu-id="8e56c-169">tooget SSO geconfigureerd voor uw toepassing, neem contact op met uw [Tangoe opdracht Premium Mobile Client ondersteuningsteam](https://www.tangoe.com/contact-2/) en biedt de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="8e56c-169">tooget SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) and provide hello following:</span></span>

   - <span data-ttu-id="8e56c-170">Hallo gedownloade metagegevensbestand</span><span class="sxs-lookup"><span data-stu-id="8e56c-170">hello downloaded metadata file</span></span>
   - <span data-ttu-id="8e56c-171">Hallo **SAML entiteit-ID**</span><span class="sxs-lookup"><span data-stu-id="8e56c-171">hello **SAML Entity ID**</span></span>
   - <span data-ttu-id="8e56c-172">Hallo **SAML Single Sign-On Service-URL**</span><span class="sxs-lookup"><span data-stu-id="8e56c-172">hello **SAML Single Sign-On Service URL**</span></span>
   - <span data-ttu-id="8e56c-173">Hallo **Sign-Out URL**</span><span class="sxs-lookup"><span data-stu-id="8e56c-173">hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="8e56c-174">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="8e56c-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8e56c-175">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="8e56c-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8e56c-176">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8e56c-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8e56c-177">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="8e56c-177">Create an Azure AD test user</span></span>
<span data-ttu-id="8e56c-178">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="8e56c-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="8e56c-180">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8e56c-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e56c-181">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8e56c-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8e56c-183">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="8e56c-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Gebruikers en groepen -> alle gebruikers](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8e56c-185">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="8e56c-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Gebruiker toevoegen](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8e56c-187">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8e56c-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Dialoogvenster op de gebruikerspagina](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8e56c-189">a.</span><span class="sxs-lookup"><span data-stu-id="8e56c-189">a.</span></span> <span data-ttu-id="8e56c-190">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8e56c-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8e56c-191">b.</span><span class="sxs-lookup"><span data-stu-id="8e56c-191">b.</span></span> <span data-ttu-id="8e56c-192">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8e56c-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8e56c-193">c.</span><span class="sxs-lookup"><span data-stu-id="8e56c-193">c.</span></span> <span data-ttu-id="8e56c-194">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="8e56c-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8e56c-195">d.</span><span class="sxs-lookup"><span data-stu-id="8e56c-195">d.</span></span> <span data-ttu-id="8e56c-196">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8e56c-196">Click **Create**.</span></span>
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="8e56c-197">Maak een testgebruiker Tangoe opdracht Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="8e56c-197">Create a Tangoe Command Premium Mobile test user</span></span>

<span data-ttu-id="8e56c-198">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Tangoe opdracht Premium Mobile maken.</span><span class="sxs-lookup"><span data-stu-id="8e56c-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="8e56c-199">Tangoe opdracht Premium mobiele App moet alle Hallo gebruikers toobe ingericht in de toepassing hello voordat u eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8e56c-199">Tangoe Command Premium Mobile application needs all hello users toobe provisioned in hello application before doing Single Sign On.</span></span> <span data-ttu-id="8e56c-200">Dus neem werk Hello [Tangoe opdracht Premium Mobile Client ondersteuningsteam](https://www.tangoe.com/contact-2/) tooprovision deze gebruikers in de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="8e56c-200">So please work with hello [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooprovision all these users into hello application.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8e56c-201">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e56c-201">Assign hello Azure AD test user</span></span>

<span data-ttu-id="8e56c-202">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooTangoe opdracht Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="8e56c-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTangoe Command Premium Mobile.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="8e56c-204">**tooassign Britta Simon tooTangoe opdracht Premium Mobile, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="8e56c-204">**tooassign Britta Simon tooTangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e56c-205">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8e56c-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="8e56c-207">Selecteer in de lijst met de toepassingen van Hallo **Tangoe opdracht Premium Mobile**.</span><span class="sxs-lookup"><span data-stu-id="8e56c-207">In hello applications list, select **Tangoe Command Premium Mobile**.</span></span>

    ![Tangoe opdracht Premium Mobile in lijst met Apps](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. <span data-ttu-id="8e56c-209">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="8e56c-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="8e56c-211">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="8e56c-211">Click **Add** button.</span></span> <span data-ttu-id="8e56c-212">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8e56c-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="8e56c-214">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="8e56c-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8e56c-215">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8e56c-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8e56c-216">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8e56c-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8e56c-217">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8e56c-217">Test single sign-on</span></span>

<span data-ttu-id="8e56c-218">In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="8e56c-218">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="8e56c-219">Als u op Hallo Tangoe opdracht Premium Mobile tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Tangoe opdracht Premium Mobile-applicatie.</span><span class="sxs-lookup"><span data-stu-id="8e56c-219">When you click hello Tangoe Command Premium Mobile tile in hello Access Panel, you should get automatically signed-on tooyour Tangoe Command Premium Mobile application.</span></span> <span data-ttu-id="8e56c-220">Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8e56c-220">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8e56c-221">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8e56c-221">Additional resources</span></span>

* [<span data-ttu-id="8e56c-222">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e56c-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8e56c-223">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8e56c-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

