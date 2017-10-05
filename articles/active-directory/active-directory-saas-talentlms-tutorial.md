---
title: 'Zelfstudie: Azure Active Directory-integratie met TalentLMS | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en TalentLMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: f28d6fbfad9dae578a20db7218b7e3b174ed859c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a><span data-ttu-id="6aed8-103">Zelfstudie: Azure Active Directory-integratie met TalentLMS</span><span class="sxs-lookup"><span data-stu-id="6aed8-103">Tutorial: Azure Active Directory integration with TalentLMS</span></span>

<span data-ttu-id="6aed8-104">In deze zelfstudie leert u hoe TalentLMS integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6aed8-104">In this tutorial, you learn how to integrate TalentLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6aed8-105">TalentLMS integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6aed8-105">Integrating TalentLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6aed8-106">U kunt beheren in Azure AD die toegang tot TalentLMS heeft</span><span class="sxs-lookup"><span data-stu-id="6aed8-106">You can control in Azure AD who has access to TalentLMS</span></span>
- <span data-ttu-id="6aed8-107">U kunt uw gebruikers automatisch ophalen aangemeld bij TalentLMS (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="6aed8-107">You can enable your users to automatically get signed-on to TalentLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6aed8-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6aed8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6aed8-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6aed8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6aed8-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6aed8-110">Prerequisites</span></span>

<span data-ttu-id="6aed8-111">Voor het configureren van Azure AD-integratie met TalentLMS, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="6aed8-111">To configure Azure AD integration with TalentLMS, you need the following items:</span></span>

- <span data-ttu-id="6aed8-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6aed8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6aed8-113">Een TalentLMS eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6aed8-113">A TalentLMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6aed8-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6aed8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6aed8-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6aed8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6aed8-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6aed8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6aed8-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6aed8-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6aed8-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6aed8-118">Scenario description</span></span>
<span data-ttu-id="6aed8-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6aed8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6aed8-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6aed8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6aed8-121">TalentLMS uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6aed8-121">Adding TalentLMS from the gallery</span></span>
2. <span data-ttu-id="6aed8-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6aed8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-talentlms-from-the-gallery"></a><span data-ttu-id="6aed8-123">TalentLMS uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6aed8-123">Adding TalentLMS from the gallery</span></span>
<span data-ttu-id="6aed8-124">Voor het configureren van de integratie van TalentLMS in Azure AD, moet u TalentLMS uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6aed8-124">To configure the integration of TalentLMS into Azure AD, you need to add TalentLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6aed8-125">**Als u wilt toevoegen TalentLMS uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6aed8-125">**To add TalentLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6aed8-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6aed8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6aed8-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6aed8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6aed8-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6aed8-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6aed8-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6aed8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6aed8-133">Typ in het zoekvak **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="6aed8-133">In the search box, type **TalentLMS**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. <span data-ttu-id="6aed8-135">Selecteer in het deelvenster resultaten **TalentLMS**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="6aed8-135">In the results panel, select **TalentLMS**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6aed8-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6aed8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6aed8-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met TalentLMS op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6aed8-138">In this section, you configure and test Azure AD single sign-on with TalentLMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6aed8-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in TalentLMS is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6aed8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TalentLMS is to a user in Azure AD.</span></span> <span data-ttu-id="6aed8-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in TalentLMS tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="6aed8-140">In other words, a link relationship between an Azure AD user and the related user in TalentLMS needs to be established.</span></span>

<span data-ttu-id="6aed8-141">Wijs in TalentLMS, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="6aed8-141">In TalentLMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6aed8-142">Om te configureren en testen van Azure AD eenmalige aanmelding met TalentLMS, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="6aed8-142">To configure and test Azure AD single sign-on with TalentLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6aed8-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6aed8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6aed8-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6aed8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6aed8-145">**[Maken van een testgebruiker TalentLMS](#creating-a-talentlms-test-user)**  - TalentLMS die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="6aed8-145">**[Creating a TalentLMS test user](#creating-a-talentlms-test-user)** - to have a counterpart of Britta Simon in TalentLMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6aed8-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6aed8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6aed8-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6aed8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6aed8-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6aed8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6aed8-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing TalentLMS configureren.</span><span class="sxs-lookup"><span data-stu-id="6aed8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TalentLMS application.</span></span>

<span data-ttu-id="6aed8-150">**Voor het configureren van Azure AD eenmalige aanmelding met TalentLMS, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6aed8-150">**To configure Azure AD single sign-on with TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="6aed8-151">In de Azure-portal op de **TalentLMS** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6aed8-151">In the Azure portal, on the **TalentLMS** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6aed8-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6aed8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. <span data-ttu-id="6aed8-155">Op de **TalentLMS domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6aed8-155">On the **TalentLMS Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    <span data-ttu-id="6aed8-157">a.</span><span class="sxs-lookup"><span data-stu-id="6aed8-157">a.</span></span> <span data-ttu-id="6aed8-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<tenant-name>.TalentLMSapp.com`</span><span class="sxs-lookup"><span data-stu-id="6aed8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.TalentLMSapp.com`</span></span>

    <span data-ttu-id="6aed8-159">b.</span><span class="sxs-lookup"><span data-stu-id="6aed8-159">b.</span></span> <span data-ttu-id="6aed8-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`http://<tenant-name>.talentlms.com`</span><span class="sxs-lookup"><span data-stu-id="6aed8-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<tenant-name>.talentlms.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6aed8-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="6aed8-161">These values are not real.</span></span> <span data-ttu-id="6aed8-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="6aed8-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6aed8-163">Neem contact op met [TalentLMS Client ondersteuningsteam](https://www.talentlms.com/contact) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="6aed8-163">Contact [TalentLMS Client support team](https://www.talentlms.com/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="6aed8-164">Op de **SAML-certificaat voor ondertekening van** sectie, Kopieer de **VINGERAFDRUK** waarde van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="6aed8-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. <span data-ttu-id="6aed8-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6aed8-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6aed8-168">Op de **TalentLMS configuratie** sectie, klikt u op **configureren TalentLMS** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="6aed8-168">On the **TalentLMS Configuration** section, click **Configure TalentLMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6aed8-169">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="6aed8-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. <span data-ttu-id="6aed8-171">In een ander browservenster, meld u aan bij uw bedrijf TalentLMS site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="6aed8-171">In a different web browser window, log in to your TalentLMS company site as an administrator.</span></span>

8. <span data-ttu-id="6aed8-172">In de **& Accountinstellingen** sectie, klikt u op de **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="6aed8-172">In the **Account & Settings** section, click the **Users** tab.</span></span>
   
    <span data-ttu-id="6aed8-173">![& Accountinstellingen](./media/active-directory-saas-talentlms-tutorial/IC777296.png "& Accountinstellingen")</span><span class="sxs-lookup"><span data-stu-id="6aed8-173">![Account & Settings](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Account & Settings")</span></span>

9. <span data-ttu-id="6aed8-174">Klik op **eenmalige aanmelding (SSO)**,</span><span class="sxs-lookup"><span data-stu-id="6aed8-174">Click **Single Sign-On (SSO)**,</span></span>

10. <span data-ttu-id="6aed8-175">Voer de volgende stappen uit in de sectie eenmalige aanmelding:</span><span class="sxs-lookup"><span data-stu-id="6aed8-175">In the Single Sign-On section, perform the following steps:</span></span>
   
    <span data-ttu-id="6aed8-176">![Eenmalige aanmelding](./media/active-directory-saas-talentlms-tutorial/IC777297.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="6aed8-176">![Single Sign-On](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span></span>   

    <span data-ttu-id="6aed8-177">a.</span><span class="sxs-lookup"><span data-stu-id="6aed8-177">a.</span></span> <span data-ttu-id="6aed8-178">Van de **SSO-Integratietype** selecteert **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="6aed8-178">From the **SSO integration type** list, select **SAML 2.0**.</span></span>

    <span data-ttu-id="6aed8-179">b.</span><span class="sxs-lookup"><span data-stu-id="6aed8-179">b.</span></span> <span data-ttu-id="6aed8-180">In de **identiteitsprovider (IDP)** textbox, plak de waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6aed8-180">In the **Identity provider (IDP)** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="6aed8-181">c.</span><span class="sxs-lookup"><span data-stu-id="6aed8-181">c.</span></span> <span data-ttu-id="6aed8-182">Plak de **vingerafdruk** waarde van de Azure-portal in de **vingerafdruk van certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="6aed8-182">Paste the **Thumbprint** value from Azure portal into the **Certificate fingerprint** textbox.</span></span>    

    <span data-ttu-id="6aed8-183">d.</span><span class="sxs-lookup"><span data-stu-id="6aed8-183">d.</span></span>  <span data-ttu-id="6aed8-184">In de **extern aanmelden URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6aed8-184">In the **Remote sign-in URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="6aed8-185">e.</span><span class="sxs-lookup"><span data-stu-id="6aed8-185">e.</span></span> <span data-ttu-id="6aed8-186">In de **externe URL voor afmelden** textbox, plak de waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6aed8-186">In the **Remote sign-out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6aed8-187">f.</span><span class="sxs-lookup"><span data-stu-id="6aed8-187">f.</span></span> <span data-ttu-id="6aed8-188">Vul in het volgende:</span><span class="sxs-lookup"><span data-stu-id="6aed8-188">Fill in the following:</span></span> 

    * <span data-ttu-id="6aed8-189">In de **TargetedID** textbox type`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span><span class="sxs-lookup"><span data-stu-id="6aed8-189">In the **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span></span>
     
    * <span data-ttu-id="6aed8-190">In de **voornaam** textbox type`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span><span class="sxs-lookup"><span data-stu-id="6aed8-190">In the **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span></span>
    
    * <span data-ttu-id="6aed8-191">In de **achternaam** textbox type`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span><span class="sxs-lookup"><span data-stu-id="6aed8-191">In the **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span></span>
    
    * <span data-ttu-id="6aed8-192">In de **e** textbox type`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="6aed8-192">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>
    
11. <span data-ttu-id="6aed8-193">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6aed8-193">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="6aed8-194">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="6aed8-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6aed8-195">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="6aed8-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6aed8-196">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6aed8-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6aed8-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6aed8-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="6aed8-198">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6aed8-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6aed8-200">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6aed8-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6aed8-201">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6aed8-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6aed8-203">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6aed8-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6aed8-205">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6aed8-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6aed8-207">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6aed8-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6aed8-209">a.</span><span class="sxs-lookup"><span data-stu-id="6aed8-209">a.</span></span> <span data-ttu-id="6aed8-210">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6aed8-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6aed8-211">b.</span><span class="sxs-lookup"><span data-stu-id="6aed8-211">b.</span></span> <span data-ttu-id="6aed8-212">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6aed8-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6aed8-213">c.</span><span class="sxs-lookup"><span data-stu-id="6aed8-213">c.</span></span> <span data-ttu-id="6aed8-214">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6aed8-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6aed8-215">d.</span><span class="sxs-lookup"><span data-stu-id="6aed8-215">d.</span></span> <span data-ttu-id="6aed8-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6aed8-216">Click **Create**.</span></span>
 
### <a name="creating-a-talentlms-test-user"></a><span data-ttu-id="6aed8-217">Een testgebruiker TalentLMS maken</span><span class="sxs-lookup"><span data-stu-id="6aed8-217">Creating a TalentLMS test user</span></span>

<span data-ttu-id="6aed8-218">Om Azure AD-gebruikers zich aanmelden bij TalentLMS, moeten ze worden ingericht in TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="6aed8-218">To enable Azure AD users to log in to TalentLMS, they must be provisioned into TalentLMS.</span></span> <span data-ttu-id="6aed8-219">In het geval van TalentLMS is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="6aed8-219">In the case of TalentLMS, provisioning is a manual task.</span></span>

<span data-ttu-id="6aed8-220">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6aed8-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="6aed8-221">Meld u aan bij uw **TalentLMS** tenant.</span><span class="sxs-lookup"><span data-stu-id="6aed8-221">Log in to your **TalentLMS** tenant.</span></span>

2. <span data-ttu-id="6aed8-222">Klik op **gebruikers**, en klik vervolgens op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6aed8-222">Click **Users**, and then click **Add User**.</span></span>

3. <span data-ttu-id="6aed8-223">Op de **gebruiker toevoegen** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6aed8-223">On the **Add user** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="6aed8-224">![Gebruiker toevoegen](./media/active-directory-saas-talentlms-tutorial/IC777299.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="6aed8-224">![Add User](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Add User")</span></span>  

    <span data-ttu-id="6aed8-225">a.</span><span class="sxs-lookup"><span data-stu-id="6aed8-225">a.</span></span> <span data-ttu-id="6aed8-226">In de **voornaam** textbox, voer de voornaam van de gebruiker zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="6aed8-226">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="6aed8-227">b.</span><span class="sxs-lookup"><span data-stu-id="6aed8-227">b.</span></span> <span data-ttu-id="6aed8-228">In de **achternaam** textbox, geef de achternaam van de gebruiker zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="6aed8-228">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="6aed8-229">c.</span><span class="sxs-lookup"><span data-stu-id="6aed8-229">c.</span></span> <span data-ttu-id="6aed8-230">In de **e-mailadres** textbox, voer het e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="6aed8-230">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="6aed8-231">d.</span><span class="sxs-lookup"><span data-stu-id="6aed8-231">d.</span></span> <span data-ttu-id="6aed8-232">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6aed8-232">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="6aed8-233">U kunt andere TalentLMS gebruiker account hulpmiddelen voor het maken of API's die is geleverd door TalentLMS aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="6aed8-233">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6aed8-234">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="6aed8-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6aed8-235">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="6aed8-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TalentLMS.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6aed8-237">**Britta Simon om aan te wijzen TalentLMS, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6aed8-237">**To assign Britta Simon to TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="6aed8-238">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6aed8-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6aed8-240">Selecteer in de lijst met toepassingen **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="6aed8-240">In the applications list, select **TalentLMS**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. <span data-ttu-id="6aed8-242">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6aed8-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6aed8-244">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6aed8-244">Click **Add** button.</span></span> <span data-ttu-id="6aed8-245">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6aed8-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6aed8-247">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6aed8-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6aed8-248">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6aed8-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6aed8-249">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6aed8-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6aed8-250">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6aed8-250">Testing single sign-on</span></span>

<span data-ttu-id="6aed8-251">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="6aed8-251">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6aed8-252">Als u op de tegel TalentLMS in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing TalentLMS</span><span class="sxs-lookup"><span data-stu-id="6aed8-252">When you click the TalentLMS tile in the Access Panel, you should get automatically signed-on to your TalentLMS application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6aed8-253">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6aed8-253">Additional resources</span></span>

* [<span data-ttu-id="6aed8-254">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6aed8-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6aed8-255">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6aed8-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

