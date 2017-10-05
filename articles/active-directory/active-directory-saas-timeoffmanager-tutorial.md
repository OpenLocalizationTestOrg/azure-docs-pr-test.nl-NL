---
title: 'Zelfstudie: Azure Active Directory-integratie met TimeOffManager | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en TimeOffManager.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 3f944ffbf704694b293b4b1e5bdb4f2c93ae35a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="1884b-103">Zelfstudie: Azure Active Directory-integratie met TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="1884b-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="1884b-104">In deze zelfstudie leert u hoe TimeOffManager integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1884b-104">In this tutorial, you learn how to integrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1884b-105">TimeOffManager integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1884b-105">Integrating TimeOffManager with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1884b-106">U kunt beheren in Azure AD die toegang tot TimeOffManager heeft</span><span class="sxs-lookup"><span data-stu-id="1884b-106">You can control in Azure AD who has access to TimeOffManager</span></span>
- <span data-ttu-id="1884b-107">U kunt uw gebruikers automatisch ophalen aangemeld bij TimeOffManager (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="1884b-107">You can enable your users to automatically get signed-on to TimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1884b-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="1884b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1884b-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1884b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1884b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1884b-110">Prerequisites</span></span>

<span data-ttu-id="1884b-111">Voor het configureren van Azure AD-integratie met TimeOffManager, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="1884b-111">To configure Azure AD integration with TimeOffManager, you need the following items:</span></span>

- <span data-ttu-id="1884b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1884b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1884b-113">Een TimeOffManager eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="1884b-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1884b-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1884b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1884b-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1884b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1884b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1884b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1884b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1884b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1884b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1884b-118">Scenario description</span></span>
<span data-ttu-id="1884b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1884b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1884b-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1884b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1884b-121">TimeOffManager uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1884b-121">Add TimeOffManager from the gallery</span></span>
2. <span data-ttu-id="1884b-122">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="1884b-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-the-gallery"></a><span data-ttu-id="1884b-123">TimeOffManager uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1884b-123">Add TimeOffManager from the gallery</span></span>
<span data-ttu-id="1884b-124">Voor het configureren van de integratie van TimeOffManager in Azure AD, moet u TimeOffManager uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1884b-124">To configure the integration of TimeOffManager into Azure AD, you need to add TimeOffManager from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1884b-125">**Als u wilt toevoegen TimeOffManager uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1884b-125">**To add TimeOffManager from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1884b-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1884b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1884b-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1884b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1884b-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1884b-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="1884b-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1884b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="1884b-133">Typ in het zoekvak **TimeOffManager**, selecteer **TimeOffManager** van resultaat deelvenster en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1884b-133">In the search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button to add the application.</span></span>

    ![Uit de galerie toevoegen](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1884b-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="1884b-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="1884b-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met TimeOffManager op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="1884b-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1884b-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in TimeOffManager is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1884b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TimeOffManager is to a user in Azure AD.</span></span> <span data-ttu-id="1884b-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in TimeOffManager tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="1884b-138">In other words, a link relationship between an Azure AD user and the related user in TimeOffManager needs to be established.</span></span>

<span data-ttu-id="1884b-139">Wijs in TimeOffManager, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="1884b-139">In TimeOffManager, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1884b-140">Om te configureren en testen van Azure AD eenmalige aanmelding met TimeOffManager, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="1884b-140">To configure and test Azure AD single sign-on with TimeOffManager, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1884b-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1884b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1884b-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1884b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1884b-143">**[Maak een testgebruiker TimeOffManager](#create-a-timeoffmanager-test-user)**  - TimeOffManager die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="1884b-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - to have a counterpart of Britta Simon in TimeOffManager that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1884b-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1884b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1884b-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1884b-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1884b-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1884b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1884b-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing TimeOffManager configureren.</span><span class="sxs-lookup"><span data-stu-id="1884b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="1884b-148">**Voor het configureren van Azure AD eenmalige aanmelding met TimeOffManager, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1884b-148">**To configure Azure AD single sign-on with TimeOffManager, perform the following steps:**</span></span>

1. <span data-ttu-id="1884b-149">In de Azure-portal op de **TimeOffManager** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1884b-149">In the Azure portal, on the **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1884b-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1884b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML op basis van eenmalige aanmelding](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. <span data-ttu-id="1884b-153">Op de **TimeOffManager domein en de URL's** sectie, voert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="1884b-153">On the **TimeOffManager Domain and URLs** section, perform the following:</span></span>

     ![Sectie TimeOffManager domein en URL 's](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="1884b-155">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span><span class="sxs-lookup"><span data-stu-id="1884b-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1884b-156">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="1884b-156">This value is not real.</span></span> <span data-ttu-id="1884b-157">Deze waarde bijwerken met de werkelijke antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="1884b-157">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="1884b-158">U krijgt deze waarde van **voor eenmalige aanmelding instellingenpagina** waarmee wordt uitgelegd later in de zelfstudie of neem contact op met [TimeOffManager ondersteuningsteam](http://www.timeoffmanager.com/contact-us.aspx).</span><span class="sxs-lookup"><span data-stu-id="1884b-158">You can get this value from **Single Sign on settings page** which is explained later in the tutorial or Contact [TimeOffManager support team](http://www.timeoffmanager.com/contact-us.aspx).</span></span>
 
4. <span data-ttu-id="1884b-159">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1884b-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Certificaat voor ondertekening van SAML-sectie](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. <span data-ttu-id="1884b-161">Het doel van deze sectie is om een overzicht van gebruikers om te verifiëren TimeOffManger aan hun account in Azure AD dat gebruikmaakt van Federatie op basis van het SAML-protocol in staat te.</span><span class="sxs-lookup"><span data-stu-id="1884b-161">The objective of this section is to outline how to enable users to authenticate to TimeOffManger with their account in Azure AD using federation based on the SAML protocol.</span></span>
    
    <span data-ttu-id="1884b-162">Uw toepassing TimeOffManger verwacht de SAML-asserties in een specifieke indeling waarvoor u aangepaste kenmerktoewijzingen toevoegen aan uw configuratie van SAML-token kenmerken.</span><span class="sxs-lookup"><span data-stu-id="1884b-162">Your TimeOffManger application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="1884b-163">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="1884b-163">The following screenshot shows an example for this.</span></span>

    <span data-ttu-id="1884b-164">![SAML-token kenmerken](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml-token kenmerken")</span><span class="sxs-lookup"><span data-stu-id="1884b-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="1884b-165">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="1884b-165">Attribute Name</span></span> | <span data-ttu-id="1884b-166">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="1884b-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="1884b-167">Voornaam</span><span class="sxs-lookup"><span data-stu-id="1884b-167">Firstname</span></span> |<span data-ttu-id="1884b-168">User.givenName</span><span class="sxs-lookup"><span data-stu-id="1884b-168">User.givenname</span></span> |
    | <span data-ttu-id="1884b-169">Achternaam</span><span class="sxs-lookup"><span data-stu-id="1884b-169">Lastname</span></span> |<span data-ttu-id="1884b-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="1884b-170">User.surname</span></span> |
    | <span data-ttu-id="1884b-171">E-mail</span><span class="sxs-lookup"><span data-stu-id="1884b-171">Email</span></span> |<span data-ttu-id="1884b-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="1884b-172">User.mail</span></span> |
    
    <span data-ttu-id="1884b-173">a.</span><span class="sxs-lookup"><span data-stu-id="1884b-173">a.</span></span>  <span data-ttu-id="1884b-174">Voor elke gegevensrij in de bovenstaande tabel, klikt u op **gebruikerskenmerk toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1884b-174">For each data row in the table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="1884b-175">![SAML-token kenmerken](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml-token kenmerken")</span><span class="sxs-lookup"><span data-stu-id="1884b-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="1884b-176">![SAML-token kenmerken](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml-token kenmerken")</span><span class="sxs-lookup"><span data-stu-id="1884b-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="1884b-177">b.</span><span class="sxs-lookup"><span data-stu-id="1884b-177">b.</span></span>  <span data-ttu-id="1884b-178">In de **kenmerknaam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="1884b-178">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="1884b-179">c.</span><span class="sxs-lookup"><span data-stu-id="1884b-179">c.</span></span>  <span data-ttu-id="1884b-180">In de **kenmerkwaarde** textbox, selecteert u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="1884b-180">In the **Attribute Value** textbox, select the attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="1884b-181">d.</span><span class="sxs-lookup"><span data-stu-id="1884b-181">d.</span></span>  <span data-ttu-id="1884b-182">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1884b-182">Click **Ok**.</span></span>
    
6. <span data-ttu-id="1884b-183">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1884b-183">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="1884b-185">Op de **TimeOffManager configuratie** sectie, klikt u op **configureren TimeOffManager** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="1884b-185">On the **TimeOffManager Configuration** section, click **Configure TimeOffManager** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1884b-186">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="1884b-186">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuratiesectie TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. <span data-ttu-id="1884b-188">In een ander browservenster, meld u bij uw bedrijf TimeOffManager site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="1884b-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

9. <span data-ttu-id="1884b-189">Ga naar **Account \> Opties Account \> eenmalige aanmelding instellingen**.</span><span class="sxs-lookup"><span data-stu-id="1884b-189">Go to **Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="1884b-190">![Eenmalige aanmelding instellingen](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="1884b-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="1884b-191">In de **instellingen voor eenmalige aanmelding** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1884b-191">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="1884b-192">![Eenmalige aanmelding instellingen](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="1884b-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="1884b-193">a.</span><span class="sxs-lookup"><span data-stu-id="1884b-193">a.</span></span> <span data-ttu-id="1884b-194">Open uw base-64 gecodeerde certificaat in Kladblok, Kopieer de inhoud ervan naar het Klembord en plak het gehele certificaat in **X.509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="1884b-194">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="1884b-195">b.</span><span class="sxs-lookup"><span data-stu-id="1884b-195">b.</span></span> <span data-ttu-id="1884b-196">In **Idp verlener** textbox, plak de waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1884b-196">In **Idp Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="1884b-197">c.</span><span class="sxs-lookup"><span data-stu-id="1884b-197">c.</span></span> <span data-ttu-id="1884b-198">In **IdP eindpunt-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1884b-198">In **IdP Endpoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="1884b-199">d.</span><span class="sxs-lookup"><span data-stu-id="1884b-199">d.</span></span> <span data-ttu-id="1884b-200">Als **afdwingen SAML**, selecteer **Nee**.</span><span class="sxs-lookup"><span data-stu-id="1884b-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="1884b-201">e.</span><span class="sxs-lookup"><span data-stu-id="1884b-201">e.</span></span> <span data-ttu-id="1884b-202">Als **gebruikers automatisch maken**, selecteer **Ja**.</span><span class="sxs-lookup"><span data-stu-id="1884b-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="1884b-203">f.</span><span class="sxs-lookup"><span data-stu-id="1884b-203">f.</span></span> <span data-ttu-id="1884b-204">In **afmelding URL** textbox, plak de waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1884b-204">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="1884b-205">g.</span><span class="sxs-lookup"><span data-stu-id="1884b-205">g.</span></span> <span data-ttu-id="1884b-206">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1884b-206">click **Save Changes**.</span></span>

11. <span data-ttu-id="1884b-207">In **voor eenmalige aanmelding instellingen** pagina, Kopieer de waarde van **Assertion Consumer Service-URL** en plak deze in de **antwoord-URL** in het tekstvak onder **TimeOffManager Domein- en URL's** sectie in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1884b-207">In **Single Sign on settings** page, copy the value of **Assertion Consumer Service URL** and paste it in the **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="1884b-208">![Eenmalige aanmelding instellingen](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="1884b-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="1884b-209">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="1884b-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1884b-210">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="1884b-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1884b-211">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1884b-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1884b-212">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1884b-212">Create an Azure AD test user</span></span>
<span data-ttu-id="1884b-213">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1884b-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="1884b-215">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1884b-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1884b-216">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1884b-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1884b-218">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1884b-218">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Gebruikers en groepen--> alle gebruikers](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1884b-220">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1884b-220">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Knop toevoegen](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1884b-222">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1884b-222">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Dialoogvenster op de gebruikerspagina](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1884b-224">a.</span><span class="sxs-lookup"><span data-stu-id="1884b-224">a.</span></span> <span data-ttu-id="1884b-225">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1884b-225">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1884b-226">b.</span><span class="sxs-lookup"><span data-stu-id="1884b-226">b.</span></span> <span data-ttu-id="1884b-227">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1884b-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1884b-228">c.</span><span class="sxs-lookup"><span data-stu-id="1884b-228">c.</span></span> <span data-ttu-id="1884b-229">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1884b-229">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1884b-230">d.</span><span class="sxs-lookup"><span data-stu-id="1884b-230">d.</span></span> <span data-ttu-id="1884b-231">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1884b-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="1884b-232">Een testgebruiker TimeOffManager maken</span><span class="sxs-lookup"><span data-stu-id="1884b-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="1884b-233">Om in te schakelen gebruikers van Azure AD aan te melden bij TimeOffManager, moeten ze worden ingericht op TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="1884b-233">In order to enable Azure AD users to log into TimeOffManager, they must be provisioned to TimeOffManager.</span></span>  

<span data-ttu-id="1884b-234">TimeOffManager ondersteunt alleen in de tijd van gebruikersinrichting.</span><span class="sxs-lookup"><span data-stu-id="1884b-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="1884b-235">Er is geen actie-item voor u.</span><span class="sxs-lookup"><span data-stu-id="1884b-235">There is no action item for you.</span></span>  

<span data-ttu-id="1884b-236">De gebruikers worden automatisch toegevoegd tijdens de eerste aanmelding met eenmalige aanmelding op.</span><span class="sxs-lookup"><span data-stu-id="1884b-236">The users are added automatically during the first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="1884b-237">U kunt andere TimeOffManager gebruiker account hulpmiddelen voor het maken of API's die is geleverd door TimeOffManager voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="1884b-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager to provision Azure AD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1884b-238">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="1884b-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="1884b-239">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="1884b-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TimeOffManager.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="1884b-241">**Britta Simon om aan te wijzen TimeOffManager, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1884b-241">**To assign Britta Simon to TimeOffManager, perform the following steps:**</span></span>

1. <span data-ttu-id="1884b-242">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1884b-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1884b-244">Selecteer in de lijst met toepassingen **TimeOffManager**.</span><span class="sxs-lookup"><span data-stu-id="1884b-244">In the applications list, select **TimeOffManager**.</span></span>

    ![TimeOffManager in lijst met Apps](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. <span data-ttu-id="1884b-246">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1884b-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="1884b-248">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1884b-248">Click **Add** button.</span></span> <span data-ttu-id="1884b-249">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1884b-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="1884b-251">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1884b-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1884b-252">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1884b-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1884b-253">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1884b-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1884b-254">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1884b-254">Test single sign-on</span></span>

<span data-ttu-id="1884b-255">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="1884b-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1884b-256">Als u op de tegel TimeOffManager in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="1884b-256">When you click the TimeOffManager tile in the Access Panel, you should get automatically signed-on to your TimeOffManager application.</span></span> <span data-ttu-id="1884b-257">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1884b-257">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1884b-258">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1884b-258">Additional resources</span></span>

* [<span data-ttu-id="1884b-259">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1884b-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1884b-260">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1884b-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

