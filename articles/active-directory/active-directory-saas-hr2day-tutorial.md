---
title: 'Zelfstudie: Azure Active Directory-integratie met HR2day door Merces | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en HR2day door Merces.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 77e2fcf9c306259286b15767f3a992510d6d79d8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="afdd1-103">Zelfstudie: Azure Active Directory-integratie met HR2day door Merces</span><span class="sxs-lookup"><span data-stu-id="afdd1-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>

<span data-ttu-id="afdd1-104">In deze zelfstudie leert u hoe HR2day door Merces integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="afdd1-104">In this tutorial, you learn how to integrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="afdd1-105">HR2day door Merces integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="afdd1-105">Integrating HR2day by Merces with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="afdd1-106">U kunt beheren in Azure AD die toegang tot HR2day door Merces heeft.</span><span class="sxs-lookup"><span data-stu-id="afdd1-106">You can control in Azure AD who has access to HR2day by Merces.</span></span>
- <span data-ttu-id="afdd1-107">U kunt uw gebruikers automatisch ophalen aangemeld bij HR2day door Merces met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="afdd1-107">You can enable your users to automatically get signed in to HR2day by Merces with their Azure AD accounts.</span></span>
- <span data-ttu-id="afdd1-108">U kunt uw accounts op één centrale locatie--de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="afdd1-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="afdd1-109">Zie voor meer informatie over de integratie met Azure AD SaaS [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="afdd1-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afdd1-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="afdd1-110">Prerequisites</span></span>

<span data-ttu-id="afdd1-111">Voor het configureren van Azure AD-integratie met HR2day door Merces, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="afdd1-111">To configure Azure AD integration with HR2day by Merces, you need the following items:</span></span>

- <span data-ttu-id="afdd1-112">Een Azure AD-abonnement.</span><span class="sxs-lookup"><span data-stu-id="afdd1-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="afdd1-113">Een HR2day door eenmalige aanmelding Merces abonnement ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="afdd1-113">An HR2day by Merces single sign-on enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="afdd1-114">Gebruik een productie-omgeving voor het testen van de stappen in deze zelfstudie aanbevolen niet.</span><span class="sxs-lookup"><span data-stu-id="afdd1-114">We don't recommend using a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="afdd1-115">Test de stappen in deze zelfstudie, volgt u deze aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="afdd1-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="afdd1-116">Gebruik uw productieomgeving geen tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="afdd1-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="afdd1-117">Ophalen van een [één maand gratis proefversie van Azure AD](https://azure.microsoft.com/pricing/free-trial/) als u nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="afdd1-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span></span>  

## <a name="scenario-description"></a><span data-ttu-id="afdd1-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="afdd1-118">Scenario description</span></span>
<span data-ttu-id="afdd1-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="afdd1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="afdd1-120">Het scenario dat hier wordt beschreven, bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="afdd1-120">The scenario that's outlined here consists of two main building blocks:</span></span>

1. <span data-ttu-id="afdd1-121">HR2day door Merces uit de galerie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="afdd1-121">Adding HR2day by Merces from the gallery.</span></span>
2. <span data-ttu-id="afdd1-122">Configureren en testen van Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="afdd1-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-hr2day-by-merces-from-the-gallery"></a><span data-ttu-id="afdd1-123">HR2day door Merces uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="afdd1-123">Add HR2day by Merces from the gallery</span></span>
<span data-ttu-id="afdd1-124">Voor het configureren van de integratie van HR2day door Merces in Azure AD HR2day door Merces uit de galerie te toevoegt aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="afdd1-124">To configure the integration of HR2day by Merces into Azure AD, add HR2day by Merces from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="afdd1-125">**Als u wilt toevoegen HR2day door Merces uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="afdd1-125">**To add HR2day by Merces from the gallery, take the following steps:**</span></span>

1. <span data-ttu-id="afdd1-126">In de [Azure-portal](https://portal.azure.com), Selecteer op het navigatiedeelvenster links de **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="afdd1-126">In the [Azure portal](https://portal.azure.com), on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="afdd1-128">Ga naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-128">Go to **Enterprise applications**.</span></span> <span data-ttu-id="afdd1-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="afdd1-131">Als u wilt een nieuwe toepassing toevoegen, selecteert u de **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="afdd1-131">To add a new application, select the **New application** button on the top of the dialog box.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="afdd1-133">Typ in het zoekvak **HR2day door Merces**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-133">In the search box, type **HR2day by Merces**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. <span data-ttu-id="afdd1-135">Selecteer in het deelvenster resultaten **HR2day door Merces**, en selecteer vervolgens de **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="afdd1-135">In the results panel, select **HR2day by Merces**, and then select the **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="afdd1-137">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="afdd1-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="afdd1-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met HR2day door Merces op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="afdd1-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="afdd1-139">Voor eenmalige aanmelding werkt, moet Azure AD te weten wie de gebruiker equivalent in HR2day door Merces is een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afdd1-139">For single sign-on to work, Azure AD needs to know who the counterpart user in HR2day by Merces is to a user in Azure AD.</span></span> <span data-ttu-id="afdd1-140">Met andere woorden, moet u een koppeling tussen een Azure AD-gebruiker en de betreffende gebruiker in HR2day door Merces vast te stellen.</span><span class="sxs-lookup"><span data-stu-id="afdd1-140">In other words, you need to establish a link between an Azure AD user and the related user in HR2day by Merces.</span></span>

<span data-ttu-id="afdd1-141">Wijs in HR2day door Merces de **gebruikersnaam** in Azure AD **gebruikersnaam** de relatie tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="afdd1-141">In HR2day by Merces, assign the **user name** in Azure AD to  **Username** to establish the relationship.</span></span>

<span data-ttu-id="afdd1-142">Om te configureren en testen van Azure AD eenmalige aanmelding met HR2day door Merces, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="afdd1-142">To configure and test Azure AD single sign-on with HR2day by Merces, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="afdd1-143">[Eenmalige aanmelding Azure AD configureren](#configuring-azure-ad-single-sign-on): uw gebruikers om deze functie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="afdd1-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users to use this feature.</span></span>
2. <span data-ttu-id="afdd1-144">[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user): Azure AD Test eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="afdd1-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="afdd1-145">[Maken van een HR2day door Merces testgebruiker](#creating-an-hr2day-by-merces-test-user): maken van een exemplaar van Britta Simon in HR2day door Merces die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="afdd1-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="afdd1-146">[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user): inschakelen Britta Simon gebruik van eenmalige aanmelding Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afdd1-146">[Assign the Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="afdd1-147">[Test eenmalige aanmelding](#testing-single-sign-on): controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="afdd1-147">[Test single sign-on](#testing-single-sign-on): Verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="afdd1-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="afdd1-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="afdd1-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw HR2day door Merces toepassing.</span><span class="sxs-lookup"><span data-stu-id="afdd1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HR2day by Merces application.</span></span>

<span data-ttu-id="afdd1-150">**Voor het configureren van Azure AD eenmalige aanmelding met HR2day door Merces, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="afdd1-150">**To configure Azure AD single sign-on with HR2day by Merces, take the following steps:**</span></span>

1. <span data-ttu-id="afdd1-151">In de Azure-portal op de **HR2day door Merces** toepassing Integratiepagina **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-151">In the Azure portal, on the **HR2day by Merces** application integration page, select **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="afdd1-153">Eenmalige aanmelding inschakelen in de **eenmalige aanmelding** dialoogvenster, **modus** als **op basis van SAML aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-153">To enable single sign-on, in the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. <span data-ttu-id="afdd1-155">In de **HR2day Merces domein en URL's** sectie, voert de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="afdd1-155">In the **HR2day by Merces Domain and URLs** section, take the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    <span data-ttu-id="afdd1-157">a.</span><span class="sxs-lookup"><span data-stu-id="afdd1-157">a.</span></span> <span data-ttu-id="afdd1-158">In de **aanmeldings-URL** vak een URL met behulp van het volgende patroon volgen: `https://<tenantname>.force.com/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="afdd1-158">In the **Sign-on URL** box, type a URL by using the following pattern: `https://<tenantname>.force.com/<instancename>`.</span></span>

    <span data-ttu-id="afdd1-159">b.</span><span class="sxs-lookup"><span data-stu-id="afdd1-159">b.</span></span> <span data-ttu-id="afdd1-160">In de **id** vak een URL met behulp van het volgende patroon volgen: `https://hr2day.force.com/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="afdd1-160">In the **Identifier** box, type a URL by using the following pattern: `https://hr2day.force.com/<companyname>`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="afdd1-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="afdd1-161">These values are not real.</span></span> <span data-ttu-id="afdd1-162">Deze waarden bijwerken met de werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="afdd1-162">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="afdd1-163">Neem contact op met de [HR2day door Merces client ondersteuningsteam](mailto:servicedesk@merces.nl) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="afdd1-163">Contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl) to get these values.</span></span> 
 


4. <span data-ttu-id="afdd1-164">Op de **SAML-certificaat voor ondertekening van** sectie **Certificate(Base64)**, en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="afdd1-164">On the **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. <span data-ttu-id="afdd1-166">Deze sectie wordt beschreven hoe gebruikers worden geverifieerd bij HR2day door Merces aan hun account in Azure AD inschakelen.</span><span class="sxs-lookup"><span data-stu-id="afdd1-166">This section describes how to enable users to authenticate to HR2day by Merces with their account in Azure AD.</span></span> <span data-ttu-id="afdd1-167">Ze doen dit met behulp van de federatieserver die gebaseerd op het SAML-protocol.</span><span class="sxs-lookup"><span data-stu-id="afdd1-167">They do this by using federation that's based on the SAML protocol.</span></span>

    <span data-ttu-id="afdd1-168">De SAML-asserties verwacht uw HR2day door Merces toepassing in een specifieke indeling waarvoor u aangepaste kenmerktoewijzingen toevoegen aan uw SAML-token.</span><span class="sxs-lookup"><span data-stu-id="afdd1-168">Your HR2day by Merces application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token.</span></span> <span data-ttu-id="afdd1-169">De volgende Schermafbeelding toont een voorbeeld hiervan.</span><span class="sxs-lookup"><span data-stu-id="afdd1-169">The following screenshot shows an example of this.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    <span data-ttu-id="afdd1-171">Voordat u de SAML-bevestiging configureren kunt, moet u contact opneemt de [HR2day door Merces Client ondersteuningsteam](mailto:servicedesk@merces.nl) en vraagt u de waarde van het kenmerk unieke id voor uw tenant.</span><span class="sxs-lookup"><span data-stu-id="afdd1-171">Before you can configure the SAML assertion, you must contact the [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="afdd1-172">U moet deze waarde de stappen in de volgende sectie uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="afdd1-172">You need this value to complete the steps in the next section.</span></span> 

6. <span data-ttu-id="afdd1-173">In de **eenmalige aanmelding** het dialoogvenster de **gebruikerskenmerken** sectie, het configureren van het kenmerk van SAML-token, zoals wordt weergegeven in de volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="afdd1-173">In the **Single sign-on** dialog box, in the **User Attributes** section, configure the SAML token attribute as shown in the following image.</span></span> <span data-ttu-id="afdd1-174">Vervolgens voert u de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="afdd1-174">Then take the following steps.</span></span>
    
      | <span data-ttu-id="afdd1-175">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="afdd1-175">Attribute name</span></span>    |   <span data-ttu-id="afdd1-176">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="afdd1-176">Attribute value</span></span> |  
    | ------------------- | -------------------- |    
    | <span data-ttu-id="afdd1-177">ATTR_LOGINCLAIM</span><span class="sxs-lookup"><span data-stu-id="afdd1-177">ATTR_LOGINCLAIM</span></span> | <span data-ttu-id="afdd1-178">join ([e] '102938475Z' ' @ '</span><span class="sxs-lookup"><span data-stu-id="afdd1-178">join([mail],"102938475Z","@"</span></span> |
    
      <span data-ttu-id="afdd1-179">a.</span><span class="sxs-lookup"><span data-stu-id="afdd1-179">a.</span></span> <span data-ttu-id="afdd1-180">Openen van de **kenmerk toevoegen** dialoogvenster, selecteer **toevoegen kenmerk**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-180">To open the **Add Attribute** dialog, select **Add attribute**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="afdd1-183">b.</span><span class="sxs-lookup"><span data-stu-id="afdd1-183">b.</span></span> <span data-ttu-id="afdd1-184">In de **naam** in het vak **ATTR_LOGINCLAIM**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-184">In the **Name** box, type **ATTR_LOGINCLAIM**.</span></span>

    <span data-ttu-id="afdd1-185">c.</span><span class="sxs-lookup"><span data-stu-id="afdd1-185">c.</span></span> <span data-ttu-id="afdd1-186">Van de **waarde** selecteert **Join()**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-186">From the **Value** list, select **Join()**.</span></span>

    <span data-ttu-id="afdd1-187">d.</span><span class="sxs-lookup"><span data-stu-id="afdd1-187">d.</span></span> <span data-ttu-id="afdd1-188">Van de **tekenreeks1** selecteert **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-188">From the **String1** list, select **user.mail**.</span></span>

    <span data-ttu-id="afdd1-189">e.</span><span class="sxs-lookup"><span data-stu-id="afdd1-189">e.</span></span> <span data-ttu-id="afdd1-190">Voor **tekenreeks2**, typt u de unieke id die wordt geleverd door uw team HR2day.</span><span class="sxs-lookup"><span data-stu-id="afdd1-190">For **String2**, type the unique identifier that's provided by your HR2day team.</span></span>

    <span data-ttu-id="afdd1-191">f.</span><span class="sxs-lookup"><span data-stu-id="afdd1-191">f.</span></span> <span data-ttu-id="afdd1-192">In de **scheidingsteken** in het vak  **@** .</span><span class="sxs-lookup"><span data-stu-id="afdd1-192">In the **Separator** box, type **@**.</span></span>
    
    <span data-ttu-id="afdd1-193">g.</span><span class="sxs-lookup"><span data-stu-id="afdd1-193">g.</span></span> <span data-ttu-id="afdd1-194">Selecteer **Ok**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-194">Select **Ok**.</span></span>

7. <span data-ttu-id="afdd1-195">Selecteer de knop **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-195">Select the **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="afdd1-197">In de **HR2day door Merces configuratie** sectie **HR2day configureren door Merces** openen de **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="afdd1-197">In the **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="afdd1-198">Kopiëren de **Sign-Out URL**, **SAML entiteit-ID**, en **SAML Single Sign-On Service-URL** van de **Naslaggids** sectie.</span><span class="sxs-lookup"><span data-stu-id="afdd1-198">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. <span data-ttu-id="afdd1-200">Voor meer informatie over het configureren van eenmalige aanmelding voor uw toepassing Neem contact op met de [HR2day door Merces client ondersteuningsteam](mailTo:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="afdd1-200">To configure SSO  for your application, contact the [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span></span> <span data-ttu-id="afdd1-201">Koppel de gedownloade **Certificate(Base64)** bestand naar uw e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="afdd1-201">Attach the downloaded **Certificate(Base64)** file to your email.</span></span> <span data-ttu-id="afdd1-202">Bieden ook de **Sign-Out URL**, **SAML entiteit-ID**, en **SAML Single Sign-On Service-URL** zodat ze kunnen worden geconfigureerd voor eenmalige aanmelding-integratie.</span><span class="sxs-lookup"><span data-stu-id="afdd1-202">Also provide the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    ><span data-ttu-id="afdd1-203">Aan het team Merces vermeld dat deze integratie de entiteit-ID moet moet worden ingesteld met het patroon **https://hr2day.force.com/INSTANCENAME**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-203">Mention to the Merces team that this integration needs the Entity ID to be set with the pattern **https://hr2day.force.com/INSTANCENAME**.</span></span>

    > [!TIP]
    ><span data-ttu-id="afdd1-204">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="afdd1-204">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="afdd1-205">Na het toevoegen van deze app uit de **Active Directory** > **bedrijfstoepassingen** sectie, selecteer de **Single Sign-On** tabblad.</span><span class="sxs-lookup"><span data-stu-id="afdd1-205">After you add this app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab.</span></span> <span data-ttu-id="afdd1-206">Vervolgens toegang krijgen tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="afdd1-206">Then access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="afdd1-207">U kunt meer lezen over de functie embedded-documentatie in de [documentatie van Azure AD ingesloten]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="afdd1-207">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="afdd1-208">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="afdd1-208">Create an Azure AD test user</span></span>
<span data-ttu-id="afdd1-209">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="afdd1-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="afdd1-211">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="afdd1-211">**To create a test user in Azure AD, take the following steps:**</span></span>

1. <span data-ttu-id="afdd1-212">In de **Azure-portal**, Selecteer op het navigatiedeelvenster links de **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="afdd1-212">In the **Azure portal**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="afdd1-214">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en selecteer vervolgens **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-214">To display the list of users, go to **Users and groups**, and then select **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="afdd1-216">Openen van de **gebruiker** dialoogvenster, **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="afdd1-216">To open the **User** dialog box, select **Add** on the top of the dialog box.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="afdd1-218">In de **gebruiker** dialoogvenster vak, voert de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="afdd1-218">In the **User** dialog box, take the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="afdd1-220">a.</span><span class="sxs-lookup"><span data-stu-id="afdd1-220">a.</span></span> <span data-ttu-id="afdd1-221">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-221">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="afdd1-222">b.</span><span class="sxs-lookup"><span data-stu-id="afdd1-222">b.</span></span> <span data-ttu-id="afdd1-223">In de **gebruikersnaam** in het vak de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="afdd1-223">In the **User name** box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="afdd1-224">c.</span><span class="sxs-lookup"><span data-stu-id="afdd1-224">c.</span></span> <span data-ttu-id="afdd1-225">Selecteer **wachtwoord weergeven**, en noteer het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="afdd1-225">Select **Show Password**, and then write down the password.</span></span>

    <span data-ttu-id="afdd1-226">d.</span><span class="sxs-lookup"><span data-stu-id="afdd1-226">d.</span></span> <span data-ttu-id="afdd1-227">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-227">Select **Create**.</span></span>
 
### <a name="create-an-hr2day-by-merces-test-user"></a><span data-ttu-id="afdd1-228">Een HR2day door Merces testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="afdd1-228">Create an HR2day by Merces test user</span></span>

<span data-ttu-id="afdd1-229">Het doel van deze sectie is het maken van een gebruiker Britta Simon in HR2day door Merces aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="afdd1-229">The objective of this section is to create a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="afdd1-230">Als u wilt toevoegen de gebruikers in het account HR2day, werken met de [HR2day door Merces client ondersteuningsteam](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="afdd1-230">To add the users in the HR2day account, work with the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span> 

> [!NOTE]
> <span data-ttu-id="afdd1-231">Als u maken van een gebruiker handmatig wilt, neem dan contact op met de [HR2day door Merces client ondersteuningsteam](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="afdd1-231">If you need to create a user manually, contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="afdd1-232">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="afdd1-232">Assign the Azure AD test user</span></span>

<span data-ttu-id="afdd1-233">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan HR2day door Merces.</span><span class="sxs-lookup"><span data-stu-id="afdd1-233">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to HR2day by Merces.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="afdd1-235">**Britta Simon om aan te wijzen HR2day door Merces, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="afdd1-235">**To assign Britta Simon to HR2day by Merces, take the following steps:**</span></span>

1. <span data-ttu-id="afdd1-236">Open de weergave van toepassingen in de Azure-portal, Ga naar de directoryweergave en gaat u naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-236">In the Azure portal, open the applications view, go to the directory view, and then go to **Enterprise applications**.</span></span> <span data-ttu-id="afdd1-237">Selecteer vervolgens **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-237">Next, select **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="afdd1-239">Selecteer in de lijst met toepassingen **HR2day door Merces**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-239">In the applications list, select **HR2day by Merces**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. <span data-ttu-id="afdd1-241">Selecteer in het menu aan de linkerkant **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-241">In the menu on the left, select **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="afdd1-243">Selecteer de **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="afdd1-243">Select the **Add** button.</span></span> <span data-ttu-id="afdd1-244">Klik in de **toevoegen toewijzing** dialoogvenster, **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-244">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="afdd1-246">In de **gebruikers en groepen** het dialoogvenster de **gebruikers** selecteert **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-246">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="afdd1-247">Klik op de **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="afdd1-247">Click the **Select** button.</span></span>

7. <span data-ttu-id="afdd1-248">In de **toevoegen toewijzing** dialoogvenster, **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="afdd1-248">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="afdd1-249">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="afdd1-249">Test single sign-on</span></span>

<span data-ttu-id="afdd1-250">Het doel van deze sectie is het testen van uw configuratie Azure AD eenmalige aanmelding met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="afdd1-250">The objective of this section is to test your Azure AD single sign-on configuration by using the Access Panel.</span></span>  

<span data-ttu-id="afdd1-251">Wanneer u de HR2day door Merces-tegel in het toegangsvenster selecteert, ophalen u automatisch aangemeld bij uw HR2day door Merces toepassing.</span><span class="sxs-lookup"><span data-stu-id="afdd1-251">When you select the HR2day by Merces tile in the Access Panel, you automatically get signed in  to your HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="afdd1-252">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="afdd1-252">Additional resources</span></span>

* [<span data-ttu-id="afdd1-253">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="afdd1-253">List of tutorials about how to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="afdd1-254">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="afdd1-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

