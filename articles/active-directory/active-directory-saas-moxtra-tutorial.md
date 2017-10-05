---
title: 'Zelfstudie: Azure Active Directory-integratie met Moxtra | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Moxtra.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: db2f041a44b6771b0a4f734e58d899298ef0847b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="ca2b5-103">Zelfstudie: Azure Active Directory-integratie met Moxtra</span><span class="sxs-lookup"><span data-stu-id="ca2b5-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="ca2b5-104">In deze zelfstudie leert u hoe Moxtra integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ca2b5-104">In this tutorial, you learn how to integrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ca2b5-105">Moxtra integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ca2b5-105">Integrating Moxtra with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ca2b5-106">U kunt beheren in Azure AD die toegang tot Moxtra heeft</span><span class="sxs-lookup"><span data-stu-id="ca2b5-106">You can control in Azure AD who has access to Moxtra</span></span>
- <span data-ttu-id="ca2b5-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Moxtra (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="ca2b5-107">You can enable your users to automatically get signed-on to Moxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ca2b5-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ca2b5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ca2b5-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ca2b5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca2b5-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ca2b5-110">Prerequisites</span></span>

<span data-ttu-id="ca2b5-111">Voor het configureren van Azure AD-integratie met Moxtra, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="ca2b5-111">To configure Azure AD integration with Moxtra, you need the following items:</span></span>

- <span data-ttu-id="ca2b5-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ca2b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ca2b5-113">Een Moxtra eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ca2b5-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ca2b5-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ca2b5-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ca2b5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ca2b5-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ca2b5-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ca2b5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ca2b5-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ca2b5-118">Scenario description</span></span>
<span data-ttu-id="ca2b5-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ca2b5-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ca2b5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ca2b5-121">Moxtra uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ca2b5-121">Adding Moxtra from the gallery</span></span>
2. <span data-ttu-id="ca2b5-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ca2b5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-the-gallery"></a><span data-ttu-id="ca2b5-123">Moxtra uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ca2b5-123">Adding Moxtra from the gallery</span></span>
<span data-ttu-id="ca2b5-124">Voor het configureren van de integratie van Moxtra in Azure AD, moet u Moxtra uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-124">To configure the integration of Moxtra into Azure AD, you need to add Moxtra from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ca2b5-125">**Als u wilt toevoegen Moxtra uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ca2b5-125">**To add Moxtra from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ca2b5-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ca2b5-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ca2b5-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ca2b5-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ca2b5-133">Typ in het zoekvak **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-133">In the search box, type **Moxtra**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="ca2b5-135">Selecteer in het deelvenster resultaten **Moxtra**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-135">In the results panel, select **Moxtra**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ca2b5-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ca2b5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ca2b5-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Moxtra op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ca2b5-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Moxtra is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Moxtra is to a user in Azure AD.</span></span> <span data-ttu-id="ca2b5-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Moxtra tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-140">In other words, a link relationship between an Azure AD user and the related user in Moxtra needs to be established.</span></span>

<span data-ttu-id="ca2b5-141">Wijs in Moxtra, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-141">In Moxtra, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ca2b5-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Moxtra, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="ca2b5-142">To configure and test Azure AD single sign-on with Moxtra, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ca2b5-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ca2b5-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ca2b5-145">**[Maken van een testgebruiker Moxtra](#creating-a-moxtra-test-user)**  - Moxtra die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - to have a counterpart of Britta Simon in Moxtra that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ca2b5-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ca2b5-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ca2b5-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ca2b5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ca2b5-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Moxtra configureren.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="ca2b5-150">**Voor het configureren van Azure AD eenmalige aanmelding met Moxtra, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ca2b5-150">**To configure Azure AD single sign-on with Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="ca2b5-151">In de Azure-portal op de **Moxtra** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-151">In the Azure portal, on the **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ca2b5-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="ca2b5-155">Op de **Moxtra domein en de URL's** sectie, voert u de volgende stap:</span><span class="sxs-lookup"><span data-stu-id="ca2b5-155">On the **Moxtra Domain and URLs** section, perform the following step:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="ca2b5-157">In de **aanmeldings-URL** textbox, typ een URL als:`https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="ca2b5-157">In the **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="ca2b5-158">De SAML-asserties verwacht Moxtra toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-158">Moxtra application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="ca2b5-159">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-159">Configure the following claims for this application.</span></span> <span data-ttu-id="ca2b5-160">U kunt beheren de waarden van deze kenmerken van de '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-160">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ca2b5-161">De volgende Schermafbeelding toont een voorbeeld voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-161">The following screenshot shows an example for this configuration.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="ca2b5-163">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding en de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ca2b5-163">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="ca2b5-164">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="ca2b5-164">Attribute Name</span></span> | <span data-ttu-id="ca2b5-165">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="ca2b5-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="ca2b5-166">Voornaam</span><span class="sxs-lookup"><span data-stu-id="ca2b5-166">firstname</span></span> | <span data-ttu-id="ca2b5-167">User.givenName</span><span class="sxs-lookup"><span data-stu-id="ca2b5-167">user.givenname</span></span> |
    | <span data-ttu-id="ca2b5-168">Achternaam</span><span class="sxs-lookup"><span data-stu-id="ca2b5-168">lastname</span></span> | <span data-ttu-id="ca2b5-169">User.surname</span><span class="sxs-lookup"><span data-stu-id="ca2b5-169">user.surname</span></span> |
    | <span data-ttu-id="ca2b5-170">idpid</span><span class="sxs-lookup"><span data-stu-id="ca2b5-170">idpid</span></span>    | <span data-ttu-id="ca2b5-171">< SAML entiteit-ID ></span><span class="sxs-lookup"><span data-stu-id="ca2b5-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="ca2b5-172">De waarde van **idpid** -kenmerk is niet echt.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-172">The value of **idpid** attribute is not real.</span></span> <span data-ttu-id="ca2b5-173">U krijgt de werkelijke waarde van **Naslaggids** onder sectie **Moxtra configuratie**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-173">You can get the actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="ca2b5-174">a.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-174">a.</span></span> <span data-ttu-id="ca2b5-175">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="ca2b5-177">b.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-177">b.</span></span> <span data-ttu-id="ca2b5-178">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ca2b5-180">c.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-180">c.</span></span> <span data-ttu-id="ca2b5-181">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="ca2b5-182">d.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-182">d.</span></span> <span data-ttu-id="ca2b5-183">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="ca2b5-184">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-184">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="ca2b5-186">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-186">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="ca2b5-188">Op de **Moxtra configuratie** sectie, klikt u op **configureren Moxtra** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-188">On the **Moxtra Configuration** section, click **Configure Moxtra** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ca2b5-189">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="ca2b5-189">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="ca2b5-191">In een ander browservenster zich aanmelden bij uw bedrijf Moxtra site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-191">In another browser window, sign on to your Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="ca2b5-192">Klik in de werkbalk aan de linkerkant op **-beheerconsole > SAML Single Sign-on**, en klik vervolgens op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-192">In the toolbar on the left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="ca2b5-194">Op de **SAML** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ca2b5-194">On the **SAML** page, perform the following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="ca2b5-196">a.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-196">a.</span></span> <span data-ttu-id="ca2b5-197">In de **naam** textbox, typ een naam voor uw configuratie (bijvoorbeeld: *SAML*).</span><span class="sxs-lookup"><span data-stu-id="ca2b5-197">In the **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="ca2b5-198">b.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-198">b.</span></span> <span data-ttu-id="ca2b5-199">In de **IdP entiteit-ID** textbox, plak de waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-199">In the **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="ca2b5-200">c.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-200">c.</span></span> <span data-ttu-id="ca2b5-201">In **aanmeldings-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-201">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="ca2b5-202">d.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-202">d.</span></span> <span data-ttu-id="ca2b5-203">In de **AuthnContextClassRef** textbox type **urn: oasis: namen: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-203">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="ca2b5-204">e.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-204">e.</span></span> <span data-ttu-id="ca2b5-205">In de **NameID indeling** textbox type **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-205">In the **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="ca2b5-206">f.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-206">f.</span></span> <span data-ttu-id="ca2b5-207">Open certificaat dat u hebt gedownload vanuit Azure-portal in Kladblok, Kopieer de inhoud en plakt u deze in de **certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-207">Open certificate which you have downloaded from Azure portal in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="ca2b5-208">g.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-208">g.</span></span> <span data-ttu-id="ca2b5-209">In het tekstvak voor SAML e-domein, typ uw e-maildomein SAML.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-209">In the SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="ca2b5-210">Als u wilt zien welke stappen om te controleren of het domein, klikt u op de '**ik**' hieronder.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-210">To see the steps to verify the domain, click the "**i**" below.</span></span>

    <span data-ttu-id="ca2b5-211">h.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-211">h.</span></span> <span data-ttu-id="ca2b5-212">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="ca2b5-213">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="ca2b5-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ca2b5-214">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ca2b5-215">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ca2b5-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ca2b5-216">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ca2b5-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="ca2b5-217">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ca2b5-219">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ca2b5-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ca2b5-220">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ca2b5-222">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ca2b5-224">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ca2b5-226">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ca2b5-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ca2b5-228">a.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-228">a.</span></span> <span data-ttu-id="ca2b5-229">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ca2b5-230">b.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-230">b.</span></span> <span data-ttu-id="ca2b5-231">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ca2b5-232">c.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-232">c.</span></span> <span data-ttu-id="ca2b5-233">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ca2b5-234">d.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-234">d.</span></span> <span data-ttu-id="ca2b5-235">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="ca2b5-236">Een testgebruiker Moxtra maken</span><span class="sxs-lookup"><span data-stu-id="ca2b5-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="ca2b5-237">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Moxtra genoemd.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-237">The objective of this section is to create a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="ca2b5-238">**Als u wilt een gebruiker Britta Simon aangeroepen in Moxtra maakt, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ca2b5-238">**To create a user called Britta Simon in Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="ca2b5-239">Meld u op met uw bedrijf Moxtra site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-239">Sign on to your Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="ca2b5-240">Klik in de werkbalk aan de linkerkant op **-beheerconsole > Gebruikersbeheer**, en vervolgens **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-240">In the toolbar on the left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="ca2b5-242">Op de **gebruiker toevoegen** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ca2b5-242">On the **Add User** dialog, perform the following steps:</span></span>
  
    <span data-ttu-id="ca2b5-243">a.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-243">a.</span></span> <span data-ttu-id="ca2b5-244">In de **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-244">In the **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="ca2b5-245">b.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-245">b.</span></span> <span data-ttu-id="ca2b5-246">In de **achternaam** textbox type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-246">In the **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="ca2b5-247">c.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-247">c.</span></span> <span data-ttu-id="ca2b5-248">In de **e** textbox type Britta van e-mailadres dezelfde als voor de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-248">In the **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="ca2b5-249">d.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-249">d.</span></span> <span data-ttu-id="ca2b5-250">In de **deling** textbox type **Dev**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-250">In the **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="ca2b5-251">e.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-251">e.</span></span> <span data-ttu-id="ca2b5-252">In de **afdeling** textbox type **IT**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-252">In the **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="ca2b5-253">f.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-253">f.</span></span> <span data-ttu-id="ca2b5-254">Selecteer **beheerder**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="ca2b5-255">g.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-255">g.</span></span> <span data-ttu-id="ca2b5-256">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ca2b5-257">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca2b5-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ca2b5-258">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Moxtra.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Moxtra.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ca2b5-260">**Britta Simon om aan te wijzen Moxtra, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ca2b5-260">**To assign Britta Simon to Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="ca2b5-261">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ca2b5-263">Selecteer in de lijst met toepassingen **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-263">In the applications list, select **Moxtra**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="ca2b5-265">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ca2b5-267">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-267">Click **Add** button.</span></span> <span data-ttu-id="ca2b5-268">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ca2b5-270">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ca2b5-271">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ca2b5-272">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ca2b5-273">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ca2b5-273">Testing single sign-on</span></span>

<span data-ttu-id="ca2b5-274">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ca2b5-275">Als u op de tegel Moxtra in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Moxtra.</span><span class="sxs-lookup"><span data-stu-id="ca2b5-275">When you click the Moxtra tile in the Access Panel, you should get automatically signed-on to your Moxtra application.</span></span>
<span data-ttu-id="ca2b5-276">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ca2b5-276">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ca2b5-277">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ca2b5-277">Additional resources</span></span>

* [<span data-ttu-id="ca2b5-278">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ca2b5-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ca2b5-279">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ca2b5-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

