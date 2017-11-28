---
title: 'Zelfstudie: Azure Active Directory-integratie met SAP Cloud voor klant | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en SAP Cloud voor de klant.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: e4d945525a45704f34e1d9e742220928a516f341
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="a7ab6-103">Zelfstudie: Azure Active Directory-integratie met SAP Cloud voor klant</span><span class="sxs-lookup"><span data-stu-id="a7ab6-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>

<span data-ttu-id="a7ab6-104">In deze zelfstudie leert u SAP Cloud voor klanten met Azure Active Directory (Azure AD) integreren.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-104">In this tutorial, you learn how to integrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7ab6-105">Integratie van SAP Cloud voor klanten met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a7ab6-105">Integrating SAP Cloud for Customer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a7ab6-106">U kunt beheren in Azure AD die toegang tot SAP Cloud voor klant heeft</span><span class="sxs-lookup"><span data-stu-id="a7ab6-106">You can control in Azure AD who has access to SAP Cloud for Customer</span></span>
- <span data-ttu-id="a7ab6-107">U kunt uw gebruikers automatisch ophalen aangemeld bij SAP Cloud voor klant (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="a7ab6-107">You can enable your users to automatically get signed-on to SAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a7ab6-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="a7ab6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a7ab6-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a7ab6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7ab6-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a7ab6-110">Prerequisites</span></span>

<span data-ttu-id="a7ab6-111">Azure AD-integratie met SAP Cloud configureren voor de klant, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="a7ab6-111">To configure Azure AD integration with SAP Cloud for Customer, you need the following items:</span></span>

- <span data-ttu-id="a7ab6-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a7ab6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a7ab6-113">Een Cloud SAP voor eenmalige aanmelding klant abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="a7ab6-113">A SAP Cloud for Customer single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7ab6-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7ab6-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a7ab6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7ab6-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a7ab6-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a7ab6-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7ab6-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a7ab6-118">Scenario description</span></span>
<span data-ttu-id="a7ab6-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7ab6-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a7ab6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7ab6-121">SAP Cloud toe te voegen voor de klant uit de galerie</span><span class="sxs-lookup"><span data-stu-id="a7ab6-121">Adding SAP Cloud for Customer from the gallery</span></span>
2. <span data-ttu-id="a7ab6-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a7ab6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-the-gallery"></a><span data-ttu-id="a7ab6-123">SAP Cloud toe te voegen voor de klant uit de galerie</span><span class="sxs-lookup"><span data-stu-id="a7ab6-123">Adding SAP Cloud for Customer from the gallery</span></span>
<span data-ttu-id="a7ab6-124">Voor het configureren van de integratie van SAP Cloud voor klanten met Azure AD, moet u SAP Cloud voor klant uit de galerie toevoegt aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-124">To configure the integration of SAP Cloud for Customer into Azure AD, you need to add SAP Cloud for Customer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a7ab6-125">**Als u wilt toevoegen SAP Cloud voor klant uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a7ab6-125">**To add SAP Cloud for Customer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a7ab6-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a7ab6-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a7ab6-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a7ab6-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a7ab6-133">Typ in het zoekvak **SAP Cloud voor klant**.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-133">In the search box, type **SAP Cloud for Customer**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. <span data-ttu-id="a7ab6-135">Selecteer in het deelvenster resultaten **SAP Cloud voor klant**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-135">In the results panel, select **SAP Cloud for Customer**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a7ab6-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a7ab6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a7ab6-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met SAP Cloud voor klant op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a7ab6-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in de Cloud SAP voor de klant is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Cloud for Customer is to a user in Azure AD.</span></span> <span data-ttu-id="a7ab6-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de Cloud SAP voor klant tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-140">In other words, a link relationship between an Azure AD user and the related user in SAP Cloud for Customer needs to be established.</span></span>

<span data-ttu-id="a7ab6-141">In de Cloud SAP voor de klant, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-141">In SAP Cloud for Customer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a7ab6-142">Om te configureren en testen van Azure AD eenmalige aanmelding met SAP Cloud voor de klant, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="a7ab6-142">To configure and test Azure AD single sign-on with SAP Cloud for Customer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a7ab6-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a7ab6-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a7ab6-145">**[Maken van een Cloud SAP voor klant testgebruiker](#creating-a-sap-cloud-for-customer-test-user)**  - bevatten een equivalent van Britta Simon SAP Cloud voor klant die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - to have a counterpart of Britta Simon in SAP Cloud for Customer that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a7ab6-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a7ab6-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a7ab6-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a7ab6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a7ab6-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw Cloud SAP voor toepassing van de klant.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span></span>

<span data-ttu-id="a7ab6-150">**Voor het configureren van Azure AD eenmalige aanmelding met SAP Cloud voor de klant, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a7ab6-150">**To configure Azure AD single sign-on with SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="a7ab6-151">In de Azure-portal op de **SAP Cloud voor klant** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-151">In the Azure portal, on the **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a7ab6-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. <span data-ttu-id="a7ab6-155">Op de **SAP Cloud voor domein van de klant en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a7ab6-155">On the **SAP Cloud for Customer Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    <span data-ttu-id="a7ab6-157">a.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-157">a.</span></span> <span data-ttu-id="a7ab6-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="a7ab6-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    <span data-ttu-id="a7ab6-159">b.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-159">b.</span></span> <span data-ttu-id="a7ab6-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="a7ab6-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a7ab6-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-161">These values are not real.</span></span> <span data-ttu-id="a7ab6-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a7ab6-163">Neem contact op met [SAP Cloud voor klant Client ondersteuningsteam](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to get these values.</span></span> 

4. <span data-ttu-id="a7ab6-164">Op de **gebruikerskenmerken** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a7ab6-164">On the **User Attributes** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    <span data-ttu-id="a7ab6-166">a.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-166">a.</span></span> <span data-ttu-id="a7ab6-167">In **gebruikers-id** lijst, selecteert de **ExtractMailPrefix()** functie.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-167">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>

    <span data-ttu-id="a7ab6-168">b.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-168">b.</span></span> <span data-ttu-id="a7ab6-169">Van de **Mail** , selecteert u het gebruikerskenmerk die u wilt gebruiken voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-169">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span>
    <span data-ttu-id="a7ab6-170">Bijvoorbeeld, als u wilt gebruiken van de werknemer-id als unieke gebruikers-id en u de waarde van het kenmerk in de ExtensionAttribute2 hebt opgeslagen, selecteert u user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-170">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>  

5. <span data-ttu-id="a7ab6-171">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-171">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. <span data-ttu-id="a7ab6-173">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-173">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="a7ab6-175">Op de **SAP Cloud voor de configuratie van de klant** sectie, klikt u op **SAP Cloud configureren voor de klant** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-175">On the **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a7ab6-176">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="a7ab6-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. <span data-ttu-id="a7ab6-178">Als u eenmalige aanmelding die zijn geconfigureerd, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a7ab6-178">To get SSO configured, perform the following steps:</span></span>
   
    <span data-ttu-id="a7ab6-179">a.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-179">a.</span></span> <span data-ttu-id="a7ab6-180">De aanmelding in de Cloud SAP voor Customer portal met beheerdersrechten.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-180">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="a7ab6-181">b.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-181">b.</span></span> <span data-ttu-id="a7ab6-182">Navigeer naar de **toepassings- en algemene beheertaak gebruiker** en klik op de **identiteitsprovider** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-182">Navigate to the **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="a7ab6-183">c.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-183">c.</span></span> <span data-ttu-id="a7ab6-184">Klik op **nieuwe identiteitsprovider** en selecteert u het XML-bestand voor metagegevens die u hebt gedownload vanuit de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-184">Click **New Identity Provider** and select the metadata XML file you have downloaded from the Azure portal.</span></span> <span data-ttu-id="a7ab6-185">U importeert de metagegevens, uploadt het systeem automatisch de vereiste handtekeningcertificaat en een versleutelingscertificaat.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-185">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="a7ab6-187">d.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-187">d.</span></span> <span data-ttu-id="a7ab6-188">Azure Active Directory is vereist voor het element Assertion Consumer Service-URL in de SAML-aanvraag, dus selecteer de **Assertion Consumer Service-URL opnemen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-188">Azure Active Directory requires the element Assertion Consumer Service URL in the SAML request, so select the **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="a7ab6-189">e.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-189">e.</span></span> <span data-ttu-id="a7ab6-190">Klik op **activeren Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-190">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="a7ab6-191">f.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-191">f.</span></span> <span data-ttu-id="a7ab6-192">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-192">Save your changes.</span></span>
   
    <span data-ttu-id="a7ab6-193">g.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-193">g.</span></span> <span data-ttu-id="a7ab6-194">Klik op de **mijn systeem** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-194">Click the **My System** tab.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="a7ab6-196">h.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-196">h.</span></span> <span data-ttu-id="a7ab6-197">In **Azure AD aanmelding URL** textbox plakken **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="a7ab6-199">ik.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-199">i.</span></span> <span data-ttu-id="a7ab6-200">Opgeven of de werknemer handmatig kiezen kunt tussen het aanmelden met gebruikersnaam en wachtwoord of eenmalige aanmelding door het selecteren van de **handmatige identiteit Provider selectie**.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-200">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting the **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="a7ab6-201">j.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-201">j.</span></span> <span data-ttu-id="a7ab6-202">In de **URL SSO** sectie, de URL opgeven die moet worden gebruikt door uw werknemers zich aanmelden op het systeem.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-202">In the **SSO URL** section, specify the URL that should be used by your employees to sign on to the system.</span></span> 
    <span data-ttu-id="a7ab6-203">In de **URL verzonden naar werknemer** wilt weergeven, kunt u kiezen uit de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="a7ab6-203">In the **URL Sent to Employee** list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="a7ab6-204">**Niet-SSO-URL**</span><span class="sxs-lookup"><span data-stu-id="a7ab6-204">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="a7ab6-205">Het systeem wordt de URL van de normale system verzendt naar de werknemer.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-205">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="a7ab6-206">De werknemer kan niet aanmelden met eenmalige aanmelding, en moet gebruik wachtwoord of certificaat in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-206">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="a7ab6-207">**URL VOOR EENMALIGE AANMELDING**</span><span class="sxs-lookup"><span data-stu-id="a7ab6-207">**SSO URL**</span></span> 
   
    <span data-ttu-id="a7ab6-208">Het systeem verzendt alleen de SSO-URL naar de werknemer.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-208">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="a7ab6-209">De werknemer kunt aanmelden met behulp van eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-209">The employee can log on using SSO.</span></span> <span data-ttu-id="a7ab6-210">Authenticatie-aanvraag wordt via de IdP omgeleid.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-210">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="a7ab6-211">**Automatische selectie**</span><span class="sxs-lookup"><span data-stu-id="a7ab6-211">**Automatic Selection**</span></span>
   
    <span data-ttu-id="a7ab6-212">Als eenmalige aanmelding niet actief is, wordt de URL van de normale systeem door het systeem verzonden naar de werknemer.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-212">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="a7ab6-213">Als eenmalige aanmelding actief is, controleert het systeem of de werknemer een wachtwoord heeft.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-213">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="a7ab6-214">Als een wachtwoord beschikbaar is, worden zowel de URL van de SSO- en Non-SSO-verzonden naar de werknemer.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-214">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="a7ab6-215">Als de werknemer geen wachtwoord heeft, wordt echter alleen de URL voor eenmalige aanmelding verzonden naar de werknemer.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-215">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="a7ab6-216">k.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-216">k.</span></span> <span data-ttu-id="a7ab6-217">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-217">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="a7ab6-218">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="a7ab6-218">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a7ab6-219">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-219">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a7ab6-220">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a7ab6-220">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a7ab6-221">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a7ab6-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="a7ab6-222">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-222">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a7ab6-224">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a7ab6-224">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a7ab6-225">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-225">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a7ab6-227">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-227">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a7ab6-229">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-229">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a7ab6-231">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a7ab6-231">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a7ab6-233">a.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-233">a.</span></span> <span data-ttu-id="a7ab6-234">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-234">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a7ab6-235">b.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-235">b.</span></span> <span data-ttu-id="a7ab6-236">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-236">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a7ab6-237">c.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-237">c.</span></span> <span data-ttu-id="a7ab6-238">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-238">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a7ab6-239">d.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-239">d.</span></span> <span data-ttu-id="a7ab6-240">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-240">Click **Create**.</span></span>
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a><span data-ttu-id="a7ab6-241">Maken van een Cloud SAP voor klant testgebruiker</span><span class="sxs-lookup"><span data-stu-id="a7ab6-241">Creating a SAP Cloud for Customer test user</span></span>

<span data-ttu-id="a7ab6-242">In deze sectie maakt u Britta Simon aangeroepen in SAP Cloud voor klant van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="a7ab6-243">Neem contact op met [SAP Cloud voor afdeling Klantenondersteuning](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) om toe te voegen de gebruikers in de Cloud SAP voor klant-platform.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to add the users in the SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="a7ab6-244">Zorg dat NameID waarde met het veld username in de Cloud SAP voor klant-platform overeenkomen moet.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-244">Please make sure that NameID value should match with the username field in the SAP Cloud for Customer platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a7ab6-245">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7ab6-245">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a7ab6-246">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot SAP Cloud voor klant.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-246">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Cloud for Customer.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a7ab6-248">**Britta Simon om aan te wijzen SAP Cloud voor de klant, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a7ab6-248">**To assign Britta Simon to SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="a7ab6-249">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-249">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a7ab6-251">Selecteer in de lijst met toepassingen **SAP Cloud voor klant**.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-251">In the applications list, select **SAP Cloud for Customer**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. <span data-ttu-id="a7ab6-253">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-253">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a7ab6-255">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-255">Click **Add** button.</span></span> <span data-ttu-id="a7ab6-256">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a7ab6-258">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-258">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a7ab6-259">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-259">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a7ab6-260">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-260">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a7ab6-261">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a7ab6-261">Testing single sign-on</span></span>

<span data-ttu-id="a7ab6-262">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-262">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a7ab6-263">Als u op de Cloud SAP voor klant-tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw SAP-Cloud voor de toepassing van de klant.</span><span class="sxs-lookup"><span data-stu-id="a7ab6-263">When you click the SAP Cloud for Customer tile in the Access Panel, you should get automatically signed-on to your SAP Cloud for Customer application.</span></span>
<span data-ttu-id="a7ab6-264">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a7ab6-264">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a7ab6-265">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a7ab6-265">Additional resources</span></span>

* [<span data-ttu-id="a7ab6-266">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7ab6-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a7ab6-267">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a7ab6-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

