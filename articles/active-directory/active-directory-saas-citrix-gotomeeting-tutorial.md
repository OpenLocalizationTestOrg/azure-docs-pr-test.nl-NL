---
title: 'Zelfstudie: Azure Active Directory-integratie met Citrix GoToMeeting | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Citrix GoToMeeting.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 46a5da7504806202a5ec29f73c504e772c61bc2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="4717d-103">Zelfstudie: Azure Active Directory-integratie met Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="4717d-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="4717d-104">In deze zelfstudie leert u hoe toointegrate Citrix GoToMeeting met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4717d-104">In this tutorial, you learn how toointegrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4717d-105">Citrix GoToMeeting integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="4717d-105">Integrating Citrix GoToMeeting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4717d-106">U kunt beheren in Azure AD wie toegang tot tooCitrix GoToMeeting heeft</span><span class="sxs-lookup"><span data-stu-id="4717d-106">You can control in Azure AD who has access tooCitrix GoToMeeting</span></span>
- <span data-ttu-id="4717d-107">U kunt uw gebruikers tooautomatically get aangemelde tooCitrix GoToMeeting (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="4717d-107">You can enable your users tooautomatically get signed-on tooCitrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4717d-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="4717d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4717d-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4717d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4717d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4717d-110">Prerequisites</span></span>

<span data-ttu-id="4717d-111">Azure AD-integratie met Citrix GoToMeeting tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="4717d-111">tooconfigure Azure AD integration with Citrix GoToMeeting, you need hello following items:</span></span>

- <span data-ttu-id="4717d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="4717d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4717d-113">Een Citrix GoToMeeting eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="4717d-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4717d-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="4717d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4717d-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="4717d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4717d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="4717d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4717d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4717d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4717d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="4717d-118">Scenario description</span></span>
<span data-ttu-id="4717d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4717d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4717d-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="4717d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4717d-121">Het toevoegen van Citrix GoToMeeting van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4717d-121">Adding Citrix GoToMeeting from hello gallery</span></span>
2. <span data-ttu-id="4717d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4717d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-hello-gallery"></a><span data-ttu-id="4717d-123">Het toevoegen van Citrix GoToMeeting van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="4717d-123">Adding Citrix GoToMeeting from hello gallery</span></span>
<span data-ttu-id="4717d-124">tooconfigure hello integratie van Citrix GoToMeeting in Azure AD, moet u Citrix GoToMeeting tooadd uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="4717d-124">tooconfigure hello integration of Citrix GoToMeeting into Azure AD, you need tooadd Citrix GoToMeeting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4717d-125">**tooadd Citrix GoToMeeting via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4717d-125">**tooadd Citrix GoToMeeting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4717d-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4717d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4717d-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4717d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4717d-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4717d-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="4717d-131">Klik op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="4717d-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="4717d-133">Typ in het zoekvak Hallo **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="4717d-133">In hello search box, type **Citrix GoToMeeting**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="4717d-135">Selecteer in het deelvenster resultaten hello, **Citrix GoToMeeting**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="4717d-135">In hello results panel, select **Citrix GoToMeeting**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4717d-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4717d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4717d-138">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met Citrix GoToMeeting op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="4717d-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4717d-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Citrix GoToMeeting is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4717d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix GoToMeeting is tooa user in Azure AD.</span></span> <span data-ttu-id="4717d-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Citrix GoToMeeting toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="4717d-140">In other words, a link relationship between an Azure AD user and hello related user in Citrix GoToMeeting needs toobe established.</span></span>

<span data-ttu-id="4717d-141">Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="4717d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="4717d-142">tooconfigure en eenmalige aanmelding Azure AD-test met Citrix GoToMeeting, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4717d-142">tooconfigure and test Azure AD single sign-on with Citrix GoToMeeting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4717d-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="4717d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4717d-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4717d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4717d-145">**[Maken van een testgebruiker Citrix GoToMeeting](#creating-a-citrix-gotomeeting-test-user)**  -toohave een equivalent van Britta Simon in Citrix GoToMeeting die is gekoppeld toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4717d-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - toohave a counterpart of Britta Simon in Citrix GoToMeeting that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4717d-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4717d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4717d-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="4717d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4717d-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="4717d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4717d-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Citrix GoToMeeting configureren.</span><span class="sxs-lookup"><span data-stu-id="4717d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="4717d-150">**Azure AD tooconfigure eenmalige aanmelding met Citrix GoToMeeting, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4717d-150">**tooconfigure Azure AD single sign-on with Citrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="4717d-151">In de Azure-portal op Hallo Hallo **Citrix GoToMeeting** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="4717d-151">In hello Azure portal, on hello **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="4717d-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4717d-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="4717d-155">Op Hallo **Citrix GoToMeeting domein en de URL's** sectie geen tooperform hoeft geen stappen.</span><span class="sxs-lookup"><span data-stu-id="4717d-155">On hello **Citrix GoToMeeting Domain and URLs** section, no need tooperform any steps.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="4717d-157">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="4717d-157">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="4717d-159">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="4717d-159">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="4717d-161">Klik op Hallo Citrix GoToMeeting SAML-configuratiesectie, configureer Citrix GoToMeeting SAML tooopen configureren aanmelding venster.</span><span class="sxs-lookup"><span data-stu-id="4717d-161">On hello Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="4717d-162">Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="4717d-162">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

6. <span data-ttu-id="4717d-163">Aanmelden in een ander browservenster tooyour [Citrix organisatie Center](https://account.citrixonline.com/organization/administration/).</span><span class="sxs-lookup"><span data-stu-id="4717d-163">In a different browser window, log in tooyour [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="4717d-164">Klik op Hallo **identiteitsprovider** tabblad en Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4717d-164">Click hello **Identity Provider** tab, and then perform hello following steps:</span></span>  
   
    <span data-ttu-id="4717d-165">![Setup van SAML](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span><span class="sxs-lookup"><span data-stu-id="4717d-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="4717d-166">a.</span><span class="sxs-lookup"><span data-stu-id="4717d-166">a.</span></span> <span data-ttu-id="4717d-167">Selecteer **handmatig**</span><span class="sxs-lookup"><span data-stu-id="4717d-167">Select **Manual**</span></span>

    <span data-ttu-id="4717d-168">b.</span><span class="sxs-lookup"><span data-stu-id="4717d-168">b.</span></span> <span data-ttu-id="4717d-169">In de Azure-portal op Hallo Hallo **op Citrix GoToMeeting eenmalige aanmelding configureren** dialoogvenster pagina, kopie Hallo **SAML Single Sign-On Service-URL** waarde en plak deze in Hallo **aanmeldingspagina URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="4717d-169">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="4717d-170">c.</span><span class="sxs-lookup"><span data-stu-id="4717d-170">c.</span></span> <span data-ttu-id="4717d-171">In de Azure-portal op Hallo Hallo **op Citrix GoToMeeting eenmalige aanmelding configureren** dialoogvenster pagina, kopie Hallo **Sign-Out URL** waarde en plak deze in Hallo **afmelden pagina-URL**textbox.</span><span class="sxs-lookup"><span data-stu-id="4717d-171">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **Sign-Out URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="4717d-172">d.</span><span class="sxs-lookup"><span data-stu-id="4717d-172">d.</span></span> <span data-ttu-id="4717d-173">In de Azure-portal op Hallo Hallo **op Citrix GoToMeeting eenmalige aanmelding configureren** dialoogvenster pagina, kopie Hallo **SAML entiteit-ID** waarde en plak deze in Hallo **identiteit Provider entiteit-ID**  textbox.</span><span class="sxs-lookup"><span data-stu-id="4717d-173">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Entity ID** value, and then paste it into hello **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="4717d-174">e.</span><span class="sxs-lookup"><span data-stu-id="4717d-174">e.</span></span> <span data-ttu-id="4717d-175">tooupload uw gedownloade certificaat, klik op **certificaat uploaden**.</span><span class="sxs-lookup"><span data-stu-id="4717d-175">tooupload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="4717d-176">f.</span><span class="sxs-lookup"><span data-stu-id="4717d-176">f.</span></span> <span data-ttu-id="4717d-177">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4717d-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4717d-178">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="4717d-178">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4717d-179">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="4717d-179">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4717d-180">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4717d-180">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4717d-181">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="4717d-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="4717d-182">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4717d-182">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="4717d-184">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4717d-184">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4717d-185">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4717d-185">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4717d-187">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="4717d-187">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4717d-189">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="4717d-189">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4717d-191">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4717d-191">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4717d-193">a.</span><span class="sxs-lookup"><span data-stu-id="4717d-193">a.</span></span> <span data-ttu-id="4717d-194">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4717d-194">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4717d-195">b.</span><span class="sxs-lookup"><span data-stu-id="4717d-195">b.</span></span> <span data-ttu-id="4717d-196">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4717d-196">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4717d-197">c.</span><span class="sxs-lookup"><span data-stu-id="4717d-197">c.</span></span> <span data-ttu-id="4717d-198">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="4717d-198">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4717d-199">d.</span><span class="sxs-lookup"><span data-stu-id="4717d-199">d.</span></span> <span data-ttu-id="4717d-200">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="4717d-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="4717d-201">Een testgebruiker Citrix GoToMeeting maken</span><span class="sxs-lookup"><span data-stu-id="4717d-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="4717d-202">In deze sectie wordt een gebruiker met de naam Britta Simon gemaakt in Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="4717d-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="4717d-203">Citrix GoToMeeting ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4717d-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="4717d-204">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="4717d-204">There is no action item for you in this section.</span></span> <span data-ttu-id="4717d-205">Als een gebruiker in Citrix GoToMeeting nog niet bestaat, wordt een nieuw gemaakt wanneer u tooaccess Citrix GoToMeeting probeert.</span><span class="sxs-lookup"><span data-stu-id="4717d-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt tooaccess Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="4717d-206">Als u een gebruiker handmatig, neem contact op met toocreate moet [ondersteuningsteam Citrix GoToMeeting](https://care.citrixonline.com/gotomeeting)</span><span class="sxs-lookup"><span data-stu-id="4717d-206">If you need toocreate a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4717d-207">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4717d-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4717d-208">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="4717d-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix GoToMeeting.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="4717d-210">**tooassign Britta Simon tooCitrix GoToMeeting, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="4717d-210">**tooassign Britta Simon tooCitrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="4717d-211">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4717d-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="4717d-213">Selecteer in de lijst met de toepassingen van Hallo **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="4717d-213">In hello applications list, select **Citrix GoToMeeting**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="4717d-215">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="4717d-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="4717d-217">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="4717d-217">Click **Add** button.</span></span> <span data-ttu-id="4717d-218">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4717d-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="4717d-220">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="4717d-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4717d-221">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4717d-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4717d-222">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4717d-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4717d-223">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4717d-223">Testing single sign-on</span></span>

<span data-ttu-id="4717d-224">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="4717d-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4717d-225">Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="4717d-225">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="4717d-226">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4717d-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4717d-227">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="4717d-227">Additional resources</span></span>

* [<span data-ttu-id="4717d-228">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4717d-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4717d-229">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4717d-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="4717d-230">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="4717d-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

