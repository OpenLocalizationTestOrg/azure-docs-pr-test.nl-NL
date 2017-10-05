---
title: 'Zelfstudie: Azure Active Directory-integratie met Questetra BPM Suite | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Questetra BPM Suite.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 7ae75446c9d19ce15a82caa9604658a528ab9941
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="87138-103">Zelfstudie: Azure Active Directory-integratie met Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="87138-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="87138-104">Er is het doel van deze zelfstudie leert u Questetra BPM Suite integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="87138-104">The objective of this tutorial is to show you how to integrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="87138-105">Questetra BPM Suite integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="87138-105">Integrating Questetra BPM Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="87138-106">U kunt beheren in Azure AD die toegang tot Questetra BPM Suite heeft</span><span class="sxs-lookup"><span data-stu-id="87138-106">You can control in Azure AD who has access to Questetra BPM Suite</span></span> 
* <span data-ttu-id="87138-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Questetra BPM Suite (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="87138-107">You can enable your users to automatically get signed-on to Questetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="87138-108">U kunt uw accounts op één centrale locatie - en de klassieke Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="87138-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="87138-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="87138-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87138-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="87138-110">Prerequisites</span></span>
<span data-ttu-id="87138-111">Voor het configureren van Azure AD-integratie met Questetra BPM Suite, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="87138-111">To configure Azure AD integration with Questetra BPM Suite, you need the following items:</span></span>

* <span data-ttu-id="87138-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="87138-112">An Azure AD subscription</span></span>
* <span data-ttu-id="87138-113">Een [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="87138-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="87138-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="87138-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="87138-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="87138-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="87138-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="87138-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="87138-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="87138-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="87138-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="87138-118">Scenario Description</span></span>
<span data-ttu-id="87138-119">Het doel van deze zelfstudie is zodat u kunt eenmalige aanmelding Azure AD te testen in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="87138-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="87138-120">Het scenario in deze zelfstudie bestaat uit drie belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="87138-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="87138-121">Questetra BPM Suite uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="87138-121">Adding Questetra BPM Suite from the gallery</span></span> 
2. <span data-ttu-id="87138-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="87138-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-the-gallery"></a><span data-ttu-id="87138-123">Questetra BPM Suite uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="87138-123">Adding Questetra BPM Suite from the gallery</span></span>
<span data-ttu-id="87138-124">Voor het configureren van de integratie van Questetra BPM Suite in Azure AD, moet u Questetra BPM Suite uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="87138-124">To configure the integration of Questetra BPM Suite into Azure AD, you need to add Questetra BPM Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="87138-125">**Als u wilt toevoegen Questetra BPM Suite uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="87138-125">**To add Questetra BPM Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="87138-126">In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="87138-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="87138-128">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="87138-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="87138-129">De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="87138-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Toepassingen][2]

4. <span data-ttu-id="87138-131">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="87138-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Toepassingen][3]

5. <span data-ttu-id="87138-133">Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.</span><span class="sxs-lookup"><span data-stu-id="87138-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Toepassingen][4]

6. <span data-ttu-id="87138-135">Typ in het zoekvak **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="87138-135">In the search box, type **Questetra BPM Suite**.</span></span>
   
    ![Toepassingen][5]

7. <span data-ttu-id="87138-137">Selecteer in het deelvenster met resultaten **Questetra BPM Suite**, en klik vervolgens op **Complete** de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="87138-137">In the results pane, select **Questetra BPM Suite**, and then click **Complete** to add the application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="87138-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="87138-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="87138-139">Het doel van deze sectie is het beschreven hoe u met het configureren en testen eenmalige aanmelding Azure AD met Questetra BPM Suite op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="87138-139">The objective of this section is to show you how to configure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="87138-140">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker van het bijbehorende equivalent in Questetra BPM Suite aan een gebruiker in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="87138-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Questetra BPM Suite to an user in Azure AD is.</span></span> <span data-ttu-id="87138-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Questetra BPM Suite tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="87138-141">In other words, a link relationship between an Azure AD user and the related user in Questetra BPM Suite needs to be established.</span></span>  
<span data-ttu-id="87138-142">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="87138-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="87138-143">Om te configureren en testen van Azure AD eenmalige aanmelding met Questetra BPM Suite, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="87138-143">To configure and test Azure AD single sign-on with Questetra BPM Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="87138-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="87138-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="87138-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="87138-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="87138-146">**[Maken van een testgebruiker Questetra BPM Suite](#creating-a-questetra-bpm-suite-test-user)**  - Questetra BPM Suite die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="87138-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - to have a counterpart of Britta Simon in Questetra BPM Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="87138-147">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="87138-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="87138-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="87138-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="87138-149">Azure AD voor eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="87138-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="87138-150">Het doel van deze sectie is Azure AD eenmalige aanmelding inschakelen in de klassieke Azure portal en eenmalige aanmelding configureren in uw toepassing Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="87138-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="87138-151">**Voor het configureren van Azure AD eenmalige aanmelding met Questetra BPM Suite, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="87138-151">**To configure Azure AD single sign-on with Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="87138-152">In de klassieke Azure-portal op de **Questetra BPM Suite** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren Single Sign-On** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="87138-152">In the Azure classic portal, on the **Questetra BPM Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Eenmalige aanmelding configureren][8]

2. <span data-ttu-id="87138-154">Op de **hoe wilt u dat gebruikers zich aanmelden op Questetra BPM Suite** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="87138-154">On the **How would you like users to sign on to Questetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][9]

3. <span data-ttu-id="87138-156">In een ander browservenster, meld u aan bij uw **Questetra BPM Suite** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="87138-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="87138-157">Klik in het menu bovenaan op **systeeminstellingen**.</span><span class="sxs-lookup"><span data-stu-id="87138-157">In the menu on the top, click **System Settings**.</span></span> 
   
    ![Azure AD voor eenmalige aanmelding][10]

5. <span data-ttu-id="87138-159">Openen van de **SingleSignOnSAML** pagina, klikt u op **eenmalige aanmelding (SAML)**.</span><span class="sxs-lookup"><span data-stu-id="87138-159">To open the **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Azure AD voor eenmalige aanmelding][11]

6. <span data-ttu-id="87138-161">In de klassieke Azure-portal op de **App-instellingen configureren** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="87138-161">In the Azure classic portal, on the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![App-instellingen configureren][13]
   
    <span data-ttu-id="87138-163">a.</span><span class="sxs-lookup"><span data-stu-id="87138-163">a.</span></span> <span data-ttu-id="87138-164">Op uw **Questetra BPM Suite** bedrijf site in de sectie SP gegevens kopiëren de **ACS URL**, en plak deze in de **aanmelding op URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="87138-164">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="87138-165">b.</span><span class="sxs-lookup"><span data-stu-id="87138-165">b.</span></span> <span data-ttu-id="87138-166">Op uw **Questetra BPM Suite** bedrijf site in de sectie SP gegevens kopiëren de **entiteit-ID**, en plak deze in de **URL-verlener** textbox.</span><span class="sxs-lookup"><span data-stu-id="87138-166">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **Entity ID**, and then paste it into the **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="87138-167">c.</span><span class="sxs-lookup"><span data-stu-id="87138-167">c.</span></span> <span data-ttu-id="87138-168">Op uw **Questetra BPM Suite** bedrijf site in de sectie SP gegevens kopiëren de **ACS URL**, en plak deze in de **antwoord-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="87138-168">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="87138-169">d.</span><span class="sxs-lookup"><span data-stu-id="87138-169">d.</span></span> <span data-ttu-id="87138-170">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="87138-170">Click **Next**.</span></span>

7. <span data-ttu-id="87138-171">Op de **op Questetra BPM Suite eenmalige aanmelding configureren** pagina, klikt u op **certificaat downloaden**, en sla het certificaatbestand lokaal op uw computer.</span><span class="sxs-lookup"><span data-stu-id="87138-171">On the **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Eenmalige aanmelding configureren][14]

8. <span data-ttu-id="87138-173">Op uw **Questetra BPM Suite** bedrijf site, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="87138-173">On you **Questetra BPM Suite** company site, perform the following steps:</span></span> 
   
    ![Eenmalige aanmelding configureren][15]
   
    <span data-ttu-id="87138-175">a.</span><span class="sxs-lookup"><span data-stu-id="87138-175">a.</span></span> <span data-ttu-id="87138-176">Selecteer **eenmalige aanmelding inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="87138-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="87138-177">b.</span><span class="sxs-lookup"><span data-stu-id="87138-177">b.</span></span> <span data-ttu-id="87138-178">Kopieer op de klassieke Azure portal, de **URL-verlener** waarde en plak deze in de **entiteit-ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="87138-178">On the Azure classic portal, copy the **Issuer URL** value, and then paste it into the **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="87138-179">c.</span><span class="sxs-lookup"><span data-stu-id="87138-179">c.</span></span> <span data-ttu-id="87138-180">Kopieer op de klassieke Azure portal, de **Single Sign-On Service-URL** waarde en plak deze in de **aanmelden pagina-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="87138-180">On the Azure classic portal, copy the **Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="87138-181">d.</span><span class="sxs-lookup"><span data-stu-id="87138-181">d.</span></span> <span data-ttu-id="87138-182">Kopieer op de klassieke Azure portal, de **Service-URL met eenmalige Sign-Out** waarde en plak deze in de **afmelden pagina-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="87138-182">On the Azure classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="87138-183">e.</span><span class="sxs-lookup"><span data-stu-id="87138-183">e.</span></span> <span data-ttu-id="87138-184">In de **NameID indeling** textbox type **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="87138-184">In the **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="87138-185">f.</span><span class="sxs-lookup"><span data-stu-id="87138-185">f.</span></span> <span data-ttu-id="87138-186">Maak een Base64-gecodeerde bestand uit het gedownloade certificaat.</span><span class="sxs-lookup"><span data-stu-id="87138-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="87138-187">Zie voor meer informatie [het converteren van een binaire certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="87138-187">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="87138-188">g.</span><span class="sxs-lookup"><span data-stu-id="87138-188">g.</span></span> <span data-ttu-id="87138-189">Open uw base-64 gecodeerde certificaat in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze in de **validatiecertificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="87138-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="87138-190">h.</span><span class="sxs-lookup"><span data-stu-id="87138-190">h.</span></span> <span data-ttu-id="87138-191">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="87138-191">Click **Save**.</span></span>

1. <span data-ttu-id="87138-192">Bij de klassieke Azure portal, selecteert u de configuratie voor één aanmelding bevestiging en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="87138-192">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Wat is Azure AD Connect?][17]

2. <span data-ttu-id="87138-194">Op de **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.</span><span class="sxs-lookup"><span data-stu-id="87138-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Wat is Azure AD Connect?][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="87138-196">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="87138-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="87138-197">Het doel van deze sectie is een testgebruiker maken in de klassieke Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="87138-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="87138-198">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="87138-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="87138-199">In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="87138-199">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD-testgebruiker maken][100] 

2. <span data-ttu-id="87138-201">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="87138-201">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="87138-202">De lijst met gebruikers, in het menu bovenaan, klikt u op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="87138-202">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Azure AD-testgebruiker maken][101] 

4. <span data-ttu-id="87138-204">Openen van de **gebruiker toevoegen** dialoogvenster op de werkbalk aan de onderkant, klikt u op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="87138-204">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Azure AD-testgebruiker maken][102] 

5. <span data-ttu-id="87138-206">Op de **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="87138-206">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Azure AD-testgebruiker maken][103]
   
    <span data-ttu-id="87138-208">a.</span><span class="sxs-lookup"><span data-stu-id="87138-208">a.</span></span> <span data-ttu-id="87138-209">Als **Type gebruiker**, selecteer **nieuwe gebruiker in uw organisatie**.</span><span class="sxs-lookup"><span data-stu-id="87138-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="87138-210">b.</span><span class="sxs-lookup"><span data-stu-id="87138-210">b.</span></span> <span data-ttu-id="87138-211">De gebruikersnaam **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="87138-211">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="87138-212">c.</span><span class="sxs-lookup"><span data-stu-id="87138-212">c.</span></span> <span data-ttu-id="87138-213">Klik op Volgende.</span><span class="sxs-lookup"><span data-stu-id="87138-213">Click Next.</span></span>

6. <span data-ttu-id="87138-214">Op de **gebruikersprofiel** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="87138-214">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Azure AD-testgebruiker maken][104] 
   
    <span data-ttu-id="87138-216">a.</span><span class="sxs-lookup"><span data-stu-id="87138-216">a.</span></span> <span data-ttu-id="87138-217">In de **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="87138-217">In the **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="87138-218">b.</span><span class="sxs-lookup"><span data-stu-id="87138-218">b.</span></span> <span data-ttu-id="87138-219">In de **achternaam** textbox type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="87138-219">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="87138-220">c.</span><span class="sxs-lookup"><span data-stu-id="87138-220">c.</span></span> <span data-ttu-id="87138-221">In de **weergavenaam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="87138-221">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="87138-222">d.</span><span class="sxs-lookup"><span data-stu-id="87138-222">d.</span></span> <span data-ttu-id="87138-223">In de **rol** selecteert **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="87138-223">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="87138-224">e.</span><span class="sxs-lookup"><span data-stu-id="87138-224">e.</span></span> <span data-ttu-id="87138-225">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="87138-225">Click **Next**.</span></span>

7. <span data-ttu-id="87138-226">Op de **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="87138-226">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD-testgebruiker maken][105]  

8. <span data-ttu-id="87138-228">Op de **tijdelijk wachtwoord** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="87138-228">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Azure AD-testgebruiker maken][106]   
   
    <span data-ttu-id="87138-230">a.</span><span class="sxs-lookup"><span data-stu-id="87138-230">a.</span></span> <span data-ttu-id="87138-231">Noteer de waarde van de **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="87138-231">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="87138-232">b.</span><span class="sxs-lookup"><span data-stu-id="87138-232">b.</span></span> <span data-ttu-id="87138-233">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="87138-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="87138-234">Maken van een testgebruiker Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="87138-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="87138-235">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="87138-235">The objective of this section is to create a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="87138-236">**Als u wilt een gebruiker Britta Simon aangeroepen in Questetra BPM Suite maakt, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="87138-236">**To create a user called Britta Simon in Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="87138-237">Aanmelding bij uw bedrijf Questetra BPM Suite site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="87138-237">Sign-on to your Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="87138-238">Ga naar **systeeminstellingen > gebruikerslijst > nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="87138-238">Go to **System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="87138-239">In het dialoogvenster Nieuwe gebruiker de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="87138-239">On the New User dialog, perform the following steps:</span></span> 
   
    ![Testgebruiker maken][300] 
   
    <span data-ttu-id="87138-241">a.</span><span class="sxs-lookup"><span data-stu-id="87138-241">a.</span></span> <span data-ttu-id="87138-242">In de **naam** textbox, typ de gebruikersnaam van Britta in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87138-242">In the **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="87138-243">b.</span><span class="sxs-lookup"><span data-stu-id="87138-243">b.</span></span> <span data-ttu-id="87138-244">In de **e** textbox, typ de gebruikersnaam van Britta in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87138-244">In the **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="87138-245">c.</span><span class="sxs-lookup"><span data-stu-id="87138-245">c.</span></span> <span data-ttu-id="87138-246">In de **wachtwoord** textbox, typ een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="87138-246">In the **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="87138-247">Klik op **nieuwe gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="87138-247">Click **Add new user**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="87138-248">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="87138-248">Assigning the Azure AD test user</span></span>
<span data-ttu-id="87138-249">Het doel van deze sectie is het Britta Simon haar toegang verlenen aan Questetra BPM Suite gebruikt Azure eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="87138-249">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Questetra BPM Suite.</span></span>

![Wat is Azure AD Connect?][200]

<span data-ttu-id="87138-251">**Als u wilt toewijzen Britta Simon Questetra BPM Suite, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="87138-251">**To assign Britta Simon to Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="87138-252">In de klassieke Azure portal, de weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="87138-252">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Wat is Azure AD Connect?][201]
2. <span data-ttu-id="87138-254">Selecteer in de lijst met toepassingen **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="87138-254">In the applications list, select **Questetra BPM Suite**.</span></span>
   
    ![Wat is Azure AD Connect?][205]
3. <span data-ttu-id="87138-256">Klik in het menu bovenaan op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="87138-256">In the menu on the top, click **Users**.</span></span>
   
    ![Wat is Azure AD Connect?][202]
4. <span data-ttu-id="87138-258">Selecteer in de lijst gebruikers **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="87138-258">In the Users list, select **Britta Simon**.</span></span>
   
    ![Wat is Azure AD Connect?][203]
5. <span data-ttu-id="87138-260">Klik in de werkbalk aan de onderkant op **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="87138-260">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Wat is Azure AD Connect?][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="87138-262">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="87138-262">Testing Single Sign-On</span></span>
<span data-ttu-id="87138-263">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="87138-263">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="87138-264">Als u op de tegel Questetra BPM Suite in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="87138-264">When you click the Questetra BPM Suite tile in the Access Panel, you should get automatically signed-on to your Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="87138-265">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="87138-265">Additional Resources</span></span>
* [<span data-ttu-id="87138-266">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87138-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="87138-267">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="87138-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
