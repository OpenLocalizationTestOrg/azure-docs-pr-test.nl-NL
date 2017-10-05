---
title: 'Zelfstudie: Azure Active Directory-integratie met Clarizen | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Clarizen.
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
ms.openlocfilehash: 574c6877bddac8be7d6d541bfabbdc10f6be3101
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="b60b6-103">Zelfstudie: Azure Active Directory-integratie met Clarizen</span><span class="sxs-lookup"><span data-stu-id="b60b6-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="b60b6-104">In deze zelfstudie leert u het integreren van Azure Active Directory (Azure AD) met Clarizen.</span><span class="sxs-lookup"><span data-stu-id="b60b6-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="b60b6-105">Deze integratie biedt u de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b60b6-105">This integration gives you the following benefits:</span></span>

- <span data-ttu-id="b60b6-106">U kunt beheren, in Azure AD, die toegang tot Clarizen heeft.</span><span class="sxs-lookup"><span data-stu-id="b60b6-106">You can control, in Azure AD, who has access to Clarizen.</span></span>
- <span data-ttu-id="b60b6-107">U kunt uw gebruikers automatisch worden aangemeld bij Clarizen (eenmalige aanmelding) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b60b6-107">You can enable your users to be automatically signed in to Clarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b60b6-108">U kunt uw accounts op één centrale locatie, de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="b60b6-108">You can manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="b60b6-109">Het scenario in deze zelfstudie bestaat uit twee belangrijke taken:</span><span class="sxs-lookup"><span data-stu-id="b60b6-109">The scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="b60b6-110">Clarizen uit de galerie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b60b6-110">Add Clarizen from the gallery.</span></span>
2. <span data-ttu-id="b60b6-111">Configureren en testen eenmalige aanmelding Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b60b6-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="b60b6-112">Als u meer informatie over de software als een dienst (SaaS)-app-integratie met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b60b6-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b60b6-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b60b6-113">Prerequisites</span></span>
<span data-ttu-id="b60b6-114">Voor het configureren van Azure AD-integratie met Clarizen, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b60b6-114">To configure Azure AD integration with Clarizen, you need the following items:</span></span>

- <span data-ttu-id="b60b6-115">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b60b6-115">An Azure AD subscription</span></span>
- <span data-ttu-id="b60b6-116">Een Clarizen-abonnement dat ingeschakeld voor eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b60b6-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="b60b6-117">Test de stappen in deze zelfstudie, volgt u deze aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="b60b6-117">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="b60b6-118">Eenmalige aanmelding Azure AD testen in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b60b6-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b60b6-119">Gebruik niet uw productieomgeving, tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b60b6-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b60b6-120">Als u een Azure AD-testomgeving geen hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b60b6-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-the-gallery"></a><span data-ttu-id="b60b6-121">Clarizen uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b60b6-121">Add Clarizen from the gallery</span></span>
<span data-ttu-id="b60b6-122">Voor het configureren van de integratie van Clarizen in Azure AD Clarizen uit de galerie te toevoegt aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b60b6-122">To configure the integration of Clarizen into Azure AD, add Clarizen from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="b60b6-123">In de [Azure-portal](https://portal.azure.com), in het linkerdeelvenster klikt u op de **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b60b6-123">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory-pictogram][1]

2. <span data-ttu-id="b60b6-125">Klik op **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="b60b6-126">Klik vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-126">Then click **All applications**.</span></span>

    ![Te klikken op 'Bedrijfstoepassingen' en 'Alle toepassingen'][2]

3. <span data-ttu-id="b60b6-128">Klik op de **toevoegen** knop aan de bovenkant van het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b60b6-128">Click the **Add** button at the top of the dialog box.</span></span>

    ![De knop "Toevoegen"][3]

4. <span data-ttu-id="b60b6-130">Typ in het zoekvak **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-130">In the search box, type **Clarizen**.</span></span>

    !['Clarizen' in het zoekvak te typen](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="b60b6-132">Selecteer in het deelvenster met resultaten **Clarizen**, en klik vervolgens op **toevoegen** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b60b6-132">In the results pane, select **Clarizen**, and then click **Add** to add the application.</span></span>

    ![Clarizen selecteren in het deelvenster met resultaten](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b60b6-134">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="b60b6-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b60b6-135">In de volgende secties die u kunt configureren en testen eenmalige aanmelding Azure AD met Clarizen op basis van de testgebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b60b6-135">In the following sections, you configure and test Azure AD single sign-on with Clarizen based on the test user Britta Simon.</span></span>

<span data-ttu-id="b60b6-136">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Clarizen is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b60b6-136">For single sign-on to work, Azure AD needs to know what the counterpart user in Clarizen is to a user in Azure AD.</span></span> <span data-ttu-id="b60b6-137">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Clarizen tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="b60b6-137">In other words, a link relationship between an Azure AD user and the related user in Clarizen needs to be established.</span></span> <span data-ttu-id="b60b6-138">U de relatie van deze koppeling tot stand brengen door toe te wijzen de waarde van **gebruikersnaam** in Azure AD als de waarde van **gebruikersnaam** in Clarizen.</span><span class="sxs-lookup"><span data-stu-id="b60b6-138">You establish this link relationship by assigning the value of **user name** in Azure AD as the value of **Username** in Clarizen.</span></span>

<span data-ttu-id="b60b6-139">Als u wilt configureren en testen Azure AD eenmalige aanmelding met Clarizen, voert u de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="b60b6-139">To configure and test Azure AD single sign-on with Clarizen, complete the following building blocks:</span></span>

1. <span data-ttu-id="b60b6-140">**[Eenmalige aanmelding Azure AD configureren](#configure-azure-ad-single-sign-on)**  zodat uw gebruikers om deze functie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b60b6-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b60b6-141">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b60b6-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b60b6-142">**[Maak een testgebruiker Clarizen](#create-a-clarizen-test-user)**  Clarizen die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="b60b6-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** to have a counterpart of Britta Simon in Clarizen that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="b60b6-143">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b60b6-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b60b6-144">**[Test eenmalige aanmelding](#test-single-sign-on)**  om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b60b6-144">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b60b6-145">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b60b6-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="b60b6-146">Schakel Azure AD eenmalige aanmelding in de Azure portal en configureer eenmalige aanmelding in uw toepassing Clarizen.</span><span class="sxs-lookup"><span data-stu-id="b60b6-146">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="b60b6-147">In de Azure-portal op de **Clarizen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-147">In the Azure portal, on the **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![Te klikken op "Single sign-on"][4]

2. <span data-ttu-id="b60b6-149">In de **eenmalige aanmelding** in het dialoogvenster voor **modus**, selecteer **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b60b6-149">In the **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** to enable single sign-on.</span></span>

    !['Op basis van SAML aanmelding' selecteren](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="b60b6-151">In de **Clarizen domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b60b6-151">In the **Clarizen Domain and URLs** section, perform the following steps:</span></span>

    ![Dialoogvensters voor id en de antwoord-URL](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="b60b6-153">a.</span><span class="sxs-lookup"><span data-stu-id="b60b6-153">a.</span></span> <span data-ttu-id="b60b6-154">In de **id** typt u de waarde als: **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="b60b6-154">In the **Identifier** box, type the value as: **Clarizen**</span></span>

    <span data-ttu-id="b60b6-155">b.</span><span class="sxs-lookup"><span data-stu-id="b60b6-155">b.</span></span> <span data-ttu-id="b60b6-156">In de **antwoord-URL** typt u een URL met behulp van het volgende patroon volgen: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="b60b6-156">In the **Reply URL** box, type a URL by using the following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="b60b6-157">Deze zijn niet de werkelijke waarden.</span><span class="sxs-lookup"><span data-stu-id="b60b6-157">These are not the real values.</span></span> <span data-ttu-id="b60b6-158">U moet de werkelijke id gebruiken en antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="b60b6-158">You have to use the actual identifier and reply URL.</span></span> <span data-ttu-id="b60b6-159">Hier is het raadzaam dat u de unieke waarde van een tekenreeks als de id gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b60b6-159">Here we suggest that you use the unique value of a string as the identifier.</span></span> <span data-ttu-id="b60b6-160">Als u de werkelijke waarden, neem contact op met de [Clarizen ondersteuningsteam](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="b60b6-160">To get the actual values, contact the [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="b60b6-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **nieuw certificaat maken**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-161">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Te klikken op 'Nieuw certificaat maken'](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="b60b6-163">In de **nieuw certificaat maken** dialoogvenster, klikt u op het pictogram Agenda en kiest u een vervaldatum.</span><span class="sxs-lookup"><span data-stu-id="b60b6-163">In the **Create New Certificate** dialog box, click the calendar icon and select an expiry date.</span></span> <span data-ttu-id="b60b6-164">Klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-164">Then click **Save**.</span></span>

    ![Selecteren en een vervaldatum opslaan](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="b60b6-166">In de **SAML-certificaat voor ondertekening van** sectie **nieuwe certificaat activeren**, en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-166">In the **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Als u het selectievakje voor het nieuwe certificaat actief te maken](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="b60b6-168">In de **rollovercertificaat** in het dialoogvenster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-168">In the **Rollover certificate** dialog box, click **OK**.</span></span>

    ![Te klikken op 'OK' om te bevestigen dat u wilt activeren van het certificaat](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b60b6-170">In de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b60b6-170">In the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Te klikken op 'Certificate (Base64)"om het downloaden te starten](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="b60b6-172">In de **Clarizen configuratie** sectie, klikt u op **configureren Clarizen** openen de **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="b60b6-172">In the **Clarizen Configuration** section, click **Configure Clarizen** to open the **Configure sign-on** window.</span></span>

    ![Te klikken op 'Clarizen configureren'](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    !['Configureren aanmelding' venster, inclusief URL's en bestanden](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="b60b6-175">In een ander browservenster aanmelden bij uw bedrijf Clarizen site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b60b6-175">In a different web browser window, sign in to your Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="b60b6-176">Klik op uw gebruikersnaam en klik vervolgens op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="b60b6-177">![Te klikken op 'Instellingen' onder uw gebruikersnaam](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="b60b6-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="b60b6-178">Klik op de **globale instellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="b60b6-178">Click the **Global Settings** tab.</span></span> <span data-ttu-id="b60b6-179">Klik naast **Federated Authentication**, klikt u op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-179">Then, next to **Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="b60b6-180">![Tabblad 'Globale instellingen'](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "globale instellingen")</span><span class="sxs-lookup"><span data-stu-id="b60b6-180">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="b60b6-181">In de **Federated Authentication** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b60b6-181">In the **Federated Authentication** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="b60b6-182">![In het dialoogvenster 'Federated Authentication'](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span><span class="sxs-lookup"><span data-stu-id="b60b6-182">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="b60b6-183">a.</span><span class="sxs-lookup"><span data-stu-id="b60b6-183">a.</span></span> <span data-ttu-id="b60b6-184">Selecteer **inschakelen voor federatieve verificatie**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-184">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="b60b6-185">b.</span><span class="sxs-lookup"><span data-stu-id="b60b6-185">b.</span></span> <span data-ttu-id="b60b6-186">Klik op **uploaden** om uw gedownloade certificaat te uploaden.</span><span class="sxs-lookup"><span data-stu-id="b60b6-186">Click **Upload** to upload your downloaded certificate.</span></span>

    <span data-ttu-id="b60b6-187">c.</span><span class="sxs-lookup"><span data-stu-id="b60b6-187">c.</span></span> <span data-ttu-id="b60b6-188">In de **aanmelden URL** en voer de waarde van **SAML Single Sign-On Service-URL** van het Configuratievenster van Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b60b6-188">In the **Sign-in URL** box, enter the value of **SAML Single Sign-On Service URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="b60b6-189">d.</span><span class="sxs-lookup"><span data-stu-id="b60b6-189">d.</span></span> <span data-ttu-id="b60b6-190">In de **Sign-out URL** en voer de waarde van **Sign-Out URL** van het Configuratievenster van Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b60b6-190">In the **Sign-out URL** box, enter the value of **Sign-Out URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="b60b6-191">e.</span><span class="sxs-lookup"><span data-stu-id="b60b6-191">e.</span></span> <span data-ttu-id="b60b6-192">Selecteer **POST gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-192">Select **Use POST**.</span></span>

    <span data-ttu-id="b60b6-193">f.</span><span class="sxs-lookup"><span data-stu-id="b60b6-193">f.</span></span> <span data-ttu-id="b60b6-194">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-194">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b60b6-195">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b60b6-195">Create an Azure AD test user</span></span>
<span data-ttu-id="b60b6-196">Maak een testgebruiker Britta Simon aangeroepen in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b60b6-196">In the Azure portal, create a test user called Britta Simon.</span></span>

![Naam en e-mailadres van de testgebruiker Azure AD][100]

1. <span data-ttu-id="b60b6-198">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b60b6-198">In the Azure portal, in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory-pictogram](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b60b6-200">Klik op **gebruikers en groepen**, en klik vervolgens op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="b60b6-200">Click **Users and groups**, and then click **All users** to display the list of users.</span></span>

    ![Te klikken op 'Gebruikers en groepen' en 'Alle gebruikers'](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b60b6-202">Klik boven in het dialoogvenster op **toevoegen** openen de **gebruiker** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b60b6-202">At the top of the dialog box, click **Add** to open the **User** dialog box.</span></span>

    ![De knop "Toevoegen"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b60b6-204">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b60b6-204">In the **User** dialog box, perform the following steps:</span></span>

    ![In het dialoogvenster met de naam, e-mailadres en wachtwoord 'Gebruiker' ingevuld](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b60b6-206">a.</span><span class="sxs-lookup"><span data-stu-id="b60b6-206">a.</span></span> <span data-ttu-id="b60b6-207">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b60b6-208">b.</span><span class="sxs-lookup"><span data-stu-id="b60b6-208">b.</span></span> <span data-ttu-id="b60b6-209">In de **gebruikersnaam** typt u het e-mailadres van het account Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b60b6-209">In the **User name** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="b60b6-210">c.</span><span class="sxs-lookup"><span data-stu-id="b60b6-210">c.</span></span> <span data-ttu-id="b60b6-211">Selecteer **wachtwoord weergeven** en noteer de waarde van **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-211">Select **Show Password** and write down the value of **Password**.</span></span>

    <span data-ttu-id="b60b6-212">d.</span><span class="sxs-lookup"><span data-stu-id="b60b6-212">d.</span></span> <span data-ttu-id="b60b6-213">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-213">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="b60b6-214">Een testgebruiker Clarizen maken</span><span class="sxs-lookup"><span data-stu-id="b60b6-214">Create a Clarizen test user</span></span>
<span data-ttu-id="b60b6-215">Om Azure AD-gebruikers aan te melden bij Clarizen, moet u gebruikersaccounts inrichten.</span><span class="sxs-lookup"><span data-stu-id="b60b6-215">To enable Azure AD users to sign in to Clarizen, you must provision user accounts.</span></span> <span data-ttu-id="b60b6-216">In het geval van Clarizen is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="b60b6-216">In the case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="b60b6-217">Meld u aan bij uw bedrijf Clarizen site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b60b6-217">Sign in to your Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="b60b6-218">Klik op **mensen**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-218">Click **People**.</span></span>

    <span data-ttu-id="b60b6-219">![Te klikken op 'Mensen'](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "personen")</span><span class="sxs-lookup"><span data-stu-id="b60b6-219">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="b60b6-220">Klik op **gebruiker uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-220">Click **Invite User**.</span></span>

    <span data-ttu-id="b60b6-221">![Knop 'Gebruiker uitnodigen'](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "gebruikers uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="b60b6-221">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="b60b6-222">In de **personen uitnodigen** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b60b6-222">In the **Invite People** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="b60b6-223">![Dialoogvenster 'Personen uitnodigen'](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "personen uitnodigen")</span><span class="sxs-lookup"><span data-stu-id="b60b6-223">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="b60b6-224">a.</span><span class="sxs-lookup"><span data-stu-id="b60b6-224">a.</span></span> <span data-ttu-id="b60b6-225">In de **e** typt u het e-mailadres van het account Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b60b6-225">In the **Email** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="b60b6-226">b.</span><span class="sxs-lookup"><span data-stu-id="b60b6-226">b.</span></span> <span data-ttu-id="b60b6-227">Klik op **uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-227">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b60b6-228">De accounthouder Azure Active Directory wordt een e-mailbericht ontvangen en Ga als volgt een koppeling om hun account te bevestigen voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="b60b6-228">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b60b6-229">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="b60b6-229">Assign the Azure AD test user</span></span>
<span data-ttu-id="b60b6-230">Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan Clarizen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b60b6-230">Enable Britta Simon to use Azure single sign-on by granting her access to Clarizen.</span></span>

![Toegewezen testgebruiker][200]

1. <span data-ttu-id="b60b6-232">In de Azure portal, opent u de toepassingen weergeven, blader naar de directoryweergave, klikt u op **bedrijfstoepassingen**, en klik vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-232">In the Azure portal, open the applications view, browse to the directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![Te klikken op 'Bedrijfstoepassingen' en 'Alle toepassingen'][201]

2. <span data-ttu-id="b60b6-234">Selecteer in de lijst met toepassingen **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-234">In the applications list, select **Clarizen**.</span></span>

    ![Clarizen selecteren in de lijst](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="b60b6-236">Klik in het linkerdeelvenster op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-236">In the left pane, click **Users and groups**.</span></span>

    ![Te klikken op 'Gebruikers en groepen'][202]

4. <span data-ttu-id="b60b6-238">Klik op de **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b60b6-238">Click the **Add** button.</span></span> <span data-ttu-id="b60b6-239">Klik in de **toevoegen toewijzing** dialoogvenster, **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b60b6-239">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![De knop "Toevoegen" en het dialoogvenster 'Toewijzing toevoegen'][203]

5. <span data-ttu-id="b60b6-241">In de **gebruikers en groepen** dialoogvenster, **Britta Simon** in de lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b60b6-241">In the **Users and groups** dialog box, select **Britta Simon** in the list of users.</span></span>

6. <span data-ttu-id="b60b6-242">In de **gebruikers en groepen** in het dialoogvenster, klikt u op de **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="b60b6-242">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="b60b6-243">In de **toevoegen toewijzing** in het dialoogvenster, klikt u op de **toewijzen** knop.</span><span class="sxs-lookup"><span data-stu-id="b60b6-243">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="b60b6-244">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b60b6-244">Test single sign-on</span></span>
<span data-ttu-id="b60b6-245">Uw Azure AD eenmalige aanmelding configuratie testen met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="b60b6-245">Test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="b60b6-246">Als u op de tegel Clarizen in het deelvenster toegang, moet u worden automatisch aangemeld bij uw toepassing Clarizen.</span><span class="sxs-lookup"><span data-stu-id="b60b6-246">When you click the Clarizen tile in the Access Panel, you should be automatically signed in to your Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b60b6-247">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b60b6-247">Additional resources</span></span>

* [<span data-ttu-id="b60b6-248">Lijst met zelfstudies over het integreren van SaaS-apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b60b6-248">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b60b6-249">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b60b6-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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
