---
title: 'Zelfstudie: Azure Active Directory-integratie met eKincare | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en eKincare.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 014eaff14974bb6cd551b6fe53409ede6a6dfea1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a><span data-ttu-id="1a1d2-103">Zelfstudie: Azure Active Directory-integratie met eKincare</span><span class="sxs-lookup"><span data-stu-id="1a1d2-103">Tutorial: Azure Active Directory integration with eKincare</span></span>

<span data-ttu-id="1a1d2-104">In deze zelfstudie leert u hoe eKincare integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1a1d2-104">In this tutorial, you learn how to integrate eKincare with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1a1d2-105">EKincare integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1a1d2-105">Integrating eKincare with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1a1d2-106">U kunt beheren in Azure AD die toegang tot eKincare heeft</span><span class="sxs-lookup"><span data-stu-id="1a1d2-106">You can control in Azure AD who has access to eKincare</span></span>
- <span data-ttu-id="1a1d2-107">U kunt uw gebruikers automatisch ophalen aangemeld bij eKincare (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="1a1d2-107">You can enable your users to automatically get signed-on to eKincare (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1a1d2-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="1a1d2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1a1d2-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1a1d2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a1d2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1a1d2-110">Prerequisites</span></span>

<span data-ttu-id="1a1d2-111">Voor het configureren van Azure AD-integratie met eKincare, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="1a1d2-111">To configure Azure AD integration with eKincare, you need the following items:</span></span>

- <span data-ttu-id="1a1d2-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1a1d2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1a1d2-113">Een eKincare eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="1a1d2-113">A eKincare single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1a1d2-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1a1d2-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1a1d2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1a1d2-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1a1d2-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a1d2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1a1d2-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1a1d2-118">Scenario description</span></span>
<span data-ttu-id="1a1d2-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1a1d2-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1a1d2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1a1d2-121">EKincare uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1a1d2-121">Adding eKincare from the gallery</span></span>
2. <span data-ttu-id="1a1d2-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1a1d2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ekincare-from-the-gallery"></a><span data-ttu-id="1a1d2-123">EKincare uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1a1d2-123">Adding eKincare from the gallery</span></span>
<span data-ttu-id="1a1d2-124">Voor het configureren van de integratie van eKincare in Azure AD, moet u eKincare uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-124">To configure the integration of eKincare into Azure AD, you need to add eKincare from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1a1d2-125">**Als u wilt toevoegen eKincare uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1a1d2-125">**To add eKincare from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1a1d2-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1a1d2-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1a1d2-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="1a1d2-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="1a1d2-133">Typ in het zoekvak **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-133">In the search box, type **eKincare**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_search.png)

5. <span data-ttu-id="1a1d2-135">Selecteer in het deelvenster resultaten **eKincare**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-135">In the results panel, select **eKincare**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1a1d2-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1a1d2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1a1d2-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met eKincare op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="1a1d2-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1a1d2-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in eKincare is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in eKincare is to a user in Azure AD.</span></span> <span data-ttu-id="1a1d2-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in eKincare tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-140">In other words, a link relationship between an Azure AD user and the related user in eKincare needs to be established.</span></span>

<span data-ttu-id="1a1d2-141">Wijs in eKincare, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-141">In eKincare, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1a1d2-142">Om te configureren en testen van Azure AD eenmalige aanmelding met eKincare, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="1a1d2-142">To configure and test Azure AD single sign-on with eKincare, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1a1d2-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1a1d2-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1a1d2-145">**[Maken van een testgebruiker eKincare](#creating-a-ekincare-test-user)**  - hebben een equivalent van Britta Simon in eKincare die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - to have a counterpart of Britta Simon in eKincare that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1a1d2-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1a1d2-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1a1d2-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1a1d2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1a1d2-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing eKincare configureren.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eKincare application.</span></span>

<span data-ttu-id="1a1d2-150">**Voor het configureren van Azure AD eenmalige aanmelding met eKincare, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1a1d2-150">**To configure Azure AD single sign-on with eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="1a1d2-151">In de Azure-portal op de **eKincare** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-151">In the Azure portal, on the **eKincare** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1a1d2-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_samlbase.png)

3. <span data-ttu-id="1a1d2-155">Op de **eKincare domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1a1d2-155">On the **eKincare Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_url.png)

    <span data-ttu-id="1a1d2-157">a.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-157">a.</span></span> <span data-ttu-id="1a1d2-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<instancename>.ekincare.com/`</span><span class="sxs-lookup"><span data-stu-id="1a1d2-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/`</span></span>

    <span data-ttu-id="1a1d2-159">b.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-159">b.</span></span> <span data-ttu-id="1a1d2-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<instancename>.ekincare.com/hul/saml`</span><span class="sxs-lookup"><span data-stu-id="1a1d2-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/hul/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1a1d2-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-161">These values are not real.</span></span> <span data-ttu-id="1a1d2-162">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="1a1d2-163">Neem contact op met [eKincare ondersteuningsteam](mailto:tech@ekincare.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-163">Contact [eKincare support team](mailto:tech@ekincare.com) to get these values.</span></span>
 
4. <span data-ttu-id="1a1d2-164">de SAML-asserties verwacht eKincare toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-164">eKincare application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="1a1d2-165">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-165">Configure the following claims for this application.</span></span> <span data-ttu-id="1a1d2-166">U kunt beheren de waarden van deze kenmerken van de '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="1a1d2-167">De volgende Schermafbeelding toont een voorbeeld voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-167">The following screenshot shows an example for this configuration.</span></span>

    <span data-ttu-id="1a1d2-168">De naam van de claim wordt altijd worden **'werknemer-id'** en de waarde die we hebben toegewezen aan user.extensionattribute1 dat de werknemer-id van de gebruiker bevat.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-168">The claim name will always be **"employeeid"** and the value of which we have mapped to user.extensionattribute1, that contains the employeeid of the user.</span></span> <span data-ttu-id="1a1d2-169">De andere twee claims naam eenledige</span><span class="sxs-lookup"><span data-stu-id="1a1d2-169">The other two claims' name i.e</span></span> <span data-ttu-id="1a1d2-170">**'organizationid'** en **'organisatienaam'** altijd dezelfde en hun waarden respectievelijk de details van de organisatie van de gebruiker bevat.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-170">**"organizationid"** and **"organizationname"** will always be same and their values contain the details of the organization of the user respectively.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ekincare-tutorial/attribute.png)
    
5. <span data-ttu-id="1a1d2-172">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding hierboven en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1a1d2-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="1a1d2-173">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="1a1d2-173">Attribute Name</span></span> | <span data-ttu-id="1a1d2-174">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="1a1d2-174">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="1a1d2-175">Werknemer-id</span><span class="sxs-lookup"><span data-stu-id="1a1d2-175">employeeid</span></span> | <span data-ttu-id="1a1d2-176">*User.extensionattribute1*</span><span class="sxs-lookup"><span data-stu-id="1a1d2-176">*user.extensionattribute1*</span></span> |
    | <span data-ttu-id="1a1d2-177">OrganizationId</span><span class="sxs-lookup"><span data-stu-id="1a1d2-177">organizationid</span></span> | <span data-ttu-id="1a1d2-178">*'uniquevalue'*</span><span class="sxs-lookup"><span data-stu-id="1a1d2-178">*"uniquevalue"*</span></span> |
    | <span data-ttu-id="1a1d2-179">Organisatienaam</span><span class="sxs-lookup"><span data-stu-id="1a1d2-179">organizationname</span></span> | <span data-ttu-id="1a1d2-180">*User.CompanyName*</span><span class="sxs-lookup"><span data-stu-id="1a1d2-180">*user.companyname*</span></span> |

    <span data-ttu-id="1a1d2-181">a.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-181">a.</span></span> <span data-ttu-id="1a1d2-182">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-182">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ekincare-tutorial/04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ekincare-tutorial/05.png)
    
    <span data-ttu-id="1a1d2-185">b.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-185">b.</span></span> <span data-ttu-id="1a1d2-186">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="1a1d2-187">c.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-187">c.</span></span> <span data-ttu-id="1a1d2-188">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-188">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="1a1d2-189">d.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-189">d.</span></span> <span data-ttu-id="1a1d2-190">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="1a1d2-190">Click **Ok**</span></span>

6. <span data-ttu-id="1a1d2-191">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_certificate.png) 

7. <span data-ttu-id="1a1d2-193">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-193">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ekincare-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1a1d2-195">Eenmalige aanmelding configureren op **eKincare** zijde, moet u de gedownloade verzenden **Metadata XML** naar [eKincare ondersteuningsteam](mailto:tech@ekincare.com).</span><span class="sxs-lookup"><span data-stu-id="1a1d2-195">To configure single sign-on on **eKincare** side, you need to send the downloaded **Metadata XML** to [eKincare support team](mailto:tech@ekincare.com).</span></span> <span data-ttu-id="1a1d2-196">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-196">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1a1d2-197">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="1a1d2-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1a1d2-198">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1a1d2-199">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1a1d2-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1a1d2-200">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1a1d2-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="1a1d2-201">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="1a1d2-203">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1a1d2-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1a1d2-204">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ekincare-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1a1d2-206">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ekincare-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1a1d2-208">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ekincare-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1a1d2-210">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1a1d2-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ekincare-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1a1d2-212">a.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-212">a.</span></span> <span data-ttu-id="1a1d2-213">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1a1d2-214">b.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-214">b.</span></span> <span data-ttu-id="1a1d2-215">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1a1d2-216">c.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-216">c.</span></span> <span data-ttu-id="1a1d2-217">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1a1d2-218">d.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-218">d.</span></span> <span data-ttu-id="1a1d2-219">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-219">Click **Create**.</span></span>
 
### <a name="creating-a-ekincare-test-user"></a><span data-ttu-id="1a1d2-220">Een testgebruiker eKincare maken</span><span class="sxs-lookup"><span data-stu-id="1a1d2-220">Creating a eKincare test user</span></span>

<span data-ttu-id="1a1d2-221">Toepassing ondersteunt Just in time gebruikers inrichten en na verificatie gebruikers automatisch in de toepassing gemaakt worden.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-221">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1a1d2-222">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a1d2-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1a1d2-223">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot eKincare.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eKincare.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="1a1d2-225">**Britta Simon om aan te wijzen eKincare, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1a1d2-225">**To assign Britta Simon to eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="1a1d2-226">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1a1d2-228">Selecteer in de lijst met toepassingen **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-228">In the applications list, select **eKincare**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_app.png) 

3. <span data-ttu-id="1a1d2-230">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="1a1d2-232">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-232">Click **Add** button.</span></span> <span data-ttu-id="1a1d2-233">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="1a1d2-235">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1a1d2-236">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1a1d2-237">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1a1d2-238">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1a1d2-238">Testing single sign-on</span></span>

<span data-ttu-id="1a1d2-239">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1a1d2-240">Als u op de tegel eKincare in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing eKincare.</span><span class="sxs-lookup"><span data-stu-id="1a1d2-240">When you click the eKincare tile in the Access Panel, you should get automatically signed-on to your eKincare application.</span></span>
<span data-ttu-id="1a1d2-241">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="1a1d2-241">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1a1d2-242">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1a1d2-242">Additional resources</span></span>

* [<span data-ttu-id="1a1d2-243">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a1d2-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1a1d2-244">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1a1d2-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_203.png

