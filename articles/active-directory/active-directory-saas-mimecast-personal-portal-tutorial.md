---
title: 'Zelfstudie: Azure Active Directory-integratie met de persoonlijke Portal Mimecast | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en persoonlijke Mimecast-Portal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: bf46da35a55608d7e4656c9dd3ad9d5f2253e225
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="48882-103">Zelfstudie: Azure Active Directory-integratie met Mimecast persoonlijke Portal</span><span class="sxs-lookup"><span data-stu-id="48882-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="48882-104">In deze zelfstudie leert u hoe Mimecast persoonlijke Portal integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48882-104">In this tutorial, you learn how to integrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48882-105">Mimecast persoonlijke Portal integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="48882-105">Integrating Mimecast Personal Portal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="48882-106">U kunt beheren in Azure AD die toegang tot de persoonlijke Portal Mimecast heeft</span><span class="sxs-lookup"><span data-stu-id="48882-106">You can control in Azure AD who has access to Mimecast Personal Portal</span></span>
- <span data-ttu-id="48882-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Mimecast persoonlijke Portal (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="48882-107">You can enable your users to automatically get signed-on to Mimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="48882-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="48882-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="48882-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="48882-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48882-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="48882-110">Prerequisites</span></span>

<span data-ttu-id="48882-111">Voor het configureren van Azure AD-integratie met Mimecast persoonlijke Portal, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="48882-111">To configure Azure AD integration with Mimecast Personal Portal, you need the following items:</span></span>

- <span data-ttu-id="48882-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="48882-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48882-113">Een persoonlijke Portal Mimecast eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="48882-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48882-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="48882-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48882-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="48882-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48882-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="48882-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48882-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48882-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48882-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="48882-118">Scenario description</span></span>
<span data-ttu-id="48882-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="48882-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48882-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="48882-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48882-121">Toevoegen van de persoonlijke Portal Mimecast uit de galerie</span><span class="sxs-lookup"><span data-stu-id="48882-121">Adding Mimecast Personal Portal from the gallery</span></span>
2. <span data-ttu-id="48882-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="48882-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-the-gallery"></a><span data-ttu-id="48882-123">Toevoegen van de persoonlijke Portal Mimecast uit de galerie</span><span class="sxs-lookup"><span data-stu-id="48882-123">Adding Mimecast Personal Portal from the gallery</span></span>
<span data-ttu-id="48882-124">Voor het configureren van de integratie van persoonlijke Portal Mimecast in Azure AD, moet u Mimecast persoonlijke Portal uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="48882-124">To configure the integration of Mimecast Personal Portal into Azure AD, you need to add Mimecast Personal Portal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="48882-125">**Als u wilt toevoegen Mimecast persoonlijke Portal uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="48882-125">**To add Mimecast Personal Portal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="48882-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="48882-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="48882-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="48882-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="48882-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="48882-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="48882-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="48882-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="48882-133">Typ in het zoekvak **Mimecast persoonlijke Portal**.</span><span class="sxs-lookup"><span data-stu-id="48882-133">In the search box, type **Mimecast Personal Portal**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="48882-135">Selecteer in het deelvenster resultaten **Mimecast persoonlijke Portal**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="48882-135">In the results panel, select **Mimecast Personal Portal**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="48882-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="48882-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="48882-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Mimecast persoonlijke Portal op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="48882-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="48882-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Mimecast persoonlijke Portal is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48882-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Personal Portal is to a user in Azure AD.</span></span> <span data-ttu-id="48882-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante Mimecast persoonlijke Portal-gebruiker worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="48882-140">In other words, a link relationship between an Azure AD user and the related user in Mimecast Personal Portal needs to be established.</span></span>

<span data-ttu-id="48882-141">Wijs in Mimecast persoonlijke Portal, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="48882-141">In Mimecast Personal Portal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="48882-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Mimecast persoonlijke Portal, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="48882-142">To configure and test Azure AD single sign-on with Mimecast Personal Portal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="48882-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="48882-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="48882-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48882-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="48882-145">**[Maken van een testgebruiker Mimecast persoonlijke Portal](#creating-a-mimecast-personal-portal-test-user)**  - Mimecast persoonlijke Portal dat is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="48882-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - to have a counterpart of Britta Simon in Mimecast Personal Portal that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="48882-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="48882-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="48882-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="48882-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="48882-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="48882-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="48882-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Mimecast persoonlijke Portal configureren.</span><span class="sxs-lookup"><span data-stu-id="48882-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="48882-150">**Voor het configureren van Azure AD eenmalige aanmelding met Mimecast persoonlijke Portal, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="48882-150">**To configure Azure AD single sign-on with Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="48882-151">In de Azure-portal op de **Mimecast persoonlijke Portal** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="48882-151">In the Azure portal, on the **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="48882-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="48882-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="48882-155">Op de **Mimecast persoonlijke Portal domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="48882-155">On the **Mimecast Personal Portal Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="48882-157">a.</span><span class="sxs-lookup"><span data-stu-id="48882-157">a.</span></span> <span data-ttu-id="48882-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="48882-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="48882-159">b.</span><span class="sxs-lookup"><span data-stu-id="48882-159">b.</span></span> <span data-ttu-id="48882-160">In de **id** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="48882-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="48882-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="48882-161">These values are not real.</span></span> <span data-ttu-id="48882-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="48882-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="48882-163">Neem contact op met [Mimecast persoonlijke Portal Client ondersteuningsteam](https://www.mimecast.com/customer-success/technical-support/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="48882-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) to get these values.</span></span> 
 


4. <span data-ttu-id="48882-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="48882-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="48882-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="48882-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="48882-168">Op de **Mimecast persoonlijke Portal-configuratie** sectie, klikt u op **Mimecast persoonlijke Portal configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="48882-168">On the **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** to open **Configure sign-on** window.</span></span> <span data-ttu-id="48882-169">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="48882-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="48882-171">In een ander browservenster, meld u bij uw persoonlijke Mimecast-Portal als beheerder.</span><span class="sxs-lookup"><span data-stu-id="48882-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="48882-172">Ga naar **Services \> toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="48882-172">Go to **Services \> Applications**.</span></span>
   
    <span data-ttu-id="48882-173">![Toepassingen](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "toepassingen")</span><span class="sxs-lookup"><span data-stu-id="48882-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="48882-174">Klik op **verificatie profielen**.</span><span class="sxs-lookup"><span data-stu-id="48882-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="48882-175">![Verificatie profielen](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "verificatie-profielen")</span><span class="sxs-lookup"><span data-stu-id="48882-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="48882-176">Klik op **nieuwe Authentication profiel**.</span><span class="sxs-lookup"><span data-stu-id="48882-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="48882-177">![Nieuwe Authentication profiel](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "nieuwe profiel voor verificatie")</span><span class="sxs-lookup"><span data-stu-id="48882-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="48882-178">In de **Authentication profiel** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="48882-178">In the **Authentication Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="48882-179">![Authentication profiel](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication profiel")</span><span class="sxs-lookup"><span data-stu-id="48882-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="48882-180">a.</span><span class="sxs-lookup"><span data-stu-id="48882-180">a.</span></span> <span data-ttu-id="48882-181">In de **beschrijving** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="48882-181">In the **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="48882-182">b.</span><span class="sxs-lookup"><span data-stu-id="48882-182">b.</span></span> <span data-ttu-id="48882-183">Selecteer **afdwingen van SAML-verificatie voor Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="48882-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="48882-184">c.</span><span class="sxs-lookup"><span data-stu-id="48882-184">c.</span></span> <span data-ttu-id="48882-185">Als **Provider**, selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="48882-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="48882-186">d.</span><span class="sxs-lookup"><span data-stu-id="48882-186">d.</span></span> <span data-ttu-id="48882-187">In **URL-verlener** textbox, plak de waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="48882-187">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="48882-188">e.</span><span class="sxs-lookup"><span data-stu-id="48882-188">e.</span></span> <span data-ttu-id="48882-189">In **aanmeldings-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="48882-189">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="48882-190">f.</span><span class="sxs-lookup"><span data-stu-id="48882-190">f.</span></span> <span data-ttu-id="48882-191">In **afmelding URL** textbox, plak de waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="48882-191">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="48882-192">g.</span><span class="sxs-lookup"><span data-stu-id="48882-192">g.</span></span> <span data-ttu-id="48882-193">Open uw **base 64-** in Kladblok een gecodeerd certificaat gedownload vanuit Azure-portal, de inhoud van het kopiëren naar het Klembord en plakt u deze naar de **Provider identiteitscertificaat (metagegevens)** textbox.</span><span class="sxs-lookup"><span data-stu-id="48882-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="48882-194">h.</span><span class="sxs-lookup"><span data-stu-id="48882-194">h.</span></span> <span data-ttu-id="48882-195">Selecteer **toestaan voor eenmalige op**.</span><span class="sxs-lookup"><span data-stu-id="48882-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="48882-196">ik.</span><span class="sxs-lookup"><span data-stu-id="48882-196">i.</span></span> <span data-ttu-id="48882-197">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="48882-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="48882-198">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="48882-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="48882-199">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="48882-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="48882-200">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="48882-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="48882-201">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="48882-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="48882-202">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="48882-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="48882-204">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="48882-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="48882-205">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="48882-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="48882-207">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="48882-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="48882-209">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="48882-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="48882-211">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="48882-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="48882-213">a.</span><span class="sxs-lookup"><span data-stu-id="48882-213">a.</span></span> <span data-ttu-id="48882-214">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48882-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48882-215">b.</span><span class="sxs-lookup"><span data-stu-id="48882-215">b.</span></span> <span data-ttu-id="48882-216">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="48882-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="48882-217">c.</span><span class="sxs-lookup"><span data-stu-id="48882-217">c.</span></span> <span data-ttu-id="48882-218">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="48882-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="48882-219">d.</span><span class="sxs-lookup"><span data-stu-id="48882-219">d.</span></span> <span data-ttu-id="48882-220">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="48882-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="48882-221">Een testgebruiker Mimecast persoonlijke Portal maken</span><span class="sxs-lookup"><span data-stu-id="48882-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="48882-222">Om in te schakelen gebruikers van Azure AD aan te melden bij Mimecast persoonlijke Portal, moeten ze worden ingericht bij Mimecast persoonlijke Portal.</span><span class="sxs-lookup"><span data-stu-id="48882-222">In order to enable Azure AD users to log into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="48882-223">Inrichting is een handmatige taak in het geval van persoonlijke Mimecast-Portal.</span><span class="sxs-lookup"><span data-stu-id="48882-223">In the case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="48882-224">U moet een domein registreren voordat u gebruikers kunt maken.</span><span class="sxs-lookup"><span data-stu-id="48882-224">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="48882-225">**Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="48882-225">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="48882-226">Meld u aan bij uw **Mimecast persoonlijke Portal** als administrator.</span><span class="sxs-lookup"><span data-stu-id="48882-226">Sign on to your **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="48882-227">Ga naar **mappen \> interne**.</span><span class="sxs-lookup"><span data-stu-id="48882-227">Go to **Directories \> Internal**.</span></span>
   
    <span data-ttu-id="48882-228">![Mappen](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "mappen")</span><span class="sxs-lookup"><span data-stu-id="48882-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="48882-229">Klik op **nieuwe domein registreren**.</span><span class="sxs-lookup"><span data-stu-id="48882-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="48882-230">![Nieuwe domein registreren](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "nieuwe domein registreren")</span><span class="sxs-lookup"><span data-stu-id="48882-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="48882-231">Nadat het nieuwe domein is gemaakt, klikt u op **nieuw adres**.</span><span class="sxs-lookup"><span data-stu-id="48882-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="48882-232">![Nieuw adres](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "nieuw adres")</span><span class="sxs-lookup"><span data-stu-id="48882-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="48882-233">In het dialoogvenster Nieuw adres Voer de volgende stappen uit van een geldig Azure AD-account die u inrichten wilt:</span><span class="sxs-lookup"><span data-stu-id="48882-233">In the new address dialog, perform the following steps of a valid Azure AD account you want to provision:</span></span>
   
    <span data-ttu-id="48882-234">![Sla](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "opslaan")</span><span class="sxs-lookup"><span data-stu-id="48882-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="48882-235">a.</span><span class="sxs-lookup"><span data-stu-id="48882-235">a.</span></span> <span data-ttu-id="48882-236">In de **e-mailadres** textbox type **e-mailadres** van de gebruiker als  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="48882-236">In the **Email Address** textbox, type **Email Address** of the user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="48882-237">b.</span><span class="sxs-lookup"><span data-stu-id="48882-237">b.</span></span> <span data-ttu-id="48882-238">In de **globale naam** textbox type de **gebruikersnaam** als **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48882-238">In the **Global Name** textbox, type the **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="48882-239">c.</span><span class="sxs-lookup"><span data-stu-id="48882-239">c.</span></span> <span data-ttu-id="48882-240">In de **wachtwoord**, en **wachtwoord bevestigen** tekstvakken, typ de **wachtwoord** van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="48882-240">In the **Password**, and **Confirm Password** textboxes, type the **Password** of the user.</span></span>
   
    <span data-ttu-id="48882-241">b.</span><span class="sxs-lookup"><span data-stu-id="48882-241">b.</span></span> <span data-ttu-id="48882-242">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="48882-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="48882-243">U kunt geen andere hulpprogramma's voor persoonlijke Portal Mimecast gebruiker-account maken of API's die worden geleverd door Mimecast persoonlijke Portal gebruiken voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="48882-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="48882-244">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="48882-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="48882-245">In deze sectie maakt inschakelen u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot persoonlijke Portal Mimecast.</span><span class="sxs-lookup"><span data-stu-id="48882-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Personal Portal.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="48882-247">**Britta Simon om aan te wijzen Mimecast persoonlijke Portal, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="48882-247">**To assign Britta Simon to Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="48882-248">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="48882-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="48882-250">Selecteer in de lijst met toepassingen **Mimecast persoonlijke Portal**.</span><span class="sxs-lookup"><span data-stu-id="48882-250">In the applications list, select **Mimecast Personal Portal**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="48882-252">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="48882-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="48882-254">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="48882-254">Click **Add** button.</span></span> <span data-ttu-id="48882-255">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="48882-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="48882-257">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="48882-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="48882-258">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="48882-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="48882-259">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="48882-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="48882-260">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="48882-260">Testing single sign-on</span></span>
<span data-ttu-id="48882-261">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="48882-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="48882-262">Als u op de tegel Mimecast persoonlijke Portal in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Mimecast persoonlijke Portal.</span><span class="sxs-lookup"><span data-stu-id="48882-262">When you click the Mimecast Personal Portal tile in the Access Panel, you should get automatically signed-on to your Mimecast Personal Portal application.</span></span> <span data-ttu-id="48882-263">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="48882-263">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="48882-264">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="48882-264">Additional resources</span></span>

* [<span data-ttu-id="48882-265">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48882-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="48882-266">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="48882-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

