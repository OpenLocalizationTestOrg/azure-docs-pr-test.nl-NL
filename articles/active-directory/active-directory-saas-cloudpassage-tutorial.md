---
title: 'Zelfstudie: Azure Active Directory-integratie met CloudPassage | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en CloudPassage.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 094740e20570665e975dec1a591989e411f90c16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="03e6f-103">Zelfstudie: Azure Active Directory-integratie met CloudPassage</span><span class="sxs-lookup"><span data-stu-id="03e6f-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="03e6f-104">In deze zelfstudie leert u hoe CloudPassage integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="03e6f-104">In this tutorial, you learn how to integrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="03e6f-105">CloudPassage integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="03e6f-105">Integrating CloudPassage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="03e6f-106">U kunt beheren in Azure AD die toegang tot CloudPassage heeft</span><span class="sxs-lookup"><span data-stu-id="03e6f-106">You can control in Azure AD who has access to CloudPassage</span></span>
- <span data-ttu-id="03e6f-107">U kunt uw gebruikers automatisch ophalen aangemeld bij CloudPassage (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="03e6f-107">You can enable your users to automatically get signed-on to CloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="03e6f-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="03e6f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="03e6f-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="03e6f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03e6f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="03e6f-110">Prerequisites</span></span>

<span data-ttu-id="03e6f-111">Voor het configureren van Azure AD-integratie met CloudPassage, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="03e6f-111">To configure Azure AD integration with CloudPassage, you need the following items:</span></span>

- <span data-ttu-id="03e6f-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="03e6f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="03e6f-113">Een CloudPassage eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="03e6f-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="03e6f-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="03e6f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="03e6f-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="03e6f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="03e6f-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="03e6f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="03e6f-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="03e6f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="03e6f-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="03e6f-118">Scenario description</span></span>
<span data-ttu-id="03e6f-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="03e6f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="03e6f-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="03e6f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="03e6f-121">CloudPassage uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="03e6f-121">Adding CloudPassage from the gallery</span></span>
2. <span data-ttu-id="03e6f-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="03e6f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-the-gallery"></a><span data-ttu-id="03e6f-123">CloudPassage uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="03e6f-123">Adding CloudPassage from the gallery</span></span>
<span data-ttu-id="03e6f-124">Voor het configureren van de integratie van CloudPassage in Azure AD, moet u CloudPassage uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="03e6f-124">To configure the integration of CloudPassage into Azure AD, you need to add CloudPassage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="03e6f-125">**Als u wilt toevoegen CloudPassage uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="03e6f-125">**To add CloudPassage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="03e6f-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="03e6f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="03e6f-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="03e6f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="03e6f-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="03e6f-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="03e6f-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="03e6f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="03e6f-133">Typ in het zoekvak **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="03e6f-133">In the search box, type **CloudPassage**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. <span data-ttu-id="03e6f-135">Selecteer in het deelvenster resultaten **CloudPassage**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="03e6f-135">In the results panel, select **CloudPassage**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="03e6f-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="03e6f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="03e6f-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met CloudPassage op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="03e6f-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="03e6f-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in CloudPassage is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03e6f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CloudPassage is to a user in Azure AD.</span></span> <span data-ttu-id="03e6f-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in CloudPassage tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="03e6f-140">In other words, a link relationship between an Azure AD user and the related user in CloudPassage needs to be established.</span></span>

<span data-ttu-id="03e6f-141">Wijs in CloudPassage, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="03e6f-141">In CloudPassage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="03e6f-142">Om te configureren en testen van Azure AD eenmalige aanmelding met CloudPassage, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="03e6f-142">To configure and test Azure AD single sign-on with CloudPassage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="03e6f-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="03e6f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="03e6f-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="03e6f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="03e6f-145">**[Maken van een testgebruiker CloudPassage](#creating-a-cloudpassage-test-user)**  - CloudPassage die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="03e6f-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - to have a counterpart of Britta Simon in CloudPassage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="03e6f-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="03e6f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="03e6f-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="03e6f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="03e6f-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="03e6f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="03e6f-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing CloudPassage configureren.</span><span class="sxs-lookup"><span data-stu-id="03e6f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="03e6f-150">**Voor het configureren van Azure AD eenmalige aanmelding met CloudPassage, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="03e6f-150">**To configure Azure AD single sign-on with CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="03e6f-151">In de Azure-portal op de **CloudPassage** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="03e6f-151">In the Azure portal, on the **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="03e6f-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="03e6f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. <span data-ttu-id="03e6f-155">Op de **CloudPassage domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="03e6f-155">On the **CloudPassage Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="03e6f-157">a.</span><span class="sxs-lookup"><span data-stu-id="03e6f-157">a.</span></span> <span data-ttu-id="03e6f-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://portal.cloudpassage.com/saml/init/accountid`</span><span class="sxs-lookup"><span data-stu-id="03e6f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="03e6f-159">b.</span><span class="sxs-lookup"><span data-stu-id="03e6f-159">b.</span></span> <span data-ttu-id="03e6f-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen: `https://portal.cloudpassage.com/saml/consume/accountid`.</span><span class="sxs-lookup"><span data-stu-id="03e6f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="03e6f-161">U kunt de waarde voor dit kenmerk opvragen door te klikken op **SSO ondersteuningsdocumentatie** in de **instellingen voor eenmalige aanmelding** gedeelte van uw CloudPassage-portal.</span><span class="sxs-lookup"><span data-stu-id="03e6f-161">You can get your value for this attribute by clicking **SSO Setup documentation** in the **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="03e6f-163">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="03e6f-163">These values are not real.</span></span> <span data-ttu-id="03e6f-164">Deze waarden bijwerken met de werkelijke antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="03e6f-164">Update these values with the actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="03e6f-165">Neem contact op met [CloudPassage Client ondersteuningsteam](https://www.cloudpassage.com/company/contact/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="03e6f-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) to get these values.</span></span> 

4. <span data-ttu-id="03e6f-166">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="03e6f-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. <span data-ttu-id="03e6f-168">Uw toepassing CloudPassage verwacht de SAML-asserties in een specifieke indeling waarvoor u aangepaste kenmerktoewijzingen toevoegen aan uw configuratie van SAML-token kenmerken.</span><span class="sxs-lookup"><span data-stu-id="03e6f-168">Your CloudPassage application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="03e6f-169">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="03e6f-169">The following screenshot shows an example for this.</span></span>
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. <span data-ttu-id="03e6f-171">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding hierboven en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="03e6f-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>

    | <span data-ttu-id="03e6f-172">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="03e6f-172">Attribute Name</span></span> | <span data-ttu-id="03e6f-173">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="03e6f-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="03e6f-174">Voornaam</span><span class="sxs-lookup"><span data-stu-id="03e6f-174">firstname</span></span> |<span data-ttu-id="03e6f-175">User.givenName</span><span class="sxs-lookup"><span data-stu-id="03e6f-175">user.givenname</span></span> |
    | <span data-ttu-id="03e6f-176">Achternaam</span><span class="sxs-lookup"><span data-stu-id="03e6f-176">lastname</span></span> |<span data-ttu-id="03e6f-177">User.surname</span><span class="sxs-lookup"><span data-stu-id="03e6f-177">user.surname</span></span> |
    | <span data-ttu-id="03e6f-178">E-mail</span><span class="sxs-lookup"><span data-stu-id="03e6f-178">email</span></span> |<span data-ttu-id="03e6f-179">User.mail</span><span class="sxs-lookup"><span data-stu-id="03e6f-179">user.mail</span></span> |
    
    <span data-ttu-id="03e6f-180">a.</span><span class="sxs-lookup"><span data-stu-id="03e6f-180">a.</span></span> <span data-ttu-id="03e6f-181">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="03e6f-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="03e6f-184">b.</span><span class="sxs-lookup"><span data-stu-id="03e6f-184">b.</span></span> <span data-ttu-id="03e6f-185">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="03e6f-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="03e6f-186">c.</span><span class="sxs-lookup"><span data-stu-id="03e6f-186">c.</span></span> <span data-ttu-id="03e6f-187">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="03e6f-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="03e6f-188">d.</span><span class="sxs-lookup"><span data-stu-id="03e6f-188">d.</span></span> <span data-ttu-id="03e6f-189">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="03e6f-189">Click **Ok**.</span></span>

7. <span data-ttu-id="03e6f-190">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="03e6f-190">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="03e6f-192">Op de **CloudPassage configuratie** sectie, klikt u op **configureren CloudPassage** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="03e6f-192">On the **CloudPassage Configuration** section, click **Configure CloudPassage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="03e6f-193">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="03e6f-193">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. <span data-ttu-id="03e6f-195">In een ander browservenster aanmelding bij uw bedrijf CloudPassage site als administrator.</span><span class="sxs-lookup"><span data-stu-id="03e6f-195">In a different browser window, sign-on to your CloudPassage company site as administrator.</span></span>

10. <span data-ttu-id="03e6f-196">Klik in het menu bovenaan op **instellingen**, en klik vervolgens op **Sitebeheer**.</span><span class="sxs-lookup"><span data-stu-id="03e6f-196">In the menu on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![Eenmalige aanmelding configureren][12]

11. <span data-ttu-id="03e6f-198">Klik op de **verificatie-instellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="03e6f-198">Click the **Authentication Settings** tab.</span></span> 
   
    ![Eenmalige aanmelding configureren][13]

12. <span data-ttu-id="03e6f-200">In de **instellingen voor eenmalige aanmelding** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="03e6f-200">In the **Single Sign-on Settings** section, perform the following steps:</span></span> 
   
    ![Eenmalige aanmelding configureren][14]

    <span data-ttu-id="03e6f-202">a.</span><span class="sxs-lookup"><span data-stu-id="03e6f-202">a.</span></span> <span data-ttu-id="03e6f-203">Selecteer **één inschakelen sign-on(SSO) (SSO Setup documentatie)** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="03e6f-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="03e6f-204">b.</span><span class="sxs-lookup"><span data-stu-id="03e6f-204">b.</span></span> <span data-ttu-id="03e6f-205">Plakken **SAML entiteit-ID** in de **URL-verlener SAML** textbox.</span><span class="sxs-lookup"><span data-stu-id="03e6f-205">Paste **SAML Entity ID** into the **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="03e6f-206">c.</span><span class="sxs-lookup"><span data-stu-id="03e6f-206">c.</span></span> <span data-ttu-id="03e6f-207">Plakken **SAML Single Sign-On Service-URL** in de **eindpunt-URL van SAML** textbox.</span><span class="sxs-lookup"><span data-stu-id="03e6f-207">Paste **SAML Single Sign-On Service URL** into the **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="03e6f-208">d.</span><span class="sxs-lookup"><span data-stu-id="03e6f-208">d.</span></span> <span data-ttu-id="03e6f-209">Plakken **Sign-Out URL** in de **afmelding startpagina** textbox.</span><span class="sxs-lookup"><span data-stu-id="03e6f-209">Paste **Sign-Out URL** into the **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="03e6f-210">e.</span><span class="sxs-lookup"><span data-stu-id="03e6f-210">e.</span></span> <span data-ttu-id="03e6f-211">Open uw gedownloade certificaat in Kladblok, Kopieer de inhoud van de gedownloade certificaat naar het Klembord en plakt u deze in de **x 509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="03e6f-211">Open your downloaded certificate in notepad, copy the content of downloaded certificate into your clipboard, and then paste it into the **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="03e6f-212">f.</span><span class="sxs-lookup"><span data-stu-id="03e6f-212">f.</span></span> <span data-ttu-id="03e6f-213">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="03e6f-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="03e6f-214">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="03e6f-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="03e6f-215">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="03e6f-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="03e6f-216">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="03e6f-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="03e6f-217">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="03e6f-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="03e6f-218">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="03e6f-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="03e6f-220">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="03e6f-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="03e6f-221">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="03e6f-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="03e6f-223">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="03e6f-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="03e6f-225">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="03e6f-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="03e6f-227">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="03e6f-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="03e6f-229">a.</span><span class="sxs-lookup"><span data-stu-id="03e6f-229">a.</span></span> <span data-ttu-id="03e6f-230">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="03e6f-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="03e6f-231">b.</span><span class="sxs-lookup"><span data-stu-id="03e6f-231">b.</span></span> <span data-ttu-id="03e6f-232">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="03e6f-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="03e6f-233">c.</span><span class="sxs-lookup"><span data-stu-id="03e6f-233">c.</span></span> <span data-ttu-id="03e6f-234">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="03e6f-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="03e6f-235">d.</span><span class="sxs-lookup"><span data-stu-id="03e6f-235">d.</span></span> <span data-ttu-id="03e6f-236">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="03e6f-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="03e6f-237">Een testgebruiker CloudPassage maken</span><span class="sxs-lookup"><span data-stu-id="03e6f-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="03e6f-238">Het doel van deze sectie is het maken van een gebruiker Britta Simon in CloudPassage genoemd.</span><span class="sxs-lookup"><span data-stu-id="03e6f-238">The objective of this section is to create a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="03e6f-239">**Als u wilt een gebruiker Britta Simon aangeroepen in CloudPassage maakt, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="03e6f-239">**To create a user called Britta Simon in CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="03e6f-240">Aanmelding bij uw **CloudPassage** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="03e6f-240">Sign-on to your **CloudPassage** company site as an administrator.</span></span> 

2. <span data-ttu-id="03e6f-241">Klik in de werkbalk bovenaan op **instellingen**, en klik vervolgens op **Sitebeheer**.</span><span class="sxs-lookup"><span data-stu-id="03e6f-241">In the toolbar on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![Een testgebruiker CloudPassage maken][22] 

3. <span data-ttu-id="03e6f-243">Klik op de **gebruikers** tabblad en klik vervolgens op **nieuwe gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="03e6f-243">Click the **Users** tab, and then click **Add New User**.</span></span> 
   
   ![Een testgebruiker CloudPassage maken][23]

4. <span data-ttu-id="03e6f-245">In de **nieuwe gebruiker toevoegen** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="03e6f-245">In the **Add New User** section, perform the following steps:</span></span> 
   
   ![Een testgebruiker CloudPassage maken][24]
    
    <span data-ttu-id="03e6f-247">a.</span><span class="sxs-lookup"><span data-stu-id="03e6f-247">a.</span></span> <span data-ttu-id="03e6f-248">In de **voornaam** textbox Britta typt.</span><span class="sxs-lookup"><span data-stu-id="03e6f-248">In the **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="03e6f-249">b.</span><span class="sxs-lookup"><span data-stu-id="03e6f-249">b.</span></span> <span data-ttu-id="03e6f-250">In de **achternaam** textbox Simon typt.</span><span class="sxs-lookup"><span data-stu-id="03e6f-250">In the **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="03e6f-251">c.</span><span class="sxs-lookup"><span data-stu-id="03e6f-251">c.</span></span> <span data-ttu-id="03e6f-252">In de **gebruikersnaam** tekstvak de **e** textbox en de **e-mailbericht opnieuw** textbox, typ de gebruikersnaam van Britta in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03e6f-252">In the **Username** textbox, the **Email** textbox and the **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="03e6f-253">d.</span><span class="sxs-lookup"><span data-stu-id="03e6f-253">d.</span></span> <span data-ttu-id="03e6f-254">Als **toegangstype**, selecteer **Halo Portal toegang inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="03e6f-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="03e6f-255">e.</span><span class="sxs-lookup"><span data-stu-id="03e6f-255">e.</span></span> <span data-ttu-id="03e6f-256">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="03e6f-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="03e6f-257">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="03e6f-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="03e6f-258">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="03e6f-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CloudPassage.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="03e6f-260">**Britta Simon om aan te wijzen CloudPassage, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="03e6f-260">**To assign Britta Simon to CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="03e6f-261">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="03e6f-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="03e6f-263">Selecteer in de lijst met toepassingen **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="03e6f-263">In the applications list, select **CloudPassage**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. <span data-ttu-id="03e6f-265">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="03e6f-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="03e6f-267">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="03e6f-267">Click **Add** button.</span></span> <span data-ttu-id="03e6f-268">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="03e6f-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="03e6f-270">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="03e6f-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="03e6f-271">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="03e6f-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="03e6f-272">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="03e6f-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="03e6f-273">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="03e6f-273">Testing single sign-on</span></span>

<span data-ttu-id="03e6f-274">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="03e6f-274">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="03e6f-275">Als u op de tegel CloudPassage in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="03e6f-275">When you click the CloudPassage tile in the Access Panel, you should get automatically signed-on to your CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="03e6f-276">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="03e6f-276">Additional resources</span></span>

* [<span data-ttu-id="03e6f-277">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03e6f-277">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="03e6f-278">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="03e6f-278">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

