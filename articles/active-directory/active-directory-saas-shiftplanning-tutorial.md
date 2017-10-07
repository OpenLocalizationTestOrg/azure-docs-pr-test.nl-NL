---
title: 'Zelfstudie: Azure Active Directory-integratie met menselijkheid | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en menselijkheid.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7d8a04a2eb3c997f86f1e199c47809fa3dad60e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="c79b0-103">Zelfstudie: Azure Active Directory-integratie met menselijkheid</span><span class="sxs-lookup"><span data-stu-id="c79b0-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="c79b0-104">In deze zelfstudie leert u hoe toointegrate menselijkheid met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c79b0-104">In this tutorial, you learn how toointegrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c79b0-105">Menselijkheid integreren met Azure AD biedt Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c79b0-105">Integrating Humanity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c79b0-106">U kunt beheren in Azure AD die tooHumanity toegang heeft</span><span class="sxs-lookup"><span data-stu-id="c79b0-106">You can control in Azure AD who has access tooHumanity</span></span>
- <span data-ttu-id="c79b0-107">U kunt uw gebruikers tooautomatically get aangemelde tooHumanity (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="c79b0-107">You can enable your users tooautomatically get signed-on tooHumanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c79b0-108">U kunt uw accounts op één centrale locatie - hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c79b0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c79b0-109">Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c79b0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c79b0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c79b0-110">Prerequisites</span></span>

<span data-ttu-id="c79b0-111">Azure AD-integratie met menselijkheid tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="c79b0-111">tooconfigure Azure AD integration with Humanity, you need hello following items:</span></span>

- <span data-ttu-id="c79b0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c79b0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c79b0-113">Een menselijkheid eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c79b0-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c79b0-114">tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c79b0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c79b0-115">tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c79b0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c79b0-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c79b0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c79b0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c79b0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c79b0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c79b0-118">Scenario description</span></span>
<span data-ttu-id="c79b0-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c79b0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c79b0-120">Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c79b0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c79b0-121">Het toevoegen van menselijkheid van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="c79b0-121">Adding Humanity from hello gallery</span></span>
2. <span data-ttu-id="c79b0-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c79b0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-hello-gallery"></a><span data-ttu-id="c79b0-123">Het toevoegen van menselijkheid van Hallo-galerie</span><span class="sxs-lookup"><span data-stu-id="c79b0-123">Adding Humanity from hello gallery</span></span>
<span data-ttu-id="c79b0-124">tooconfigure hello integratie van menselijkheid met Azure AD, moet u tooadd menselijkheid uit Hallo galerie tooyour lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c79b0-124">tooconfigure hello integration of Humanity into Azure AD, you need tooadd Humanity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c79b0-125">**tooadd menselijkheid via Hallo gallery uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c79b0-125">**tooadd Humanity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c79b0-126">In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c79b0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c79b0-128">Navigeer te**bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c79b0-129">Ga te**alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-129">Then go too**All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c79b0-131">de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c79b0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c79b0-133">Typ in het zoekvak Hallo **menselijkheid**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-133">In hello search box, type **Humanity**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="c79b0-135">Selecteer in het deelvenster resultaten hello, **menselijkheid**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c79b0-135">In hello results panel, select **Humanity**, and then click **Add** button tooadd hello application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c79b0-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c79b0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c79b0-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met menselijkheid op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="c79b0-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c79b0-139">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in menselijkheid is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c79b0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Humanity is tooa user in Azure AD.</span></span> <span data-ttu-id="c79b0-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in menselijkheid toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="c79b0-140">In other words, a link relationship between an Azure AD user and hello related user in Humanity needs toobe established.</span></span>

<span data-ttu-id="c79b0-141">Wijs in menselijkheid, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.</span><span class="sxs-lookup"><span data-stu-id="c79b0-141">In Humanity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c79b0-142">tooconfigure en eenmalige aanmelding Azure AD-test met menselijkheid, moet u toocomplete Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c79b0-142">tooconfigure and test Azure AD single sign-on with Humanity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c79b0-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="c79b0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c79b0-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c79b0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c79b0-145">**[Maken van een testgebruiker menselijkheid](#creating-a-humanity-test-user)**  -toohave een equivalent van Britta Simon in menselijkheid die gekoppelde toohello Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c79b0-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - toohave a counterpart of Britta Simon in Humanity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c79b0-146">**[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c79b0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c79b0-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c79b0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c79b0-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c79b0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c79b0-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing menselijkheid configureren.</span><span class="sxs-lookup"><span data-stu-id="c79b0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="c79b0-150">**Azure AD tooconfigure eenmalige aanmelding met menselijkheid, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c79b0-150">**tooconfigure Azure AD single sign-on with Humanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="c79b0-151">In de Azure-portal op Hallo Hallo **menselijkheid** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-151">In hello Azure portal, on hello **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c79b0-153">Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c79b0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="c79b0-155">Op Hallo **menselijkheid domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c79b0-155">On hello **Humanity Domain and URLs** section, perform hello following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="c79b0-157">a.</span><span class="sxs-lookup"><span data-stu-id="c79b0-157">a.</span></span> <span data-ttu-id="c79b0-158">In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://company.humanity.com/includes/saml/`</span><span class="sxs-lookup"><span data-stu-id="c79b0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="c79b0-159">b.</span><span class="sxs-lookup"><span data-stu-id="c79b0-159">b.</span></span> <span data-ttu-id="c79b0-160">In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="c79b0-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c79b0-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="c79b0-161">These values are not real.</span></span> <span data-ttu-id="c79b0-162">Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id.</span><span class="sxs-lookup"><span data-stu-id="c79b0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c79b0-163">Neem contact op met [menselijkheid Client ondersteuningsteam](https://www.humanity.com/support/) tooget deze waarden.</span><span class="sxs-lookup"><span data-stu-id="c79b0-163">Contact [Humanity Client support team](https://www.humanity.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="c79b0-164">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c79b0-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="c79b0-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c79b0-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c79b0-168">Op Hallo **menselijkheid configuratie** sectie, klikt u op **menselijkheid configureren** tooopen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="c79b0-168">On hello **Humanity Configuration** section, click **Configure Humanity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c79b0-169">Kopiëren Hallo **SAML Single Sign-On Service-URL en Sign-Out URL** van Hallo **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="c79b0-169">Copy hello **SAML Single Sign-On Service URL, and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="c79b0-171">Aanmelden in een ander browservenster tooyour **menselijkheid** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c79b0-171">In a different web browser window, log in tooyour **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="c79b0-172">Klik in het menu bovenaan Hallo Hallo **Admin**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="c79b0-173">![Beheerder](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="c79b0-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="c79b0-174">Onder **integratie**, klikt u op **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="c79b0-175">![Eenmalige aanmelding](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="c79b0-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="c79b0-176">In Hallo **Single Sign-On** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c79b0-176">In hello **Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c79b0-177">![Eenmalige aanmelding](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="c79b0-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="c79b0-178">a.</span><span class="sxs-lookup"><span data-stu-id="c79b0-178">a.</span></span> <span data-ttu-id="c79b0-179">Selecteer **SAML ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="c79b0-180">b.</span><span class="sxs-lookup"><span data-stu-id="c79b0-180">b.</span></span> <span data-ttu-id="c79b0-181">Selecteer **wachtwoord aanmelding toestaan**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="c79b0-182">c.</span><span class="sxs-lookup"><span data-stu-id="c79b0-182">c.</span></span> <span data-ttu-id="c79b0-183">Plakken Hallo **SAML Single Sign-On Service-URL** waarde in Hallo **URL-verlener SAML** textbox.</span><span class="sxs-lookup"><span data-stu-id="c79b0-183">Paste hello **SAML Single Sign-On Service URL** value into hello **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="c79b0-184">d.</span><span class="sxs-lookup"><span data-stu-id="c79b0-184">d.</span></span> <span data-ttu-id="c79b0-185">Plakken Hallo **Sign-Out URL** waarde in Hallo **externe URL voor afmelden** textbox.</span><span class="sxs-lookup"><span data-stu-id="c79b0-185">Paste hello **Sign-Out URL** value into hello **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="c79b0-186">e.</span><span class="sxs-lookup"><span data-stu-id="c79b0-186">e.</span></span> <span data-ttu-id="c79b0-187">De base-64 gecodeerde certificaat openen in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **X.509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="c79b0-187">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="c79b0-188">Klik op **instellingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="c79b0-189">U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.</span><span class="sxs-lookup"><span data-stu-id="c79b0-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c79b0-190">Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="c79b0-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c79b0-191">U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c79b0-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c79b0-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c79b0-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="c79b0-193">Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c79b0-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c79b0-195">**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c79b0-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c79b0-196">In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c79b0-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c79b0-198">toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c79b0-200">Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.</span><span class="sxs-lookup"><span data-stu-id="c79b0-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c79b0-202">Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c79b0-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c79b0-204">a.</span><span class="sxs-lookup"><span data-stu-id="c79b0-204">a.</span></span> <span data-ttu-id="c79b0-205">In Hallo **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c79b0-206">b.</span><span class="sxs-lookup"><span data-stu-id="c79b0-206">b.</span></span> <span data-ttu-id="c79b0-207">In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c79b0-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c79b0-208">c.</span><span class="sxs-lookup"><span data-stu-id="c79b0-208">c.</span></span> <span data-ttu-id="c79b0-209">Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c79b0-210">d.</span><span class="sxs-lookup"><span data-stu-id="c79b0-210">d.</span></span> <span data-ttu-id="c79b0-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="c79b0-212">Een testgebruiker menselijkheid maken</span><span class="sxs-lookup"><span data-stu-id="c79b0-212">Creating a Humanity test user</span></span>

<span data-ttu-id="c79b0-213">In de volgorde tooenable Azure AD gebruikers toolog in tooHumanity, moeten ze worden ingericht in menselijkheid.</span><span class="sxs-lookup"><span data-stu-id="c79b0-213">In order tooenable Azure AD users toolog in tooHumanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="c79b0-214">In geval van menselijkheid Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="c79b0-214">In hello case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="c79b0-215">**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c79b0-215">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c79b0-216">Meld u bij tooyour **menselijkheid** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c79b0-216">Log in tooyour **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="c79b0-217">Klik op **Admin**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="c79b0-218">![Beheerder](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="c79b0-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="c79b0-219">Klik op **personeel**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="c79b0-220">![Personeel](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "personeel")</span><span class="sxs-lookup"><span data-stu-id="c79b0-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="c79b0-221">Onder **acties**, klikt u op **werknemers toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="c79b0-222">![Werknemers toevoegen](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "werknemers toevoegen")</span><span class="sxs-lookup"><span data-stu-id="c79b0-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="c79b0-223">In Hallo **werknemers toevoegen** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c79b0-223">In hello **Add Employees** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c79b0-224">![Opslaan van werknemers](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "werknemers opslaan")</span><span class="sxs-lookup"><span data-stu-id="c79b0-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="c79b0-225">a.</span><span class="sxs-lookup"><span data-stu-id="c79b0-225">a.</span></span> <span data-ttu-id="c79b0-226">Type Hallo **voornaam**, **achternaam**, en **e** van tekstvakken met betrekking tot een geldige AAD-account u wilt dat tooprovision in Hallo.</span><span class="sxs-lookup"><span data-stu-id="c79b0-226">Type hello **First Name**, **Last Name**, and **Email** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="c79b0-227">b.</span><span class="sxs-lookup"><span data-stu-id="c79b0-227">b.</span></span> <span data-ttu-id="c79b0-228">Klik op **opslaan werknemers**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="c79b0-229">U kunt andere menselijkheid gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door menselijkheid tooprovision AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="c79b0-229">You can use any other Humanity user account creation tools or APIs provided by Humanity tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c79b0-230">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c79b0-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c79b0-231">In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooHumanity toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="c79b0-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHumanity.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c79b0-233">**tooassign Britta Simon tooHumanity, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="c79b0-233">**tooassign Britta Simon tooHumanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="c79b0-234">In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c79b0-236">Selecteer in de lijst met de toepassingen van Hallo **menselijkheid**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-236">In hello applications list, select **Humanity**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="c79b0-238">Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c79b0-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c79b0-240">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c79b0-240">Click **Add** button.</span></span> <span data-ttu-id="c79b0-241">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c79b0-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c79b0-243">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="c79b0-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c79b0-244">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c79b0-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c79b0-245">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c79b0-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c79b0-246">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c79b0-246">Testing single sign-on</span></span>

<span data-ttu-id="c79b0-247">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="c79b0-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c79b0-248">Als u op Hallo menselijkheid tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour menselijkheid toepassing.</span><span class="sxs-lookup"><span data-stu-id="c79b0-248">When you click hello Humanity tile in hello Access Panel, you should get automatically signed-on tooyour Humanity application.</span></span>
<span data-ttu-id="c79b0-249">Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c79b0-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c79b0-250">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c79b0-250">Additional resources</span></span>

* [<span data-ttu-id="c79b0-251">Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c79b0-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c79b0-252">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c79b0-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

