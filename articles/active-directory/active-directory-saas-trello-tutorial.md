---
title: 'Zelfstudie: Azure Active Directory-integratie met Trello | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Trello.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: d93667f16f2d72995e4a42e79e9125b8e3f6b07c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="3a63b-103">Zelfstudie: Azure Active Directory-integratie met Trello</span><span class="sxs-lookup"><span data-stu-id="3a63b-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="3a63b-104">In deze zelfstudie leert u hoe Trello integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3a63b-104">In this tutorial, you learn how to integrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3a63b-105">Trello integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="3a63b-105">Integrating Trello with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3a63b-106">U kunt beheren in Azure AD die toegang tot Trello heeft</span><span class="sxs-lookup"><span data-stu-id="3a63b-106">You can control in Azure AD who has access to Trello</span></span>
- <span data-ttu-id="3a63b-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Trello (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="3a63b-107">You can enable your users to automatically get signed-on to Trello (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3a63b-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="3a63b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3a63b-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3a63b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a63b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3a63b-110">Prerequisites</span></span>

<span data-ttu-id="3a63b-111">Voor het configureren van Azure AD-integratie met Trello, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="3a63b-111">To configure Azure AD integration with Trello, you need the following items:</span></span>

- <span data-ttu-id="3a63b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="3a63b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3a63b-113">Een Trello eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="3a63b-113">A Trello single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3a63b-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3a63b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3a63b-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="3a63b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3a63b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="3a63b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3a63b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3a63b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3a63b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="3a63b-118">Scenario description</span></span>
<span data-ttu-id="3a63b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="3a63b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3a63b-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="3a63b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3a63b-121">Trello uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3a63b-121">Adding Trello from the gallery</span></span>
2. <span data-ttu-id="3a63b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3a63b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-the-gallery"></a><span data-ttu-id="3a63b-123">Trello uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3a63b-123">Adding Trello from the gallery</span></span>
<span data-ttu-id="3a63b-124">Voor het configureren van de integratie van Trello in Azure AD, moet u Trello uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="3a63b-124">To configure the integration of Trello into Azure AD, you need to add Trello from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3a63b-125">**Als u wilt toevoegen Trello uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3a63b-125">**To add Trello from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3a63b-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3a63b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3a63b-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3a63b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3a63b-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3a63b-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="3a63b-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3a63b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="3a63b-133">Typ in het zoekvak **Trello**.</span><span class="sxs-lookup"><span data-stu-id="3a63b-133">In the search box, type **Trello**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. <span data-ttu-id="3a63b-135">Selecteer in het deelvenster resultaten **Trello**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="3a63b-135">In the results panel, select **Trello**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3a63b-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3a63b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3a63b-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Trello op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="3a63b-138">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3a63b-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Trello is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a63b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trello is to a user in Azure AD.</span></span> <span data-ttu-id="3a63b-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Trello tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="3a63b-140">In other words, a link relationship between an Azure AD user and the related user in Trello needs to be established.</span></span>

<span data-ttu-id="3a63b-141">Wijs in Trello, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="3a63b-141">In Trello, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3a63b-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Trello, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="3a63b-142">To configure and test Azure AD single sign-on with Trello, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3a63b-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3a63b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3a63b-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a63b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3a63b-145">**[Maken van een testgebruiker Trello](#creating-a-trello-test-user)**  - Trello die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="3a63b-145">**[Creating a Trello test user](#creating-a-trello-test-user)** - to have a counterpart of Britta Simon in Trello that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3a63b-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3a63b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3a63b-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="3a63b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3a63b-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="3a63b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3a63b-149">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Trello.</span><span class="sxs-lookup"><span data-stu-id="3a63b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="3a63b-150">**Voor het configureren van Azure AD eenmalige aanmelding met Trello, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3a63b-150">**To configure Azure AD single sign-on with Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="3a63b-151">In de Azure-portal op de **Trello** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="3a63b-151">In the Azure portal, on the **Trello** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="3a63b-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3a63b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. <span data-ttu-id="3a63b-155">Op de **Trello domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP geïnitieerd modus**, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3a63b-155">On the **Trello Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    <span data-ttu-id="3a63b-157">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="3a63b-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

4. <span data-ttu-id="3a63b-158">Op de **Trello domein en de URL's** sectie als u wilt configureren van de toepassing in **SP geïnitieerd modus**, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3a63b-158">On the **Trello Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="3a63b-160">a.</span><span class="sxs-lookup"><span data-stu-id="3a63b-160">a.</span></span> <span data-ttu-id="3a63b-161">Klik op de **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="3a63b-161">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="3a63b-162">b.</span><span class="sxs-lookup"><span data-stu-id="3a63b-162">b.</span></span> <span data-ttu-id="3a63b-163">In de **aanmelding op URL** textbox, typ een URL met het volgende patroon volgen:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="3a63b-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

    >[!NOTE]
    ><span data-ttu-id="3a63b-164">Deze krijgt u de  **\<enterprise\>**  slug van Trello.</span><span class="sxs-lookup"><span data-stu-id="3a63b-164">You should get the **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="3a63b-165">Als u de slug-waarde niet hebt, neem dan contact op met [Trello ondersteuningsteam](mailto:support@trello.com) ophalen van de slug voor u enterprise.</span><span class="sxs-lookup"><span data-stu-id="3a63b-165">If you don't have the slug value, contact [Trello support team](mailto:support@trello.com) to get the slug for you enterprise.</span></span>
    > 

5. <span data-ttu-id="3a63b-166">Trello toepassing verwacht de SAML-asserties naar specifieke kenmerken bevatten.</span><span class="sxs-lookup"><span data-stu-id="3a63b-166">Trello application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="3a63b-167">Configureer de volgende kenmerken voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="3a63b-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="3a63b-168">U kunt de waarden van deze kenmerken van beheren de **'Gebruikerskenmerken'** van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="3a63b-168">You can manage the values of these attributes from the **"User Attributes"** of the application.</span></span> <span data-ttu-id="3a63b-169">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="3a63b-169">The following screenshot shows an example for this.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. <span data-ttu-id="3a63b-171">Op de **SAML-token kenmerken** dialoogvenster uitvoeren voor elke rij in de onderstaande tabel wordt weergegeven op de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3a63b-171">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
    | <span data-ttu-id="3a63b-172">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="3a63b-172">Attribute Name</span></span> | <span data-ttu-id="3a63b-173">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="3a63b-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="3a63b-174">User.Email</span><span class="sxs-lookup"><span data-stu-id="3a63b-174">User.Email</span></span> | <span data-ttu-id="3a63b-175">User.mail</span><span class="sxs-lookup"><span data-stu-id="3a63b-175">user.mail</span></span> |
    | <span data-ttu-id="3a63b-176">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="3a63b-176">User.FirstName</span></span> | <span data-ttu-id="3a63b-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="3a63b-177">user.givenname</span></span> |
    | <span data-ttu-id="3a63b-178">User.LastName</span><span class="sxs-lookup"><span data-stu-id="3a63b-178">User.LastName</span></span> | <span data-ttu-id="3a63b-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="3a63b-179">user.surname</span></span> |

    <span data-ttu-id="3a63b-180">a.</span><span class="sxs-lookup"><span data-stu-id="3a63b-180">a.</span></span> <span data-ttu-id="3a63b-181">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3a63b-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="3a63b-184">b.</span><span class="sxs-lookup"><span data-stu-id="3a63b-184">b.</span></span> <span data-ttu-id="3a63b-185">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="3a63b-185">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

    <span data-ttu-id="3a63b-186">c.</span><span class="sxs-lookup"><span data-stu-id="3a63b-186">c.</span></span> <span data-ttu-id="3a63b-187">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="3a63b-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="3a63b-188">d.</span><span class="sxs-lookup"><span data-stu-id="3a63b-188">d.</span></span> <span data-ttu-id="3a63b-189">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3a63b-189">Click **Ok**.</span></span> 
 
7. <span data-ttu-id="3a63b-190">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3a63b-190">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. <span data-ttu-id="3a63b-192">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="3a63b-192">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3a63b-194">Op de **Trello configuratie** sectie, klikt u op **configureren Trello** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="3a63b-194">On the **Trello Configuration** section, click **Configure Trello** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3a63b-195">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="3a63b-195">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. <span data-ttu-id="3a63b-197">Eenmalige aanmelding voor uw toepassing is geconfigureerd, Ga naar [Trello SSO Ondernemingsconfiguratie](https://trello.com/sso-configuration) pagina verzenden [Trello ondersteuningsteam](mailto:support@trello.com) de **SAML Single Sign-On Service-URL** en Koppel de **certificaat (Base64)**.</span><span class="sxs-lookup"><span data-stu-id="3a63b-197">To get SSO configured for your application, go to [Trello enterprise SSO configuration](https://trello.com/sso-configuration) page to send [Trello support team](mailto:support@trello.com) the **SAML Single Sign-On Service URL** and attach the **Certificate (Base64)**.</span></span>

> [!TIP]
> <span data-ttu-id="3a63b-198">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="3a63b-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3a63b-199">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="3a63b-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3a63b-200">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3a63b-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3a63b-201">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3a63b-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="3a63b-202">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3a63b-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="3a63b-204">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3a63b-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3a63b-205">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3a63b-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3a63b-207">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3a63b-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3a63b-209">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3a63b-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3a63b-211">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3a63b-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3a63b-213">a.</span><span class="sxs-lookup"><span data-stu-id="3a63b-213">a.</span></span> <span data-ttu-id="3a63b-214">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3a63b-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3a63b-215">b.</span><span class="sxs-lookup"><span data-stu-id="3a63b-215">b.</span></span> <span data-ttu-id="3a63b-216">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3a63b-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3a63b-217">c.</span><span class="sxs-lookup"><span data-stu-id="3a63b-217">c.</span></span> <span data-ttu-id="3a63b-218">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="3a63b-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3a63b-219">d.</span><span class="sxs-lookup"><span data-stu-id="3a63b-219">d.</span></span> <span data-ttu-id="3a63b-220">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3a63b-220">Click **Create**.</span></span>
 
### <a name="creating-a-trello-test-user"></a><span data-ttu-id="3a63b-221">Een testgebruiker Trello maken</span><span class="sxs-lookup"><span data-stu-id="3a63b-221">Creating a Trello test user</span></span>

<span data-ttu-id="3a63b-222">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Trello maken.</span><span class="sxs-lookup"><span data-stu-id="3a63b-222">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="3a63b-223">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Trello maken.</span><span class="sxs-lookup"><span data-stu-id="3a63b-223">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="3a63b-224">Trello ondersteunt just-in-time-inrichting en een nieuw account is gemaakt de eerste keer dat u zich aanmeldt vanuit Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a63b-224">Trello supports just-in-time provisioning and a new account is created the first time you sign in from Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3a63b-225">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a63b-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3a63b-226">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Trello.</span><span class="sxs-lookup"><span data-stu-id="3a63b-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trello.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="3a63b-228">**Britta Simon om aan te wijzen Trello, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3a63b-228">**To assign Britta Simon to Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="3a63b-229">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3a63b-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="3a63b-231">Selecteer in de lijst met toepassingen **Trello**.</span><span class="sxs-lookup"><span data-stu-id="3a63b-231">In the applications list, select **Trello**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. <span data-ttu-id="3a63b-233">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="3a63b-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="3a63b-235">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="3a63b-235">Click **Add** button.</span></span> <span data-ttu-id="3a63b-236">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3a63b-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="3a63b-238">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="3a63b-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3a63b-239">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3a63b-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3a63b-240">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3a63b-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3a63b-241">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3a63b-241">Testing single sign-on</span></span>

<span data-ttu-id="3a63b-242">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="3a63b-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="3a63b-243">Als u op de tegel Trello in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Trello.</span><span class="sxs-lookup"><span data-stu-id="3a63b-243">When you click the Trello tile in the Access Panel, you should get automatically signed-on to your Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3a63b-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3a63b-244">Additional resources</span></span>

* [<span data-ttu-id="3a63b-245">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a63b-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3a63b-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3a63b-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

