---
title: 'Zelfstudie: Azure Active Directory-integratie met Pluralsight | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Pluralsight.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 62429643a108665544e42001d264046b5db1ec97
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a><span data-ttu-id="600d5-103">Zelfstudie: Azure Active Directory-integratie met Pluralsight</span><span class="sxs-lookup"><span data-stu-id="600d5-103">Tutorial: Azure Active Directory integration with Pluralsight</span></span>

<span data-ttu-id="600d5-104">In deze zelfstudie leert u hoe Pluralsight integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="600d5-104">In this tutorial, you learn how to integrate Pluralsight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="600d5-105">Pluralsight integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="600d5-105">Integrating Pluralsight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="600d5-106">U kunt beheren in Azure AD die toegang tot Pluralsight heeft</span><span class="sxs-lookup"><span data-stu-id="600d5-106">You can control in Azure AD who has access to Pluralsight</span></span>
- <span data-ttu-id="600d5-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Pluralsight (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="600d5-107">You can enable your users to automatically get signed-on to Pluralsight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="600d5-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="600d5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="600d5-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="600d5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="600d5-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="600d5-110">Prerequisites</span></span>

<span data-ttu-id="600d5-111">Voor het configureren van Azure AD-integratie met Pluralsight, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="600d5-111">To configure Azure AD integration with Pluralsight, you need the following items:</span></span>

- <span data-ttu-id="600d5-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="600d5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="600d5-113">Een Pluralsight eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="600d5-113">A Pluralsight single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="600d5-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="600d5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="600d5-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="600d5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="600d5-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="600d5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="600d5-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="600d5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="600d5-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="600d5-118">Scenario description</span></span>
<span data-ttu-id="600d5-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="600d5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="600d5-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="600d5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="600d5-121">Pluralsight uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="600d5-121">Adding Pluralsight from the gallery</span></span>
2. <span data-ttu-id="600d5-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="600d5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pluralsight-from-the-gallery"></a><span data-ttu-id="600d5-123">Pluralsight uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="600d5-123">Adding Pluralsight from the gallery</span></span>
<span data-ttu-id="600d5-124">Voor het configureren van de integratie van Pluralsight in Azure AD, moet u Pluralsight uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="600d5-124">To configure the integration of Pluralsight into Azure AD, you need to add Pluralsight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="600d5-125">**Als u wilt toevoegen Pluralsight uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="600d5-125">**To add Pluralsight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="600d5-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="600d5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="600d5-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="600d5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="600d5-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="600d5-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="600d5-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="600d5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="600d5-133">Typ in het zoekvak **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="600d5-133">In the search box, type **Pluralsight**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_search.png)

5. <span data-ttu-id="600d5-135">Selecteer in het deelvenster resultaten **Pluralsight**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="600d5-135">In the results panel, select **Pluralsight**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="600d5-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="600d5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="600d5-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Pluralsight op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="600d5-138">In this section, you configure and test Azure AD single sign-on with Pluralsight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="600d5-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Pluralsight is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="600d5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pluralsight is to a user in Azure AD.</span></span> <span data-ttu-id="600d5-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Pluralsight tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="600d5-140">In other words, a link relationship between an Azure AD user and the related user in Pluralsight needs to be established.</span></span>

<span data-ttu-id="600d5-141">Wijs in Pluralsight, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="600d5-141">In Pluralsight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="600d5-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Pluralsight, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="600d5-142">To configure and test Azure AD single sign-on with Pluralsight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="600d5-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="600d5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="600d5-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="600d5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="600d5-145">**[Maken van een testgebruiker Pluralsight](#creating-a-pluralsight-test-user)**  - Pluralsight die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="600d5-145">**[Creating a Pluralsight test user](#creating-a-pluralsight-test-user)** - to have a counterpart of Britta Simon in Pluralsight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="600d5-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="600d5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="600d5-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="600d5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="600d5-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="600d5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="600d5-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Pluralsight configureren.</span><span class="sxs-lookup"><span data-stu-id="600d5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pluralsight application.</span></span>

<span data-ttu-id="600d5-150">**Voor het configureren van Azure AD eenmalige aanmelding met Pluralsight, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="600d5-150">**To configure Azure AD single sign-on with Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="600d5-151">In de Azure-portal op de **Pluralsight** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="600d5-151">In the Azure portal, on the **Pluralsight** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="600d5-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="600d5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. <span data-ttu-id="600d5-155">Op de **Pluralsight domein en de URL's** sectie, voert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="600d5-155">On the **Pluralsight Domain and URLs** section, perform the following:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    <span data-ttu-id="600d5-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<instance name>.pluralsight.com/sso/<company name>`</span><span class="sxs-lookup"><span data-stu-id="600d5-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.pluralsight.com/sso/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="600d5-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="600d5-158">This value is not real.</span></span> <span data-ttu-id="600d5-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="600d5-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="600d5-160">Neem contact op met [Pluralsight Client ondersteuningsteam](mailto:support@pluralsight.com) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="600d5-160">Contact [Pluralsight Client support team](mailto:support@pluralsight.com) to get this value.</span></span> 
 


4. <span data-ttu-id="600d5-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="600d5-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. <span data-ttu-id="600d5-163">Het doel van deze sectie is Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in de toepassing Pluralsight configureren.</span><span class="sxs-lookup"><span data-stu-id="600d5-163">The objective of this section is to enable Azure AD single sign-on in the Azure portal and to configure SSO in the Pluralsight application.</span></span>

    <span data-ttu-id="600d5-164">De toepassing Pluralsight verwacht de SAML-asserties in een specifieke indeling waarvoor u aangepaste kenmerktoewijzingen toevoegen aan uw configuratie van SAML-token kenmerken.</span><span class="sxs-lookup"><span data-stu-id="600d5-164">The Pluralsight application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="600d5-165">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="600d5-165">The following screenshot shows an example for this.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    ><span data-ttu-id="600d5-167">U kunt ook toevoegen de **'Unieke ID'** kenmerk met de juiste waarde zoals werknemer-id of iets anders dat tegemoetkomt aan voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="600d5-167">You can also add the **"Unique ID"** attribute with the appropriate value like EmployeeID or something else which suits for your organization.</span></span> <span data-ttu-id="600d5-168">Zoals u ziet, is dit niet het vereiste kenmerk; u kunt echter toevoegen om de gebruiker uniek identificeren.</span><span class="sxs-lookup"><span data-stu-id="600d5-168">Also note that this is not the required attribute; however, you can add it to  identify the unique user.</span></span> 

6. <span data-ttu-id="600d5-169">Toevoegen van de vereiste **SAML-token kenmerken**, voor elke rij in de onderstaande tabel wordt weergegeven, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="600d5-169">To add the required **SAML token attributes**, for each row shown in the table below, perform the following steps:</span></span>
   
   | <span data-ttu-id="600d5-170">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="600d5-170">Attribute Name</span></span> | <span data-ttu-id="600d5-171">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="600d5-171">Attribute Value</span></span> |
   | ---| --- |
   | <span data-ttu-id="600d5-172">Voornaam</span><span class="sxs-lookup"><span data-stu-id="600d5-172">First Name</span></span> |<span data-ttu-id="600d5-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="600d5-173">user.givenname</span></span> |
   | <span data-ttu-id="600d5-174">Achternaam</span><span class="sxs-lookup"><span data-stu-id="600d5-174">Last Name</span></span> |<span data-ttu-id="600d5-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="600d5-175">user.surname</span></span> |
   | <span data-ttu-id="600d5-176">E-mail</span><span class="sxs-lookup"><span data-stu-id="600d5-176">Email</span></span> |<span data-ttu-id="600d5-177">User.mail</span><span class="sxs-lookup"><span data-stu-id="600d5-177">user.mail</span></span> |
   
   <span data-ttu-id="600d5-178">a.</span><span class="sxs-lookup"><span data-stu-id="600d5-178">a.</span></span> <span data-ttu-id="600d5-179">Klik op **gebruikerskenmerk toevoegen** openen de **toevoegen gebruiker Attribure** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="600d5-179">Click **add user attribute** to open the **Add User Attribure** dialog.</span></span>
    
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   <span data-ttu-id="600d5-181">b.</span><span class="sxs-lookup"><span data-stu-id="600d5-181">b.</span></span> <span data-ttu-id="600d5-182">In de **kenmerknaam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="600d5-182">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
  
   <span data-ttu-id="600d5-183">c.</span><span class="sxs-lookup"><span data-stu-id="600d5-183">c.</span></span> <span data-ttu-id="600d5-184">Van de **kenmerkwaarde** , selecteert u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="600d5-184">From the **Attribute Value** list, select the attribute value shown for that row.</span></span>
  
   <span data-ttu-id="600d5-185">d.</span><span class="sxs-lookup"><span data-stu-id="600d5-185">d.</span></span> <span data-ttu-id="600d5-186">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="600d5-186">Click **Ok**.</span></span>    

7. <span data-ttu-id="600d5-187">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="600d5-187">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="600d5-189">Als u eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, neem contact op met [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team en het metagegevensbestand van de gedownloade bieden.</span><span class="sxs-lookup"><span data-stu-id="600d5-189">To get SSO configured for your application, contact [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team and provide the downloaded metadata file.</span></span>

> [!TIP]
> <span data-ttu-id="600d5-190">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="600d5-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="600d5-191">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="600d5-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="600d5-192">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="600d5-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="600d5-193">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="600d5-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="600d5-194">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="600d5-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="600d5-196">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="600d5-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="600d5-197">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="600d5-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="600d5-199">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="600d5-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="600d5-201">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="600d5-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="600d5-203">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="600d5-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="600d5-205">a.</span><span class="sxs-lookup"><span data-stu-id="600d5-205">a.</span></span> <span data-ttu-id="600d5-206">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="600d5-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="600d5-207">b.</span><span class="sxs-lookup"><span data-stu-id="600d5-207">b.</span></span> <span data-ttu-id="600d5-208">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="600d5-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="600d5-209">c.</span><span class="sxs-lookup"><span data-stu-id="600d5-209">c.</span></span> <span data-ttu-id="600d5-210">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="600d5-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="600d5-211">d.</span><span class="sxs-lookup"><span data-stu-id="600d5-211">d.</span></span> <span data-ttu-id="600d5-212">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="600d5-212">Click **Create**.</span></span>
 
### <a name="creating-a-pluralsight-test-user"></a><span data-ttu-id="600d5-213">Een testgebruiker Pluralsight maken</span><span class="sxs-lookup"><span data-stu-id="600d5-213">Creating a Pluralsight test user</span></span>

<span data-ttu-id="600d5-214">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Pluralsight genoemd.</span><span class="sxs-lookup"><span data-stu-id="600d5-214">The objective of this section is to create a user called Britta Simon in Pluralsight.</span></span> <span data-ttu-id="600d5-215">Neem contact op met [Pluralsight Client ondersteuningsteam](mailto:support@pluralsight.com) de gebruikers in het account Pluralsight toevoegen.</span><span class="sxs-lookup"><span data-stu-id="600d5-215">Please work with [Pluralsight Client support team](mailto:support@pluralsight.com) to add the users in the Pluralsight account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="600d5-216">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="600d5-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="600d5-217">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="600d5-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pluralsight.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="600d5-219">**Britta Simon om aan te wijzen Pluralsight, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="600d5-219">**To assign Britta Simon to Pluralsight, perform the following steps:**</span></span>

1. <span data-ttu-id="600d5-220">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="600d5-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="600d5-222">Selecteer in de lijst met toepassingen **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="600d5-222">In the applications list, select **Pluralsight**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png) 

3. <span data-ttu-id="600d5-224">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="600d5-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="600d5-226">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="600d5-226">Click **Add** button.</span></span> <span data-ttu-id="600d5-227">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="600d5-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="600d5-229">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="600d5-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="600d5-230">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="600d5-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="600d5-231">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="600d5-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="600d5-232">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="600d5-232">Testing single sign-on</span></span>

<span data-ttu-id="600d5-233">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="600d5-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="600d5-234">Als u op de tegel Pluralsight in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="600d5-234">When you click the Pluralsight tile in the Access Panel, you should get automatically signed-on to your Pluralsight application.</span></span> <span data-ttu-id="600d5-235">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="600d5-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="600d5-236">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="600d5-236">Additional resources</span></span>

* [<span data-ttu-id="600d5-237">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="600d5-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="600d5-238">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="600d5-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png

