---
title: 'Zelfstudie: Azure Active Directory-integratie met iLMS | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en iLMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 22c72020200138e78835ed7dd2661f18b824c785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="f6810-103">Zelfstudie: Azure Active Directory-integratie met iLMS</span><span class="sxs-lookup"><span data-stu-id="f6810-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="f6810-104">In deze zelfstudie leert u hoe iLMS integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f6810-104">In this tutorial, you learn how to integrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f6810-105">ILMS integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f6810-105">Integrating iLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f6810-106">U kunt beheren in Azure AD die toegang tot iLMS heeft</span><span class="sxs-lookup"><span data-stu-id="f6810-106">You can control in Azure AD who has access to iLMS</span></span>
- <span data-ttu-id="f6810-107">U kunt uw gebruikers automatisch ophalen aangemeld bij iLMS (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="f6810-107">You can enable your users to automatically get signed-on to iLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f6810-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f6810-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f6810-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f6810-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6810-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f6810-110">Prerequisites</span></span>

<span data-ttu-id="f6810-111">Voor het configureren van Azure AD-integratie met iLMS, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="f6810-111">To configure Azure AD integration with iLMS, you need the following items:</span></span>

- <span data-ttu-id="f6810-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f6810-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f6810-113">Een iLMS eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f6810-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f6810-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f6810-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f6810-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f6810-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f6810-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f6810-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f6810-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f6810-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f6810-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f6810-118">Scenario description</span></span>
<span data-ttu-id="f6810-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f6810-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f6810-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f6810-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f6810-121">ILMS uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f6810-121">Adding iLMS from the gallery</span></span>
2. <span data-ttu-id="f6810-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f6810-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-the-gallery"></a><span data-ttu-id="f6810-123">ILMS uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f6810-123">Adding iLMS from the gallery</span></span>
<span data-ttu-id="f6810-124">Voor het configureren van de integratie van iLMS in Azure AD, moet u iLMS uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f6810-124">To configure the integration of iLMS into Azure AD, you need to add iLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f6810-125">**Als u wilt toevoegen iLMS uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f6810-125">**To add iLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f6810-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f6810-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f6810-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f6810-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f6810-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f6810-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f6810-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f6810-131">To add new application, click **New application** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f6810-133">Typ in het zoekvak **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="f6810-133">In the search box, type **iLMS**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="f6810-135">Selecteer in het deelvenster resultaten **iLMS**, klikt u vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f6810-135">In the results panel, select **iLMS**, then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f6810-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f6810-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f6810-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met iLMS op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f6810-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f6810-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in iLMS is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6810-139">For single sign-on to work, Azure AD needs to know what the counterpart user in iLMS is to a user in Azure AD.</span></span> <span data-ttu-id="f6810-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in iLMS tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="f6810-140">In other words, a link relationship between an Azure AD user and the related user in iLMS needs to be established.</span></span>

<span data-ttu-id="f6810-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in iLMS.</span><span class="sxs-lookup"><span data-stu-id="f6810-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in iLMS.</span></span>

<span data-ttu-id="f6810-142">Om te configureren en testen van Azure AD eenmalige aanmelding met iLMS, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="f6810-142">To configure and test Azure AD single sign-on with iLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f6810-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f6810-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f6810-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f6810-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f6810-145">**[Maken van een testgebruiker iLMS](#creating-an-ilms-test-user)**  : een equivalent van Britta Simon in iLMS die is gekoppeld aan de Azure AD-representatie van haar hebben.</span><span class="sxs-lookup"><span data-stu-id="f6810-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - to have a counterpart of Britta Simon in iLMS that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="f6810-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f6810-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f6810-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f6810-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f6810-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f6810-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f6810-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing iLMS configureren.</span><span class="sxs-lookup"><span data-stu-id="f6810-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="f6810-150">**Voor het configureren van Azure AD eenmalige aanmelding met iLMS, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f6810-150">**To configure Azure AD single sign-on with iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="f6810-151">In de Azure-portal op de **iLMS** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f6810-151">In the Azure portal, on the **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f6810-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f6810-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="f6810-155">Op de **iLMS domein en de URL's** sectie, voert u de volgende stappen uit als u wilt configureren, de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="f6810-155">On the **iLMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="f6810-157">a.</span><span class="sxs-lookup"><span data-stu-id="f6810-157">a.</span></span> <span data-ttu-id="f6810-158">In de **id** textbox, plak de **id** waarde u van kopiëren **serviceprovider** sectie van SAML-instellingen in de beheerportal iLMS.</span><span class="sxs-lookup"><span data-stu-id="f6810-158">In the **Identifier** textbox, paste the **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="f6810-159">b.</span><span class="sxs-lookup"><span data-stu-id="f6810-159">b.</span></span> <span data-ttu-id="f6810-160">In de **antwoord-URL** textbox, plak de **eindpunt (URL)** waarde u van kopiëren **serviceprovider** sectie van SAML-instellingen in het volgende patroon iLMS-beheerportal`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="f6810-160">In the **Reply URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having the following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="f6810-161">Deze '123456' is een van de Voorbeeldwaarde van id.</span><span class="sxs-lookup"><span data-stu-id="f6810-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="f6810-162">Controleer **weergeven geavanceerde instellingen voor URL**, als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="f6810-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="f6810-164">In de **aanmeldings-URL** textbox, plak de **eindpunt (URL)** waarde u van kopiëren **serviceprovider** sectie van SAML-instellingen in de beheerportal iLMS als`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="f6810-164">In the **Sign-on URL** textbox, paste the **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="f6810-165">Om in te schakelen JIT-inrichting, verwacht iLMS toepassing de SAML-asserties in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="f6810-165">To enable JIT provisioning, iLMS application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="f6810-166">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="f6810-166">Configure the following claims for this application.</span></span> <span data-ttu-id="f6810-167">U kunt de waarden van deze kenmerken van beheren de **gebruikerskenmerken** sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="f6810-167">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="f6810-168">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="f6810-168">The following screenshot shows an example for this.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="f6810-170">Maak **afdeling, regio** en **deling** kenmerken en voegt u de naam van deze kenmerken in iLMS.</span><span class="sxs-lookup"><span data-stu-id="f6810-170">Create **Department, Region** and **Division** attributes and add the name of these attributes in iLMS.</span></span> <span data-ttu-id="f6810-171">Alle deze kenmerken die hierboven zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="f6810-171">All these attributes shown above are required.</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="f6810-172">U moet inschakelen **Un-recognized-gebruikersaccount maken** in iLMS deze kenmerken toewijzen.</span><span class="sxs-lookup"><span data-stu-id="f6810-172">You have to enable **Create Un-recognized User Account** in iLMS to map these attributes.</span></span> <span data-ttu-id="f6810-173">Volg de instructies [hier](http://support.inspiredelearning.com/customer/portal/articles/2204526) voor een beter beeld van de configuratie van de kenmerken.</span><span class="sxs-lookup"><span data-stu-id="f6810-173">Follow the instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) to get an idea on the attributes configuration.</span></span>

6. <span data-ttu-id="f6810-174">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding hierboven en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f6810-174">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="f6810-175">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="f6810-175">Attribute Name</span></span> | <span data-ttu-id="f6810-176">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="f6810-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="f6810-177">deling</span><span class="sxs-lookup"><span data-stu-id="f6810-177">division</span></span> | <span data-ttu-id="f6810-178">User.Department</span><span class="sxs-lookup"><span data-stu-id="f6810-178">user.department</span></span> |
    | <span data-ttu-id="f6810-179">Regio</span><span class="sxs-lookup"><span data-stu-id="f6810-179">region</span></span> | <span data-ttu-id="f6810-180">User.state</span><span class="sxs-lookup"><span data-stu-id="f6810-180">user.state</span></span> |
    | <span data-ttu-id="f6810-181">Afdeling</span><span class="sxs-lookup"><span data-stu-id="f6810-181">department</span></span> | <span data-ttu-id="f6810-182">User.jobtitle</span><span class="sxs-lookup"><span data-stu-id="f6810-182">user.jobtitle</span></span> |

    <span data-ttu-id="f6810-183">a.</span><span class="sxs-lookup"><span data-stu-id="f6810-183">a.</span></span> <span data-ttu-id="f6810-184">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f6810-184">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="f6810-187">b.</span><span class="sxs-lookup"><span data-stu-id="f6810-187">b.</span></span> <span data-ttu-id="f6810-188">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="f6810-188">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="f6810-189">c.</span><span class="sxs-lookup"><span data-stu-id="f6810-189">c.</span></span> <span data-ttu-id="f6810-190">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="f6810-190">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="f6810-191">d.</span><span class="sxs-lookup"><span data-stu-id="f6810-191">d.</span></span> <span data-ttu-id="f6810-192">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="f6810-192">Click **Ok**</span></span>

7. <span data-ttu-id="f6810-193">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f6810-193">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="f6810-195">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f6810-195">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="f6810-197">In een ander browservenster geopend, moet u zich aanmelden bij uw **iLMS-beheerportal** als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f6810-197">In a different web browser window, log in to your **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="f6810-198">Klik op **SSO:SAML** onder **instellingen** tabblad SAML-instellingen openen en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f6810-198">Click **SSO:SAML** under **Settings** tab to open SAML settings and perform the following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="f6810-200">a.</span><span class="sxs-lookup"><span data-stu-id="f6810-200">a.</span></span> <span data-ttu-id="f6810-201">Vouw de **serviceprovider** sectie en kopieer de **id** en **eindpunt (URL)** waarde.</span><span class="sxs-lookup"><span data-stu-id="f6810-201">Expand the **Service Provider** section and copy the **Identifier** and **Endpoint (URL)** value.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="f6810-203">b.</span><span class="sxs-lookup"><span data-stu-id="f6810-203">b.</span></span> <span data-ttu-id="f6810-204">Onder **identiteitsprovider** sectie, klikt u op **metagegevens importeren**.</span><span class="sxs-lookup"><span data-stu-id="f6810-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="f6810-205">c.</span><span class="sxs-lookup"><span data-stu-id="f6810-205">c.</span></span> <span data-ttu-id="f6810-206">Selecteer de **metagegevens** bestand gedownload van Azure-Portal **certificaat voor ondertekening van SAML** sectie.</span><span class="sxs-lookup"><span data-stu-id="f6810-206">Select the **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="f6810-208">d.</span><span class="sxs-lookup"><span data-stu-id="f6810-208">d.</span></span> <span data-ttu-id="f6810-209">Als u inschakelen wilt voor het maken van accounts iLMS voor ongedaan maken inrichting JIT-gebruikers herkennen, volgt u onderstaande stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f6810-209">If you want to enable JIT provisioning to create iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="f6810-210">Controleer **Account maken voor niet-herkende gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="f6810-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="f6810-212">De kenmerken in Azure AD met de kenmerken in iLMS toewijzen.</span><span class="sxs-lookup"><span data-stu-id="f6810-212">Map the attributes in Azure AD with the attributes in iLMS.</span></span> <span data-ttu-id="f6810-213">Geef de naam van de kenmerken of de standaardwaarde in de kenmerkkolom.</span><span class="sxs-lookup"><span data-stu-id="f6810-213">In the attribute column, specify the attributes name or the default value.</span></span>

    <span data-ttu-id="f6810-214">e.</span><span class="sxs-lookup"><span data-stu-id="f6810-214">e.</span></span> <span data-ttu-id="f6810-215">Ga naar **bedrijfsregels** tabblad en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f6810-215">Go to **Business Rules** tab and perform the following steps:</span></span> 
        
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="f6810-217">Controleer **Un-recognized regio's maken, afdelingen en afdelingen** regio's, afdelingen en afdelingen die nog niet aanwezig op het moment van eenmalige aanmelding maken.</span><span class="sxs-lookup"><span data-stu-id="f6810-217">Check **Create Un-recognized Regions, Divisions and Departments** to create Regions, Divisions, and Departments that do not already exist at the time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="f6810-218">Controleer **Update gebruiker profiel tijdens aanmelden** om op te geven of profiel van de gebruiker is bijgewerkt met elke eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f6810-218">Check **Update User Profile During Sign-in** to specify whether the user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="f6810-219">Als de **'Update lege waarden voor niet verplichte velden in gebruikersprofiel'** optie is ingeschakeld, optionele profiel velden leeg bij het aanmelden wordt zijn ook voor zorgen dat het iLMS gebruikersprofiel bevat lege waarden voor deze velden.</span><span class="sxs-lookup"><span data-stu-id="f6810-219">If the **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause the user’s iLMS profile to contain blank values for those fields.</span></span>
        
       - <span data-ttu-id="f6810-220">Controleer **fout meldingse-mail verzenden** en voer het e-mailadres van de gebruiker waarop u wilt ontvangen van de e-mailmelding fout.</span><span class="sxs-lookup"><span data-stu-id="f6810-220">Check **Send Error Notification Email** and enter the email of the user where you want to receive the error notification email.</span></span>

11. <span data-ttu-id="f6810-221">Klik op **opslaan** knop de instellingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="f6810-221">Click **Save** button to save the settings.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="f6810-223">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="f6810-223">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f6810-224">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="f6810-224">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f6810-225">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f6810-225">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f6810-226">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f6810-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="f6810-227">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f6810-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f6810-229">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f6810-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f6810-230">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f6810-230">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f6810-232">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="f6810-232">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f6810-234">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f6810-234">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f6810-236">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f6810-236">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f6810-238">a.</span><span class="sxs-lookup"><span data-stu-id="f6810-238">a.</span></span> <span data-ttu-id="f6810-239">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f6810-239">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f6810-240">b.</span><span class="sxs-lookup"><span data-stu-id="f6810-240">b.</span></span> <span data-ttu-id="f6810-241">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f6810-241">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f6810-242">c.</span><span class="sxs-lookup"><span data-stu-id="f6810-242">c.</span></span> <span data-ttu-id="f6810-243">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f6810-243">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f6810-244">d.</span><span class="sxs-lookup"><span data-stu-id="f6810-244">d.</span></span> <span data-ttu-id="f6810-245">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f6810-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="f6810-246">Een testgebruiker iLMS maken</span><span class="sxs-lookup"><span data-stu-id="f6810-246">Creating an iLMS test user</span></span>

<span data-ttu-id="f6810-247">Toepassing ondersteunt Just in time gebruikers inrichten en na verificatie gebruikers automatisch in de toepassing gemaakt worden.</span><span class="sxs-lookup"><span data-stu-id="f6810-247">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="f6810-248">JIT werkt als u hebt geklikt op de **Un-recognized-gebruikersaccount maken** selectievakje tijdens SAML-configuratie-instelling op iLMS-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="f6810-248">JIT will work, if you have clicked the **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="f6810-249">Als u een gebruiker handmatig maken wilt, volgt u onderstaande stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f6810-249">If you need to create an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="f6810-250">Meld u aan bij uw bedrijf iLMS site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f6810-250">Log in to your iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="f6810-251">Klik op **'Gebruiker registreren'** onder **gebruikers** tabblad openen **gebruiker registreren** pagina.</span><span class="sxs-lookup"><span data-stu-id="f6810-251">Click **“Register User”** under **Users** tab to open **Register User** page.</span></span> 
   
   ![Werknemer toevoegen](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="f6810-253">Op de **'Gebruiker registreren'** pagina, de volgende stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f6810-253">On the **“Register User”** page, perform the following steps.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="f6810-255">a.</span><span class="sxs-lookup"><span data-stu-id="f6810-255">a.</span></span> <span data-ttu-id="f6810-256">In de **voornaam** textbox Britta de eerste typenaam.</span><span class="sxs-lookup"><span data-stu-id="f6810-256">In the **First Name** textbox, type the first name Britta.</span></span>
   
    <span data-ttu-id="f6810-257">b.</span><span class="sxs-lookup"><span data-stu-id="f6810-257">b.</span></span> <span data-ttu-id="f6810-258">In de **achternaam** textbox, typ de achternaam Simon.</span><span class="sxs-lookup"><span data-stu-id="f6810-258">In the **Last Name** textbox, type the last name Simon.</span></span>

    <span data-ttu-id="f6810-259">c.</span><span class="sxs-lookup"><span data-stu-id="f6810-259">c.</span></span> <span data-ttu-id="f6810-260">In de **E-mail-ID** textbox, typ de e-mailadres van Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="f6810-260">In the **Email ID** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="f6810-261">d.</span><span class="sxs-lookup"><span data-stu-id="f6810-261">d.</span></span> <span data-ttu-id="f6810-262">In de **regio** vervolgkeuzelijst, selecteer de waarde voor de regio.</span><span class="sxs-lookup"><span data-stu-id="f6810-262">In the **Region** dropdown, select the value for region.</span></span>

    <span data-ttu-id="f6810-263">e.</span><span class="sxs-lookup"><span data-stu-id="f6810-263">e.</span></span> <span data-ttu-id="f6810-264">In de **deling** vervolgkeuzelijst, selecteer de waarde voor verdeling.</span><span class="sxs-lookup"><span data-stu-id="f6810-264">In the **Division** dropdown, select the value for division.</span></span>

    <span data-ttu-id="f6810-265">f.</span><span class="sxs-lookup"><span data-stu-id="f6810-265">f.</span></span> <span data-ttu-id="f6810-266">In de **afdeling** vervolgkeuzelijst, selecteer de waarde voor afdeling.</span><span class="sxs-lookup"><span data-stu-id="f6810-266">In the **Department** dropdown, select the value for department.</span></span>

    <span data-ttu-id="f6810-267">g.</span><span class="sxs-lookup"><span data-stu-id="f6810-267">g.</span></span> <span data-ttu-id="f6810-268">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f6810-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f6810-269">U kunt registratie-e-mail naar gebruiker verzenden door te selecteren **registratie E-mail verzenden** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="f6810-269">You can send registration mail to user by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f6810-270">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6810-270">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f6810-271">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen tot iLMS.</span><span class="sxs-lookup"><span data-stu-id="f6810-271">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to iLMS.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f6810-273">**Britta Simon om aan te wijzen iLMS, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f6810-273">**To assign Britta Simon to iLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="f6810-274">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f6810-274">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f6810-276">Selecteer in de lijst met toepassingen **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="f6810-276">In the applications list, select **iLMS**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="f6810-278">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f6810-278">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f6810-280">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f6810-280">Click **Add** button.</span></span> <span data-ttu-id="f6810-281">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f6810-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f6810-283">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="f6810-283">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f6810-284">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f6810-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f6810-285">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f6810-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f6810-286">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f6810-286">Testing single sign-on</span></span>

<span data-ttu-id="f6810-287">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="f6810-287">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f6810-288">Als u op de tegel iLMS in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing iLMS.</span><span class="sxs-lookup"><span data-stu-id="f6810-288">When you click the iLMS tile in the Access Panel, you should get automatically signed-on to your iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f6810-289">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f6810-289">Additional resources</span></span>

* [<span data-ttu-id="f6810-290">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6810-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f6810-291">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f6810-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

