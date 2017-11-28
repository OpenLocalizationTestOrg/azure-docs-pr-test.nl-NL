---
title: 'Zelfstudie: Azure Active Directory-integratie met FilesAnywhere | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en FilesAnywhere.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 4153056bd21006061c6ad8ff9cf3c17de9248628
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="f0018-103">Zelfstudie: Azure Active Directory-integratie met FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="f0018-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="f0018-104">In deze zelfstudie leert u hoe FilesAnywhere integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f0018-104">In this tutorial, you learn how to integrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f0018-105">FilesAnywhere integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f0018-105">Integrating FilesAnywhere with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f0018-106">U kunt beheren in Azure AD die toegang tot FilesAnywhere heeft</span><span class="sxs-lookup"><span data-stu-id="f0018-106">You can control in Azure AD who has access to FilesAnywhere</span></span>
- <span data-ttu-id="f0018-107">U kunt uw gebruikers automatisch ophalen aangemeld bij FilesAnywhere (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="f0018-107">You can enable your users to automatically get signed-on to FilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f0018-108">U kunt uw accounts op één centrale locatie - en de Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="f0018-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="f0018-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f0018-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0018-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f0018-110">Prerequisites</span></span>

<span data-ttu-id="f0018-111">Voor het configureren van Azure AD-integratie met FilesAnywhere, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="f0018-111">To configure Azure AD integration with FilesAnywhere, you need the following items:</span></span>

- <span data-ttu-id="f0018-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f0018-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f0018-113">Een FilesAnywhere eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f0018-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="f0018-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f0018-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="f0018-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f0018-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f0018-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f0018-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f0018-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f0018-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="f0018-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f0018-118">Scenario description</span></span>
<span data-ttu-id="f0018-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f0018-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f0018-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f0018-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f0018-121">FilesAnywhere uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f0018-121">Adding FilesAnywhere from the gallery</span></span>
2. <span data-ttu-id="f0018-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f0018-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-the-gallery"></a><span data-ttu-id="f0018-123">FilesAnywhere uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f0018-123">Adding FilesAnywhere from the gallery</span></span>
<span data-ttu-id="f0018-124">Voor het configureren van de integratie van FilesAnywhere in Azure AD, moet u FilesAnywhere uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f0018-124">To configure the integration of FilesAnywhere into Azure AD, you need to add FilesAnywhere from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f0018-125">**Als u wilt toevoegen FilesAnywhere uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f0018-125">**To add FilesAnywhere from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f0018-126">In de  **[Azure Management Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f0018-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f0018-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f0018-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f0018-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f0018-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f0018-131">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f0018-131">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f0018-133">Typ in het zoekvak **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="f0018-133">In the search box, type **FilesAnywhere**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. <span data-ttu-id="f0018-135">Selecteer in het deelvenster resultaten **FilesAnywhere**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f0018-135">In the results panel, select **FilesAnywhere**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f0018-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f0018-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f0018-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met FilesAnywhere op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f0018-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f0018-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in FilesAnywhere is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0018-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FilesAnywhere is to a user in Azure AD.</span></span> <span data-ttu-id="f0018-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in FilesAnywhere tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="f0018-140">In other words, a link relationship between an Azure AD user and the related user in FilesAnywhere needs to be established.</span></span>

<span data-ttu-id="f0018-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="f0018-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="f0018-142">Om te configureren en testen van Azure AD eenmalige aanmelding met FilesAnywhere, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="f0018-142">To configure and test Azure AD single sign-on with FilesAnywhere, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f0018-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f0018-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f0018-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0018-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f0018-145">**[Maken van een testgebruiker FilesAnywhere](#creating-a-filesanywhere-test-user)**  - FilesAnywhere die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="f0018-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - to have a counterpart of Britta Simon in FilesAnywhere that is linked to the Azure AD representation of her.</span></span>
3. <span data-ttu-id="f0018-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f0018-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
4. <span data-ttu-id="f0018-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f0018-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f0018-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f0018-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f0018-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure-beheerportal en eenmalige aanmelding in uw toepassing FilesAnywhere configureren.</span><span class="sxs-lookup"><span data-stu-id="f0018-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="f0018-150">**Voor het configureren van Azure AD eenmalige aanmelding met FilesAnywhere, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f0018-150">**To configure Azure AD single sign-on with FilesAnywhere, perform the following steps:**</span></span>

1. <span data-ttu-id="f0018-151">In de Azure-beheerportal op de **FilesAnywhere** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f0018-151">In the Azure Management portal, on the **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f0018-153">Op de **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** eenmalige aanmelding inschakelen op.</span><span class="sxs-lookup"><span data-stu-id="f0018-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. <span data-ttu-id="f0018-155">Op de **FilesAnywhere domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP geïnitieerd modus**:</span><span class="sxs-lookup"><span data-stu-id="f0018-155">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="f0018-157">a.</span><span class="sxs-lookup"><span data-stu-id="f0018-157">a.</span></span> <span data-ttu-id="f0018-158">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span><span class="sxs-lookup"><span data-stu-id="f0018-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>
> [!NOTE]
> <span data-ttu-id="f0018-159">Houd er rekening mee dat de waarde **215** is een **clientid** en is slechts een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f0018-159">Please note that the value **215** is a **clientid** and is just an example.</span></span> <span data-ttu-id="f0018-160">U wilt vervangen door de werkelijke clientid-waarde.</span><span class="sxs-lookup"><span data-stu-id="f0018-160">You need to replace it with the actual clientid value.</span></span>

4. <span data-ttu-id="f0018-161">Op de **FilesAnywhere domein en de URL's** sectie als u wilt configureren van de toepassing in **SP geïnitieerd modus**, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f0018-161">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="f0018-163">a.</span><span class="sxs-lookup"><span data-stu-id="f0018-163">a.</span></span> <span data-ttu-id="f0018-164">Klik op de **weergeven geavanceerde instellingen voor URL** optie</span><span class="sxs-lookup"><span data-stu-id="f0018-164">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="f0018-165">b.</span><span class="sxs-lookup"><span data-stu-id="f0018-165">b.</span></span> <span data-ttu-id="f0018-166">In de **aanmelding op URL** textbox, typ een URL met het volgende patroon volgen:`https://<sub domain>.filesanywhere.com/`</span><span class="sxs-lookup"><span data-stu-id="f0018-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f0018-167">Houd er rekening mee dat deze niet de werkelijke waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="f0018-167">Please note that these are not the real values.</span></span> <span data-ttu-id="f0018-168">U hebt deze waarden bijwerken met de werkelijke aanmelding op de URL en antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="f0018-168">You have to update these values with the actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="f0018-169">Neem contact op met [FilesAnywhere ondersteuningsteam](mailto:support@FilesAnywhere.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="f0018-169">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) to get these values.</span></span> 

5. <span data-ttu-id="f0018-170">De SAML-asserties verwacht FilesAnywhere softwaretoepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="f0018-170">FilesAnywhere Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="f0018-171">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="f0018-171">Please configure the following claims for this application.</span></span> <span data-ttu-id="f0018-172">U kunt beheren de waarden van deze kenmerken van de '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="f0018-172">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="f0018-173">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="f0018-173">The following screenshot shows an example for this.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="f0018-175">Als de gebruikers zich aanmeldt met FilesAnywhere krijgen ze de waarde van **clientid** kenmerk uit [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span><span class="sxs-lookup"><span data-stu-id="f0018-175">When the users signs up with FilesAnywhere they get the value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="f0018-176">U moet het kenmerk 'Client-Id' met de unieke waarde die is geleverd door FilesAnywhere toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f0018-176">You have to add the "Client Id" attribute with the unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="f0018-177">Alle deze kenmerken die hierboven zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="f0018-177">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="f0018-178">Houd er rekening mee dat de waarde **. 2331** van **clientid** is slechts een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f0018-178">Please note that the value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="f0018-179">U moet de werkelijke waarde opgeven.</span><span class="sxs-lookup"><span data-stu-id="f0018-179">You need to provide the actual value.</span></span>


6. <span data-ttu-id="f0018-180">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding hierboven en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f0018-180">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="f0018-181">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="f0018-181">Attribute Name</span></span> | <span data-ttu-id="f0018-182">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="f0018-182">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="f0018-183">clientid</span><span class="sxs-lookup"><span data-stu-id="f0018-183">clientid</span></span> | <span data-ttu-id="f0018-184">*'uniquevalue'*</span><span class="sxs-lookup"><span data-stu-id="f0018-184">*"uniquevalue"*</span></span> |

    <span data-ttu-id="f0018-185">a.</span><span class="sxs-lookup"><span data-stu-id="f0018-185">a.</span></span> <span data-ttu-id="f0018-186">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f0018-186">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="f0018-189">b.</span><span class="sxs-lookup"><span data-stu-id="f0018-189">b.</span></span> <span data-ttu-id="f0018-190">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="f0018-190">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="f0018-191">c.</span><span class="sxs-lookup"><span data-stu-id="f0018-191">c.</span></span> <span data-ttu-id="f0018-192">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="f0018-192">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="f0018-193">d.</span><span class="sxs-lookup"><span data-stu-id="f0018-193">d.</span></span> <span data-ttu-id="f0018-194">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="f0018-194">Click **Ok**</span></span>

7. <span data-ttu-id="f0018-195">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f0018-195">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f0018-197">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f0018-197">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. <span data-ttu-id="f0018-199">Op de **FilesAnywhere configuratie** sectie, klikt u op **configureren FilesAnywhere** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="f0018-199">On the **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** to open **Configure sign-on** window.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. <span data-ttu-id="f0018-202">Als u eenmalige aanmelding configuratie voltooid voor uw toepassing aan FilesAnywhere einde, neem contact op met [FilesAnywhere ondersteuningsteam](mailto:support@FilesAnywhere.com) en geeft u het gedownloade SAML token-ondertekening van certificaten en eenmalige aanmelding op (SSO)-URL.</span><span class="sxs-lookup"><span data-stu-id="f0018-202">To get SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them the downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f0018-203">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f0018-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="f0018-204">Het doel van deze sectie is het een testgebruiker maken in Azure Management portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f0018-204">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f0018-206">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f0018-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f0018-207">In de **Azure Management portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f0018-207">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f0018-209">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="f0018-209">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f0018-211">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f0018-211">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f0018-213">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f0018-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f0018-215">a.</span><span class="sxs-lookup"><span data-stu-id="f0018-215">a.</span></span> <span data-ttu-id="f0018-216">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f0018-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f0018-217">b.</span><span class="sxs-lookup"><span data-stu-id="f0018-217">b.</span></span> <span data-ttu-id="f0018-218">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f0018-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f0018-219">c.</span><span class="sxs-lookup"><span data-stu-id="f0018-219">c.</span></span> <span data-ttu-id="f0018-220">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f0018-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f0018-221">d.</span><span class="sxs-lookup"><span data-stu-id="f0018-221">d.</span></span> <span data-ttu-id="f0018-222">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f0018-222">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="f0018-223">Een testgebruiker FilesAnywhere maken</span><span class="sxs-lookup"><span data-stu-id="f0018-223">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="f0018-224">Toepassing ondersteunt Just in tijd gebruikers inrichten en na verificatie gebruikers wordt in de toepassing automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f0018-224">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f0018-225">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0018-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f0018-226">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="f0018-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FilesAnywhere.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f0018-228">**Britta Simon om aan te wijzen FilesAnywhere, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f0018-228">**To assign Britta Simon to FilesAnywhere, perform the following steps:**</span></span>

1. <span data-ttu-id="f0018-229">In de Azure-beheerportal, opent u de weergave toepassingen en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f0018-229">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f0018-231">Selecteer in de lijst met toepassingen **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="f0018-231">In the applications list, select **FilesAnywhere**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. <span data-ttu-id="f0018-233">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f0018-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f0018-235">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f0018-235">Click **Add** button.</span></span> <span data-ttu-id="f0018-236">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f0018-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f0018-238">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="f0018-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f0018-239">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f0018-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f0018-240">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f0018-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="f0018-241">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f0018-241">Testing single sign-on</span></span>

<span data-ttu-id="f0018-242">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="f0018-242">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f0018-243">Als u op de tegel FilesAnywhere in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="f0018-243">When you click the FilesAnywhere tile in the Access Panel, you should get automatically signed-on to your FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f0018-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f0018-244">Additional resources</span></span>

* [<span data-ttu-id="f0018-245">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0018-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f0018-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f0018-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
