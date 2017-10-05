---
title: 'Zelfstudie: Azure Active Directory-integratie met Veracode | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Veracode.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d49349c5ae08e67d91e30967f3644623211823ce
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="b60a5-103">Zelfstudie: Azure Active Directory-integratie met Veracode</span><span class="sxs-lookup"><span data-stu-id="b60a5-103">Tutorial: Azure Active Directory integration with Veracode</span></span>

<span data-ttu-id="b60a5-104">In deze zelfstudie leert u hoe Veracode integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b60a5-104">In this tutorial, you learn how to integrate Veracode with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b60a5-105">Veracode integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b60a5-105">Integrating Veracode with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b60a5-106">U kunt beheren in Azure AD die toegang tot Veracode heeft.</span><span class="sxs-lookup"><span data-stu-id="b60a5-106">You can control in Azure AD who has access to Veracode.</span></span>
- <span data-ttu-id="b60a5-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Veracode (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b60a5-107">You can enable your users to automatically get signed-on to Veracode (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b60a5-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="b60a5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b60a5-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b60a5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b60a5-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b60a5-110">Prerequisites</span></span>

<span data-ttu-id="b60a5-111">Voor het configureren van Azure AD-integratie met Veracode, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b60a5-111">To configure Azure AD integration with Veracode, you need the following items:</span></span>

- <span data-ttu-id="b60a5-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b60a5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b60a5-113">Een Veracode eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b60a5-113">A Veracode single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b60a5-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b60a5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b60a5-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b60a5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b60a5-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b60a5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b60a5-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b60a5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b60a5-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b60a5-118">Scenario description</span></span>
<span data-ttu-id="b60a5-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b60a5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b60a5-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b60a5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b60a5-121">Veracode uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b60a5-121">Add Veracode from the gallery</span></span>
2. <span data-ttu-id="b60a5-122">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="b60a5-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-veracode-from-the-gallery"></a><span data-ttu-id="b60a5-123">Veracode uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b60a5-123">Add Veracode from the gallery</span></span>
<span data-ttu-id="b60a5-124">Voor het configureren van de integratie van Veracode in Azure AD, moet u Veracode uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b60a5-124">To configure the integration of Veracode into Azure AD, you need to add Veracode from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b60a5-125">**Als u wilt toevoegen Veracode uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b60a5-125">**To add Veracode from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b60a5-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b60a5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="b60a5-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b60a5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b60a5-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b60a5-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="b60a5-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b60a5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="b60a5-133">Typ in het zoekvak **Veracode**, selecteer **Veracode** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b60a5-133">In the search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button to add the application.</span></span>

    ![Veracode in de lijst met resultaten](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b60a5-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="b60a5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b60a5-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Veracode op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b60a5-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b60a5-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Veracode is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b60a5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Veracode is to a user in Azure AD.</span></span> <span data-ttu-id="b60a5-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Veracode tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="b60a5-138">In other words, a link relationship between an Azure AD user and the related user in Veracode needs to be established.</span></span>

<span data-ttu-id="b60a5-139">Wijs in Veracode, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="b60a5-139">In Veracode, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b60a5-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Veracode, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="b60a5-140">To configure and test Azure AD single sign-on with Veracode, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b60a5-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b60a5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b60a5-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b60a5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b60a5-143">**[Maak een testgebruiker Veracode](#create-a-veracode-test-user)**  - Veracode die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="b60a5-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - to have a counterpart of Britta Simon in Veracode that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b60a5-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b60a5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b60a5-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b60a5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b60a5-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b60a5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b60a5-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Veracode configureren.</span><span class="sxs-lookup"><span data-stu-id="b60a5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Veracode application.</span></span>

<span data-ttu-id="b60a5-148">**Voor het configureren van Azure AD eenmalige aanmelding met Veracode, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b60a5-148">**To configure Azure AD single sign-on with Veracode, perform the following steps:**</span></span>

1. <span data-ttu-id="b60a5-149">In de Azure-portal op de **Veracode** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b60a5-149">In the Azure portal, on the **Veracode** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b60a5-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b60a5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. <span data-ttu-id="b60a5-153">Op de **Veracode domein en de URL's** sectie, de gebruiker heeft geen alle stappen uitvoeren als de app al vooraf is geïntegreerd met Azure.</span><span class="sxs-lookup"><span data-stu-id="b60a5-153">On the **Veracode Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. <span data-ttu-id="b60a5-155">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b60a5-155">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. <span data-ttu-id="b60a5-157">Het doel van deze sectie is om een overzicht van gebruikers om te verifiëren Veracode aan hun account in Azure AD dat gebruikmaakt van Federatie op basis van het SAML-protocol in staat te.</span><span class="sxs-lookup"><span data-stu-id="b60a5-157">The objective of this section is to outline how to enable users to authenticate to Veracode with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="b60a5-158">Uw toepassing Veracode verwacht de SAML-asserties in een specifieke indeling waarvoor u het toevoegen van aangepast kenmerktoewijzingen aan uw **saml-token kenmerken** configuratie.</span><span class="sxs-lookup"><span data-stu-id="b60a5-158">Your Veracode application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> <span data-ttu-id="b60a5-159">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="b60a5-159">The following screenshot shows an example for this.</span></span>
    
    <span data-ttu-id="b60a5-160">![Kenmerken](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="b60a5-160">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span></span>

6. <span data-ttu-id="b60a5-161">Als u wilt de vereiste kenmerktoewijzingen toevoegen, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b60a5-161">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="b60a5-162">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="b60a5-162">Attribute Name</span></span> | <span data-ttu-id="b60a5-163">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="b60a5-163">Attribute Value</span></span> |
    |--- |--- |
    | <span data-ttu-id="b60a5-164">Voornaam</span><span class="sxs-lookup"><span data-stu-id="b60a5-164">firstname</span></span> |<span data-ttu-id="b60a5-165">User.givenName</span><span class="sxs-lookup"><span data-stu-id="b60a5-165">User.givenname</span></span> |
    | <span data-ttu-id="b60a5-166">Achternaam</span><span class="sxs-lookup"><span data-stu-id="b60a5-166">lastname</span></span> |<span data-ttu-id="b60a5-167">User.surname</span><span class="sxs-lookup"><span data-stu-id="b60a5-167">User.surname</span></span> |
    | <span data-ttu-id="b60a5-168">E-mail</span><span class="sxs-lookup"><span data-stu-id="b60a5-168">email</span></span> |<span data-ttu-id="b60a5-169">User.mail</span><span class="sxs-lookup"><span data-stu-id="b60a5-169">User.mail</span></span> |
    
    <span data-ttu-id="b60a5-170">a.</span><span class="sxs-lookup"><span data-stu-id="b60a5-170">a.</span></span> <span data-ttu-id="b60a5-171">Voor elke gegevensrij in de bovenstaande tabel, klikt u op **gebruikerskenmerk toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b60a5-171">For each data row in the table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="b60a5-172">![Kenmerken](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="b60a5-172">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span></span>
    
    <span data-ttu-id="b60a5-173">![Kenmerken](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="b60a5-173">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span></span>
    
    <span data-ttu-id="b60a5-174">b.</span><span class="sxs-lookup"><span data-stu-id="b60a5-174">b.</span></span> <span data-ttu-id="b60a5-175">In de **kenmerknaam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="b60a5-175">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="b60a5-176">c.</span><span class="sxs-lookup"><span data-stu-id="b60a5-176">c.</span></span> <span data-ttu-id="b60a5-177">In de **kenmerkwaarde** textbox, selecteert u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="b60a5-177">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b60a5-178">d.</span><span class="sxs-lookup"><span data-stu-id="b60a5-178">d.</span></span> <span data-ttu-id="b60a5-179">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b60a5-179">Click **Ok**.</span></span>

7. <span data-ttu-id="b60a5-180">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b60a5-180">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b60a5-182">Op de **Veracode configuratie** sectie, klikt u op **configureren Veracode** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="b60a5-182">On the **Veracode Configuration** section, click **Configure Veracode** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b60a5-183">Kopieer de **SAML entiteit-ID** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="b60a5-183">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Veracode configuratie](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. <span data-ttu-id="b60a5-185">In een ander browservenster, meld u bij uw bedrijf Veracode site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b60a5-185">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

10. <span data-ttu-id="b60a5-186">Klik in het menu bovenaan op **instellingen**, en klik vervolgens op **Admin**.</span><span class="sxs-lookup"><span data-stu-id="b60a5-186">In the menu on the top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="b60a5-187">![Beheer](./media/active-directory-saas-veracode-tutorial/ic802911.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="b60a5-187">![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")</span></span>

11. <span data-ttu-id="b60a5-188">Klik op de **SAML** tabblad.</span><span class="sxs-lookup"><span data-stu-id="b60a5-188">Click the **SAML** tab.</span></span>

12. <span data-ttu-id="b60a5-189">In de **organisatie SAML-instellingen** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b60a5-189">In the **Organization SAML Settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="b60a5-190">![Beheer](./media/active-directory-saas-veracode-tutorial/ic802912.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="b60a5-190">![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")</span></span>
   
    <span data-ttu-id="b60a5-191">a.</span><span class="sxs-lookup"><span data-stu-id="b60a5-191">a.</span></span>  <span data-ttu-id="b60a5-192">In **verlener** textbox, plak de waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b60a5-192">In  **Issuer** textbox, paste the value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="b60a5-193">b.</span><span class="sxs-lookup"><span data-stu-id="b60a5-193">b.</span></span> <span data-ttu-id="b60a5-194">Als u wilt uploaden uw gedownloade certificaat vanuit Azure-portal, klikt u op **bestand kiezen**.</span><span class="sxs-lookup"><span data-stu-id="b60a5-194">To upload your downloaded certificate from Azure portal, click **Choose File**.</span></span>
   
    <span data-ttu-id="b60a5-195">c.</span><span class="sxs-lookup"><span data-stu-id="b60a5-195">c.</span></span> <span data-ttu-id="b60a5-196">Selecteer **Self-registratie inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="b60a5-196">Select **Enable Self Registration**.</span></span>

13. <span data-ttu-id="b60a5-197">In de **Self-instellingen voor statusregistratie** sectie, het uitvoeren van de volgende stappen uit en klik vervolgens op **opslaan**:</span><span class="sxs-lookup"><span data-stu-id="b60a5-197">In the **Self Registration Settings** section, perform the following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="b60a5-198">![Beheer](./media/active-directory-saas-veracode-tutorial/ic802913.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="b60a5-198">![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")</span></span>
   
    <span data-ttu-id="b60a5-199">a.</span><span class="sxs-lookup"><span data-stu-id="b60a5-199">a.</span></span> <span data-ttu-id="b60a5-200">Als **nieuwe gebruikersactivering**, selecteer **Nee activering vereist**.</span><span class="sxs-lookup"><span data-stu-id="b60a5-200">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="b60a5-201">b.</span><span class="sxs-lookup"><span data-stu-id="b60a5-201">b.</span></span> <span data-ttu-id="b60a5-202">Als **gebruiker Gegevensupdates**, selecteer **voorkeur Veracode gebruikersgegevens**.</span><span class="sxs-lookup"><span data-stu-id="b60a5-202">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="b60a5-203">c.</span><span class="sxs-lookup"><span data-stu-id="b60a5-203">c.</span></span> <span data-ttu-id="b60a5-204">Voor **Details van SAML-kenmerk**, selecteert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="b60a5-204">For **SAML Attribute Details**, select the following:</span></span>
      * <span data-ttu-id="b60a5-205">**Gebruikersrollen**</span><span class="sxs-lookup"><span data-stu-id="b60a5-205">**User Roles**</span></span>
      * <span data-ttu-id="b60a5-206">**Beleid beheerder**</span><span class="sxs-lookup"><span data-stu-id="b60a5-206">**Policy Administrator**</span></span>
      * <span data-ttu-id="b60a5-207">**Revisor**</span><span class="sxs-lookup"><span data-stu-id="b60a5-207">**Reviewer**</span></span>
      * <span data-ttu-id="b60a5-208">**Beveiliging Lead**</span><span class="sxs-lookup"><span data-stu-id="b60a5-208">**Security Lead**</span></span>
      * <span data-ttu-id="b60a5-209">**Executive**</span><span class="sxs-lookup"><span data-stu-id="b60a5-209">**Executive**</span></span>
      * <span data-ttu-id="b60a5-210">**Indienings**</span><span class="sxs-lookup"><span data-stu-id="b60a5-210">**Submitter**</span></span>
      * <span data-ttu-id="b60a5-211">**Maker**</span><span class="sxs-lookup"><span data-stu-id="b60a5-211">**Creator**</span></span>
      * <span data-ttu-id="b60a5-212">**Alle scannen typen**</span><span class="sxs-lookup"><span data-stu-id="b60a5-212">**All Scan Types**</span></span>
      * <span data-ttu-id="b60a5-213">**Lidmaatschap van een team**</span><span class="sxs-lookup"><span data-stu-id="b60a5-213">**Team Memberships**</span></span>
      * <span data-ttu-id="b60a5-214">**Standaardteam**</span><span class="sxs-lookup"><span data-stu-id="b60a5-214">**Default Team**</span></span>

> [!TIP]
> <span data-ttu-id="b60a5-215">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="b60a5-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b60a5-216">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="b60a5-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b60a5-217">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b60a5-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b60a5-218">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b60a5-218">Create an Azure AD test user</span></span>

<span data-ttu-id="b60a5-219">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b60a5-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="b60a5-221">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b60a5-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b60a5-222">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="b60a5-222">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b60a5-224">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b60a5-224">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b60a5-226">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b60a5-226">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b60a5-228">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b60a5-228">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b60a5-230">a.</span><span class="sxs-lookup"><span data-stu-id="b60a5-230">a.</span></span> <span data-ttu-id="b60a5-231">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b60a5-231">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b60a5-232">b.</span><span class="sxs-lookup"><span data-stu-id="b60a5-232">b.</span></span> <span data-ttu-id="b60a5-233">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b60a5-233">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b60a5-234">c.</span><span class="sxs-lookup"><span data-stu-id="b60a5-234">c.</span></span> <span data-ttu-id="b60a5-235">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="b60a5-235">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b60a5-236">d.</span><span class="sxs-lookup"><span data-stu-id="b60a5-236">d.</span></span> <span data-ttu-id="b60a5-237">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b60a5-237">Click **Create**.</span></span>
 
### <a name="create-a-veracode-test-user"></a><span data-ttu-id="b60a5-238">Een testgebruiker Veracode maken</span><span class="sxs-lookup"><span data-stu-id="b60a5-238">Create a Veracode test user</span></span>
<span data-ttu-id="b60a5-239">Om in te schakelen gebruikers van Azure AD aan te melden bij Veracode, moeten ze worden ingericht in Veracode.</span><span class="sxs-lookup"><span data-stu-id="b60a5-239">In order to enable Azure AD users to log into Veracode, they must be provisioned into Veracode.</span></span> <span data-ttu-id="b60a5-240">In het geval van Veracode is inrichting een geautomatiseerde taak.</span><span class="sxs-lookup"><span data-stu-id="b60a5-240">In the case of Veracode, provisioning is an automated task.</span></span> <span data-ttu-id="b60a5-241">Er is geen actie-item voor u.</span><span class="sxs-lookup"><span data-stu-id="b60a5-241">There is no action item for you.</span></span> <span data-ttu-id="b60a5-242">Gebruikers worden automatisch gemaakt indien nodig tijdens de eerste eenmalige aanmelding poging.</span><span class="sxs-lookup"><span data-stu-id="b60a5-242">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="b60a5-243">U kunt andere Veracode gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Veracode voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="b60a5-243">You can use any other Veracode user account creation tools or APIs provided by Veracode to provision Azure AD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b60a5-244">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="b60a5-244">Assign the Azure AD test user</span></span>

<span data-ttu-id="b60a5-245">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Veracode.</span><span class="sxs-lookup"><span data-stu-id="b60a5-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Veracode.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="b60a5-247">**Britta Simon om aan te wijzen Veracode, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b60a5-247">**To assign Britta Simon to Veracode, perform the following steps:**</span></span>

1. <span data-ttu-id="b60a5-248">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b60a5-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b60a5-250">Selecteer in de lijst met toepassingen **Veracode**.</span><span class="sxs-lookup"><span data-stu-id="b60a5-250">In the applications list, select **Veracode**.</span></span>

    ![De koppeling Veracode in de lijst met toepassingen](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. <span data-ttu-id="b60a5-252">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b60a5-252">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="b60a5-254">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b60a5-254">Click **Add** button.</span></span> <span data-ttu-id="b60a5-255">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b60a5-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="b60a5-257">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b60a5-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b60a5-258">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b60a5-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b60a5-259">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b60a5-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b60a5-260">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b60a5-260">Test single sign-on</span></span>

<span data-ttu-id="b60a5-261">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b60a5-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b60a5-262">Als u op de tegel Veracode in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Veracode.</span><span class="sxs-lookup"><span data-stu-id="b60a5-262">When you click the Veracode tile in the Access Panel, you should get automatically signed-on to your Veracode application.</span></span>
<span data-ttu-id="b60a5-263">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b60a5-263">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b60a5-264">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b60a5-264">Additional resources</span></span>

* [<span data-ttu-id="b60a5-265">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b60a5-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b60a5-266">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b60a5-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

