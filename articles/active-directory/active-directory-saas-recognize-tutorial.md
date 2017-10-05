---
title: 'Zelfstudie: Azure Active Directory-integratie met herkennen | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en herkennen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 97d85183d0307c41a3b879d440d87a6fb0c53190
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="92c94-103">Zelfstudie: Azure Active Directory-integratie met herkennen</span><span class="sxs-lookup"><span data-stu-id="92c94-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="92c94-104">In deze zelfstudie leert u hoe herkennen integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="92c94-104">In this tutorial, you learn how to integrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92c94-105">Herkennen integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="92c94-105">Integrating Recognize with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="92c94-106">U kunt beheren in Azure AD die toegang tot herkennen heeft</span><span class="sxs-lookup"><span data-stu-id="92c94-106">You can control in Azure AD who has access to Recognize</span></span>
- <span data-ttu-id="92c94-107">U kunt uw gebruikers automatisch ophalen aangemeld bij herkennen (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="92c94-107">You can enable your users to automatically get signed-on to Recognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92c94-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="92c94-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="92c94-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92c94-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92c94-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="92c94-110">Prerequisites</span></span>

<span data-ttu-id="92c94-111">Voor het configureren van Azure AD-integratie met herkennen, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="92c94-111">To configure Azure AD integration with Recognize, you need the following items:</span></span>

- <span data-ttu-id="92c94-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="92c94-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92c94-113">Een herkennen eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="92c94-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92c94-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="92c94-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92c94-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="92c94-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92c94-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="92c94-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="92c94-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92c94-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92c94-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="92c94-118">Scenario description</span></span>
<span data-ttu-id="92c94-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="92c94-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92c94-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="92c94-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92c94-121">Herkennen in de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="92c94-121">Adding Recognize from the gallery</span></span>
2. <span data-ttu-id="92c94-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="92c94-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-the-gallery"></a><span data-ttu-id="92c94-123">Herkennen in de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="92c94-123">Adding Recognize from the gallery</span></span>
<span data-ttu-id="92c94-124">Voor het configureren van de integratie van herkennen in Azure AD, moet u herkennen in de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="92c94-124">To configure the integration of Recognize into Azure AD, you need to add Recognize from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="92c94-125">**Om te herkennen in de galerie toevoegen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="92c94-125">**To add Recognize from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="92c94-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="92c94-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="92c94-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="92c94-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="92c94-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="92c94-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="92c94-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="92c94-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="92c94-133">Typ in het zoekvak **herkennen**.</span><span class="sxs-lookup"><span data-stu-id="92c94-133">In the search box, type **Recognize**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. <span data-ttu-id="92c94-135">Selecteer in het deelvenster resultaten **herkennen**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="92c94-135">In the results panel, select **Recognize**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92c94-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="92c94-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92c94-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met herkennen op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="92c94-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="92c94-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in herkennen is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92c94-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Recognize is to a user in Azure AD.</span></span> <span data-ttu-id="92c94-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in herkennen tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="92c94-140">In other words, a link relationship between an Azure AD user and the related user in Recognize needs to be established.</span></span>

<span data-ttu-id="92c94-141">Wijs in herkennen, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="92c94-141">In Recognize, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="92c94-142">Om te configureren en testen van Azure AD eenmalige aanmelding met herkennen, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="92c94-142">To configure and test Azure AD single sign-on with Recognize, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="92c94-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="92c94-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="92c94-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92c94-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92c94-145">**[Maken van een testgebruiker herkennen](#creating-a-recognize-test-user)**  - herkennen die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="92c94-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - to have a counterpart of Britta Simon in Recognize that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="92c94-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="92c94-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92c94-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="92c94-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92c94-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="92c94-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92c94-149">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing herkennen.</span><span class="sxs-lookup"><span data-stu-id="92c94-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="92c94-150">**Voor het configureren van Azure AD eenmalige aanmelding met herkennen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="92c94-150">**To configure Azure AD single sign-on with Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="92c94-151">In de Azure-portal op de **herkennen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="92c94-151">In the Azure portal, on the **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="92c94-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="92c94-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. <span data-ttu-id="92c94-155">Op de **domein herkennen en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="92c94-155">On the **Recognize Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="92c94-157">a.</span><span class="sxs-lookup"><span data-stu-id="92c94-157">a.</span></span> <span data-ttu-id="92c94-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://recognizeapp.com/<your-domain>/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="92c94-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="92c94-159">b.</span><span class="sxs-lookup"><span data-stu-id="92c94-159">b.</span></span> <span data-ttu-id="92c94-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://recognizeapp.com/<your-domain>`</span><span class="sxs-lookup"><span data-stu-id="92c94-160">In the **Identifier** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="92c94-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="92c94-161">These values are not real.</span></span> <span data-ttu-id="92c94-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="92c94-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="92c94-163">Neem contact op met [Client herkennen support team](mailto:support@recognizeapp.com) ophalen aanmeldings-URL en u de id-waarde kunt ophalen door het openen van metagegevens van de URL van de Provider van de sectie instellingen voor eenmalige aanmelding die verderop in de zelfstudie wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="92c94-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening the Service Provider Metadata URL from the SSO Settings section that is explained later in the tutorial.</span></span> <span data-ttu-id="92c94-164">.</span><span class="sxs-lookup"><span data-stu-id="92c94-164">.</span></span> 
 
4. <span data-ttu-id="92c94-165">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="92c94-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. <span data-ttu-id="92c94-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="92c94-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="92c94-169">Op de **herkent Configuration** sectie, klikt u op **configureren herkennen** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="92c94-169">On the **Recognize Configuration** section, click **Configure Recognize** to open **Configure sign-on** window.</span></span> <span data-ttu-id="92c94-170">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="92c94-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. <span data-ttu-id="92c94-172">In een ander browservenster aanmelding bij uw tenant herkennen als beheerder.</span><span class="sxs-lookup"><span data-stu-id="92c94-172">In a different web browser window, sign-on to your Recognize tenant as an administrator.</span></span>

8. <span data-ttu-id="92c94-173">Klik in de rechterbovenhoek op **Menu**.</span><span class="sxs-lookup"><span data-stu-id="92c94-173">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="92c94-174">Ga naar **Admin bedrijf**.</span><span class="sxs-lookup"><span data-stu-id="92c94-174">Go to **Company Admin**.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. <span data-ttu-id="92c94-176">Klik in het navigatiedeelvenster links op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="92c94-176">On the left navigation pane, click **Settings**.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. <span data-ttu-id="92c94-178">Voer de volgende stappen uit op **SSO instellingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="92c94-178">Perform the following steps on **SSO Settings** section.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="92c94-180">a.</span><span class="sxs-lookup"><span data-stu-id="92c94-180">a.</span></span> <span data-ttu-id="92c94-181">Als **eenmalige aanmelding inschakelen**, selecteer **ON**.</span><span class="sxs-lookup"><span data-stu-id="92c94-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="92c94-182">b.</span><span class="sxs-lookup"><span data-stu-id="92c94-182">b.</span></span> <span data-ttu-id="92c94-183">In de **IDP entiteit-ID** textbox, plak de waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="92c94-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="92c94-184">c.</span><span class="sxs-lookup"><span data-stu-id="92c94-184">c.</span></span> <span data-ttu-id="92c94-185">In de **doel-url voor eenmalige aanmelding** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="92c94-185">In the **Sso target url** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="92c94-186">d.</span><span class="sxs-lookup"><span data-stu-id="92c94-186">d.</span></span> <span data-ttu-id="92c94-187">In de **Slo-doel-url** textbox, plak de waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="92c94-187">In the **Slo target url** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="92c94-188">e.</span><span class="sxs-lookup"><span data-stu-id="92c94-188">e.</span></span> <span data-ttu-id="92c94-189">Open uw gedownloade **certificaat (Base64)** bestand in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="92c94-189">Open your downloaded **Certificate (Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>
    
    <span data-ttu-id="92c94-190">f.</span><span class="sxs-lookup"><span data-stu-id="92c94-190">f.</span></span> <span data-ttu-id="92c94-191">Klik op de **instellingen opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="92c94-191">Click the **Save settings** button.</span></span> 

11. <span data-ttu-id="92c94-192">Naast de **SSO instellingen** sectie, Kopieer de URL onder **Service Provider metagegevens-url**.</span><span class="sxs-lookup"><span data-stu-id="92c94-192">Beside the **SSO Settings** section, copy the URL under **Service Provider Metadata url**.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. <span data-ttu-id="92c94-194">Open de **metagegevens-URL koppeling** onder een lege browser voor het downloaden van het metagegevensdocument.</span><span class="sxs-lookup"><span data-stu-id="92c94-194">Open the **Metadata URL link** under a blank browser to download the metadata document.</span></span> <span data-ttu-id="92c94-195">Vervolgens de value(entityID) EntityDescriptor uit het bestand kopiëren en plakken in **id** textbox in **sectie domein herkennen en URL's** op Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="92c94-195">Then copy the EntityDescriptor value(entityID) from the file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="92c94-197">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="92c94-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="92c94-198">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="92c94-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="92c94-199">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="92c94-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92c94-200">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="92c94-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="92c94-201">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="92c94-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="92c94-203">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="92c94-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="92c94-204">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="92c94-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="92c94-206">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="92c94-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="92c94-208">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="92c94-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="92c94-210">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="92c94-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="92c94-212">a.</span><span class="sxs-lookup"><span data-stu-id="92c94-212">a.</span></span> <span data-ttu-id="92c94-213">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92c94-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92c94-214">b.</span><span class="sxs-lookup"><span data-stu-id="92c94-214">b.</span></span> <span data-ttu-id="92c94-215">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="92c94-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="92c94-216">c.</span><span class="sxs-lookup"><span data-stu-id="92c94-216">c.</span></span> <span data-ttu-id="92c94-217">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="92c94-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="92c94-218">d.</span><span class="sxs-lookup"><span data-stu-id="92c94-218">d.</span></span> <span data-ttu-id="92c94-219">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="92c94-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="92c94-220">Maken van een testgebruiker herkennen</span><span class="sxs-lookup"><span data-stu-id="92c94-220">Creating a Recognize test user</span></span>

<span data-ttu-id="92c94-221">Om in te schakelen gebruikers aan te melden bij het herkennen van Azure AD, moeten ze worden ingericht in herkennen.</span><span class="sxs-lookup"><span data-stu-id="92c94-221">In order to enable Azure AD users to log into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="92c94-222">In het geval van herkennen is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="92c94-222">In the case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="92c94-223">Deze app biedt geen ondersteuning voor het inrichten van SCIM, maar heeft een andere gebruiker synchronisatie die gebruikers richt.</span><span class="sxs-lookup"><span data-stu-id="92c94-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="92c94-224">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="92c94-224">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="92c94-225">Meld u aan bij uw bedrijf herkennen site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="92c94-225">Log into your Recognize company site as an administrator.</span></span>

2. <span data-ttu-id="92c94-226">Klik in de rechterbovenhoek op **Menu**.</span><span class="sxs-lookup"><span data-stu-id="92c94-226">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="92c94-227">Ga naar **Admin bedrijf**.</span><span class="sxs-lookup"><span data-stu-id="92c94-227">Go to **Company Admin**.</span></span>

3. <span data-ttu-id="92c94-228">Klik in het navigatiedeelvenster links op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="92c94-228">On the left navigation pane, click **Settings**.</span></span>

4. <span data-ttu-id="92c94-229">Voer de volgende stappen uit op **gebruiker Sync** sectie.</span><span class="sxs-lookup"><span data-stu-id="92c94-229">Perform the following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="92c94-230">![Nieuwe gebruiker](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="92c94-230">![New User](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="92c94-231">a.</span><span class="sxs-lookup"><span data-stu-id="92c94-231">a.</span></span> <span data-ttu-id="92c94-232">Als **synchroniseren ingeschakeld**, selecteer **ON**.</span><span class="sxs-lookup"><span data-stu-id="92c94-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="92c94-233">b.</span><span class="sxs-lookup"><span data-stu-id="92c94-233">b.</span></span> <span data-ttu-id="92c94-234">Als **Kies sync provider**, selecteer **Microsoft / Office 365**.</span><span class="sxs-lookup"><span data-stu-id="92c94-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="92c94-235">c.</span><span class="sxs-lookup"><span data-stu-id="92c94-235">c.</span></span> <span data-ttu-id="92c94-236">Klik op **Voer gebruiker synchronisatie**.</span><span class="sxs-lookup"><span data-stu-id="92c94-236">Click **Run User Sync**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="92c94-237">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="92c94-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="92c94-238">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan herkennen.</span><span class="sxs-lookup"><span data-stu-id="92c94-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Recognize.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="92c94-240">**Britta Simon om aan te wijzen herkennen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="92c94-240">**To assign Britta Simon to Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="92c94-241">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="92c94-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="92c94-243">Selecteer in de lijst met toepassingen **herkennen**.</span><span class="sxs-lookup"><span data-stu-id="92c94-243">In the applications list, select **Recognize**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. <span data-ttu-id="92c94-245">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="92c94-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="92c94-247">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="92c94-247">Click **Add** button.</span></span> <span data-ttu-id="92c94-248">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="92c94-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="92c94-250">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="92c94-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="92c94-251">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="92c94-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="92c94-252">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="92c94-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="92c94-253">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="92c94-253">Testing single sign-on</span></span>

<span data-ttu-id="92c94-254">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="92c94-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="92c94-255">Als u op de tegel herkennen in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing herkennen.</span><span class="sxs-lookup"><span data-stu-id="92c94-255">When you click the Recognize tile in the Access Panel, you should get automatically signed-on to your Recognize application.</span></span> <span data-ttu-id="92c94-256">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="92c94-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92c94-257">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="92c94-257">Additional resources</span></span>

* [<span data-ttu-id="92c94-258">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92c94-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92c94-259">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="92c94-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

