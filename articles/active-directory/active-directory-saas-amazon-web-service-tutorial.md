---
title: 'Zelfstudie: Azure Active Directory-integratie met Amazon Web Services (AWS) | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Amazon Web Services (AWS).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 0fb9c8f428368271b548e3f174726fa01ea910c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="9d621-103">Zelfstudie: Azure Active Directory-integratie met Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="9d621-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="9d621-104">In deze zelfstudie leert u hoe Amazon Web Services (AWS) integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9d621-104">In this tutorial, you learn how to integrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d621-105">Amazon Web Services (AWS) integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="9d621-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9d621-106">U kunt beheren in Azure AD met toegang op de Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="9d621-106">You can control in Azure AD who has access to Amazon Web Services (AWS)</span></span>
- <span data-ttu-id="9d621-107">U kunt uw gebruikers automatisch ophalen aangemelde naar Amazon Web Services (AWS) (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="9d621-107">You can enable your users to automatically get signed-on to Amazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9d621-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="9d621-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9d621-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9d621-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Amazon Web Services (AWS), it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="9d621-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9d621-110">Prerequisites</span></span>

<span data-ttu-id="9d621-111">Voor het configureren van Azure AD-integratie met Amazon Web Services (AWS), moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="9d621-111">To configure Azure AD integration with Amazon Web Services (AWS), you need the following items:</span></span>

- <span data-ttu-id="9d621-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="9d621-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9d621-113">Amazon Web Services (AWS) eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="9d621-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d621-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="9d621-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9d621-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="9d621-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9d621-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="9d621-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9d621-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d621-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d621-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="9d621-118">Scenario description</span></span>
<span data-ttu-id="9d621-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="9d621-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9d621-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="9d621-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9d621-121">Amazon Web Services (AWS) uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9d621-121">Adding Amazon Web Services (AWS) from the gallery</span></span>
2. <span data-ttu-id="9d621-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9d621-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-the-gallery"></a><span data-ttu-id="9d621-123">Amazon Web Services (AWS) uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9d621-123">Adding Amazon Web Services (AWS) from the gallery</span></span>
<span data-ttu-id="9d621-124">Voor het configureren van de integratie van Amazon Web Services (AWS) in Azure AD, moet u Amazon Web Services (AWS) uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="9d621-124">To configure the integration of Amazon Web Services (AWS) into Azure AD, you need to add Amazon Web Services (AWS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9d621-125">**Als u wilt toevoegen Amazon Web Services (AWS) uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9d621-125">**To add Amazon Web Services (AWS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9d621-126">In de  **[Azure Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9d621-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9d621-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9d621-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9d621-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9d621-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="9d621-131">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d621-131">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="9d621-133">Typ in het zoekvak **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="9d621-133">In the search box, type **Amazon Web Services (AWS)**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="9d621-135">Selecteer in het deelvenster resultaten **Amazon Web Services (AWS)**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9d621-135">In the results panel, select **Amazon Web Services (AWS)**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9d621-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9d621-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9d621-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Amazon Web Services (AWS) op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="9d621-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9d621-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Amazon Web Services (AWS) is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d621-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Amazon Web Services (AWS) is to a user in Azure AD.</span></span> <span data-ttu-id="9d621-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Amazon Web Services (AWS) tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="9d621-140">In other words, a link relationship between an Azure AD user and the related user in Amazon Web Services (AWS) needs to be established.</span></span>

<span data-ttu-id="9d621-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="9d621-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="9d621-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Amazon Web Services (AWS), moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="9d621-142">To configure and test Azure AD single sign-on with Amazon Web Services (AWS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9d621-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9d621-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9d621-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d621-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9d621-145">**[Maken van een gebruiker met Amazon Web Services test](#creating-an-amazon-web-services-test-user)**  - hebben een equivalent van Britta Simon in Amazon Web Services (AWS) die is gekoppeld aan de Azure AD-representatie van haar.</span><span class="sxs-lookup"><span data-stu-id="9d621-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - to have a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="9d621-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9d621-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9d621-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="9d621-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9d621-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="9d621-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9d621-149">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="9d621-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="9d621-150">**Voor het configureren van Azure AD eenmalige aanmelding met Amazon Web Services (AWS), moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9d621-150">**To configure Azure AD single sign-on with Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="9d621-151">In de Azure-Portal op de **Amazon Web Services (AWS)** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="9d621-151">In the Azure Portal, on the **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="9d621-153">Op de **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9d621-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="9d621-155">Op de **Amazon Web Services (AWS) domein en de URL's** sectie, de gebruiker heeft geen alle stappen uitvoeren als de app al vooraf is geïntegreerd met Azure.</span><span class="sxs-lookup"><span data-stu-id="9d621-155">On the **Amazon Web Services (AWS) Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="9d621-157">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9d621-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="9d621-159">De SAML-asserties verwacht de Amazon Web Services (AWS) softwaretoepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="9d621-159">The Amazon Web Services (AWS) Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="9d621-160">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="9d621-160">Please configure the following claims for this application.</span></span> <span data-ttu-id="9d621-161">U kunt beheren de waarden van deze kenmerken van de '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="9d621-161">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="9d621-162">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="9d621-162">The following screenshot shows an example for this.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="9d621-164">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding hierboven en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9d621-164">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="9d621-165">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="9d621-165">Attribute Name</span></span>  | <span data-ttu-id="9d621-166">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="9d621-166">Attribute Value</span></span> | <span data-ttu-id="9d621-167">naamruimte</span><span class="sxs-lookup"><span data-stu-id="9d621-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="9d621-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="9d621-168">RoleSessionName</span></span> | <span data-ttu-id="9d621-169">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="9d621-169">user.userprincipalname</span></span> | <span data-ttu-id="9d621-170">https://AWS.Amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="9d621-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="9d621-171">Rol</span><span class="sxs-lookup"><span data-stu-id="9d621-171">Role</span></span>            | <span data-ttu-id="9d621-172">User.assignedroles</span><span class="sxs-lookup"><span data-stu-id="9d621-172">user.assignedroles</span></span> |  <span data-ttu-id="9d621-173">https://AWS.Amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="9d621-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="9d621-174">U moet de gebruiker wordt ingericht in Azure AD ophalen van alle functies van de AWS-Console configureren.</span><span class="sxs-lookup"><span data-stu-id="9d621-174">You need to configure the user provisioning in Azure AD to fetch all the roles from AWS Console.</span></span> <span data-ttu-id="9d621-175">Raadpleeg de onderstaande stappen inrichting.</span><span class="sxs-lookup"><span data-stu-id="9d621-175">Please refer the provisioning steps below.</span></span>

    <span data-ttu-id="9d621-176">a.</span><span class="sxs-lookup"><span data-stu-id="9d621-176">a.</span></span> <span data-ttu-id="9d621-177">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d621-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="9d621-179">b.</span><span class="sxs-lookup"><span data-stu-id="9d621-179">b.</span></span> <span data-ttu-id="9d621-180">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="9d621-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="9d621-182">c.</span><span class="sxs-lookup"><span data-stu-id="9d621-182">c.</span></span> <span data-ttu-id="9d621-183">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="9d621-183">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="9d621-184">De waarde Namespace toevoegen zoals hierboven vermeld.</span><span class="sxs-lookup"><span data-stu-id="9d621-184">Add the Namespace value as given above.</span></span>
    
    <span data-ttu-id="9d621-185">d.</span><span class="sxs-lookup"><span data-stu-id="9d621-185">d.</span></span> <span data-ttu-id="9d621-186">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d621-186">Click **Ok**.</span></span>

7. <span data-ttu-id="9d621-187">Klik op **opslaan** knop om de instellingen in Azure.</span><span class="sxs-lookup"><span data-stu-id="9d621-187">Click **Save** button to save the settings on Azure.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9d621-189">In een ander browservenster aanmelding bij uw bedrijf Amazon Web Services (AWS) site als administrator.</span><span class="sxs-lookup"><span data-stu-id="9d621-189">In a different browser window, sign-on to your Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="9d621-190">Klik op **Console-startpagina**.</span><span class="sxs-lookup"><span data-stu-id="9d621-190">Click **Console Home**.</span></span>
   
    ![Eenmalige aanmelding configureren][11]

10. <span data-ttu-id="9d621-192">Klik op **IAM** van **beveiliging, identiteit en compatibiliteit** service.</span><span class="sxs-lookup"><span data-stu-id="9d621-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![Eenmalige aanmelding configureren][12]

11. <span data-ttu-id="9d621-194">Klik op **identiteitsproviders**, en klik vervolgens op **Provider maken**.</span><span class="sxs-lookup"><span data-stu-id="9d621-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![Eenmalige aanmelding configureren][13]

12. <span data-ttu-id="9d621-196">Op de **Provider configureren** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9d621-196">On the **Configure Provider** dialog page, perform the following steps:</span></span>
   
    ![Eenmalige aanmelding configureren][14]
 
    <span data-ttu-id="9d621-198">a.</span><span class="sxs-lookup"><span data-stu-id="9d621-198">a.</span></span> <span data-ttu-id="9d621-199">Als **providertype**, selecteer **SAML**.</span><span class="sxs-lookup"><span data-stu-id="9d621-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="9d621-200">b.</span><span class="sxs-lookup"><span data-stu-id="9d621-200">b.</span></span> <span data-ttu-id="9d621-201">In de **providernaam** textbox, typ een providernaam (bijvoorbeeld: *WAAD*).</span><span class="sxs-lookup"><span data-stu-id="9d621-201">In the **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="9d621-202">c.</span><span class="sxs-lookup"><span data-stu-id="9d621-202">c.</span></span> <span data-ttu-id="9d621-203">Als u wilt uw van het gedownloade metagegevensbestand uploadt, klikt u op **bestand kiezen**.</span><span class="sxs-lookup"><span data-stu-id="9d621-203">To upload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="9d621-204">d.</span><span class="sxs-lookup"><span data-stu-id="9d621-204">d.</span></span> <span data-ttu-id="9d621-205">Klik op **volgende stap**.</span><span class="sxs-lookup"><span data-stu-id="9d621-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="9d621-206">Op de **providerinformatie controleren** dialoogvenster pagina, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="9d621-206">On the **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![Eenmalige aanmelding configureren][15]

14. <span data-ttu-id="9d621-208">Klik op **rollen**, en klik vervolgens op **nieuwe rol maken**.</span><span class="sxs-lookup"><span data-stu-id="9d621-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![Eenmalige aanmelding configureren][16]

15. <span data-ttu-id="9d621-210">Op de **rolnaam ingesteld** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9d621-210">On the **Set Role Name** dialog, perform the following steps:</span></span> 
    
    ![Eenmalige aanmelding configureren][17] 

    <span data-ttu-id="9d621-212">a.</span><span class="sxs-lookup"><span data-stu-id="9d621-212">a.</span></span> <span data-ttu-id="9d621-213">In de **rolnaam** textbox, typ een rolnaam (bijvoorbeeld: *testgebruiker*).</span><span class="sxs-lookup"><span data-stu-id="9d621-213">In the **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="9d621-214">b.</span><span class="sxs-lookup"><span data-stu-id="9d621-214">b.</span></span> <span data-ttu-id="9d621-215">Klik op **volgende stap**.</span><span class="sxs-lookup"><span data-stu-id="9d621-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="9d621-216">Op de **Roltype Selecteer** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9d621-216">On the **Select Role Type** dialog, perform the following steps:</span></span> 
    
    ![Eenmalige aanmelding configureren][18] 

    <span data-ttu-id="9d621-218">a.</span><span class="sxs-lookup"><span data-stu-id="9d621-218">a.</span></span> <span data-ttu-id="9d621-219">Selecteer **rol voor toegang van de Provider identiteit**.</span><span class="sxs-lookup"><span data-stu-id="9d621-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="9d621-220">b.</span><span class="sxs-lookup"><span data-stu-id="9d621-220">b.</span></span> <span data-ttu-id="9d621-221">In de **Grant Web eenmalige aanmelding (WebSSO) toegang tot de SAML-providers** sectie, klikt u op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="9d621-221">In the **Grant Web Single Sign-On (WebSSO) access to SAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="9d621-222">Op de **vertrouwensrelatie tot stand brengen** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9d621-222">On the **Establish Trust** dialog, perform the following steps:</span></span>  
    
    ![Eenmalige aanmelding configureren][19] 

    <span data-ttu-id="9d621-224">a.</span><span class="sxs-lookup"><span data-stu-id="9d621-224">a.</span></span> <span data-ttu-id="9d621-225">Selecteer de SAML-provider die u eerder hebt gemaakt als SAML-provider (bijvoorbeeld: *WAAD*)</span><span class="sxs-lookup"><span data-stu-id="9d621-225">As SAML provider, select the SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="9d621-226">b.</span><span class="sxs-lookup"><span data-stu-id="9d621-226">b.</span></span> <span data-ttu-id="9d621-227">Klik op **volgende stap**.</span><span class="sxs-lookup"><span data-stu-id="9d621-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="9d621-228">Op de **controleren rol vertrouwen** dialoogvenster, klikt u op **volgende stap**.</span><span class="sxs-lookup"><span data-stu-id="9d621-228">On the **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![Eenmalige aanmelding configureren][32]

19. <span data-ttu-id="9d621-230">Op de **beleid koppelen** dialoogvenster, klikt u op **volgende stap**.</span><span class="sxs-lookup"><span data-stu-id="9d621-230">On the **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![Eenmalige aanmelding configureren][33]

20. <span data-ttu-id="9d621-232">Op de **revisie** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9d621-232">On the **Review** dialog, perform the following steps:</span></span>
    
    ![Eenmalige aanmelding configureren][34]
 
    <span data-ttu-id="9d621-234">a.</span><span class="sxs-lookup"><span data-stu-id="9d621-234">a.</span></span> <span data-ttu-id="9d621-235">Klik op **rol maken**.</span><span class="sxs-lookup"><span data-stu-id="9d621-235">Click **Create Role**.</span></span>

    <span data-ttu-id="9d621-236">b.</span><span class="sxs-lookup"><span data-stu-id="9d621-236">b.</span></span> <span data-ttu-id="9d621-237">Zo veel functies naar behoefte maken en toe te wijzen aan de id-Provider.</span><span class="sxs-lookup"><span data-stu-id="9d621-237">Create as many roles as needed and map them to the Identity Provider.</span></span>

21. <span data-ttu-id="9d621-238">De gebruiker om het ophalen van alle functies van de AWS nu configureren</span><span class="sxs-lookup"><span data-stu-id="9d621-238">Now configure the user provisioning to fetch all the roles from AWS</span></span>

    <span data-ttu-id="9d621-239">a.</span><span class="sxs-lookup"><span data-stu-id="9d621-239">a.</span></span> <span data-ttu-id="9d621-240">In het AWS-Console-aanmelding met het root-account</span><span class="sxs-lookup"><span data-stu-id="9d621-240">In the AWS Console login with your root account</span></span>

    <span data-ttu-id="9d621-241">b.</span><span class="sxs-lookup"><span data-stu-id="9d621-241">b.</span></span> <span data-ttu-id="9d621-242">Klik op uw naam in de rechterbovenhoek en klik vervolgens op de **mijn beveiligingsreferenties** optie.</span><span class="sxs-lookup"><span data-stu-id="9d621-242">In the top right corner click your name and then click the **My Security Credentials** option.</span></span> <span data-ttu-id="9d621-243">Hiermee opent u een scherm als een waarschuwing weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9d621-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="9d621-244">Klik op de knop **beveiligingsreferenties** knop om door te geven van het scherm.</span><span class="sxs-lookup"><span data-stu-id="9d621-244">Click the button **Security Credentials** button to pass the screen.</span></span>
        
       ![Eenmalige aanmelding configureren][36]

       ![Eenmalige aanmelding configureren][37]

    <span data-ttu-id="9d621-247">c.</span><span class="sxs-lookup"><span data-stu-id="9d621-247">c.</span></span> <span data-ttu-id="9d621-248">Klik in de sectie toegangstoetsen op de **toegangssleutel maken** knop.</span><span class="sxs-lookup"><span data-stu-id="9d621-248">In the Access Keys section click the **Create New Access Key** button.</span></span> <span data-ttu-id="9d621-249">Hiermee wordt de toegangssleutel-ID en een token waarde gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="9d621-249">This generates the Access Key ID and a token value.</span></span>
    
       ![Eenmalige aanmelding configureren][38]

    <span data-ttu-id="9d621-251">d.</span><span class="sxs-lookup"><span data-stu-id="9d621-251">d.</span></span> <span data-ttu-id="9d621-252">Kopieer deze beide waarden en ook downloaden, zodat u deze niet kwijtraakt.</span><span class="sxs-lookup"><span data-stu-id="9d621-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="9d621-253">e.</span><span class="sxs-lookup"><span data-stu-id="9d621-253">e.</span></span> <span data-ttu-id="9d621-254">Klik in de Azure-Portal op de pagina Amazon Web Services (AWS) toepassingen integratie **inrichten**.</span><span class="sxs-lookup"><span data-stu-id="9d621-254">In the Azure Portal, on the Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![Eenmalige aanmelding configureren][35]

    <span data-ttu-id="9d621-256">f.</span><span class="sxs-lookup"><span data-stu-id="9d621-256">f.</span></span> <span data-ttu-id="9d621-257">De modus inrichten instellen op **automatische**</span><span class="sxs-lookup"><span data-stu-id="9d621-257">Set the Provisioning mode to **Automatic**</span></span>
        
       ![Eenmalige aanmelding configureren][39]

    <span data-ttu-id="9d621-259">g.</span><span class="sxs-lookup"><span data-stu-id="9d621-259">g.</span></span> <span data-ttu-id="9d621-260">Nu in de **clientsecret** en **geheim Token** plakt u de bijbehorende waarden die u hebt gekopieerd vanaf AWS-Console.</span><span class="sxs-lookup"><span data-stu-id="9d621-260">Now in the **clientsecret** and **Secret Token** paste the corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="9d621-261">h.</span><span class="sxs-lookup"><span data-stu-id="9d621-261">h.</span></span> <span data-ttu-id="9d621-262">U kunt klikken op de **verbinding testen** knop voor het testen van de connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="9d621-262">You can click the **Test Connection** button to test the connectivity.</span></span> <span data-ttu-id="9d621-263">Als dat is geslaagd kunt u de inrichting connector starten.</span><span class="sxs-lookup"><span data-stu-id="9d621-263">Once that is successful then you can start the provisioning connector.</span></span>
       
       ![Eenmalige aanmelding configureren][40]

    <span data-ttu-id="9d621-265">ik.</span><span class="sxs-lookup"><span data-stu-id="9d621-265">i.</span></span> <span data-ttu-id="9d621-266">Nu de Status van inrichting in inschakelen **op**.</span><span class="sxs-lookup"><span data-stu-id="9d621-266">Now enable the Provisioning Status to **On**.</span></span> <span data-ttu-id="9d621-267">Hiermee start u de rollen ophalen uit de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9d621-267">This starts fetching the roles from the application.</span></span>

       ![Eenmalige aanmelding configureren][41]

    > [!NOTE]
    > <span data-ttu-id="9d621-269">Azure AD inrichten de service wordt uitgevoerd elke na enige tijd om te synchroniseren van de rollen van AWS.</span><span class="sxs-lookup"><span data-stu-id="9d621-269">Azure AD Provisioning service runs every after some time to sync the roles from AWS.</span></span> <span data-ttu-id="9d621-270">U ziet de identiteitsprovider gekoppeld AWS rollen in Azure AD en u ze kunt gebruiken bij het toewijzen van de toepassing aan gebruikers of groepen.</span><span class="sxs-lookup"><span data-stu-id="9d621-270">You should see all the Identity Provider attached AWS roles into Azure AD and you can use them while assigning the application to users or groups.</span></span>

<!--### Next steps

To ensure users can sign-in to Amazon Web Services (AWS) after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Amazon Web Services (AWS) in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9d621-271">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="9d621-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="9d621-272">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9d621-272">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="9d621-274">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9d621-274">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9d621-275">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9d621-275">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9d621-277">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="9d621-277">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9d621-279">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d621-279">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9d621-281">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9d621-281">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9d621-283">a.</span><span class="sxs-lookup"><span data-stu-id="9d621-283">a.</span></span> <span data-ttu-id="9d621-284">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9d621-284">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d621-285">b.</span><span class="sxs-lookup"><span data-stu-id="9d621-285">b.</span></span> <span data-ttu-id="9d621-286">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9d621-286">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9d621-287">c.</span><span class="sxs-lookup"><span data-stu-id="9d621-287">c.</span></span> <span data-ttu-id="9d621-288">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="9d621-288">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9d621-289">d.</span><span class="sxs-lookup"><span data-stu-id="9d621-289">d.</span></span> <span data-ttu-id="9d621-290">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="9d621-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="9d621-291">Maken van een testgebruiker Amazon Web Services</span><span class="sxs-lookup"><span data-stu-id="9d621-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="9d621-292">Om in te schakelen Azure AD-gebruikers zich aanmelden op de Amazon Web Services (AWS), als ze in Amazon Web Services (AWS) worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="9d621-292">In order to enable Azure AD users to log in to Amazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="9d621-293">In het geval van Amazon Web Services (AWS) is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="9d621-293">In the case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="9d621-294">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9d621-294">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="9d621-295">Meld u aan bij uw **Amazon Web Services (AWS)** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="9d621-295">Log in to your **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="9d621-296">Klik op de **Console-startpagina** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9d621-296">Click the **Console Home** icon.</span></span> 
   
    ![Eenmalige aanmelding configureren][11]

3. <span data-ttu-id="9d621-298">Klik op Identity and Access Management.</span><span class="sxs-lookup"><span data-stu-id="9d621-298">Click Identity and Access Management.</span></span> 
   
    ![Eenmalige aanmelding configureren][28]

4. <span data-ttu-id="9d621-300">Klik in het Dashboard op **gebruikers**, en klik vervolgens op **Create New Users**.</span><span class="sxs-lookup"><span data-stu-id="9d621-300">In the Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![Eenmalige aanmelding configureren][29]

5. <span data-ttu-id="9d621-302">Voer de volgende stappen uit in het dialoogvenster gebruiker maken:</span><span class="sxs-lookup"><span data-stu-id="9d621-302">On the Create User dialog, perform the following steps:</span></span> 
   
    ![Eenmalige aanmelding configureren][30]   
    
    <span data-ttu-id="9d621-304">a.</span><span class="sxs-lookup"><span data-stu-id="9d621-304">a.</span></span> <span data-ttu-id="9d621-305">In de **Voer gebruikersnamen** tekstvakken, typ de naam van Brita Simon gebruiker (userprincipalname) in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d621-305">In the **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="9d621-306">b.</span><span class="sxs-lookup"><span data-stu-id="9d621-306">b.</span></span> <span data-ttu-id="9d621-307">Klik op **maken.**</span><span class="sxs-lookup"><span data-stu-id="9d621-307">Click **Create.**</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9d621-308">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d621-308">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9d621-309">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="9d621-309">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Amazon Web Services (AWS).</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="9d621-311">**Als u wilt toewijzen Britta Simon naar Amazon Web Services (AWS), moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9d621-311">**To assign Britta Simon to Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="9d621-312">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9d621-312">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="9d621-314">Selecteer in de lijst met toepassingen **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="9d621-314">In the applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="9d621-316">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="9d621-316">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="9d621-318">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="9d621-318">Click **Add** button.</span></span> <span data-ttu-id="9d621-319">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d621-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="9d621-321">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="9d621-321">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9d621-322">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d621-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9d621-323">Op **rol selecteren** tabblad, selecteer de juiste rol voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="9d621-323">On **Select Role** tab, select the appropriate role for the user.</span></span> <span data-ttu-id="9d621-324">Alle deze rollen worden weergegeven met de rolnaam en de naam van de id-provider.</span><span class="sxs-lookup"><span data-stu-id="9d621-324">All these roles are shown with the role name and identity provider name.</span></span> <span data-ttu-id="9d621-325">Op deze manier kunt u eenvoudig de rollen van AWS identificeren.</span><span class="sxs-lookup"><span data-stu-id="9d621-325">This way you can easily identify the roles from AWS.</span></span>

8. <span data-ttu-id="9d621-326">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d621-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9d621-327">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9d621-327">Testing single sign-on</span></span>

<span data-ttu-id="9d621-328">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="9d621-328">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9d621-329">Als u op de tegel Amazon Web Services (AWS) in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="9d621-329">When you click the Amazon Web Services (AWS) tile in the Access Panel, you should get automatically signed-on to your Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9d621-330">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="9d621-330">Additional resources</span></span>

* [<span data-ttu-id="9d621-331">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d621-331">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d621-332">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9d621-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
