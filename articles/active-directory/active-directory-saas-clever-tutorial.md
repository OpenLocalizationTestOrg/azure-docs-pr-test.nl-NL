---
title: 'Zelfstudie: Azure Active Directory-integratie met Clever | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Clever.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 84082ff567e37d7fff80be9e089c67cfab911861
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="3d5e9-103">Zelfstudie: Azure Active Directory-integratie met Clever</span><span class="sxs-lookup"><span data-stu-id="3d5e9-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="3d5e9-104">In deze zelfstudie leert u hoe Clever integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3d5e9-104">In this tutorial, you learn how to integrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3d5e9-105">Clever integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="3d5e9-105">Integrating Clever with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3d5e9-106">U kunt beheren in Azure AD die toegang tot Clever heeft.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-106">You can control in Azure AD who has access to Clever.</span></span>
- <span data-ttu-id="3d5e9-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Clever (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-107">You can enable your users to automatically get signed-on to Clever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3d5e9-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="3d5e9-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3d5e9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d5e9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3d5e9-110">Prerequisites</span></span>

<span data-ttu-id="3d5e9-111">Voor het configureren van Azure AD-integratie met Clever, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="3d5e9-111">To configure Azure AD integration with Clever, you need the following items:</span></span>

- <span data-ttu-id="3d5e9-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="3d5e9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3d5e9-113">Een slimme eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="3d5e9-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3d5e9-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3d5e9-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="3d5e9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3d5e9-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3d5e9-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d5e9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3d5e9-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="3d5e9-118">Scenario description</span></span>
<span data-ttu-id="3d5e9-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3d5e9-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="3d5e9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3d5e9-121">Clever uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3d5e9-121">Adding Clever from the gallery</span></span>
2. <span data-ttu-id="3d5e9-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3d5e9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-the-gallery"></a><span data-ttu-id="3d5e9-123">Clever uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3d5e9-123">Adding Clever from the gallery</span></span>
<span data-ttu-id="3d5e9-124">Voor het configureren van de integratie van Clever in Azure AD, moet u Clever uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-124">To configure the integration of Clever into Azure AD, you need to add Clever from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3d5e9-125">**Als u wilt toevoegen Clever uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3d5e9-125">**To add Clever from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3d5e9-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="3d5e9-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3d5e9-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="3d5e9-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="3d5e9-133">Typ in het zoekvak **Clever**, selecteer **Clever** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-133">In the search box, type **Clever**, select **Clever** from result panel then click **Add** button to add the application.</span></span>

    ![Slimme in de lijst met resultaten](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3d5e9-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d5e9-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3d5e9-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Clever op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3d5e9-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Clever is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Clever is to a user in Azure AD.</span></span> <span data-ttu-id="3d5e9-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Clever tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-138">In other words, a link relationship between an Azure AD user and the related user in Clever needs to be established.</span></span>

<span data-ttu-id="3d5e9-139">Wijs in Clever, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-139">In Clever, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3d5e9-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Clever, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="3d5e9-140">To configure and test Azure AD single sign-on with Clever, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3d5e9-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3d5e9-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3d5e9-143">**[Maak een slimme testgebruiker](#create-a-clever-test-user)**  - Clever die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-143">**[Create a Clever test user](#create-a-clever-test-user)** - to have a counterpart of Britta Simon in Clever that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3d5e9-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3d5e9-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3d5e9-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="3d5e9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3d5e9-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing slimme configureren.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="3d5e9-148">**Voor het configureren van Azure AD eenmalige aanmelding met Clever, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3d5e9-148">**To configure Azure AD single sign-on with Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="3d5e9-149">In de Azure-portal op de **Clever** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-149">In the Azure portal, on the **Clever** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="3d5e9-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. <span data-ttu-id="3d5e9-153">Op de **slimme domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3d5e9-153">On the **Clever Domain and URLs** section, perform the following steps:</span></span>

    ![Slimme domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="3d5e9-155">a.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-155">a.</span></span> <span data-ttu-id="3d5e9-156">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://clever.com/in/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="3d5e9-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="3d5e9-157">b.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-157">b.</span></span> <span data-ttu-id="3d5e9-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://clever.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="3d5e9-158">In the **Identifier** textbox, type a URL using the following pattern: `https://clever.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3d5e9-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-159">These values are not real.</span></span> <span data-ttu-id="3d5e9-160">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3d5e9-161">Neem contact op met [slimme Client ondersteuningsteam](https://clever.com/about/contact/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-161">Contact [Clever Client support team](https://clever.com/about/contact/) to get these values.</span></span>

4. <span data-ttu-id="3d5e9-162">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. <span data-ttu-id="3d5e9-164">De slimme toepassing de SAML-asserties verwacht in een specifieke indeling waarvoor u het toevoegen van aangepast kenmerktoewijzingen aan uw **SAML-Token kenmerken** configuratie.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-164">The Clever application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="3d5e9-165">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-165">The following screenshot shows an example for this.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. <span data-ttu-id="3d5e9-167">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding hierboven en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3d5e9-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="3d5e9-168">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="3d5e9-168">Attribute Name</span></span>  | <span data-ttu-id="3d5e9-169">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="3d5e9-169">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="3d5e9-170">clever.student.credentials.district\_gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="3d5e9-170">clever.student.credentials.district\_username</span></span>  | <span data-ttu-id="3d5e9-171">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="3d5e9-171">user.userprincipalname</span></span> |
    | <span data-ttu-id="3d5e9-172">Voornaam</span><span class="sxs-lookup"><span data-stu-id="3d5e9-172">Firstname</span></span>  | <span data-ttu-id="3d5e9-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="3d5e9-173">user.givenname</span></span> |
    | <span data-ttu-id="3d5e9-174">Achternaam</span><span class="sxs-lookup"><span data-stu-id="3d5e9-174">Lastname</span></span>  | <span data-ttu-id="3d5e9-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="3d5e9-175">user.surname</span></span> |    

    <span data-ttu-id="3d5e9-176">a.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-176">a.</span></span> <span data-ttu-id="3d5e9-177">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="3d5e9-180">b.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-180">b.</span></span> <span data-ttu-id="3d5e9-181">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="3d5e9-182">c.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-182">c.</span></span> <span data-ttu-id="3d5e9-183">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-183">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="3d5e9-184">d.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-184">d.</span></span> <span data-ttu-id="3d5e9-185">Laat de **Namespace** textbox leeg.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-185">Leave the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="3d5e9-186">d.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-186">d.</span></span> <span data-ttu-id="3d5e9-187">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-187">Click **Ok**.</span></span>     

5. <span data-ttu-id="3d5e9-188">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-188">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3d5e9-190">Voor het genereren van de **metagegevens** -url, de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3d5e9-190">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="3d5e9-191">a.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-191">a.</span></span> <span data-ttu-id="3d5e9-192">Klik op **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-192">Click **App registrations**.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    <span data-ttu-id="3d5e9-194">b.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-194">b.</span></span> <span data-ttu-id="3d5e9-195">Klik op **eindpunten** openen **eindpunten** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-195">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    <span data-ttu-id="3d5e9-197">c.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-197">c.</span></span> <span data-ttu-id="3d5e9-198">Klik op de knop kopiëren om te kopiëren **DOCUMENT met federatieve metagegevens** url en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-198">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    <span data-ttu-id="3d5e9-200">d.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-200">d.</span></span> <span data-ttu-id="3d5e9-201">Nu gaat u naar de eigenschappenpagina van **Clever** en kopieer de **toepassings-Id** met **kopie** knop en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-201">Now go to the property page of **Clever** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    <span data-ttu-id="3d5e9-203">e.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-203">e.</span></span> <span data-ttu-id="3d5e9-204">Genereren van de **metagegevens-URL** met het volgende patroon volgen:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="3d5e9-204">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>   

9. <span data-ttu-id="3d5e9-205">In een ander browservenster, meld u aan bij uw site slimme bedrijf als beheerder.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-205">In a different web browser window, log in to your Clever company site as an administrator.</span></span>

10. <span data-ttu-id="3d5e9-206">Klik in de werkbalk op **directe aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-206">In the toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="3d5e9-207">![Directe aanmelding](./media/active-directory-saas-clever-tutorial/ic798984.png "directe aanmelding")</span><span class="sxs-lookup"><span data-stu-id="3d5e9-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span></span>

11. <span data-ttu-id="3d5e9-208">Op de **directe aanmelding** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3d5e9-208">On the **Instant Login** page, perform the following steps:</span></span>
      
      <span data-ttu-id="3d5e9-209">![Directe aanmelding](./media/active-directory-saas-clever-tutorial/ic798985.png "directe aanmelding")</span><span class="sxs-lookup"><span data-stu-id="3d5e9-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span></span>
      
      <span data-ttu-id="3d5e9-210">a.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-210">a.</span></span> <span data-ttu-id="3d5e9-211">Typ de **aanmeldings-URL**.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-211">Type the **Login URL**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="3d5e9-212">De **aanmeldings-URL** is een aangepaste waarde.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-212">The **Login URL** is a custom value.</span></span> <span data-ttu-id="3d5e9-213">Neem contact op met [slimme Client ondersteuningsteam](https://clever.com/about/contact/) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-213">Contact [Clever Client support team](https://clever.com/about/contact/) to get this value.</span></span>
      
      <span data-ttu-id="3d5e9-214">b.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-214">b.</span></span> <span data-ttu-id="3d5e9-215">Als **identiteitsbeheersysteem**, selecteer **ADFS**.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-215">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="3d5e9-216">c.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-216">c.</span></span> <span data-ttu-id="3d5e9-217">Typ de **metagegevens-URL** in de **metagegevens-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-217">Type the **Metadata URL** in the **Metadata URL** textbox.</span></span>
      
      <span data-ttu-id="3d5e9-218">d.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-218">d.</span></span> <span data-ttu-id="3d5e9-219">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-219">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3d5e9-220">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="3d5e9-220">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3d5e9-221">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-221">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3d5e9-222">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3d5e9-222">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3d5e9-223">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3d5e9-223">Create an Azure AD test user</span></span>

<span data-ttu-id="3d5e9-224">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-224">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="3d5e9-226">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3d5e9-226">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3d5e9-227">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-227">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3d5e9-229">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-229">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3d5e9-231">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-231">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3d5e9-233">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3d5e9-233">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3d5e9-235">a.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-235">a.</span></span> <span data-ttu-id="3d5e9-236">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-236">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3d5e9-237">b.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-237">b.</span></span> <span data-ttu-id="3d5e9-238">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-238">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3d5e9-239">c.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-239">c.</span></span> <span data-ttu-id="3d5e9-240">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-240">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3d5e9-241">d.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-241">d.</span></span> <span data-ttu-id="3d5e9-242">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-242">Click **Create**.</span></span>
 
### <a name="create-a-clever-test-user"></a><span data-ttu-id="3d5e9-243">Een slimme testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3d5e9-243">Create a Clever test user</span></span>

<span data-ttu-id="3d5e9-244">Om Azure AD-gebruikers zich aanmelden bij Clever, moeten ze worden ingericht in Clever.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-244">To enable Azure AD users to log in to Clever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="3d5e9-245">In geval van een Clever, werken met [slimme Client ondersteuningsteam](https://clever.com/about/contact/) toevoegen van de gebruikers in de slimme platform.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-245">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add the users in the Clever platform.</span></span> <span data-ttu-id="3d5e9-246">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-246">Users must be created and activated before you use single sign-on.</span></span> 

>[!NOTE]
><span data-ttu-id="3d5e9-247">U kunt een andere gebruiker slimme account hulpmiddelen voor het maken of API's die is geleverd door Clever voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-247">You can use any other Clever user account creation tools or APIs provided by Clever to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3d5e9-248">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="3d5e9-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="3d5e9-249">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Clever.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Clever.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="3d5e9-251">**Britta Simon om aan te wijzen Clever, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3d5e9-251">**To assign Britta Simon to Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="3d5e9-252">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="3d5e9-254">Selecteer in de lijst met toepassingen **Clever**.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-254">In the applications list, select **Clever**.</span></span>

    ![De Clever koppelen in de lijst met toepassingen](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. <span data-ttu-id="3d5e9-256">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-256">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="3d5e9-258">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-258">Click **Add** button.</span></span> <span data-ttu-id="3d5e9-259">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="3d5e9-261">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3d5e9-262">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3d5e9-263">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3d5e9-264">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3d5e9-264">Test single sign-on</span></span>

<span data-ttu-id="3d5e9-265">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-265">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3d5e9-266">Wanneer u klikt op de slimme tegel in het deelvenster toegang u moet ophalen automatisch aangemeld bij uw slimme toepassing.</span><span class="sxs-lookup"><span data-stu-id="3d5e9-266">When you click the Clever tile in the Access Panel, you should get automatically signed-on to your Clever application.</span></span>
<span data-ttu-id="3d5e9-267">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3d5e9-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3d5e9-268">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3d5e9-268">Additional resources</span></span>

* [<span data-ttu-id="3d5e9-269">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3d5e9-269">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3d5e9-270">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3d5e9-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

