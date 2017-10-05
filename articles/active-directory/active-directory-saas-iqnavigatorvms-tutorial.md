---
title: 'Zelfstudie: Azure Active Directory-integratie met IQNavigator VMS | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en IQNavigator VMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a8a09b25-dfa5-4c31-aea2-53bf1853b365
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 1164723a171843541098f6adbda0e65f7e82a0cb
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-iqnavigator-vms"></a><span data-ttu-id="ef224-103">Zelfstudie: Azure Active Directory-integratie met IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="ef224-103">Tutorial: Azure Active Directory integration with IQNavigator VMS</span></span>

<span data-ttu-id="ef224-104">In deze zelfstudie leert u hoe IQNavigator VMS integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ef224-104">In this tutorial, you learn how to integrate IQNavigator VMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ef224-105">IQNavigator VMS integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ef224-105">Integrating IQNavigator VMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ef224-106">U kunt beheren in Azure AD die toegang tot IQNavigator VMS heeft</span><span class="sxs-lookup"><span data-stu-id="ef224-106">You can control in Azure AD who has access to IQNavigator VMS</span></span>
- <span data-ttu-id="ef224-107">U kunt uw gebruikers automatisch ophalen aangemeld bij IQNavigator VMS (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="ef224-107">You can enable your users to automatically get signed-on to IQNavigator VMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ef224-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ef224-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ef224-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ef224-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef224-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ef224-110">Prerequisites</span></span>

<span data-ttu-id="ef224-111">Voor het configureren van Azure AD-integratie met IQNavigator VMS, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="ef224-111">To configure Azure AD integration with IQNavigator VMS, you need the following items:</span></span>

- <span data-ttu-id="ef224-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ef224-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ef224-113">Een IQNavigator VMS eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ef224-113">A IQNavigator VMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ef224-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ef224-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ef224-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ef224-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ef224-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ef224-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ef224-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u hier een proefversie van één maand krijgen [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ef224-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ef224-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ef224-118">Scenario description</span></span>
<span data-ttu-id="ef224-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ef224-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ef224-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ef224-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ef224-121">IQNavigator VMS uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ef224-121">Adding IQNavigator VMS from the gallery</span></span>
2. <span data-ttu-id="ef224-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ef224-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-iqnavigator-vms-from-the-gallery"></a><span data-ttu-id="ef224-123">IQNavigator VMS uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ef224-123">Adding IQNavigator VMS from the gallery</span></span>
<span data-ttu-id="ef224-124">Voor het configureren van de integratie van IQNavigator VMS in Azure AD, moet u IQNavigator VMS uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ef224-124">To configure the integration of IQNavigator VMS into Azure AD, you need to add IQNavigator VMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ef224-125">**Als u wilt toevoegen IQNavigator VMS uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ef224-125">**To add IQNavigator VMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ef224-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ef224-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ef224-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ef224-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ef224-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ef224-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ef224-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ef224-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ef224-133">Typ in het zoekvak **IQNavigator VMS**.</span><span class="sxs-lookup"><span data-stu-id="ef224-133">In the search box, type **IQNavigator VMS**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_search.png)

5. <span data-ttu-id="ef224-135">Selecteer in het deelvenster resultaten **IQNavigator VMS**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="ef224-135">In the results panel, select **IQNavigator VMS**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ef224-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ef224-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ef224-138">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD IQNavigator VMS op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="ef224-138">In this section, you configure and test Azure AD single sign-on with IQNavigator VMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ef224-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in IQNavigator VMS is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef224-139">For single sign-on to work, Azure AD needs to know what the counterpart user in IQNavigator VMS is to a user in Azure AD.</span></span> <span data-ttu-id="ef224-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in IQNavigator VMS tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="ef224-140">In other words, a link relationship between an Azure AD user and the related user in IQNavigator VMS needs to be established.</span></span>

<span data-ttu-id="ef224-141">Wijs in IQNavigator VMS, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="ef224-141">In IQNavigator VMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ef224-142">Om te configureren en testen van Azure AD eenmalige aanmelding met IQNavigator VMS, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="ef224-142">To configure and test Azure AD single sign-on with IQNavigator VMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ef224-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ef224-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ef224-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ef224-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ef224-145">**[Maken van een testgebruiker IQNavigator VMS](#creating-a-iqnavigator-vms-test-user)**  - IQNavigator VMS die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="ef224-145">**[Creating a IQNavigator VMS test user](#creating-a-iqnavigator-vms-test-user)** - to have a counterpart of Britta Simon in IQNavigator VMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ef224-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ef224-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ef224-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ef224-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ef224-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ef224-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ef224-149">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="ef224-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IQNavigator VMS application.</span></span>

<span data-ttu-id="ef224-150">**Voor het configureren van Azure AD eenmalige aanmelding met IQNavigator VMS, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ef224-150">**To configure Azure AD single sign-on with IQNavigator VMS, perform the following steps:**</span></span>

1. <span data-ttu-id="ef224-151">In de Azure-portal op de **IQNavigator VMS** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ef224-151">In the Azure portal, on the **IQNavigator VMS** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ef224-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ef224-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_samlbase.png)

3. <span data-ttu-id="ef224-155">Op de **IQNavigator VMS domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ef224-155">On the **IQNavigator VMS Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url.png)

    <span data-ttu-id="ef224-157">a.</span><span class="sxs-lookup"><span data-stu-id="ef224-157">a.</span></span> <span data-ttu-id="ef224-158">In de **id** textbox, typ de URL:`iqn.com`</span><span class="sxs-lookup"><span data-stu-id="ef224-158">In the **Identifier** textbox, type the URL:`iqn.com`</span></span>

    <span data-ttu-id="ef224-159">b.</span><span class="sxs-lookup"><span data-stu-id="ef224-159">b.</span></span> <span data-ttu-id="ef224-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="ef224-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span></span>

4. <span data-ttu-id="ef224-161">Controleer **weergeven geavanceerde instellingen voor URL**, voer de volgende stap:</span><span class="sxs-lookup"><span data-stu-id="ef224-161">Check **Show advanced URL settings**, perform the following step:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url1.png)

    <span data-ttu-id="ef224-163">In de **Relay-status** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.iqnavigator.com`</span><span class="sxs-lookup"><span data-stu-id="ef224-163">In the **Relay state** textbox, type a URL using the following pattern:`https://<subdomain>.iqnavigator.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ef224-164">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="ef224-164">These values are not real.</span></span> <span data-ttu-id="ef224-165">Deze waarden bijwerken met de huidige status van de antwoord-URL en de Relay.</span><span class="sxs-lookup"><span data-stu-id="ef224-165">Update these values with the actual Reply URL and Relay state.</span></span> <span data-ttu-id="ef224-166">Neem contact op met [IQNavigator VMS Client ondersteuningsteam](https://www.beeline.com/iqn-product-support/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="ef224-166">Contact [IQNavigator VMS Client support team](https://www.beeline.com/iqn-product-support/) to get these values.</span></span> 

5. <span data-ttu-id="ef224-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ef224-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ef224-169">Voor het genereren van de **metagegevens** -url, de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ef224-169">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="ef224-170">a.</span><span class="sxs-lookup"><span data-stu-id="ef224-170">a.</span></span> <span data-ttu-id="ef224-171">Klik op **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="ef224-171">Click **App registrations**.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appregistrations.png)
   
    <span data-ttu-id="ef224-173">b.</span><span class="sxs-lookup"><span data-stu-id="ef224-173">b.</span></span> <span data-ttu-id="ef224-174">Klik op **eindpunten** openen **eindpunten** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ef224-174">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpointicon.png)

    <span data-ttu-id="ef224-176">c.</span><span class="sxs-lookup"><span data-stu-id="ef224-176">c.</span></span> <span data-ttu-id="ef224-177">Klik op de knop kopiëren om te kopiëren **DOCUMENT met federatieve metagegevens** url en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="ef224-177">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpoint.png)
     
    <span data-ttu-id="ef224-179">d.</span><span class="sxs-lookup"><span data-stu-id="ef224-179">d.</span></span> <span data-ttu-id="ef224-180">Nu gaat u naar de eigenschappenpagina van **IQNavigator VMS** en kopieer de **toepassings-Id** met **kopie** knop en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="ef224-180">Now go to the property page of **IQNavigator VMS** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appid.png)

    <span data-ttu-id="ef224-182">e.</span><span class="sxs-lookup"><span data-stu-id="ef224-182">e.</span></span> <span data-ttu-id="ef224-183">Genereren van de **metagegevens-URL** met het volgende patroon volgen:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="ef224-183">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="ef224-184">IQNavigator toepassing verwachten dat de waarde van de unieke gebruikers-id in de claim-naam-id.</span><span class="sxs-lookup"><span data-stu-id="ef224-184">IQNavigator application expect the unique user identifier value in the Name Identifier claim.</span></span> <span data-ttu-id="ef224-185">Klanten kan de juiste waarde voor de claim-naam-id toewijzen.</span><span class="sxs-lookup"><span data-stu-id="ef224-185">Customer can map the correct value for the Name Identifier claim.</span></span> <span data-ttu-id="ef224-186">In dit geval hebben we de gebruiker toegewezen. UserPrincipalName voor de demo-doel.</span><span class="sxs-lookup"><span data-stu-id="ef224-186">In this case we have mapped the user.UserPrincipalName for the demo purpose.</span></span> <span data-ttu-id="ef224-187">Maar volgens de instellingen van uw organisatie moet u de juiste waarde voor het toewijzen.</span><span class="sxs-lookup"><span data-stu-id="ef224-187">But according to your organization settings you should map the correct value for it.</span></span>   

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_attribute.png)

8. <span data-ttu-id="ef224-189">Op de **IQNavigator VMS configuratie** sectie, klikt u op **IQNavigator virtuele machines configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="ef224-189">On the **IQNavigator VMS Configuration** section, click **Configure IQNavigator VMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ef224-190">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="ef224-190">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_configure.png) 

9. <span data-ttu-id="ef224-192">Eenmalige aanmelding configureren op **IQNavigator VMS** kant die u wilt verzenden de **metagegevens-URL**, **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** naar [IQNavigator VMS ondersteuningsteam](https://www.beeline.com/iqn-product-support/).</span><span class="sxs-lookup"><span data-stu-id="ef224-192">To configure single sign-on on **IQNavigator VMS** side, you need to send the **Metadata URL**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/).</span></span> <span data-ttu-id="ef224-193">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ef224-193">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ef224-194">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="ef224-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ef224-195">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="ef224-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ef224-196">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ef224-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ef224-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ef224-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="ef224-198">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ef224-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ef224-200">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ef224-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ef224-201">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ef224-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ef224-203">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ef224-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ef224-205">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ef224-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ef224-207">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ef224-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ef224-209">a.</span><span class="sxs-lookup"><span data-stu-id="ef224-209">a.</span></span> <span data-ttu-id="ef224-210">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ef224-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ef224-211">b.</span><span class="sxs-lookup"><span data-stu-id="ef224-211">b.</span></span> <span data-ttu-id="ef224-212">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ef224-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ef224-213">c.</span><span class="sxs-lookup"><span data-stu-id="ef224-213">c.</span></span> <span data-ttu-id="ef224-214">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ef224-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ef224-215">d.</span><span class="sxs-lookup"><span data-stu-id="ef224-215">d.</span></span> <span data-ttu-id="ef224-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ef224-216">Click **Create**.</span></span>
 
### <a name="creating-a-iqnavigator-vms-test-user"></a><span data-ttu-id="ef224-217">Een testgebruiker IQNavigator VMS maken</span><span class="sxs-lookup"><span data-stu-id="ef224-217">Creating a IQNavigator VMS test user</span></span>

<span data-ttu-id="ef224-218">Het doel van deze sectie is het maken van een gebruiker Britta Simon in IQNavigator VMS genoemd.</span><span class="sxs-lookup"><span data-stu-id="ef224-218">The objective of this section is to create a user called Britta Simon in IQNavigator VMS.</span></span> <span data-ttu-id="ef224-219">Werken met [IQNavigator VMS ondersteuningsteam](https://www.beeline.com/iqn-product-support/) de gebruikers in het IQNavigator VMS-account toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ef224-219">Work with  [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/) to add the users in the IQNavigator VMS account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ef224-220">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef224-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ef224-221">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="ef224-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IQNavigator VMS.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ef224-223">**Britta Simon om aan te wijzen IQNavigator VMS, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ef224-223">**To assign Britta Simon to IQNavigator VMS, perform the following steps:**</span></span>

1. <span data-ttu-id="ef224-224">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ef224-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ef224-226">Selecteer in de lijst met toepassingen **IQNavigator VMS**.</span><span class="sxs-lookup"><span data-stu-id="ef224-226">In the applications list, select **IQNavigator VMS**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_app.png) 

3. <span data-ttu-id="ef224-228">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ef224-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ef224-230">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ef224-230">Click **Add** button.</span></span> <span data-ttu-id="ef224-231">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ef224-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ef224-233">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="ef224-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ef224-234">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ef224-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ef224-235">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ef224-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ef224-236">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ef224-236">Testing single sign-on</span></span>

<span data-ttu-id="ef224-237">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ef224-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ef224-238">Als u op de tegel IQNavigator VMS in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="ef224-238">When you click the IQNavigator VMS tile in the Access Panel, you should get automatically signed-on to your IQNavigator VMS application.</span></span>
<span data-ttu-id="ef224-239">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ef224-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ef224-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ef224-240">Additional resources</span></span>

* [<span data-ttu-id="ef224-241">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ef224-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ef224-242">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ef224-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_203.png

