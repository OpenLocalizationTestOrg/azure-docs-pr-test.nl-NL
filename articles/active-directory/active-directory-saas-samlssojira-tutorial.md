---
title: 'Zelfstudie: Azure Active Directory-integratie met SAML SSO voor Jira door resolutie GmbH | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en SAML SSO voor Jira door resolutie GmbH.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: cde5983710185d1e46a5601b16bbfb1c0fcae382
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a><span data-ttu-id="88af2-103">Zelfstudie: Azure Active Directory-integratie met SAML SSO voor Jira door resolutie GmbH</span><span class="sxs-lookup"><span data-stu-id="88af2-103">Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH</span></span>

<span data-ttu-id="88af2-104">In deze zelfstudie leert u het integreren van SAML SSO voor Jira door resolutie GmbH met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88af2-104">In this tutorial, you learn how to integrate SAML SSO for Jira by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88af2-105">Integratie van SAML SSO voor Jira door resolutie GmbH met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="88af2-105">Integrating SAML SSO for Jira by resolution GmbH with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="88af2-106">U kunt beheren in Azure AD die toegang tot SAML SSO voor Jira door resolutie GmbH heeft</span><span class="sxs-lookup"><span data-stu-id="88af2-106">You can control in Azure AD who has access to SAML SSO for Jira by resolution GmbH</span></span>
- <span data-ttu-id="88af2-107">U kunt uw gebruikers automatisch ophalen aangemeld bij SAML SSO voor Jira door resolutie GmbH (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="88af2-107">You can enable your users to automatically get signed-on to SAML SSO for Jira by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="88af2-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="88af2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="88af2-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="88af2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88af2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="88af2-110">Prerequisites</span></span>

<span data-ttu-id="88af2-111">Voor het configureren van Azure AD-integratie met SAML SSO voor Jira door resolutie GmbH, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="88af2-111">To configure Azure AD integration with SAML SSO for Jira by resolution GmbH, you need the following items:</span></span>

- <span data-ttu-id="88af2-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="88af2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="88af2-113">Een SAML SSO voor Jira door resolutie GmbH eenmalige aanmelding voor ingeschakelde abonnement</span><span class="sxs-lookup"><span data-stu-id="88af2-113">A SAML SSO for Jira by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="88af2-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="88af2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="88af2-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="88af2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="88af2-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="88af2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="88af2-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88af2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="88af2-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="88af2-118">Scenario description</span></span>
<span data-ttu-id="88af2-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="88af2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="88af2-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="88af2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88af2-121">SAML SSO voor Jira door resolutie GmbH uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="88af2-121">Adding SAML SSO for Jira by resolution GmbH from the gallery</span></span>
2. <span data-ttu-id="88af2-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="88af2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-the-gallery"></a><span data-ttu-id="88af2-123">SAML SSO voor Jira door resolutie GmbH uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="88af2-123">Adding SAML SSO for Jira by resolution GmbH from the gallery</span></span>
<span data-ttu-id="88af2-124">Voor het configureren van de integratie van SAML SSO voor Jira door resolutie GmbH in Azure AD, moet u SAML SSO voor Jira door resolutie GmbH uit de galerie toevoegt aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="88af2-124">To configure the integration of SAML SSO for Jira by resolution GmbH into Azure AD, you need to add SAML SSO for Jira by resolution GmbH from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="88af2-125">**Als u wilt toevoegen SAML SSO voor Jira resolutie GmbH uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="88af2-125">**To add SAML SSO for Jira by resolution GmbH from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="88af2-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="88af2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="88af2-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="88af2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="88af2-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="88af2-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="88af2-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="88af2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="88af2-133">Typ in het zoekvak **SAML SSO voor Jira door resolutie GmbH**.</span><span class="sxs-lookup"><span data-stu-id="88af2-133">In the search box, type **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. <span data-ttu-id="88af2-135">Selecteer in het deelvenster resultaten **SAML SSO voor Jira door resolutie GmbH**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="88af2-135">In the results panel, select **SAML SSO for Jira by resolution GmbH**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="88af2-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="88af2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="88af2-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met SAML SSO voor Jira door resolutie die GmbH op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="88af2-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="88af2-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de equivalente gebruiker in SAML SSO voor Jira door resolutie GmbH aan een gebruiker in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="88af2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Jira by resolution GmbH is to a user in Azure AD.</span></span> <span data-ttu-id="88af2-140">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in SAML SSO voor Jira door de resolutie GmbH moet tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="88af2-140">In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Jira by resolution GmbH needs to be established.</span></span>

<span data-ttu-id="88af2-141">Wijs in SAML SSO voor Jira door resolutie GmbH, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="88af2-141">In SAML SSO for Jira by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="88af2-142">Om te configureren en testen van Azure AD eenmalige aanmelding met SAML SSO voor Jira door resolutie GmbH, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="88af2-142">To configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="88af2-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="88af2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="88af2-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88af2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="88af2-145">**[Maken van een SAML SSO voor Jira door resolutie GmbH testgebruiker](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  - bevatten een equivalent van Britta Simon SAML SSO voor Jira door resolutie GmbH die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="88af2-145">**[Creating a SAML SSO for Jira by resolution GmbH test user](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Jira by resolution GmbH that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="88af2-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="88af2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="88af2-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="88af2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="88af2-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="88af2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="88af2-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw SAML SSO voor Jira configureren door de resolutie GmbH toepassing.</span><span class="sxs-lookup"><span data-stu-id="88af2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Jira by resolution GmbH application.</span></span>

<span data-ttu-id="88af2-150">**Voor het configureren van Azure AD eenmalige aanmelding met SAML SSO voor Jira door resolutie GmbH, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="88af2-150">**To configure Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="88af2-151">In de Azure-portal op de **SAML SSO voor Jira door resolutie GmbH** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="88af2-151">In the Azure portal, on the **SAML SSO for Jira by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="88af2-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="88af2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. <span data-ttu-id="88af2-155">Op de **SAML SSO voor Jira door resolutie GmbH domein en URL's** sectie als u wilt configureren van de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="88af2-155">On the **SAML SSO for Jira by resolution GmbH Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    <span data-ttu-id="88af2-157">a.</span><span class="sxs-lookup"><span data-stu-id="88af2-157">a.</span></span> <span data-ttu-id="88af2-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="88af2-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="88af2-159">b.</span><span class="sxs-lookup"><span data-stu-id="88af2-159">b.</span></span> <span data-ttu-id="88af2-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="88af2-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="88af2-161">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="88af2-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="88af2-162">Als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="88af2-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    <span data-ttu-id="88af2-164">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="88af2-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="88af2-165">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="88af2-165">These values are not real.</span></span> <span data-ttu-id="88af2-166">Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="88af2-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="88af2-167">Neem contact op met [SAML SSO voor Jira door resolutie GmbH Client ondersteuningsteam](https://www.resolution.de/go/support) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="88af2-167">Contact [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support) to get these values.</span></span> 

5. <span data-ttu-id="88af2-168">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="88af2-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. <span data-ttu-id="88af2-170">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="88af2-170">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="88af2-172">In een ander browservenster geopend, moet u zich aanmelden bij uw **SAML SSO voor Jira door resolutie GmbH beheerportal** als beheerder.</span><span class="sxs-lookup"><span data-stu-id="88af2-172">In a different web browser window, log in to your **SAML SSO for Jira by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="88af2-173">Beweeg de muisaanwijzer op het tandwiel en klik op de **invoegtoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="88af2-173">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. <span data-ttu-id="88af2-175">U omgeleid naar de pagina toegang als beheerder.</span><span class="sxs-lookup"><span data-stu-id="88af2-175">You are redirected to Administrator Access page.</span></span> <span data-ttu-id="88af2-176">Voer de **wachtwoord** en klik op **bevestigen** knop.</span><span class="sxs-lookup"><span data-stu-id="88af2-176">Enter the **Password** and click **Confirm** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. <span data-ttu-id="88af2-178">Klik onder sectie tabblad invoegtoepassingen op **vinden van nieuwe invoegtoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="88af2-178">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="88af2-179">Search **SAML eenmalige aanmelding op (SSO) voor JIRA** en klik op **installeren** knop voor het installeren van de nieuwe SAML-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="88af2-179">Search **SAML Single Sign On (SSO) for JIRA** and click **Install** button to install the new SAML plugin.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. <span data-ttu-id="88af2-181">De installatie van de invoegtoepassing wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="88af2-181">The plugin installation will start.</span></span> <span data-ttu-id="88af2-182">Klik op **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="88af2-182">Click **Close**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. <span data-ttu-id="88af2-185">Klik op **Beheren**.</span><span class="sxs-lookup"><span data-stu-id="88af2-185">Click **Manage**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. <span data-ttu-id="88af2-187">Klik op **configureren** voor het configureren van de nieuwe invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="88af2-187">Click **Configure** to configure the new plugin.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. <span data-ttu-id="88af2-189">Op **SAML-configuratie voor invoegtoepassing van SingleSignOn** pagina, klikt u op **toevoegen van extra identiteitsprovider** knop voor het configureren van de instellingen van de id-Provider.</span><span class="sxs-lookup"><span data-stu-id="88af2-189">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button to configure the settings of Identity Provider.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. <span data-ttu-id="88af2-191">Voer de volgende stappen uit op deze pagina:</span><span class="sxs-lookup"><span data-stu-id="88af2-191">Perform following steps on this page:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    <span data-ttu-id="88af2-193">a.</span><span class="sxs-lookup"><span data-stu-id="88af2-193">a.</span></span> <span data-ttu-id="88af2-194">Voeg **naam** van de id-Provider (bijvoorbeeld Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88af2-194">Add **Name** of the Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="88af2-195">b.</span><span class="sxs-lookup"><span data-stu-id="88af2-195">b.</span></span> <span data-ttu-id="88af2-196">Voeg **beschrijving** van de id-Provider (bijvoorbeeld Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88af2-196">Add **Description** of the Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="88af2-197">c.</span><span class="sxs-lookup"><span data-stu-id="88af2-197">c.</span></span> <span data-ttu-id="88af2-198">Klik op **XML** en selecteer de **metagegevens** bestand, dat u hebt gedownload vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="88af2-198">Click **XML** and select the **Metadata** file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="88af2-199">d.</span><span class="sxs-lookup"><span data-stu-id="88af2-199">d.</span></span> <span data-ttu-id="88af2-200">Klik op **Load** knop.</span><span class="sxs-lookup"><span data-stu-id="88af2-200">Click **Load** button.</span></span>

    <span data-ttu-id="88af2-201">e.</span><span class="sxs-lookup"><span data-stu-id="88af2-201">e.</span></span> <span data-ttu-id="88af2-202">Deze leest de IdP-metagegevens en de velden zoals gemarkeerd in de schermafbeelding gevuld.</span><span class="sxs-lookup"><span data-stu-id="88af2-202">It reads the IdP metadata and populates the fields as highlighted in the screenshot.</span></span> 

16. <span data-ttu-id="88af2-203">Klik op **instellingen opslaan** knop de instellingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="88af2-203">Click **Save settings** button to save the settings.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="88af2-205">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="88af2-205">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="88af2-206">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="88af2-206">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="88af2-207">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="88af2-207">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="88af2-208">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="88af2-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="88af2-209">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="88af2-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="88af2-211">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="88af2-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="88af2-212">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="88af2-212">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="88af2-214">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="88af2-214">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="88af2-216">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="88af2-216">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="88af2-218">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="88af2-218">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="88af2-220">a.</span><span class="sxs-lookup"><span data-stu-id="88af2-220">a.</span></span> <span data-ttu-id="88af2-221">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88af2-221">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="88af2-222">b.</span><span class="sxs-lookup"><span data-stu-id="88af2-222">b.</span></span> <span data-ttu-id="88af2-223">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="88af2-223">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="88af2-224">c.</span><span class="sxs-lookup"><span data-stu-id="88af2-224">c.</span></span> <span data-ttu-id="88af2-225">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="88af2-225">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="88af2-226">d.</span><span class="sxs-lookup"><span data-stu-id="88af2-226">d.</span></span> <span data-ttu-id="88af2-227">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="88af2-227">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a><span data-ttu-id="88af2-228">Maken van een SAML SSO voor Jira door resolutie GmbH testgebruiker</span><span class="sxs-lookup"><span data-stu-id="88af2-228">Creating a SAML SSO for Jira by resolution GmbH test user</span></span>

<span data-ttu-id="88af2-229">Om Azure AD-gebruikers aan te melden bij SAML SSO voor Jira door resolutie GmbH, moeten ze in SAML SSO voor Jira worden ingericht met behulp van de resolutie GmbH.</span><span class="sxs-lookup"><span data-stu-id="88af2-229">To enable Azure AD users to log in to SAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH.</span></span>  
<span data-ttu-id="88af2-230">In SAML SSO voor Jira door resolutie GmbH is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="88af2-230">In SAML SSO for Jira by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="88af2-231">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="88af2-231">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="88af2-232">Aanmelden bij uw SAML SSO voor Jira door resolutie GmbH bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="88af2-232">Log in to your SAML SSO for Jira by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="88af2-233">Beweeg de muisaanwijzer op het tandwiel en klik op de **Gebruikersbeheer**.</span><span class="sxs-lookup"><span data-stu-id="88af2-233">Hover on cog and click the **User management**.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. <span data-ttu-id="88af2-235">U wordt omgeleid naar de pagina beheerderstoegang in te voeren **wachtwoord** en klik op **bevestigen** knop.</span><span class="sxs-lookup"><span data-stu-id="88af2-235">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. <span data-ttu-id="88af2-237">Onder **Gebruikersbeheer** tabblad gedeelte, klikt u op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="88af2-237">Under **User management** tab section, click **create user**.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. <span data-ttu-id="88af2-239">Op de **'Een nieuwe gebruiker maken'** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="88af2-239">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    <span data-ttu-id="88af2-241">a.</span><span class="sxs-lookup"><span data-stu-id="88af2-241">a.</span></span> <span data-ttu-id="88af2-242">In de **e-mailadres** textbox, typ het e-mailadres van gebruiker, zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="88af2-242">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="88af2-243">b.</span><span class="sxs-lookup"><span data-stu-id="88af2-243">b.</span></span> <span data-ttu-id="88af2-244">In de **volledige naam** textbox, volledige naam van de gebruiker zoals Britta Simon type.</span><span class="sxs-lookup"><span data-stu-id="88af2-244">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="88af2-245">c.</span><span class="sxs-lookup"><span data-stu-id="88af2-245">c.</span></span> <span data-ttu-id="88af2-246">In de **gebruikersnaam** textbox, typ het e-mailadres van gebruiker, zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="88af2-246">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="88af2-247">d.</span><span class="sxs-lookup"><span data-stu-id="88af2-247">d.</span></span> <span data-ttu-id="88af2-248">In de **wachtwoord** textbox, typt u het wachtwoord van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="88af2-248">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="88af2-249">e.</span><span class="sxs-lookup"><span data-stu-id="88af2-249">e.</span></span> <span data-ttu-id="88af2-250">Klik op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="88af2-250">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="88af2-251">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="88af2-251">Assigning the Azure AD test user</span></span>

<span data-ttu-id="88af2-252">In deze sectie maakt inschakelen u Britta Simon SAML SSO voor Jira toegang verlenen door resolutie GmbH gebruikt Azure eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="88af2-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Jira by resolution GmbH.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="88af2-254">**Britta Simon om aan te wijzen SAML SSO voor Jira door resolutie GmbH, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="88af2-254">**To assign Britta Simon to SAML SSO for Jira by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="88af2-255">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="88af2-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="88af2-257">Selecteer in de lijst met toepassingen **SAML SSO voor Jira door resolutie GmbH**.</span><span class="sxs-lookup"><span data-stu-id="88af2-257">In the applications list, select **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. <span data-ttu-id="88af2-259">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="88af2-259">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="88af2-261">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="88af2-261">Click **Add** button.</span></span> <span data-ttu-id="88af2-262">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="88af2-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="88af2-264">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="88af2-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="88af2-265">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="88af2-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="88af2-266">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="88af2-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="88af2-267">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="88af2-267">Testing single sign-on</span></span>

<span data-ttu-id="88af2-268">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="88af2-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="88af2-269">Als u op het SAML SSO voor Jira door resolutie GmbH tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw SAML SSO voor Jira door resolutie GmbH toepassing.</span><span class="sxs-lookup"><span data-stu-id="88af2-269">When you click the SAML SSO for Jira by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Jira by resolution GmbH application.</span></span>
<span data-ttu-id="88af2-270">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="88af2-270">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="88af2-271">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="88af2-271">Additional resources</span></span>

* [<span data-ttu-id="88af2-272">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88af2-272">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="88af2-273">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="88af2-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

