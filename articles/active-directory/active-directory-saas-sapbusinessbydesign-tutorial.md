---
title: 'Zelfstudie: Azure Active Directory-integratie met SAP Business ByDesign | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en SAP Business ByDesign.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ab76a0ac1ef954efd3c66e6f565514b889ed9444
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="07b3d-103">Zelfstudie: Azure Active Directory-integratie met SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="07b3d-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="07b3d-104">In deze zelfstudie leert u hoe SAP Business ByDesign integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="07b3d-104">In this tutorial, you learn how to integrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="07b3d-105">SAP Business ByDesign integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="07b3d-105">Integrating SAP Business ByDesign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="07b3d-106">U kunt beheren in Azure AD die toegang tot een SAP Business ByDesign heeft.</span><span class="sxs-lookup"><span data-stu-id="07b3d-106">You can control in Azure AD who has access to SAP Business ByDesign.</span></span>
- <span data-ttu-id="07b3d-107">U kunt uw gebruikers automatisch ophalen aangemeld bij SAP Business ByDesign (Single Sign-On) inschakelen met hun Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="07b3d-107">You can enable your users to automatically get signed-on to SAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="07b3d-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="07b3d-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="07b3d-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="07b3d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07b3d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="07b3d-110">Prerequisites</span></span>

<span data-ttu-id="07b3d-111">Voor het configureren van Azure AD-integratie met SAP Business ByDesign, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="07b3d-111">To configure Azure AD integration with SAP Business ByDesign, you need the following items:</span></span>

- <span data-ttu-id="07b3d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="07b3d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="07b3d-113">Een SAP Business ByDesign eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="07b3d-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="07b3d-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="07b3d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="07b3d-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="07b3d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="07b3d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="07b3d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="07b3d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="07b3d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="07b3d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="07b3d-118">Scenario description</span></span>
<span data-ttu-id="07b3d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="07b3d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="07b3d-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="07b3d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="07b3d-121">SAP Business ByDesign uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="07b3d-121">Adding SAP Business ByDesign from the gallery</span></span>
2. <span data-ttu-id="07b3d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="07b3d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-the-gallery"></a><span data-ttu-id="07b3d-123">SAP Business ByDesign uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="07b3d-123">Adding SAP Business ByDesign from the gallery</span></span>
<span data-ttu-id="07b3d-124">Voor het configureren van de integratie van SAP Business ByDesign in Azure AD, moet u een SAP Business ByDesign uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="07b3d-124">To configure the integration of SAP Business ByDesign into Azure AD, you need to add SAP Business ByDesign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="07b3d-125">**Als u wilt toevoegen SAP Business ByDesign uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="07b3d-125">**To add SAP Business ByDesign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="07b3d-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="07b3d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="07b3d-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="07b3d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="07b3d-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="07b3d-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="07b3d-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="07b3d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="07b3d-133">Typ in het zoekvak **SAP Business ByDesign**, selecteer **SAP Business ByDesign** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="07b3d-133">In the search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button to add the application.</span></span>

    ![SAP Business ByDesign in de lijst met resultaten](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="07b3d-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="07b3d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="07b3d-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met SAP Business ByDesign op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="07b3d-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="07b3d-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in SAP Business ByDesign is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07b3d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Business ByDesign is to a user in Azure AD.</span></span> <span data-ttu-id="07b3d-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in een SAP Business ByDesign tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="07b3d-138">In other words, a link relationship between an Azure AD user and the related user in SAP Business ByDesign needs to be established.</span></span>

<span data-ttu-id="07b3d-139">In een SAP Business ByDesign, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="07b3d-139">In SAP Business ByDesign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="07b3d-140">Om te configureren en testen van Azure AD eenmalige aanmelding met SAP Business ByDesign, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="07b3d-140">To configure and test Azure AD single sign-on with SAP Business ByDesign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="07b3d-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="07b3d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="07b3d-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07b3d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="07b3d-143">**[Maken van een SAP Business ByDesign testgebruiker](#create-an-sap-business-bydesign-test-user)**  - SAP Business ByDesign die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="07b3d-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - to have a counterpart of Britta Simon in SAP Business ByDesign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="07b3d-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="07b3d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="07b3d-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="07b3d-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="07b3d-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="07b3d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="07b3d-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing SAP Business ByDesign configureren.</span><span class="sxs-lookup"><span data-stu-id="07b3d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="07b3d-148">**Voor het configureren van Azure AD eenmalige aanmelding met SAP Business ByDesign, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="07b3d-148">**To configure Azure AD single sign-on with SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="07b3d-149">In de Azure-portal op de **SAP Business ByDesign** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="07b3d-149">In the Azure portal, on the **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="07b3d-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="07b3d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="07b3d-153">Op de **SAP Business ByDesign domein en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="07b3d-153">On the **SAP Business ByDesign Domain and URLs** section, perform the following steps:</span></span>

    ![URL's en SAP Business ByDesign domein eenmalige aanmelding informatie](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="07b3d-155">a.</span><span class="sxs-lookup"><span data-stu-id="07b3d-155">a.</span></span> <span data-ttu-id="07b3d-156">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="07b3d-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="07b3d-157">b.</span><span class="sxs-lookup"><span data-stu-id="07b3d-157">b.</span></span> <span data-ttu-id="07b3d-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="07b3d-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="07b3d-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="07b3d-159">These values are not real.</span></span> <span data-ttu-id="07b3d-160">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="07b3d-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="07b3d-161">Neem contact op met [SAP Business ByDesign Client ondersteuningsteam](https://www.sap.com/products/cloud-analytics.support.html) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="07b3d-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to get these values.</span></span>

4. <span data-ttu-id="07b3d-162">Op de **gebruikerskenmerken** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="07b3d-162">On the **User Attributes** section, perform the following steps:</span></span>

    ![SAP Business ByDesign kenmerk sectie](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="07b3d-164">a.</span><span class="sxs-lookup"><span data-stu-id="07b3d-164">a.</span></span> <span data-ttu-id="07b3d-165">In **gebruikers-id** lijst, selecteert de **ExtractMailPrefix()** functie.</span><span class="sxs-lookup"><span data-stu-id="07b3d-165">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="07b3d-166">b.</span><span class="sxs-lookup"><span data-stu-id="07b3d-166">b.</span></span> <span data-ttu-id="07b3d-167">Van de **Mail** , selecteert u het gebruikerskenmerk die u wilt gebruiken voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="07b3d-167">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span> <span data-ttu-id="07b3d-168">Bijvoorbeeld, als u wilt gebruiken van de werknemer-id als unieke gebruikers-id en u de waarde van het kenmerk in de ExtensionAttribute2 hebt opgeslagen, selecteert u user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="07b3d-168">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>     

5. <span data-ttu-id="07b3d-169">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="07b3d-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="07b3d-171">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="07b3d-171">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="07b3d-173">Op de **SAP Business ByDesign configuratie** sectie, klikt u op **configureren SAP Business ByDesign** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="07b3d-173">On the **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** to open **Configure sign-on** window.</span></span> <span data-ttu-id="07b3d-174">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="07b3d-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![SAP Business ByDesign-configuratie](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="07b3d-176">Als u eenmalige aanmelding voor uw toepassing is geconfigureerd, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="07b3d-176">To get SSO configured for your application, perform the following steps:</span></span>
   
    <span data-ttu-id="07b3d-177">a.</span><span class="sxs-lookup"><span data-stu-id="07b3d-177">a.</span></span> <span data-ttu-id="07b3d-178">Meld u aan op uw portal SAP Business ByDesign met beheerdersrechten.</span><span class="sxs-lookup"><span data-stu-id="07b3d-178">Sign on to your SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="07b3d-179">b.</span><span class="sxs-lookup"><span data-stu-id="07b3d-179">b.</span></span> <span data-ttu-id="07b3d-180">Navigeer naar **toepassings- en algemene beheertaak gebruiker** en klik op de **identiteitsprovider** tabblad.</span><span class="sxs-lookup"><span data-stu-id="07b3d-180">Navigate to **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="07b3d-181">c.</span><span class="sxs-lookup"><span data-stu-id="07b3d-181">c.</span></span> <span data-ttu-id="07b3d-182">Klik op **nieuwe identiteitsprovider** en selecteert u de XML-bestand met metagegevens die u hebt gedownload vanuit de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="07b3d-182">Click **New Identity Provider** and select the metadata XML file that you have downloaded from the Azure portal.</span></span> <span data-ttu-id="07b3d-183">U importeert de metagegevens, uploadt het systeem automatisch de vereiste handtekeningcertificaat en een versleutelingscertificaat.</span><span class="sxs-lookup"><span data-stu-id="07b3d-183">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="07b3d-185">d.</span><span class="sxs-lookup"><span data-stu-id="07b3d-185">d.</span></span> <span data-ttu-id="07b3d-186">Om op te nemen de **Assertion Consumer Service-URL** selecteren in het SAML-aanvraag **Assertion Consumer Service-URL opnemen**.</span><span class="sxs-lookup"><span data-stu-id="07b3d-186">To include the **Assertion Consumer Service URL** into the SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="07b3d-187">e.</span><span class="sxs-lookup"><span data-stu-id="07b3d-187">e.</span></span> <span data-ttu-id="07b3d-188">Klik op **activeren Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="07b3d-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="07b3d-189">f.</span><span class="sxs-lookup"><span data-stu-id="07b3d-189">f.</span></span> <span data-ttu-id="07b3d-190">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="07b3d-190">Save your changes.</span></span>
   
    <span data-ttu-id="07b3d-191">g.</span><span class="sxs-lookup"><span data-stu-id="07b3d-191">g.</span></span> <span data-ttu-id="07b3d-192">Klik op de **mijn systeem** tabblad.</span><span class="sxs-lookup"><span data-stu-id="07b3d-192">Click the **My System** tab.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="07b3d-194">h.</span><span class="sxs-lookup"><span data-stu-id="07b3d-194">h.</span></span> <span data-ttu-id="07b3d-195">Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit de Azure-portal in de **Azure AD aanmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="07b3d-195">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal it into the **Azure AD Sign On URL** textbox.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="07b3d-197">ik.</span><span class="sxs-lookup"><span data-stu-id="07b3d-197">i.</span></span> <span data-ttu-id="07b3d-198">Opgeven of de werknemer handmatig kiezen kunt tussen het aanmelden met gebruikersnaam en wachtwoord of eenmalige aanmelding door te selecteren **handmatige identiteit Provider selectie**.</span><span class="sxs-lookup"><span data-stu-id="07b3d-198">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="07b3d-199">j.</span><span class="sxs-lookup"><span data-stu-id="07b3d-199">j.</span></span> <span data-ttu-id="07b3d-200">In de **URL SSO** sectie, de URL opgeven die moet worden gebruikt door de werknemer voor aanmelding bij het systeem.</span><span class="sxs-lookup"><span data-stu-id="07b3d-200">In the **SSO URL** section, specify the URL that should be used by the employee to logon to the system.</span></span> 
    <span data-ttu-id="07b3d-201">In de URL naar verzonden werknemer vervolgkeuzelijst wordt weergegeven, kunt u kiezen uit de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="07b3d-201">In the URL Sent to Employee dropdown list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="07b3d-202">**Niet-SSO-URL**</span><span class="sxs-lookup"><span data-stu-id="07b3d-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="07b3d-203">Het systeem wordt de URL van de normale system verzendt naar de werknemer.</span><span class="sxs-lookup"><span data-stu-id="07b3d-203">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="07b3d-204">De werknemer kan niet aanmelden met eenmalige aanmelding, en moet gebruik wachtwoord of certificaat in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="07b3d-204">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="07b3d-205">**URL VOOR EENMALIGE AANMELDING**</span><span class="sxs-lookup"><span data-stu-id="07b3d-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="07b3d-206">Het systeem verzendt alleen de SSO-URL naar de werknemer.</span><span class="sxs-lookup"><span data-stu-id="07b3d-206">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="07b3d-207">De werknemer kunt aanmelden met behulp van eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="07b3d-207">The employee can log on using SSO.</span></span> <span data-ttu-id="07b3d-208">Authenticatie-aanvraag wordt via de IdP omgeleid.</span><span class="sxs-lookup"><span data-stu-id="07b3d-208">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="07b3d-209">**Automatische selectie**</span><span class="sxs-lookup"><span data-stu-id="07b3d-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="07b3d-210">Als eenmalige aanmelding niet actief is, wordt de URL van de normale systeem door het systeem verzonden naar de werknemer.</span><span class="sxs-lookup"><span data-stu-id="07b3d-210">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="07b3d-211">Als eenmalige aanmelding actief is, controleert het systeem of de werknemer een wachtwoord heeft.</span><span class="sxs-lookup"><span data-stu-id="07b3d-211">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="07b3d-212">Als een wachtwoord beschikbaar is, worden zowel de URL van de SSO- en Non-SSO-verzonden naar de werknemer.</span><span class="sxs-lookup"><span data-stu-id="07b3d-212">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="07b3d-213">Als de werknemer geen wachtwoord heeft, wordt echter alleen de URL voor eenmalige aanmelding verzonden naar de werknemer.</span><span class="sxs-lookup"><span data-stu-id="07b3d-213">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="07b3d-214">k.</span><span class="sxs-lookup"><span data-stu-id="07b3d-214">k.</span></span> <span data-ttu-id="07b3d-215">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="07b3d-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="07b3d-216">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="07b3d-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="07b3d-217">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="07b3d-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="07b3d-218">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="07b3d-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="07b3d-219">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="07b3d-219">Create an Azure AD test user</span></span>

<span data-ttu-id="07b3d-220">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="07b3d-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="07b3d-222">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="07b3d-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="07b3d-223">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="07b3d-223">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="07b3d-225">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="07b3d-225">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="07b3d-227">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="07b3d-227">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="07b3d-229">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="07b3d-229">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="07b3d-231">a.</span><span class="sxs-lookup"><span data-stu-id="07b3d-231">a.</span></span> <span data-ttu-id="07b3d-232">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="07b3d-232">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="07b3d-233">b.</span><span class="sxs-lookup"><span data-stu-id="07b3d-233">b.</span></span> <span data-ttu-id="07b3d-234">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07b3d-234">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="07b3d-235">c.</span><span class="sxs-lookup"><span data-stu-id="07b3d-235">c.</span></span> <span data-ttu-id="07b3d-236">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="07b3d-236">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="07b3d-237">d.</span><span class="sxs-lookup"><span data-stu-id="07b3d-237">d.</span></span> <span data-ttu-id="07b3d-238">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="07b3d-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="07b3d-239">Een SAP Business ByDesign testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="07b3d-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="07b3d-240">In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in een SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="07b3d-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="07b3d-241">Neem contact op met [SAP Business ByDesign Client ondersteuningsteam](https://www.sap.com/products/cloud-analytics.support.html) om toe te voegen de gebruikers van het SAP Business ByDesign-platform.</span><span class="sxs-lookup"><span data-stu-id="07b3d-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to add the users in the SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="07b3d-242">Zorg dat NameID waarde met het veld username van het SAP Business ByDesign-platform overeenkomen moet.</span><span class="sxs-lookup"><span data-stu-id="07b3d-242">Please make sure that NameID value should match with the username field in the SAP Business ByDesign platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="07b3d-243">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="07b3d-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="07b3d-244">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="07b3d-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Business ByDesign.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="07b3d-246">**Britta Simon om aan te wijzen SAP Business ByDesign, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="07b3d-246">**To assign Britta Simon to SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="07b3d-247">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="07b3d-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="07b3d-249">Selecteer in de lijst met toepassingen **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="07b3d-249">In the applications list, select **SAP Business ByDesign**.</span></span>

    ![De koppeling SAP Business ByDesign in de lijst met toepassingen](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="07b3d-251">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="07b3d-251">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="07b3d-253">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="07b3d-253">Click **Add** button.</span></span> <span data-ttu-id="07b3d-254">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="07b3d-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="07b3d-256">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="07b3d-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="07b3d-257">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="07b3d-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="07b3d-258">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="07b3d-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="07b3d-259">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="07b3d-259">Test single sign-on</span></span>

<span data-ttu-id="07b3d-260">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="07b3d-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="07b3d-261">Als u op de tegel SAP Business ByDesign in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="07b3d-261">When you click the SAP Business ByDesign tile in the Access Panel, you should get automatically signed-on to your SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="07b3d-262">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="07b3d-262">Additional resources</span></span>

* [<span data-ttu-id="07b3d-263">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07b3d-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07b3d-264">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="07b3d-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

