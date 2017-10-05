---
title: 'Zelfstudie: Azure Active Directory-integratie met TINFOIL SECURITY | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en TINFOIL SECURITY.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 614e4de3335574f4b56c7d641af4fcfafdb17d12
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="b24f6-103">Zelfstudie: Azure Active Directory-integratie met TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="b24f6-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="b24f6-104">In deze zelfstudie leert u hoe TINFOIL SECURITY integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b24f6-104">In this tutorial, you learn how to integrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b24f6-105">TINFOIL SECURITY integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b24f6-105">Integrating TINFOIL SECURITY with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b24f6-106">U kunt beheren in Azure AD die toegang tot TINFOIL SECURITY heeft</span><span class="sxs-lookup"><span data-stu-id="b24f6-106">You can control in Azure AD who has access to TINFOIL SECURITY</span></span>
- <span data-ttu-id="b24f6-107">U kunt uw gebruikers automatisch ophalen aangemeld bij TINFOIL SECURITY (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="b24f6-107">You can enable your users to automatically get signed-on to TINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b24f6-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b24f6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b24f6-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b24f6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b24f6-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b24f6-110">Prerequisites</span></span>

<span data-ttu-id="b24f6-111">Voor het configureren van Azure AD-integratie met TINFOIL SECURITY, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b24f6-111">To configure Azure AD integration with TINFOIL SECURITY, you need the following items:</span></span>

- <span data-ttu-id="b24f6-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b24f6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b24f6-113">Een TINFOIL SECURITY eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b24f6-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b24f6-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b24f6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b24f6-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b24f6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b24f6-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b24f6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b24f6-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b24f6-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b24f6-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b24f6-118">Scenario description</span></span>
<span data-ttu-id="b24f6-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b24f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b24f6-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b24f6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b24f6-121">TINFOIL SECURITY uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b24f6-121">Add TINFOIL SECURITY from the gallery</span></span>
2. <span data-ttu-id="b24f6-122">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="b24f6-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-the-gallery"></a><span data-ttu-id="b24f6-123">TINFOIL SECURITY uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b24f6-123">Add TINFOIL SECURITY from the gallery</span></span>
<span data-ttu-id="b24f6-124">Voor het configureren van de integratie van TINFOIL SECURITY in Azure AD, moet u TINFOIL SECURITY uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b24f6-124">To configure the integration of TINFOIL SECURITY into Azure AD, you need to add TINFOIL SECURITY from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b24f6-125">**Als u wilt toevoegen TINFOIL SECURITY uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b24f6-125">**To add TINFOIL SECURITY from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b24f6-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b24f6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b24f6-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b24f6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b24f6-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b24f6-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="b24f6-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b24f6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="b24f6-133">Typ in het zoekvak **TINFOIL SECURITY**, selecteer **TINFOIL SECURITY** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b24f6-133">In the search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button to add the application.</span></span>

    ![TINFOIL SECURITY vanuit galerie](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b24f6-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="b24f6-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b24f6-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met TINFOIL SECURITY op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b24f6-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b24f6-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in TINFOIL SECURITY is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b24f6-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TINFOIL SECURITY is to a user in Azure AD.</span></span> <span data-ttu-id="b24f6-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante TINFOIL SECURITY-gebruiker worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b24f6-138">In other words, a link relationship between an Azure AD user and the related user in TINFOIL SECURITY needs to be established.</span></span>

<span data-ttu-id="b24f6-139">Wijs in TINFOIL SECURITY de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="b24f6-139">In TINFOIL SECURITY, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b24f6-140">Om te configureren en testen van Azure AD eenmalige aanmelding met TINFOIL SECURITY, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="b24f6-140">To configure and test Azure AD single sign-on with TINFOIL SECURITY, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b24f6-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b24f6-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b24f6-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b24f6-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b24f6-143">**[Maak een testgebruiker TINFOIL SECURITY](#create-a-tinfoil-security-test-user)**  - TINFOIL SECURITY die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="b24f6-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - to have a counterpart of Britta Simon in TINFOIL SECURITY that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b24f6-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b24f6-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b24f6-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b24f6-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b24f6-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b24f6-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b24f6-147">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="b24f6-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="b24f6-148">**Voor het configureren van Azure AD eenmalige aanmelding met TINFOIL SECURITY, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b24f6-148">**To configure Azure AD single sign-on with TINFOIL SECURITY, perform the following steps:**</span></span>

1. <span data-ttu-id="b24f6-149">In de Azure-portal op de **TINFOIL SECURITY** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b24f6-149">In the Azure portal, on the **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b24f6-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b24f6-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML op basis van eenmalige aanmelding](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. <span data-ttu-id="b24f6-153">Op de **TINFOIL SECURITY domein en de URL's** sectie, de gebruiker heeft geen alle stappen uitvoeren als de app al vooraf is geïntegreerd met Azure.</span><span class="sxs-lookup"><span data-stu-id="b24f6-153">On the **TINFOIL SECURITY Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. <span data-ttu-id="b24f6-155">Op de **SAML-certificaat voor ondertekening van** sectie, Kopieer de **VINGERAFDRUK** waarde.</span><span class="sxs-lookup"><span data-stu-id="b24f6-155">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value.</span></span>

    ![Certificaat voor ondertekening van SAML-sectie](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. <span data-ttu-id="b24f6-157">Als u wilt de vereiste kenmerktoewijzingen toevoegen, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b24f6-157">To add the required attribute mappings, perform the following steps:</span></span>
    
    <span data-ttu-id="b24f6-158">![Kenmerken](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="b24f6-158">![Attributes](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="b24f6-159">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="b24f6-159">Attribute Name</span></span>    |   <span data-ttu-id="b24f6-160">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="b24f6-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="b24f6-161">AccountId</span><span class="sxs-lookup"><span data-stu-id="b24f6-161">accountid</span></span> | <span data-ttu-id="b24f6-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="b24f6-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="b24f6-163">a.</span><span class="sxs-lookup"><span data-stu-id="b24f6-163">a.</span></span> <span data-ttu-id="b24f6-164">Klik op **gebruikerskenmerk toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b24f6-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="b24f6-165">![Kenmerk toevoegen](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="b24f6-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="b24f6-166">![Kenmerk toevoegen](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="b24f6-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="b24f6-167">b.</span><span class="sxs-lookup"><span data-stu-id="b24f6-167">b.</span></span> <span data-ttu-id="b24f6-168">In de **kenmerknaam** textbox type **accountid**.</span><span class="sxs-lookup"><span data-stu-id="b24f6-168">In the **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="b24f6-169">c.</span><span class="sxs-lookup"><span data-stu-id="b24f6-169">c.</span></span> <span data-ttu-id="b24f6-170">In de **kenmerkwaarde** textbox, plak de account-ID-waarde die u later in de zelfstudie krijgt.</span><span class="sxs-lookup"><span data-stu-id="b24f6-170">In the **Attribute Value** textbox, paste the account ID value which you will get later on the tutorial.</span></span>
    
    <span data-ttu-id="b24f6-171">d.</span><span class="sxs-lookup"><span data-stu-id="b24f6-171">d.</span></span> <span data-ttu-id="b24f6-172">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b24f6-172">Click **Ok**.</span></span>    

6. <span data-ttu-id="b24f6-173">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b24f6-173">Click **Save** button.</span></span>

    ![knop Opslaan](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="b24f6-175">Op de **TINFOIL SECURITY Configuration** sectie, klikt u op **TINFOIL SECURITY configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="b24f6-175">On the **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b24f6-176">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="b24f6-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![TINFOIL SECURITY Configuration](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. <span data-ttu-id="b24f6-178">In een ander browservenster, meld u bij uw bedrijf TINFOIL SECURITY site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b24f6-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

9. <span data-ttu-id="b24f6-179">Klik in de werkbalk bovenaan op **Mijn Account**.</span><span class="sxs-lookup"><span data-stu-id="b24f6-179">In the toolbar on the top, click **My Account**.</span></span>
   
    <span data-ttu-id="b24f6-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span><span class="sxs-lookup"><span data-stu-id="b24f6-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

10. <span data-ttu-id="b24f6-181">Klik op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="b24f6-181">Click **Security**.</span></span>
   
    <span data-ttu-id="b24f6-182">![Beveiliging](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "beveiliging")</span><span class="sxs-lookup"><span data-stu-id="b24f6-182">![Security](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Security")</span></span>

11. <span data-ttu-id="b24f6-183">Op de **Single Sign-On** configuratie pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b24f6-183">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="b24f6-184">![Eenmalige aanmelding](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="b24f6-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="b24f6-185">a.</span><span class="sxs-lookup"><span data-stu-id="b24f6-185">a.</span></span> <span data-ttu-id="b24f6-186">Selecteer **SAML inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="b24f6-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="b24f6-187">b.</span><span class="sxs-lookup"><span data-stu-id="b24f6-187">b.</span></span> <span data-ttu-id="b24f6-188">Klik op **handmatige configuratie**.</span><span class="sxs-lookup"><span data-stu-id="b24f6-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="b24f6-189">c.</span><span class="sxs-lookup"><span data-stu-id="b24f6-189">c.</span></span> <span data-ttu-id="b24f6-190">In **SAML Post URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal</span><span class="sxs-lookup"><span data-stu-id="b24f6-190">In **SAML Post URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="b24f6-191">d.</span><span class="sxs-lookup"><span data-stu-id="b24f6-191">d.</span></span> <span data-ttu-id="b24f6-192">In **SAML certificaat vingerafdruk** textbox, plak de waarde van **vingerafdruk** die u hebt gekopieerd uit **certificaat voor ondertekening van SAML** sectie.</span><span class="sxs-lookup"><span data-stu-id="b24f6-192">In **SAML Certificate Fingerprint** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="b24f6-193">e.</span><span class="sxs-lookup"><span data-stu-id="b24f6-193">e.</span></span> <span data-ttu-id="b24f6-194">Kopiëren **uw Account-ID** waarde en plak de waarde in **kenmerkwaarde** textbox onder **kenmerk toevoegen** sectie in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b24f6-194">Copy **Your Account ID** value and paste the value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="b24f6-195">f.</span><span class="sxs-lookup"><span data-stu-id="b24f6-195">f.</span></span> <span data-ttu-id="b24f6-196">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b24f6-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b24f6-197">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="b24f6-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b24f6-198">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="b24f6-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b24f6-199">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b24f6-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b24f6-200">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b24f6-200">Create an Azure AD test user</span></span>
<span data-ttu-id="b24f6-201">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b24f6-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="b24f6-203">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b24f6-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b24f6-204">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b24f6-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b24f6-206">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b24f6-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="b24f6-207">Gebruikers en groepen -> alle gebruikers</span><span class="sxs-lookup"><span data-stu-id="b24f6-207">Users and groups -> All users</span></span> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b24f6-208">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b24f6-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Gebruiker](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b24f6-210">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b24f6-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b24f6-212">a.</span><span class="sxs-lookup"><span data-stu-id="b24f6-212">a.</span></span> <span data-ttu-id="b24f6-213">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b24f6-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b24f6-214">b.</span><span class="sxs-lookup"><span data-stu-id="b24f6-214">b.</span></span> <span data-ttu-id="b24f6-215">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b24f6-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b24f6-216">c.</span><span class="sxs-lookup"><span data-stu-id="b24f6-216">c.</span></span> <span data-ttu-id="b24f6-217">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b24f6-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b24f6-218">d.</span><span class="sxs-lookup"><span data-stu-id="b24f6-218">d.</span></span> <span data-ttu-id="b24f6-219">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b24f6-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="b24f6-220">Een testgebruiker TINFOIL SECURITY maken</span><span class="sxs-lookup"><span data-stu-id="b24f6-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="b24f6-221">Om in te schakelen gebruikers van Azure AD aan te melden bij TINFOIL SECURITY, moeten ze worden ingericht in TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="b24f6-221">In order to enable Azure AD users to log into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="b24f6-222">In het geval van TINFOIL SECURITY is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="b24f6-222">In the case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="b24f6-223">**Als u een gebruiker die zijn ingericht, kunt u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b24f6-223">**To get a user provisioned, perform the following steps:**</span></span>

1. <span data-ttu-id="b24f6-224">Als de gebruiker deel van een Enterprise-account uitmaakt, moet u [Neem contact op met het ondersteuningsteam TINFOIL SECURITY](https://www.tinfoilsecurity.com/contact) ophalen van het gebruikersaccount dat is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b24f6-224">If the user is a part of an Enterprise account, you need to [contact the TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) to get the user account created.</span></span>

2. <span data-ttu-id="b24f6-225">Als de gebruiker een gewone TINFOIL SECURITY SaaS-gebruiker is, kunnen de gebruiker kan een samenwerker toevoegen aan een van de sites van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b24f6-225">If the user is a regular TINFOIL SECURITY SaaS user, then the user can add a collaborator to any of the user’s sites.</span></span> <span data-ttu-id="b24f6-226">Dit activeert een proces voor het verzenden van een uitnodiging voor het opgegeven e-mailbericht voor het maken van een nieuw TINFOIL SECURITY-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="b24f6-226">This triggers a process to send an invitation to the specified email to create a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="b24f6-227">U kunt geen andere hulpprogramma's van TINFOIL SECURITY gebruiker-account maken of API's die worden geleverd door TINFOIL SECURITY voor het inrichten van Azure AD-gebruikersaccounts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b24f6-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY to provision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b24f6-228">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="b24f6-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="b24f6-229">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="b24f6-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TINFOIL SECURITY.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b24f6-231">**Britta Simon om aan te wijzen TINFOIL SECURITY, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b24f6-231">**To assign Britta Simon to TINFOIL SECURITY, perform the following steps:**</span></span>

1. <span data-ttu-id="b24f6-232">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b24f6-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b24f6-234">Selecteer in de lijst met toepassingen **TINFOIL SECURITY**.</span><span class="sxs-lookup"><span data-stu-id="b24f6-234">In the applications list, select **TINFOIL SECURITY**.</span></span>

    ![TINFOIL SECURITY selecteren](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. <span data-ttu-id="b24f6-236">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b24f6-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="b24f6-238">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b24f6-238">Click **Add** button.</span></span> <span data-ttu-id="b24f6-239">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b24f6-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="b24f6-241">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b24f6-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b24f6-242">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b24f6-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b24f6-243">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b24f6-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b24f6-244">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b24f6-244">Test single sign-on</span></span>

<span data-ttu-id="b24f6-245">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b24f6-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b24f6-246">Als u op de tegel TINFOIL SECURITY in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="b24f6-246">When you click the TINFOIL SECURITY tile in the Access Panel, you should get automatically signed-on to your TINFOIL SECURITY application.</span></span> <span data-ttu-id="b24f6-247">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b24f6-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b24f6-248">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b24f6-248">Additional resources</span></span>

* [<span data-ttu-id="b24f6-249">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b24f6-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b24f6-250">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b24f6-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

