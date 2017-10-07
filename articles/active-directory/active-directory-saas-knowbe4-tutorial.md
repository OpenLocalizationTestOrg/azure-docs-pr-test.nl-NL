---
title: 'Zelfstudie: Azure Active Directory-integratie met KnowBe4 Awareness beveiligingstraining | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en KnowBe4 Awareness beveiligingstraining.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b80d2212-cc5f-4adb-836c-570640810c39
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 907fa814b82c9ffb2376f73470b746a37104c66e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-knowbe4-security-awareness-training"></a><span data-ttu-id="57cc9-103">Zelfstudie: Azure Active Directory-integratie met KnowBe4 Awareness beveiligingstraining</span><span class="sxs-lookup"><span data-stu-id="57cc9-103">Tutorial: Azure Active Directory integration with KnowBe4 Security Awareness Training</span></span>

<span data-ttu-id="57cc9-104">In deze zelfstudie leert u hoe toointegrate KnowBe4 beveiligingstraining Awareness met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="57cc9-104">In this tutorial, you learn how toointegrate KnowBe4 Security Awareness Training with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="57cc9-105">KnowBe4 Awareness beveiligingstraining integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="57cc9-105">Integrating KnowBe4 Security Awareness Training with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="57cc9-106">U kunt beheren in Azure AD wie heeft toegang tot tooKnowBe4 Awareness beveiligingstraining</span><span class="sxs-lookup"><span data-stu-id="57cc9-106">You can control in Azure AD who has access tooKnowBe4 Security Awareness Training</span></span>
- <span data-ttu-id="57cc9-107">U kunt uw gebruikers in staat om tooautomatically aangemelde tooKnowBe4 beveiligingstraining Awareness (Single Sign-On) met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="57cc9-107">You can enable your users tooautomatically get signed-on tooKnowBe4 Security Awareness Training (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="57cc9-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="57cc9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="57cc9-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="57cc9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57cc9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="57cc9-110">Prerequisites</span></span>

<span data-ttu-id="57cc9-111">Azure AD-integratie met KnowBe4 Awareness beveiligingstraining tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="57cc9-111">tooconfigure Azure AD integration with KnowBe4 Security Awareness Training, you need hello following items:</span></span>

- <span data-ttu-id="57cc9-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="57cc9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="57cc9-113">Een KnowBe4 Awareness beveiligingstraining eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="57cc9-113">A KnowBe4 Security Awareness Training single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="57cc9-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="57cc9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="57cc9-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="57cc9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57cc9-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="57cc9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="57cc9-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57cc9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="57cc9-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="57cc9-118">Scenario description</span></span>
<span data-ttu-id="57cc9-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="57cc9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="57cc9-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="57cc9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="57cc9-121">Het toevoegen van KnowBe4 Awareness beveiligingstraining van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="57cc9-121">Adding KnowBe4 Security Awareness Training from hello gallery</span></span>
2. <span data-ttu-id="57cc9-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="57cc9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-knowbe4-security-awareness-training-from-hello-gallery"></a><span data-ttu-id="57cc9-123">Het toevoegen van KnowBe4 Awareness beveiligingstraining van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="57cc9-123">Adding KnowBe4 Security Awareness Training from hello gallery</span></span>
<span data-ttu-id="57cc9-124">tooconfigure hello integratie van KnowBe4 Awareness beveiligingstraining in Azure AD, moet u tooadd KnowBe4 Awareness beveiligingstraining van Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="57cc9-124">tooconfigure hello integration of KnowBe4 Security Awareness Training into Azure AD, you need tooadd KnowBe4 Security Awareness Training from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="57cc9-125">**tooadd KnowBe4 beveiligingstraining Awareness via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="57cc9-125">**tooadd KnowBe4 Security Awareness Training from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="57cc9-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="57cc9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="57cc9-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="57cc9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="57cc9-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="57cc9-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="57cc9-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57cc9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="57cc9-133">Typ in het zoekvak Hallo **KnowBe4 Awareness beveiligingstraining**.</span><span class="sxs-lookup"><span data-stu-id="57cc9-133">In hello search box, type **KnowBe4 Security Awareness Training**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_search.png)

5. <span data-ttu-id="57cc9-135">Selecteer in het deelvenster resultaten hello, **KnowBe4 Awareness beveiligingstraining**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="57cc9-135">In hello results panel, select **KnowBe4 Security Awareness Training**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="57cc9-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="57cc9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="57cc9-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met KnowBe4 Awareness beveiligingstraining op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="57cc9-138">In this section, you configure and test Azure AD single sign-on with KnowBe4 Security Awareness Training based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="57cc9-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in KnowBe4 Awareness beveiligingstraining is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57cc9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in KnowBe4 Security Awareness Training is tooa user in Azure AD.</span></span> <span data-ttu-id="57cc9-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in KnowBe4 Awareness beveiligingstraining toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="57cc9-140">In other words, a link relationship between an Azure AD user and hello related user in KnowBe4 Security Awareness Training needs toobe established.</span></span>

<span data-ttu-id="57cc9-141">Wijs in KnowBe4-Awareness beveiligingstraining Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="57cc9-141">In KnowBe4 Security Awareness Training, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="57cc9-142">tooconfigure en eenmalige aanmelding Azure AD-test met KnowBe4 Awareness beveiligingstraining, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="57cc9-142">tooconfigure and test Azure AD single sign-on with KnowBe4 Security Awareness Training, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="57cc9-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="57cc9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="57cc9-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57cc9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="57cc9-145">**[Maken van een testgebruiker KnowBe4 Awareness beveiligingstraining](#creating-a-knowbe4-security-awareness-training-test-user)**  -toohave een equivalent van Britta Simon in KnowBe4 Awareness beveiligingstraining die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="57cc9-145">**[Creating a KnowBe4 Security Awareness Training test user](#creating-a-knowbe4-security-awareness-training-test-user)** - toohave a counterpart of Britta Simon in KnowBe4 Security Awareness Training that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="57cc9-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="57cc9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="57cc9-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="57cc9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="57cc9-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="57cc9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="57cc9-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing KnowBe4 Awareness beveiligingstraining configureren.</span><span class="sxs-lookup"><span data-stu-id="57cc9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your KnowBe4 Security Awareness Training application.</span></span>

<span data-ttu-id="57cc9-150">**tooconfigure eenmalige aanmelding Azure AD met KnowBe4-Awareness beveiligingstraining Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="57cc9-150">**tooconfigure Azure AD single sign-on with KnowBe4 Security Awareness Training, perform hello following steps:**</span></span>

1. <span data-ttu-id="57cc9-151">In Azure-portal op Hallo Hallo **KnowBe4 Awareness beveiligingstraining** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="57cc9-151">In hello Azure portal, on hello **KnowBe4 Security Awareness Training** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="57cc9-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="57cc9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_samlbase.png)

3. <span data-ttu-id="57cc9-155">Op Hallo **Awareness KnowBe4-Training beveiligingsdomein en URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="57cc9-155">On hello **KnowBe4 Security Awareness Training Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_url.png)

    <span data-ttu-id="57cc9-157">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="57cc9-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="57cc9-158">Hallo-waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="57cc9-158">hello value is not real.</span></span> <span data-ttu-id="57cc9-159">Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="57cc9-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="57cc9-160">Neem contact op met [KnowBe4 beveiliging Awareness Training Client ondersteuningsteam](mailto:support@KnowBe4.com) tooget Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="57cc9-160">Contact [KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com) tooget hello value.</span></span> 
 

4. <span data-ttu-id="57cc9-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Raw)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="57cc9-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_certificate.png) 

5. <span data-ttu-id="57cc9-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="57cc9-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="57cc9-165">Op Hallo **Awareness KnowBe4-Training Beveiligingsconfiguratie** sectie, klikt u op **configureren KnowBe4 Awareness beveiligingstraining** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="57cc9-165">On hello **KnowBe4 Security Awareness Training Configuration** section, click **Configure KnowBe4 Security Awareness Training** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="57cc9-166">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="57cc9-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_configure.png) 

7. <span data-ttu-id="57cc9-168">tooconfigure eenmalige aanmelding op **KnowBe4 Awareness beveiligingstraining** zijde, moet u toosend Hallo gedownload **certificaat (Raw)**, **Sign-Out-URL, SAML entiteit-ID en eenmalige aanmelding SAML Service-URL** te[KnowBe4 beveiliging Awareness Training Client ondersteuningsteam](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="57cc9-168">tooconfigure single sign-on on **KnowBe4 Security Awareness Training** side, you need toosend hello downloaded **Certificate (Raw)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com).</span></span>

> [!TIP]
> <span data-ttu-id="57cc9-169">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="57cc9-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="57cc9-170">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="57cc9-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="57cc9-171">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="57cc9-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="57cc9-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="57cc9-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="57cc9-173">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="57cc9-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="57cc9-175">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="57cc9-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="57cc9-176">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="57cc9-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="57cc9-178">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="57cc9-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="57cc9-180">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="57cc9-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="57cc9-182">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="57cc9-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="57cc9-184">a.</span><span class="sxs-lookup"><span data-stu-id="57cc9-184">a.</span></span> <span data-ttu-id="57cc9-185">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="57cc9-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="57cc9-186">b.</span><span class="sxs-lookup"><span data-stu-id="57cc9-186">b.</span></span> <span data-ttu-id="57cc9-187">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="57cc9-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="57cc9-188">c.</span><span class="sxs-lookup"><span data-stu-id="57cc9-188">c.</span></span> <span data-ttu-id="57cc9-189">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="57cc9-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="57cc9-190">d.</span><span class="sxs-lookup"><span data-stu-id="57cc9-190">d.</span></span> <span data-ttu-id="57cc9-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="57cc9-191">Click **Create**.</span></span>
 
### <a name="creating-a-knowbe4-security-awareness-training-test-user"></a><span data-ttu-id="57cc9-192">Een testgebruiker KnowBe4 Awareness beveiligingstraining maken</span><span class="sxs-lookup"><span data-stu-id="57cc9-192">Creating a KnowBe4 Security Awareness Training test user</span></span>

<span data-ttu-id="57cc9-193">Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in KnowBe4 Awareness beveiligingstraining van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="57cc9-193">hello objective of this section is toocreate a user called Britta Simon in KnowBe4 Security Awareness Training.</span></span> <span data-ttu-id="57cc9-194">KnowBe4 Awareness beveiligingstraining ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="57cc9-194">KnowBe4 Security Awareness Training supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="57cc9-195">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="57cc9-195">There is no action item for you in this section.</span></span> <span data-ttu-id="57cc9-196">Een nieuwe gebruiker wordt tijdens een poging tooaccess KnowBe4 Awareness beveiligingstraining gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="57cc9-196">A new user is created during an attempt tooaccess KnowBe4 Security Awareness Training if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="57cc9-197">Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello [KnowBe4 Awareness beveiligingstraining ondersteuningsteam](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="57cc9-197">If you need toocreate a user manually, you need toocontact hello [KnowBe4 Security Awareness Training support team](mailto:support@KnowBe4.com).</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="57cc9-198">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="57cc9-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="57cc9-199">In deze sectie, schakelt u Britta Simon toouse Azure eenmalige aanmelding verleent toegang tot tooKnowBe4 Awareness beveiligingstraining.</span><span class="sxs-lookup"><span data-stu-id="57cc9-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKnowBe4 Security Awareness Training.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="57cc9-201">**tooassign Britta Simon tooKnowBe4-Awareness beveiligingstraining Hallo stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="57cc9-201">**tooassign Britta Simon tooKnowBe4 Security Awareness Training, perform hello following steps:**</span></span>

1. <span data-ttu-id="57cc9-202">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="57cc9-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="57cc9-204">Selecteer in de lijst met de toepassingen van Hallo **KnowBe4 Awareness beveiligingstraining**.</span><span class="sxs-lookup"><span data-stu-id="57cc9-204">In hello applications list, select **KnowBe4 Security Awareness Training**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_app.png) 

3. <span data-ttu-id="57cc9-206">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="57cc9-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="57cc9-208">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="57cc9-208">Click **Add** button.</span></span> <span data-ttu-id="57cc9-209">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57cc9-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="57cc9-211">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="57cc9-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="57cc9-212">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57cc9-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="57cc9-213">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57cc9-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="57cc9-214">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="57cc9-214">Testing single sign-on</span></span>

<span data-ttu-id="57cc9-215">Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="57cc9-215">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
  
<span data-ttu-id="57cc9-216">Als u op Hallo KnowBe4 Awareness beveiligingstraining tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour KnowBe4 Awareness beveiligingstraining toepassing.</span><span class="sxs-lookup"><span data-stu-id="57cc9-216">When you click hello KnowBe4 Security Awareness Training tile in hello Access Panel, you should get automatically signed-on tooyour KnowBe4 Security Awareness Training application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="57cc9-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="57cc9-217">Additional resources</span></span>

* [<span data-ttu-id="57cc9-218">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57cc9-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57cc9-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="57cc9-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_203.png

