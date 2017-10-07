---
title: 'Zelfstudie: Azure Active Directory-integratie met Clarizen | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Clarizen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="c8459-103">Zelfstudie: Azure Active Directory-integratie met Clarizen</span><span class="sxs-lookup"><span data-stu-id="c8459-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="c8459-104">In deze zelfstudie leert u hoe toointegrate Azure Active Directory (Azure AD) met Clarizen.</span><span class="sxs-lookup"><span data-stu-id="c8459-104">In this tutorial, you learn how toointegrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="c8459-105">Deze integratie biedt u Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c8459-105">This integration gives you hello following benefits:</span></span>

- <span data-ttu-id="c8459-106">U kunt beheren, in Azure AD, die toegang tooClarizen heeft.</span><span class="sxs-lookup"><span data-stu-id="c8459-106">You can control, in Azure AD, who has access tooClarizen.</span></span>
- <span data-ttu-id="c8459-107">U kunt uw gebruikers toobe tooClarizen (eenmalige aanmelding) met hun Azure AD-accounts automatisch aangemeld inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c8459-107">You can enable your users toobe automatically signed in tooClarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c8459-108">U kunt uw accounts op één centrale locatie, hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="c8459-108">You can manage your accounts in one central location, hello Azure portal.</span></span>

<span data-ttu-id="c8459-109">Hallo-scenario in deze zelfstudie bestaat uit twee belangrijke taken:</span><span class="sxs-lookup"><span data-stu-id="c8459-109">hello scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="c8459-110">Clarizen uit Hallo galerie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c8459-110">Add Clarizen from hello gallery.</span></span>
2. <span data-ttu-id="c8459-111">Configureren en testen eenmalige aanmelding Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8459-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="c8459-112">Als u meer informatie over de software als een dienst (SaaS)-app-integratie met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c8459-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8459-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c8459-113">Prerequisites</span></span>
<span data-ttu-id="c8459-114">Azure AD-integratie met Clarizen tooconfigure, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="c8459-114">tooconfigure Azure AD integration with Clarizen, you need hello following items:</span></span>

- <span data-ttu-id="c8459-115">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c8459-115">An Azure AD subscription</span></span>
- <span data-ttu-id="c8459-116">Een Clarizen-abonnement dat ingeschakeld voor eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c8459-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="c8459-117">tootest hello stappen in deze zelfstudie volgt u deze aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="c8459-117">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="c8459-118">Eenmalige aanmelding Azure AD testen in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c8459-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c8459-119">Gebruik niet uw productieomgeving, tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c8459-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c8459-120">Als u een Azure AD-testomgeving geen hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c8459-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-hello-gallery"></a><span data-ttu-id="c8459-121">Clarizen van Hallo galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="c8459-121">Add Clarizen from hello gallery</span></span>
<span data-ttu-id="c8459-122">tooconfigure hello integratie van Clarizen in Azure AD Clarizen uit Hallo galerie tooyour lijst met beheerde SaaS-apps toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c8459-122">tooconfigure hello integration of Clarizen into Azure AD, add Clarizen from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="c8459-123">In Hallo [Azure-portal](https://portal.azure.com), in linkerdeelvenster hello, klik op Hallo **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c8459-123">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory-pictogram][1]

2. <span data-ttu-id="c8459-125">Klik op **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c8459-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="c8459-126">Klik vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c8459-126">Then click **All applications**.</span></span>

    ![Te klikken op 'Bedrijfstoepassingen' en 'Alle toepassingen'][2]

3. <span data-ttu-id="c8459-128">Klik op Hallo **toevoegen** knop Hallo boven aan het Hallo-dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c8459-128">Click hello **Add** button at hello top of hello dialog box.</span></span>

    ![de knop "Toevoegen" Hello][3]

4. <span data-ttu-id="c8459-130">Typ in het zoekvak Hallo **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="c8459-130">In hello search box, type **Clarizen**.</span></span>

    !['Clarizen' hello zoekvak te typen](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="c8459-132">Selecteer in het deelvenster met resultaten Hallo **Clarizen**, en klik vervolgens op **toevoegen** tooadd Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c8459-132">In hello results pane, select **Clarizen**, and then click **Add** tooadd hello application.</span></span>

    ![Clarizen selecteren in het resultatenvenster Hallo](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c8459-134">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8459-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="c8459-135">In de Hallo uit te voeren, configureren en testen eenmalige aanmelding Azure AD met Clarizen op basis van de testgebruiker Hallo Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c8459-135">In hello following sections, you configure and test Azure AD single sign-on with Clarizen based on hello test user Britta Simon.</span></span>

<span data-ttu-id="c8459-136">Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Clarizen is tooa gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8459-136">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clarizen is tooa user in Azure AD.</span></span> <span data-ttu-id="c8459-137">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Clarizen toobe tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="c8459-137">In other words, a link relationship between an Azure AD user and hello related user in Clarizen needs toobe established.</span></span> <span data-ttu-id="c8459-138">U de relatie van deze koppeling tot stand brengen door toe te wijzen Hallo-waarde van **gebruikersnaam** in Azure AD als Hallo-waarde van **gebruikersnaam** in Clarizen.</span><span class="sxs-lookup"><span data-stu-id="c8459-138">You establish this link relationship by assigning hello value of **user name** in Azure AD as hello value of **Username** in Clarizen.</span></span>

<span data-ttu-id="c8459-139">tooconfigure en eenmalige aanmelding Azure AD-test met Clarizen, volledige Hallo bouwstenen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c8459-139">tooconfigure and test Azure AD single sign-on with Clarizen, complete hello following building blocks:</span></span>

1. <span data-ttu-id="c8459-140">**[Eenmalige aanmelding Azure AD configureren](#configure-azure-ad-single-sign-on)**  tooenable uw toouse gebruikers deze functie.</span><span class="sxs-lookup"><span data-stu-id="c8459-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c8459-141">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  tootest eenmalige aanmelding Azure AD met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c8459-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c8459-142">**[Maak een testgebruiker Clarizen](#create-a-clarizen-test-user)**  toohave een equivalent van Britta Simon in Clarizen die is gekoppeld toohello Azure AD-weergave van haar.</span><span class="sxs-lookup"><span data-stu-id="c8459-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** toohave a counterpart of Britta Simon in Clarizen that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="c8459-143">**[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  tooenable Britta Simon toouse Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c8459-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c8459-144">**[Test eenmalige aanmelding](#test-single-sign-on)**  tooverify Hallo of configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c8459-144">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c8459-145">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c8459-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="c8459-146">Schakel Azure AD eenmalige aanmelding in hello Azure-portal en configureer eenmalige aanmelding in uw toepassing Clarizen.</span><span class="sxs-lookup"><span data-stu-id="c8459-146">Enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="c8459-147">In de Azure-portal op Hallo Hallo **Clarizen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c8459-147">In hello Azure portal, on hello **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![Te klikken op "Single sign-on"][4]

2. <span data-ttu-id="c8459-149">In Hallo **eenmalige aanmelding** in het dialoogvenster voor **modus**, selecteer **op basis van SAML aanmelding** tooenable eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c8459-149">In hello **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** tooenable single sign-on.</span></span>

    !['Op basis van SAML aanmelding' selecteren](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="c8459-151">In Hallo **Clarizen domein en de URL's** sectie, voert u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c8459-151">In hello **Clarizen Domain and URLs** section, perform hello following steps:</span></span>

    ![Dialoogvensters voor id en de antwoord-URL](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="c8459-153">a.</span><span class="sxs-lookup"><span data-stu-id="c8459-153">a.</span></span> <span data-ttu-id="c8459-154">In Hallo **id** vak Hallo typewaarde als: **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="c8459-154">In hello **Identifier** box, type hello value as: **Clarizen**</span></span>

    <span data-ttu-id="c8459-155">b.</span><span class="sxs-lookup"><span data-stu-id="c8459-155">b.</span></span> <span data-ttu-id="c8459-156">In Hallo **antwoord-URL** typt u een URL met behulp van Hallo patroon volgen: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="c8459-156">In hello **Reply URL** box, type a URL by using hello following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="c8459-157">Deze zijn niet Hallo echte waarden.</span><span class="sxs-lookup"><span data-stu-id="c8459-157">These are not hello real values.</span></span> <span data-ttu-id="c8459-158">U hebt toouse Hallo werkelijke id en antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="c8459-158">You have toouse hello actual identifier and reply URL.</span></span> <span data-ttu-id="c8459-159">Hier is het raadzaam Hallo unieke waarde van een tekenreeks te gebruiken, zoals id Hallo.</span><span class="sxs-lookup"><span data-stu-id="c8459-159">Here we suggest that you use hello unique value of a string as hello identifier.</span></span> <span data-ttu-id="c8459-160">tooget Werkelijke waarden, neem contact op met Hallo Hallo [Clarizen ondersteuningsteam](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="c8459-160">tooget hello actual values, contact hello [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="c8459-161">Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **nieuw certificaat maken**.</span><span class="sxs-lookup"><span data-stu-id="c8459-161">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Te klikken op 'Nieuw certificaat maken'](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="c8459-163">In Hallo **nieuw certificaat maken** dialoogvenster, klikt u op het pictogram Kalender Hallo en kiest u een vervaldatum.</span><span class="sxs-lookup"><span data-stu-id="c8459-163">In hello **Create New Certificate** dialog box, click hello calendar icon and select an expiry date.</span></span> <span data-ttu-id="c8459-164">Klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c8459-164">Then click **Save**.</span></span>

    ![Selecteren en een vervaldatum opslaan](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="c8459-166">In Hallo **SAML-certificaat voor ondertekening van** sectie **nieuwe certificaat activeren**, en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c8459-166">In hello **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Als u het selectievakje Hallo voor het nieuwe certificaat Hallo actief maken](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="c8459-168">In Hallo **rollovercertificaat** in het dialoogvenster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c8459-168">In hello **Rollover certificate** dialog box, click **OK**.</span></span>

    ![Te klikken op 'OK' tooconfirm die u toomake Hallo certificaat active wilt](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c8459-170">In Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c8459-170">In hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    !['Certificaat (Base64)' toostart Hallo downloaden te klikken op](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="c8459-172">In Hallo **Clarizen configuratie** sectie, klikt u op **configureren Clarizen** tooopen hello **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="c8459-172">In hello **Clarizen Configuration** section, click **Configure Clarizen** tooopen hello **Configure sign-on** window.</span></span>

    ![Te klikken op 'Clarizen configureren'](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    !['Configureren aanmelding' venster, inclusief URL's en bestanden](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="c8459-175">Meld u tooyour Clarizen bedrijf site als een beheerder in een ander browservenster.</span><span class="sxs-lookup"><span data-stu-id="c8459-175">In a different web browser window, sign in tooyour Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="c8459-176">Klik op uw gebruikersnaam en klik vervolgens op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="c8459-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="c8459-177">![Te klikken op 'Instellingen' onder uw gebruikersnaam](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="c8459-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="c8459-178">Klik op Hallo **globale instellingen** tabblad. Vervolgens volgende te**Federated Authentication**, klikt u op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="c8459-178">Click hello **Global Settings** tab. Then, next too**Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="c8459-179">![Tabblad 'Globale instellingen'](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "globale instellingen")</span><span class="sxs-lookup"><span data-stu-id="c8459-179">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="c8459-180">In Hallo **Federated Authentication** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c8459-180">In hello **Federated Authentication** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="c8459-181">![In het dialoogvenster 'Federated Authentication'](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span><span class="sxs-lookup"><span data-stu-id="c8459-181">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="c8459-182">a.</span><span class="sxs-lookup"><span data-stu-id="c8459-182">a.</span></span> <span data-ttu-id="c8459-183">Selecteer **inschakelen voor federatieve verificatie**.</span><span class="sxs-lookup"><span data-stu-id="c8459-183">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="c8459-184">b.</span><span class="sxs-lookup"><span data-stu-id="c8459-184">b.</span></span> <span data-ttu-id="c8459-185">Klik op **uploaden** tooupload uw gedownloade certificaat.</span><span class="sxs-lookup"><span data-stu-id="c8459-185">Click **Upload** tooupload your downloaded certificate.</span></span>

    <span data-ttu-id="c8459-186">c.</span><span class="sxs-lookup"><span data-stu-id="c8459-186">c.</span></span> <span data-ttu-id="c8459-187">In Hallo **aanmelden URL** Voer Hallo-waarde van **SAML Single Sign-On Service-URL** van venster hello Azure AD-toepassing-configuratie.</span><span class="sxs-lookup"><span data-stu-id="c8459-187">In hello **Sign-in URL** box, enter hello value of **SAML Single Sign-On Service URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="c8459-188">d.</span><span class="sxs-lookup"><span data-stu-id="c8459-188">d.</span></span> <span data-ttu-id="c8459-189">In Hallo **Sign-out URL** Voer Hallo-waarde van **Sign-Out URL** van venster hello Azure AD-toepassing-configuratie.</span><span class="sxs-lookup"><span data-stu-id="c8459-189">In hello **Sign-out URL** box, enter hello value of **Sign-Out URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="c8459-190">e.</span><span class="sxs-lookup"><span data-stu-id="c8459-190">e.</span></span> <span data-ttu-id="c8459-191">Selecteer **POST gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="c8459-191">Select **Use POST**.</span></span>

    <span data-ttu-id="c8459-192">f.</span><span class="sxs-lookup"><span data-stu-id="c8459-192">f.</span></span> <span data-ttu-id="c8459-193">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c8459-193">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c8459-194">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c8459-194">Create an Azure AD test user</span></span>
<span data-ttu-id="c8459-195">In hello Azure-portal, maakt u een testgebruiker Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c8459-195">In hello Azure portal, create a test user called Britta Simon.</span></span>

![Naam en e-mailadres van de testgebruiker hello Azure AD][100]

1. <span data-ttu-id="c8459-197">Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c8459-197">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory-pictogram](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c8459-199">Klik op **gebruikers en groepen**, en klik vervolgens op **alle gebruikers** toodisplay Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c8459-199">Click **Users and groups**, and then click **All users** toodisplay hello list of users.</span></span>

    ![Te klikken op 'Gebruikers en groepen' en 'Alle gebruikers'](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c8459-201">Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c8459-201">At hello top of hello dialog box, click **Add** tooopen hello **User** dialog box.</span></span>

    ![de knop "Toevoegen" Hello](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c8459-203">In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c8459-203">In hello **User** dialog box, perform hello following steps:</span></span>

    ![In het dialoogvenster met de naam, e-mailadres en wachtwoord 'Gebruiker' ingevuld](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c8459-205">a.</span><span class="sxs-lookup"><span data-stu-id="c8459-205">a.</span></span> <span data-ttu-id="c8459-206">In Hallo **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c8459-206">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c8459-207">b.</span><span class="sxs-lookup"><span data-stu-id="c8459-207">b.</span></span> <span data-ttu-id="c8459-208">In Hallo **gebruikersnaam** vak type Hallo e-mailadres van Hallo Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="c8459-208">In hello **User name** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="c8459-209">c.</span><span class="sxs-lookup"><span data-stu-id="c8459-209">c.</span></span> <span data-ttu-id="c8459-210">Selecteer **wachtwoord weergeven** en noteer de waarde Hallo van **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c8459-210">Select **Show Password** and write down hello value of **Password**.</span></span>

    <span data-ttu-id="c8459-211">d.</span><span class="sxs-lookup"><span data-stu-id="c8459-211">d.</span></span> <span data-ttu-id="c8459-212">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c8459-212">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="c8459-213">Een testgebruiker Clarizen maken</span><span class="sxs-lookup"><span data-stu-id="c8459-213">Create a Clarizen test user</span></span>
<span data-ttu-id="c8459-214">Azure AD gebruikers toosign tooenable in tooClarizen, moet u gebruikersaccounts inrichten.</span><span class="sxs-lookup"><span data-stu-id="c8459-214">tooenable Azure AD users toosign in tooClarizen, you must provision user accounts.</span></span> <span data-ttu-id="c8459-215">In geval van Clarizen Hallo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="c8459-215">In hello case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="c8459-216">Meld u tooyour Clarizen bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c8459-216">Sign in tooyour Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="c8459-217">Klik op **mensen**.</span><span class="sxs-lookup"><span data-stu-id="c8459-217">Click **People**.</span></span>

    <span data-ttu-id="c8459-218">![Te klikken op 'Mensen'](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "personen")</span><span class="sxs-lookup"><span data-stu-id="c8459-218">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="c8459-219">Klik op **gebruiker uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="c8459-219">Click **Invite User**.</span></span>

    <span data-ttu-id="c8459-220">![Knop 'Gebruiker uitnodigen'](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "gebruikers uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="c8459-220">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="c8459-221">In Hallo **personen uitnodigen** dialoogvenster Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c8459-221">In hello **Invite People** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="c8459-222">![Dialoogvenster 'Personen uitnodigen'](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "personen uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="c8459-222">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="c8459-223">a.</span><span class="sxs-lookup"><span data-stu-id="c8459-223">a.</span></span> <span data-ttu-id="c8459-224">In Hallo **e** vak type Hallo e-mailadres van Hallo Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="c8459-224">In hello **Email** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="c8459-225">b.</span><span class="sxs-lookup"><span data-stu-id="c8459-225">b.</span></span> <span data-ttu-id="c8459-226">Klik op **uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="c8459-226">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c8459-227">Hello Azure Active Directory-accounthouder wordt een e-mailbericht ontvangen en volg een koppeling tooconfirm hun account maken voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="c8459-227">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c8459-228">Toewijzen van de testgebruiker hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8459-228">Assign hello Azure AD test user</span></span>
<span data-ttu-id="c8459-229">Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooClarizen toegang verlenen.</span><span class="sxs-lookup"><span data-stu-id="c8459-229">Enable Britta Simon toouse Azure single sign-on by granting her access tooClarizen.</span></span>

![Toegewezen testgebruiker][200]

1. <span data-ttu-id="c8459-231">In hello Azure-portal, Hallo toepassingen weergave opent, blader toohello directory weergeven, klikt u op **bedrijfstoepassingen**, en klik vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c8459-231">In hello Azure portal, open hello applications view, browse toohello directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![Te klikken op 'Bedrijfstoepassingen' en 'Alle toepassingen'][201]

2. <span data-ttu-id="c8459-233">Selecteer in de lijst met de toepassingen van Hallo **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="c8459-233">In hello applications list, select **Clarizen**.</span></span>

    ![Clarizen selecteren in lijst Hallo](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="c8459-235">Klik in het linkerdeelvenster Hallo **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c8459-235">In hello left pane, click **Users and groups**.</span></span>

    ![Te klikken op 'Gebruikers en groepen'][202]

4. <span data-ttu-id="c8459-237">Klik op Hallo **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c8459-237">Click hello **Add** button.</span></span> <span data-ttu-id="c8459-238">Klik op Hallo **toevoegen toewijzing** dialoogvenster, **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c8459-238">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Hallo "Toevoegen" knop en Hallo 'Toewijzing toevoegen' dialoogvenster][203]

5. <span data-ttu-id="c8459-240">In Hallo **gebruikers en groepen** dialoogvenster, **Britta Simon** in Hallo lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c8459-240">In hello **Users and groups** dialog box, select **Britta Simon** in hello list of users.</span></span>

6. <span data-ttu-id="c8459-241">In Hallo **gebruikers en groepen** dialoogvenster vak, klikt u op Hallo **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="c8459-241">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="c8459-242">In Hallo **toevoegen toewijzing** dialoogvenster vak, klikt u op Hallo **toewijzen** knop.</span><span class="sxs-lookup"><span data-stu-id="c8459-242">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="c8459-243">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c8459-243">Test single sign-on</span></span>
<span data-ttu-id="c8459-244">Test uw configuratie Azure AD eenmalige aanmelding met Hallo Toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="c8459-244">Test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="c8459-245">Wanneer u Hallo Clarizen tegel in Hallo toegangsvenster klikt, moet u tooyour Clarizen toepassing automatisch worden aangemeld.</span><span class="sxs-lookup"><span data-stu-id="c8459-245">When you click hello Clarizen tile in hello Access Panel, you should be automatically signed in tooyour Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c8459-246">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c8459-246">Additional resources</span></span>

* [<span data-ttu-id="c8459-247">Lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c8459-247">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c8459-248">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c8459-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
