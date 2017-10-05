---
title: 'Zelfstudie: Azure Active Directory-integratie met Zendesk | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Zendesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 51c06d838c5ed6286dfb99ea25faaaf33bad5f3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="fc4c7-103">Zelfstudie: Azure Active Directory-integratie met Zendesk</span><span class="sxs-lookup"><span data-stu-id="fc4c7-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="fc4c7-104">In deze zelfstudie leert u hoe Zendesk integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fc4c7-104">In this tutorial, you learn how to integrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fc4c7-105">Zendesk integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="fc4c7-105">Integrating Zendesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fc4c7-106">U kunt beheren in Azure AD die toegang tot Zendesk heeft</span><span class="sxs-lookup"><span data-stu-id="fc4c7-106">You can control in Azure AD who has access to Zendesk</span></span>
- <span data-ttu-id="fc4c7-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Zendesk (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="fc4c7-107">You can enable your users to automatically get signed-on to Zendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fc4c7-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="fc4c7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fc4c7-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fc4c7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc4c7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fc4c7-110">Prerequisites</span></span>

<span data-ttu-id="fc4c7-111">Voor het configureren van Azure AD-integratie met Zendesk, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="fc4c7-111">To configure Azure AD integration with Zendesk, you need the following items:</span></span>

- <span data-ttu-id="fc4c7-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="fc4c7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fc4c7-113">Een Zendesk eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="fc4c7-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="fc4c7-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="fc4c7-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="fc4c7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fc4c7-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fc4c7-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fc4c7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="fc4c7-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="fc4c7-118">Scenario description</span></span>
<span data-ttu-id="fc4c7-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fc4c7-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="fc4c7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fc4c7-121">Zendesk uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="fc4c7-121">Adding Zendesk from the gallery</span></span>
2. <span data-ttu-id="fc4c7-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fc4c7-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-the-gallery"></a><span data-ttu-id="fc4c7-123">Zendesk uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="fc4c7-123">Adding Zendesk from the gallery</span></span>
<span data-ttu-id="fc4c7-124">Voor het configureren van de integratie van Zendesk in Azure AD, moet u Zendesk uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-124">To configure the integration of Zendesk into Azure AD, you need to add Zendesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fc4c7-125">**Als u wilt toevoegen Zendesk uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fc4c7-125">**To add Zendesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fc4c7-126">In de  **[Azure Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fc4c7-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fc4c7-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="fc4c7-131">Klik op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-131">Click **New application** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="fc4c7-133">Typ in het zoekvak **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-133">In the search box, type **Zendesk**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="fc4c7-135">Selecteer in het deelvenster resultaten **Zendesk**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-135">In the results panel, select **Zendesk**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fc4c7-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fc4c7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fc4c7-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Zendesk op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fc4c7-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in de Zendesk is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zendesk is to a user in Azure AD.</span></span> <span data-ttu-id="fc4c7-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de Zendesk tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-140">In other words, a link relationship between an Azure AD user and the related user in Zendesk needs to be established.</span></span>

<span data-ttu-id="fc4c7-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Zendesk.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zendesk.</span></span>

<span data-ttu-id="fc4c7-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Zendesk, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="fc4c7-142">To configure and test Azure AD single sign-on with Zendesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fc4c7-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fc4c7-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fc4c7-145">**[Maken van een testgebruiker Zendesk](#creating-a-zendesk-test-user)**  - Zendesk die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - to have a counterpart of Britta Simon in Zendesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fc4c7-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fc4c7-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fc4c7-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="fc4c7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fc4c7-149">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw Zendesk-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="fc4c7-150">**Voor het configureren van Azure AD eenmalige aanmelding met Zendesk, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fc4c7-150">**To configure Azure AD single sign-on with Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="fc4c7-151">In de Azure-portal op de **Zendesk** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-151">In the Azure portal, on the **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="fc4c7-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="fc4c7-155">Op de **Zendesk-domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="fc4c7-155">On the **Zendesk Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="fc4c7-157">a.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-157">a.</span></span> <span data-ttu-id="fc4c7-158">In de **aanmeldings-URL** textbox, typ de waarde met het volgende patroon volgen:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="fc4c7-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="fc4c7-159">b.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-159">b.</span></span> <span data-ttu-id="fc4c7-160">In de **id** textbox, typ de waarde met het volgende patroon volgen:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="fc4c7-160">In the **Identifier** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fc4c7-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-161">These values are not real.</span></span> <span data-ttu-id="fc4c7-162">Deze waarden bijwerken met de werkelijke aanmeldings-URL en identificatie-URL.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-162">Update these values with the actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="fc4c7-163">Neem contact op met [Zendesk-ondersteuningsteam](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) to get these values.</span></span> 

4. <span data-ttu-id="fc4c7-164">De SAML-asserties verwacht Zendesk in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-164">Zendesk expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="fc4c7-165">Er zijn geen verplichte SAML-kenmerken, maar u kunt desgewenst een kenmerk uit toevoegen **gebruikerskenmerken** sectie volgens de onderstaande stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fc4c7-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following the below steps:</span></span> 

     ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="fc4c7-167">a.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-167">a.</span></span> <span data-ttu-id="fc4c7-168">Klik op de **weergeven en bewerken van de kenmerken** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-168">Click the **View and edit all the other attributes** check box.</span></span>
     
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="fc4c7-170">b.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-170">b.</span></span> <span data-ttu-id="fc4c7-171">Klik op de **kenmerk toevoegen** openen **toevoegen kenmerk** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-171">Click the **Add Attribute** to open **Add attribute** dialog.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="fc4c7-173">c.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-173">c.</span></span> <span data-ttu-id="fc4c7-174">In de **naam** textbox, typ de naam van het kenmerk (bijvoorbeeld **emailaddress**).</span><span class="sxs-lookup"><span data-stu-id="fc4c7-174">In the **Name** textbox, type the attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="fc4c7-175">d.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-175">d.</span></span> <span data-ttu-id="fc4c7-176">Van de **waarde** , selecteert u de waarde van het kenmerk (als **user.mail**).</span><span class="sxs-lookup"><span data-stu-id="fc4c7-176">From the **Value** list, select the attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="fc4c7-177">e.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-177">e.</span></span> <span data-ttu-id="fc4c7-178">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="fc4c7-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="fc4c7-179">Uitbreidingskenmerken kunt u kenmerken die zich niet in Azure AD standaard toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-179">You use extension attributes to add attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="fc4c7-180">Klik op [gebruikerskenmerken die kunnen worden ingesteld in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) ophalen van de volledige lijst met kenmerken die met SAML **Zendesk** accepteert.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) to get the complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="fc4c7-181">Op de **SAML-certificaat voor ondertekening van** sectie, Kopieer de **VINGERAFDRUK** waarde van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-181">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="fc4c7-183">Op de **Zendesk configuratie** sectie, klikt u op **configureren Zendesk** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-183">On the **Zendesk Configuration** section, click **Configure Zendesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fc4c7-184">Kopieer de **Sign-Out URL's en SAML Single Sign-On Service** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="fc4c7-184">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="fc4c7-186">In een ander browservenster, meld u bij uw bedrijf Zendesk site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="fc4c7-187">Klik op **Admin**.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-187">Click **Admin**.</span></span>

9. <span data-ttu-id="fc4c7-188">Klik in het navigatiedeelvenster links op **instellingen**, en klik vervolgens op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-188">In the left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="fc4c7-189">Op de **beveiliging** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="fc4c7-189">On the **Security** page, perform the following steps:</span></span> 
   
     <span data-ttu-id="fc4c7-190">![Beveiliging](./media/active-directory-saas-zendesk-tutorial/ic773089.png "beveiliging")</span><span class="sxs-lookup"><span data-stu-id="fc4c7-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="fc4c7-191">![Eenmalige aanmelding](./media/active-directory-saas-zendesk-tutorial/ic773090.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="fc4c7-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="fc4c7-192">a.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-192">a.</span></span> <span data-ttu-id="fc4c7-193">Klik op de **Admin & Agents** tabblad.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-193">Click the **Admin & Agents** tab.</span></span>

     <span data-ttu-id="fc4c7-194">b.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-194">b.</span></span> <span data-ttu-id="fc4c7-195">Selecteer **eenmalige aanmelding (SSO) en SAML**, en selecteer vervolgens **SAML**.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="fc4c7-196">c.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-196">c.</span></span> <span data-ttu-id="fc4c7-197">In **SAML SSO URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-197">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="fc4c7-198">d.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-198">d.</span></span> <span data-ttu-id="fc4c7-199">In **externe URL voor afmelden** textbox, plak de waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-199">In **Remote Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="fc4c7-200">e.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-200">e.</span></span> <span data-ttu-id="fc4c7-201">In **vingerafdruk van certificaat** textbox, plak de **vingerafdruk** waarde van het certificaat dat u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-201">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="fc4c7-202">f.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-202">f.</span></span> <span data-ttu-id="fc4c7-203">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fc4c7-204">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="fc4c7-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="fc4c7-205">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="fc4c7-207">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fc4c7-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fc4c7-208">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-208">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fc4c7-210">Om weer te geven naar de lijst met gebruikers gaan **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-210">To display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fc4c7-212">Aan de bovenkant van het dialoogvenster, klikt u op **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-212">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fc4c7-214">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="fc4c7-214">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fc4c7-216">a.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-216">a.</span></span> <span data-ttu-id="fc4c7-217">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-217">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fc4c7-218">b.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-218">b.</span></span> <span data-ttu-id="fc4c7-219">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-219">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fc4c7-220">c.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-220">c.</span></span> <span data-ttu-id="fc4c7-221">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-221">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fc4c7-222">d.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-222">d.</span></span> <span data-ttu-id="fc4c7-223">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="fc4c7-224">Een testgebruiker Zendesk maken</span><span class="sxs-lookup"><span data-stu-id="fc4c7-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="fc4c7-225">Meld u aan bij Azure AD-gebruikers inschakelen **Zendesk**, deze moeten worden ingericht in **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-225">To enable Azure AD users to log into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="fc4c7-226">Afhankelijk van de rol in de apps is het verwachte gedrag:</span><span class="sxs-lookup"><span data-stu-id="fc4c7-226">Depending on the role assigned in the apps, it's the expected behavior:</span></span>

 1. <span data-ttu-id="fc4c7-227">**Eindgebruikers** accounts automatisch worden ingericht als u zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="fc4c7-228">**Agent** en **Admin** accounts moeten handmatig worden ingericht **Zendesk** voordat u zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-228">**Agent** and **Admin** accounts need to be manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="fc4c7-229">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fc4c7-229">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="fc4c7-230">Meld u aan bij uw **Zendesk** tenant.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-230">Log in to your **Zendesk** tenant.</span></span>

2. <span data-ttu-id="fc4c7-231">Selecteer de **klantenlijst** tabblad.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-231">Select the **Customer List** tab.</span></span>

3. <span data-ttu-id="fc4c7-232">Selecteer de **gebruiker** tabblad en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-232">Select the **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="fc4c7-233">![Gebruiker toevoegen](./media/active-directory-saas-zendesk-tutorial/ic773632.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="fc4c7-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="fc4c7-234">Typ de e-mailadres van een bestaande Azure AD-account dat u wilt inrichten, en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-234">Type the email address of an existing Azure AD account you want to provision, and then click **Save**.</span></span>
   
    <span data-ttu-id="fc4c7-235">![Nieuwe gebruiker](./media/active-directory-saas-zendesk-tutorial/ic773633.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="fc4c7-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="fc4c7-236">U kunt andere Zendesk gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Zendesk aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk to provision AAD user accounts.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fc4c7-237">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc4c7-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fc4c7-238">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Zendesk.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zendesk.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="fc4c7-240">**Britta Simon om aan te wijzen Zendesk, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fc4c7-240">**To assign Britta Simon to Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="fc4c7-241">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="fc4c7-243">Selecteer in de lijst met toepassingen **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-243">In the applications list, select **Zendesk**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="fc4c7-245">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="fc4c7-247">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-247">Click **Add** button.</span></span> <span data-ttu-id="fc4c7-248">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="fc4c7-250">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fc4c7-251">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fc4c7-252">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fc4c7-253">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fc4c7-253">Testing single sign-on</span></span>

<span data-ttu-id="fc4c7-254">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fc4c7-255">Als u op de Zendesk-tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw Zendesk-toepassing.</span><span class="sxs-lookup"><span data-stu-id="fc4c7-255">When you click the Zendesk tile in the Access Panel, you should get automatically signed-on to your Zendesk application.</span></span>
<span data-ttu-id="fc4c7-256">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fc4c7-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fc4c7-257">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="fc4c7-257">Additional resources</span></span>

* [<span data-ttu-id="fc4c7-258">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fc4c7-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fc4c7-259">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fc4c7-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
