---
title: 'Zelfstudie: Azure Active Directory-integratie met SD-elementen | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en SD-elementen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 624eff0a0da8f548877e4a4346b21df89cd37b67
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="fc010-103">Zelfstudie: Azure Active Directory-integratie met SD-elementen</span><span class="sxs-lookup"><span data-stu-id="fc010-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>

<span data-ttu-id="fc010-104">In deze zelfstudie leert u hoe SD-elementen integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fc010-104">In this tutorial, you learn how to integrate SD Elements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fc010-105">SD-elementen integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="fc010-105">Integrating SD Elements with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fc010-106">U kunt beheren in Azure AD die toegang tot de SD-elementen heeft</span><span class="sxs-lookup"><span data-stu-id="fc010-106">You can control in Azure AD who has access to SD Elements</span></span>
- <span data-ttu-id="fc010-107">U kunt uw gebruikers automatisch ophalen aangemeld bij SD-elementen (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="fc010-107">You can enable your users to automatically get signed-on to SD Elements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fc010-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="fc010-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fc010-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fc010-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc010-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fc010-110">Prerequisites</span></span>

<span data-ttu-id="fc010-111">Voor het configureren van Azure AD-integratie met SD-elementen, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="fc010-111">To configure Azure AD integration with SD Elements, you need the following items:</span></span>

- <span data-ttu-id="fc010-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="fc010-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fc010-113">Een SD-elementen eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="fc010-113">A SD Elements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fc010-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="fc010-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fc010-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="fc010-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fc010-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="fc010-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fc010-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fc010-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fc010-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="fc010-118">Scenario description</span></span>
<span data-ttu-id="fc010-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="fc010-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fc010-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="fc010-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fc010-121">Het toevoegen van SD-elementen in de galerie</span><span class="sxs-lookup"><span data-stu-id="fc010-121">Adding SD Elements from the gallery</span></span>
2. <span data-ttu-id="fc010-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fc010-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-the-gallery"></a><span data-ttu-id="fc010-123">Het toevoegen van SD-elementen in de galerie</span><span class="sxs-lookup"><span data-stu-id="fc010-123">Adding SD Elements from the gallery</span></span>
<span data-ttu-id="fc010-124">Voor het configureren van de integratie van SD-elementen in Azure AD, moet u SD-elementen in de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="fc010-124">To configure the integration of SD Elements into Azure AD, you need to add SD Elements from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fc010-125">**Als u wilt toevoegen SD-elementen in de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fc010-125">**To add SD Elements from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fc010-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="fc010-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fc010-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fc010-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fc010-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fc010-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="fc010-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fc010-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="fc010-133">Typ in het zoekvak **SD-elementen**.</span><span class="sxs-lookup"><span data-stu-id="fc010-133">In the search box, type **SD Elements**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. <span data-ttu-id="fc010-135">Selecteer in het deelvenster resultaten **SD-elementen**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="fc010-135">In the results panel, select **SD Elements**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fc010-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fc010-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fc010-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met SD-elementen die op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="fc010-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fc010-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in SD-elementen in Azure AD voor een gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="fc010-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SD Elements is to a user in Azure AD.</span></span> <span data-ttu-id="fc010-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in SD-elementen tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="fc010-140">In other words, a link relationship between an Azure AD user and the related user in SD Elements needs to be established.</span></span>

<span data-ttu-id="fc010-141">In de SD-elementen, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="fc010-141">In SD Elements, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fc010-142">Om te configureren en testen van Azure AD eenmalige aanmelding met SD-elementen, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="fc010-142">To configure and test Azure AD single sign-on with SD Elements, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fc010-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fc010-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fc010-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fc010-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fc010-145">**[Maken van een SD-elementen testgebruiker](#creating-a-sd-elements-test-user)**  - SD-elementen die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="fc010-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - to have a counterpart of Britta Simon in SD Elements that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fc010-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="fc010-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fc010-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="fc010-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fc010-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="fc010-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fc010-149">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing SD-elementen.</span><span class="sxs-lookup"><span data-stu-id="fc010-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="fc010-150">**Voor het configureren van Azure AD eenmalige aanmelding met SD-elementen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fc010-150">**To configure Azure AD single sign-on with SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="fc010-151">In de Azure-portal op de **SD-elementen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="fc010-151">In the Azure portal, on the **SD Elements** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="fc010-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="fc010-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. <span data-ttu-id="fc010-155">Op de **SD-elementen domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="fc010-155">On the **SD Elements Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    <span data-ttu-id="fc010-157">a.</span><span class="sxs-lookup"><span data-stu-id="fc010-157">a.</span></span> <span data-ttu-id="fc010-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<tenantname>.sdelements.com/sso/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="fc010-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="fc010-159">b.</span><span class="sxs-lookup"><span data-stu-id="fc010-159">b.</span></span> <span data-ttu-id="fc010-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<tenantname>.sdelements.com/sso/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="fc010-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fc010-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="fc010-161">These values are not real.</span></span> <span data-ttu-id="fc010-162">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="fc010-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="fc010-163">Neem contact op met [SD-elementen ondersteuningsteam](mailto:support@sdelements.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="fc010-163">Contact [SD Elements support team](mailto:support@sdelements.com) to get these values.</span></span>

4. <span data-ttu-id="fc010-164">De SAML-asserties verwacht toepassing SD-elementen in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="fc010-164">SD Elements application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="fc010-165">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="fc010-165">Configure the following claims for this application.</span></span> <span data-ttu-id="fc010-166">U kunt de waarden van deze kenmerken van beheren de **'Gebruikerskenmerk'** tabblad van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="fc010-166">You can manage the values of these attributes from the **"User Attribute"** tab of the application.</span></span> <span data-ttu-id="fc010-167">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="fc010-167">The following screenshot shows an example for this.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. <span data-ttu-id="fc010-169">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding en de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="fc010-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span> 

    | <span data-ttu-id="fc010-170">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="fc010-170">Attribute Name</span></span> | <span data-ttu-id="fc010-171">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="fc010-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="fc010-172">E-mail</span><span class="sxs-lookup"><span data-stu-id="fc010-172">email</span></span> |<span data-ttu-id="fc010-173">User.mail</span><span class="sxs-lookup"><span data-stu-id="fc010-173">user.mail</span></span> |
    | <span data-ttu-id="fc010-174">Voornaam</span><span class="sxs-lookup"><span data-stu-id="fc010-174">firstname</span></span> |<span data-ttu-id="fc010-175">User.givenName</span><span class="sxs-lookup"><span data-stu-id="fc010-175">user.givenname</span></span> |
    | <span data-ttu-id="fc010-176">Achternaam</span><span class="sxs-lookup"><span data-stu-id="fc010-176">lastname</span></span> |<span data-ttu-id="fc010-177">User.surname</span><span class="sxs-lookup"><span data-stu-id="fc010-177">user.surname</span></span> |

    <span data-ttu-id="fc010-178">a.</span><span class="sxs-lookup"><span data-stu-id="fc010-178">a.</span></span> <span data-ttu-id="fc010-179">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fc010-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="fc010-182">b.</span><span class="sxs-lookup"><span data-stu-id="fc010-182">b.</span></span> <span data-ttu-id="fc010-183">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="fc010-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="fc010-184">c.</span><span class="sxs-lookup"><span data-stu-id="fc010-184">c.</span></span> <span data-ttu-id="fc010-185">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="fc010-185">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="fc010-186">d.</span><span class="sxs-lookup"><span data-stu-id="fc010-186">d.</span></span> <span data-ttu-id="fc010-187">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="fc010-187">Click **Ok**.</span></span>
 
6. <span data-ttu-id="fc010-188">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="fc010-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. <span data-ttu-id="fc010-190">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="fc010-190">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="fc010-192">Op de **SD-elementen configuratie** sectie, klikt u op **SD-elementen configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="fc010-192">On the **SD Elements Configuration** section, click **Configure SD Elements** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fc010-193">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="fc010-193">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. <span data-ttu-id="fc010-195">Als u eenmalige aanmelding is ingeschakeld, neem contact op met uw [SD-elementen ondersteuningsteam](mailto:support@sdelements.com) en geeft u het gedownloade certificaatbestand.</span><span class="sxs-lookup"><span data-stu-id="fc010-195">To get single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with the downloaded certificate file.</span></span> 

10. <span data-ttu-id="fc010-196">In een ander browservenster aanmelding in uw tenant, SD-elementen als beheerder.</span><span class="sxs-lookup"><span data-stu-id="fc010-196">In a different browser window, sign-on to your SD Elements tenant as an administrator.</span></span>

11. <span data-ttu-id="fc010-197">Klik in het menu bovenaan op **System**, en vervolgens **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="fc010-197">In the menu on the top, click **System**, and then **Single Sign-on**.</span></span> 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. <span data-ttu-id="fc010-199">Op de **instellingen voor eenmalige aanmelding** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="fc010-199">On the **Single Sign-On Settings** dialog, perform the following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="fc010-201">a.</span><span class="sxs-lookup"><span data-stu-id="fc010-201">a.</span></span> <span data-ttu-id="fc010-202">Als **SSO Type**, selecteer **SAML**.</span><span class="sxs-lookup"><span data-stu-id="fc010-202">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="fc010-203">b.</span><span class="sxs-lookup"><span data-stu-id="fc010-203">b.</span></span> <span data-ttu-id="fc010-204">In de **identiteit Provider entiteit-ID** textbox, plak de waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fc010-204">In the **Identity Provider Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="fc010-205">c.</span><span class="sxs-lookup"><span data-stu-id="fc010-205">c.</span></span> <span data-ttu-id="fc010-206">In de **Provider Single Sign-On Identiteitsservice** textbox, plakt u de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fc010-206">In the **Identity Provider Single Sign-On Service** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="fc010-207">d.</span><span class="sxs-lookup"><span data-stu-id="fc010-207">d.</span></span> <span data-ttu-id="fc010-208">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="fc010-208">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="fc010-209">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="fc010-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fc010-210">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="fc010-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fc010-211">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fc010-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fc010-212">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="fc010-212">Creating an Azure AD test user</span></span>
<span data-ttu-id="fc010-213">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="fc010-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="fc010-215">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fc010-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fc010-216">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="fc010-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fc010-218">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="fc010-218">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fc010-220">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fc010-220">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fc010-222">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="fc010-222">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fc010-224">a.</span><span class="sxs-lookup"><span data-stu-id="fc010-224">a.</span></span> <span data-ttu-id="fc010-225">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fc010-225">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fc010-226">b.</span><span class="sxs-lookup"><span data-stu-id="fc010-226">b.</span></span> <span data-ttu-id="fc010-227">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fc010-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fc010-228">c.</span><span class="sxs-lookup"><span data-stu-id="fc010-228">c.</span></span> <span data-ttu-id="fc010-229">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="fc010-229">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fc010-230">d.</span><span class="sxs-lookup"><span data-stu-id="fc010-230">d.</span></span> <span data-ttu-id="fc010-231">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="fc010-231">Click **Create**.</span></span>
 
### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="fc010-232">Maken van een testgebruiker SD-elementen</span><span class="sxs-lookup"><span data-stu-id="fc010-232">Creating a SD Elements test user</span></span>

<span data-ttu-id="fc010-233">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in SD-elementen.</span><span class="sxs-lookup"><span data-stu-id="fc010-233">The objective of this section is to create a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="fc010-234">In het geval van SD-elementen is elementen van de SD-gebruikers te maken een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="fc010-234">In the case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="fc010-235">**Als u wilt Britta Simon in SD-elementen maken, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fc010-235">**To create Britta Simon in SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="fc010-236">In een browservenster geopend, aanmelding bij uw bedrijf SD-elementen site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="fc010-236">In a web browser window, sign-on to your SD Elements company site as an administrator.</span></span>

2. <span data-ttu-id="fc010-237">Klik in het menu bovenaan op **Gebruikersbeheer**, en vervolgens **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="fc010-237">In the menu on the top, click **User Management**, and then **Users**.</span></span>
   
    ![Maken van een testgebruiker SD-elementen](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. <span data-ttu-id="fc010-239">Klik op **nieuwe gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="fc010-239">Click **Add New User**.</span></span>
   
    ![Maken van een testgebruiker SD-elementen](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. <span data-ttu-id="fc010-241">Op de **nieuwe gebruiker toevoegen** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="fc010-241">On the **Add New User** dialog, perform the following steps:</span></span>
   
    ![Maken van een testgebruiker SD-elementen](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    <span data-ttu-id="fc010-243">a.</span><span class="sxs-lookup"><span data-stu-id="fc010-243">a.</span></span> <span data-ttu-id="fc010-244">In de **e** textbox, voer het e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="fc010-244">In the **E-mail** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="fc010-245">b.</span><span class="sxs-lookup"><span data-stu-id="fc010-245">b.</span></span> <span data-ttu-id="fc010-246">In de **voornaam** textbox, voer de voornaam van de gebruiker zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="fc010-246">In the **First Name** textbox, enter the first name of user like **Britta**.</span></span>
   
    <span data-ttu-id="fc010-247">c.</span><span class="sxs-lookup"><span data-stu-id="fc010-247">c.</span></span> <span data-ttu-id="fc010-248">In de **achternaam** textbox, geef de achternaam van de gebruiker zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="fc010-248">In the **Last Name** textbox, enter the last name of user like **Simon**.</span></span>
   
    <span data-ttu-id="fc010-249">d.</span><span class="sxs-lookup"><span data-stu-id="fc010-249">d.</span></span> <span data-ttu-id="fc010-250">Als **rol**, selecteer **gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="fc010-250">As **Role**, select **User**.</span></span> 
   
    <span data-ttu-id="fc010-251">e.</span><span class="sxs-lookup"><span data-stu-id="fc010-251">e.</span></span> <span data-ttu-id="fc010-252">Klik op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="fc010-252">Click **Create User**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fc010-253">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc010-253">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fc010-254">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan SD-elementen.</span><span class="sxs-lookup"><span data-stu-id="fc010-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SD Elements.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="fc010-256">**Als u wilt toewijzen Britta Simon naar SD-elementen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="fc010-256">**To assign Britta Simon to SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="fc010-257">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fc010-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="fc010-259">Selecteer in de lijst met toepassingen **SD-elementen**.</span><span class="sxs-lookup"><span data-stu-id="fc010-259">In the applications list, select **SD Elements**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. <span data-ttu-id="fc010-261">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="fc010-261">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="fc010-263">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="fc010-263">Click **Add** button.</span></span> <span data-ttu-id="fc010-264">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fc010-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="fc010-266">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="fc010-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fc010-267">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fc010-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fc010-268">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="fc010-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fc010-269">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="fc010-269">Testing single sign-on</span></span>

<span data-ttu-id="fc010-270">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="fc010-270">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
  
<span data-ttu-id="fc010-271">Als u op de tegel SD-elementen in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing SD-elementen.</span><span class="sxs-lookup"><span data-stu-id="fc010-271">When you click the SD Elements tile in the Access Panel, you should get automatically signed-on to your SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fc010-272">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="fc010-272">Additional resources</span></span>

* [<span data-ttu-id="fc010-273">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fc010-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fc010-274">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fc010-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

