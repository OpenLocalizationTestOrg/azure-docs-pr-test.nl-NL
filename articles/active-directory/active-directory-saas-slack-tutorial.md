---
title: 'Zelfstudie: Azure Active Directory-integratie met Slack | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en de toegestane vertraging.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 5aca630b2077d3f7d4ce9273ee668ed6a5f9843d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="7c8e5-103">Zelfstudie: Azure Active Directory-integratie met Slack</span><span class="sxs-lookup"><span data-stu-id="7c8e5-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="7c8e5-104">In deze zelfstudie leert u hoe Slack integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7c8e5-104">In this tutorial, you learn how to integrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7c8e5-105">Vertraging integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7c8e5-105">Integrating Slack with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7c8e5-106">U kunt beheren in Azure AD die toegang tot de toegestane vertraging heeft</span><span class="sxs-lookup"><span data-stu-id="7c8e5-106">You can control in Azure AD who has access to Slack</span></span>
- <span data-ttu-id="7c8e5-107">U kunt uw gebruikers automatisch ophalen aangemeld bij de vertraging (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="7c8e5-107">You can enable your users to automatically get signed-on to Slack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7c8e5-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="7c8e5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7c8e5-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7c8e5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c8e5-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7c8e5-110">Prerequisites</span></span>

<span data-ttu-id="7c8e5-111">Voor het configureren van Azure AD-integratie met Slack, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="7c8e5-111">To configure Azure AD integration with Slack, you need the following items:</span></span>

- <span data-ttu-id="7c8e5-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="7c8e5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7c8e5-113">Een toegestane eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="7c8e5-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7c8e5-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7c8e5-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="7c8e5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7c8e5-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7c8e5-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7c8e5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7c8e5-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="7c8e5-118">Scenario description</span></span>
<span data-ttu-id="7c8e5-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7c8e5-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="7c8e5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7c8e5-121">Vertraging in de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="7c8e5-121">Adding Slack from the gallery</span></span>
2. <span data-ttu-id="7c8e5-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7c8e5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-the-gallery"></a><span data-ttu-id="7c8e5-123">Vertraging in de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="7c8e5-123">Adding Slack from the gallery</span></span>
<span data-ttu-id="7c8e5-124">Voor het configureren van de integratie van Slack met Azure AD, moet u de vertraging in de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-124">To configure the integration of Slack into Azure AD, you need to add Slack from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7c8e5-125">**Als u wilt toevoegen Slack uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7c8e5-125">**To add Slack from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7c8e5-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7c8e5-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7c8e5-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="7c8e5-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="7c8e5-133">Typ in het zoekvak **Slack**.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-133">In the search box, type **Slack**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="7c8e5-135">Selecteer in het deelvenster resultaten **Slack**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-135">In the results panel, select **Slack**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7c8e5-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7c8e5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7c8e5-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Slack op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7c8e5-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Slack is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Slack is to a user in Azure AD.</span></span> <span data-ttu-id="7c8e5-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Slack tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-140">In other words, a link relationship between an Azure AD user and the related user in Slack needs to be established.</span></span>

<span data-ttu-id="7c8e5-141">Wijs in Slack, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-141">In Slack, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7c8e5-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Slack, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="7c8e5-142">To configure and test Azure AD single sign-on with Slack, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7c8e5-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7c8e5-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7c8e5-145">**[Maken van een toegestane testgebruiker](#creating-a-slack-test-user)**  - vertraging die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - to have a counterpart of Britta Simon in Slack that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7c8e5-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7c8e5-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7c8e5-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="7c8e5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7c8e5-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing toegestane configureren.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="7c8e5-150">**Voor het configureren van Azure AD eenmalige aanmelding met Slack, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7c8e5-150">**To configure Azure AD single sign-on with Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="7c8e5-151">In de Azure-portal op de **Slack** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-151">In the Azure portal, on the **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="7c8e5-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="7c8e5-155">Op de **Slack-domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7c8e5-155">On the **Slack Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="7c8e5-157">a.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-157">a.</span></span> <span data-ttu-id="7c8e5-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="7c8e5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="7c8e5-159">b.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-159">b.</span></span> <span data-ttu-id="7c8e5-160">In de **id** textbox, typ de URL:`https://slack.com`</span><span class="sxs-lookup"><span data-stu-id="7c8e5-160">In the **Identifier** textbox, type the URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7c8e5-161">De waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-161">The value is not real.</span></span> <span data-ttu-id="7c8e5-162">U moet de waarde wordt bijgewerkt met de werkelijke aanmelding op de URL.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-162">You have to update the value with the actual Sign On URL.</span></span> <span data-ttu-id="7c8e5-163">Neem contact op met [toegestane ondersteuningsteam](https://slack.com/help/contact) de waarde op te halen</span><span class="sxs-lookup"><span data-stu-id="7c8e5-163">Contact [Slack support team](https://slack.com/help/contact) to get the value</span></span>
     
4. <span data-ttu-id="7c8e5-164">De SAML-asserties verwacht toegestane toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-164">Slack application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="7c8e5-165">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-165">Configure the following claims for this application.</span></span> <span data-ttu-id="7c8e5-166">U kunt beheren de waarden van deze kenmerken van de '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="7c8e5-167">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-167">The following screenshot shows an example for this.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="7c8e5-169">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster Selecteer **user.mail** als **gebruikers-id** en voor elke rij in de onderstaande tabel wordt weergegeven, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7c8e5-169">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="7c8e5-170">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="7c8e5-170">Attribute Name</span></span> | <span data-ttu-id="7c8e5-171">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="7c8e5-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="7c8e5-172">Voornaam</span><span class="sxs-lookup"><span data-stu-id="7c8e5-172">first_name</span></span> | <span data-ttu-id="7c8e5-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="7c8e5-173">user.givenname</span></span> |
    | <span data-ttu-id="7c8e5-174">Achternaam</span><span class="sxs-lookup"><span data-stu-id="7c8e5-174">last_name</span></span> | <span data-ttu-id="7c8e5-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="7c8e5-175">user.surname</span></span> |
    | <span data-ttu-id="7c8e5-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="7c8e5-176">User.Email</span></span> | <span data-ttu-id="7c8e5-177">User.mail</span><span class="sxs-lookup"><span data-stu-id="7c8e5-177">user.mail</span></span> |  
    | <span data-ttu-id="7c8e5-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="7c8e5-178">User.Username</span></span> | <span data-ttu-id="7c8e5-179">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="7c8e5-179">user.userprincipalname</span></span> |

    <span data-ttu-id="7c8e5-180">a.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-180">a.</span></span> <span data-ttu-id="7c8e5-181">Klik op **kenmerk** openen **kenmerk bewerken** dialoogvenster vak en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7c8e5-181">Click on **Attribute** to open **Edit Attribute** dialog box and perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="7c8e5-183">a.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-183">a.</span></span> <span data-ttu-id="7c8e5-184">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="7c8e5-185">b.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-185">b.</span></span> <span data-ttu-id="7c8e5-186">Van de **waarde** , selecteert u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-186">From the **Value** list, select the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7c8e5-187">c.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-187">c.</span></span> <span data-ttu-id="7c8e5-188">Klik op **OK**</span><span class="sxs-lookup"><span data-stu-id="7c8e5-188">Click **OK**</span></span>

6. <span data-ttu-id="7c8e5-189">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-189">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="7c8e5-191">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-191">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7c8e5-193">Op de **Slack configuratie** sectie, klikt u op **Slack configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-193">On the **Slack Configuration** section, click **Configure Slack** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7c8e5-194">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="7c8e5-194">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="7c8e5-196">In een ander browservenster, meld u aan bij uw site toegestane bedrijf als beheerder.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-196">In a different web browser window, log in to your Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="7c8e5-197">Navigeer naar **Microsoft Azure AD** Ga vervolgens naar **instellingen Team**.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-197">Navigate to **Microsoft Azure AD** then go to **Team Settings**.</span></span>

     ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="7c8e5-199">In de **instellingen Team** sectie, klikt u op de **verificatie** tabblad en klik vervolgens op **Wijzigingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-199">In the **Team Settings** section, click the **Authentication** tab, and then click **Change Settings**.</span></span>

     ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="7c8e5-201">Op de **SAML-verificatie-instellingen** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7c8e5-201">On the **SAML Authentication Settings** dialog, perform the following steps:</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="7c8e5-203">a.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-203">a.</span></span>  <span data-ttu-id="7c8e5-204">In de **SAML 2.0-eindpunt (HTTP)** textbox, plak de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-204">In the **SAML 2.0 Endpoint (HTTP)** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7c8e5-205">b.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-205">b.</span></span>  <span data-ttu-id="7c8e5-206">In de **identiteit Provider verlener** textbox, plak de waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-206">In the **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7c8e5-207">c.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-207">c.</span></span>  <span data-ttu-id="7c8e5-208">Open uw gedownloade certificaat-bestand in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **openbaar certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-208">Open your downloaded certificate file in notepad, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>

    <span data-ttu-id="7c8e5-209">d.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-209">d.</span></span> <span data-ttu-id="7c8e5-210">Configureer de bovenstaande drie instellingen voor uw team toegestane.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-210">Configure the above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="7c8e5-211">Voor meer informatie over de instellingen, gaat u naar de **vertraging van SSO configuratiehandleiding** hier.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-211">For more information about the settings, please find the **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="7c8e5-212">e.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-212">e.</span></span>  <span data-ttu-id="7c8e5-213">Klik op **configuratie op te slaan**.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users to change their email address**.

    e.  Select **Allow users to choose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="7c8e5-214">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="7c8e5-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7c8e5-215">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7c8e5-216">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7c8e5-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7c8e5-217">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="7c8e5-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="7c8e5-218">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="7c8e5-220">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7c8e5-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7c8e5-221">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7c8e5-223">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7c8e5-225">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7c8e5-227">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7c8e5-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7c8e5-229">a.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-229">a.</span></span> <span data-ttu-id="7c8e5-230">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7c8e5-231">b.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-231">b.</span></span> <span data-ttu-id="7c8e5-232">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7c8e5-233">c.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-233">c.</span></span> <span data-ttu-id="7c8e5-234">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7c8e5-235">d.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-235">d.</span></span> <span data-ttu-id="7c8e5-236">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="7c8e5-237">Een toegestane testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="7c8e5-237">Creating a Slack test user</span></span>

<span data-ttu-id="7c8e5-238">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Slack genoemd.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-238">The objective of this section is to create a user called Britta Simon in Slack.</span></span> <span data-ttu-id="7c8e5-239">Vertraging ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="7c8e5-240">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-240">There is no action item for you in this section.</span></span> <span data-ttu-id="7c8e5-241">Een nieuwe gebruiker is gemaakt tijdens een poging tot toegang tot de toegestane vertraging als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-241">A new user is created during an attempt to access Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="7c8e5-242">Als u een gebruiker handmatig maken wilt, moet u contact op met [toegestane ondersteuningsteam](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="7c8e5-242">If you need to create a user manually, you need to Contact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7c8e5-243">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c8e5-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7c8e5-244">In deze sectie maakt inschakelen u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang met Slack.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Slack.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="7c8e5-246">**Als u wilt toewijzen Britta Simon met Slack, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7c8e5-246">**To assign Britta Simon to Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="7c8e5-247">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="7c8e5-249">Selecteer in de lijst met toepassingen **Slack**.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-249">In the applications list, select **Slack**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="7c8e5-251">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="7c8e5-253">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-253">Click **Add** button.</span></span> <span data-ttu-id="7c8e5-254">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="7c8e5-256">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7c8e5-257">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7c8e5-258">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7c8e5-259">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7c8e5-259">Testing single sign-on</span></span>

<span data-ttu-id="7c8e5-260">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7c8e5-261">Wanneer u klikt op de toegestane tegel in het deelvenster toegang u moet ophalen automatisch aangemeld bij uw toegestane toepassing.</span><span class="sxs-lookup"><span data-stu-id="7c8e5-261">When you click the Slack tile in the Access Panel, you should get automatically signed-on to your Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7c8e5-262">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7c8e5-262">Additional resources</span></span>

* [<span data-ttu-id="7c8e5-263">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c8e5-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7c8e5-264">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7c8e5-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

