---
title: 'Zelfstudie: Azure Active Directory-integratie met ADP Globalview | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en ADP Globalview.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: e9a5e65c484dfb98d1a7bc63d55f6ef92039554b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a><span data-ttu-id="7ca4f-103">Zelfstudie: Azure Active Directory-integratie met ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="7ca4f-103">Tutorial: Azure Active Directory integration with ADP Globalview</span></span>

<span data-ttu-id="7ca4f-104">In deze zelfstudie leert u hoe ADP Globalview integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7ca4f-104">In this tutorial, you learn how to integrate ADP Globalview with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7ca4f-105">ADP Globalview integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7ca4f-105">Integrating ADP Globalview with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7ca4f-106">U kunt beheren in Azure AD die toegang tot ADP Globalview heeft</span><span class="sxs-lookup"><span data-stu-id="7ca4f-106">You can control in Azure AD who has access to ADP Globalview</span></span>
- <span data-ttu-id="7ca4f-107">U kunt uw gebruikers automatisch ophalen aangemeld bij ADP Globalview (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="7ca4f-107">You can enable your users to automatically get signed-on to ADP Globalview (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7ca4f-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="7ca4f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7ca4f-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7ca4f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ca4f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7ca4f-110">Prerequisites</span></span>

<span data-ttu-id="7ca4f-111">Voor het configureren van Azure AD-integratie met ADP Globalview, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="7ca4f-111">To configure Azure AD integration with ADP Globalview, you need the following items:</span></span>

- <span data-ttu-id="7ca4f-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="7ca4f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7ca4f-113">Een ADP Globalview eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="7ca4f-113">An ADP Globalview single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7ca4f-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7ca4f-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="7ca4f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7ca4f-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7ca4f-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ca4f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7ca4f-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="7ca4f-118">Scenario description</span></span>
<span data-ttu-id="7ca4f-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7ca4f-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="7ca4f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7ca4f-121">ADP Globalview uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="7ca4f-121">Adding ADP Globalview from the gallery</span></span>
2. <span data-ttu-id="7ca4f-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7ca4f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-globalview-from-the-gallery"></a><span data-ttu-id="7ca4f-123">ADP Globalview uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="7ca4f-123">Adding ADP Globalview from the gallery</span></span>
<span data-ttu-id="7ca4f-124">Voor het configureren van de integratie van ADP Globalview in Azure AD, moet u ADP Globalview uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-124">To configure the integration of ADP Globalview into Azure AD, you need to add ADP Globalview from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7ca4f-125">**Als u wilt toevoegen ADP Globalview uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7ca4f-125">**To add ADP Globalview from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7ca4f-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7ca4f-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7ca4f-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="7ca4f-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="7ca4f-133">Typ in het zoekvak **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-133">In the search box, type **ADP Globalview**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_search.png)

5. <span data-ttu-id="7ca4f-135">Selecteer in het deelvenster resultaten **ADP Globalview**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-135">In the results panel, select **ADP Globalview**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7ca4f-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7ca4f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7ca4f-138">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met ADP Globalview op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="7ca4f-138">In this section, you configure and test Azure AD single sign-on with ADP Globalview based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7ca4f-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in ADP Globalview is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP Globalview is to a user in Azure AD.</span></span> <span data-ttu-id="7ca4f-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in ADP Globalview tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-140">In other words, a link relationship between an Azure AD user and the related user in ADP Globalview needs to be established.</span></span>

<span data-ttu-id="7ca4f-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP Globalview.</span></span>

<span data-ttu-id="7ca4f-142">Om te configureren en testen van Azure AD eenmalige aanmelding met ADP Globalview, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="7ca4f-142">To configure and test Azure AD single sign-on with ADP Globalview, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7ca4f-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7ca4f-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7ca4f-145">**[Maken van een testgebruiker ADP Globalview](#creating-an-adp-globalview-test-user)**  - ADP Globalview die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-145">**[Creating an ADP Globalview test user](#creating-an-adp-globalview-test-user)** - to have a counterpart of Britta Simon in ADP Globalview that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7ca4f-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7ca4f-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7ca4f-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="7ca4f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7ca4f-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing ADP Globalview configureren.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP Globalview application.</span></span>

<span data-ttu-id="7ca4f-150">**Voor het configureren van Azure AD eenmalige aanmelding met ADP Globalview, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7ca4f-150">**To configure Azure AD single sign-on with ADP Globalview, perform the following steps:**</span></span>

1. <span data-ttu-id="7ca4f-151">In de Azure-portal op de **ADP Globalview** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-151">In the Azure portal, on the **ADP Globalview** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="7ca4f-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_samlbase.png)

3. <span data-ttu-id="7ca4f-155">Op de **ADP Globalview domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7ca4f-155">On the **ADP Globalview Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_url.png)

     <span data-ttu-id="7ca4f-157">In de **id** textbox, typ een URL met het volgende patroon volgen: `https://<subdomain>.globalview.adp.com/federate` of`https://<subdomain>.globalview.adp.com/federate2`</span><span class="sxs-lookup"><span data-stu-id="7ca4f-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.globalview.adp.com/federate` or `https://<subdomain>.globalview.adp.com/federate2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7ca4f-158">De waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-158">The value is not real.</span></span> <span data-ttu-id="7ca4f-159">Werk de waarde met de werkelijke identificatie.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-159">Update the value with the actual Identifier.</span></span> <span data-ttu-id="7ca4f-160">Neem contact op met [ADP Globalview ondersteuning](https://www.adp.com/contact-us/overview.aspx) de waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-160">Contact [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to get the value.</span></span>
 
4. <span data-ttu-id="7ca4f-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_certificate.png) 

5. <span data-ttu-id="7ca4f-163">De toepassing ADP GlobalView verwacht de SAML-asserties in een specifieke indeling waarvoor u aangepaste kenmerktoewijzingen toevoegen aan uw configuratie van SAML-token kenmerken.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-163">The ADP GlobalView application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> 

6. <span data-ttu-id="7ca4f-164">De volgende Schermafbeelding toont een voorbeeld voor het.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-164">The following screenshot shows an example for it.</span></span> <span data-ttu-id="7ca4f-165">De namen van de claim worden altijd **'PersonImmutableID'** en de waarde die we hebben toegewezen aan ExtensionAttribute2 waarin de werknemer-id van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-165">The claim names always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2, which contains the EmployeeID of the user.</span></span> <span data-ttu-id="7ca4f-166">Hier de gebruiker toewijzen van Azure AD aan ADP GlobalView is uitgevoerd op de werknemer-id, maar u kunt deze toewijzen aan een andere waarde ook op basis van de toepassingsinstellingen van uw.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-166">Here the user mapping from Azure AD to ADP GlobalView is done on the EmployeeID but you can map it to a different value also based on your application settings.</span></span> <span data-ttu-id="7ca4f-167">U kunt werken met het ADP GlobalView team eerst gebruikt u de juiste id van een gebruiker en wijs die waarde met de **'PersonImmutableID'** claim.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-167">You can work with the ADP GlobalView team first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span> <span data-ttu-id="7ca4f-168">U kunt ook de e-mail en UserID claim toewijzen zoals weergegeven in de afbeelding.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-168">You can also map the Email and UserID claim as shown in the picture.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_attribute.png)

7. <span data-ttu-id="7ca4f-170">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding en de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7ca4f-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="7ca4f-171">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="7ca4f-171">Attribute Name</span></span> | <span data-ttu-id="7ca4f-172">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="7ca4f-172">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="7ca4f-173">personalimmutableid</span><span class="sxs-lookup"><span data-stu-id="7ca4f-173">personalimmutableid</span></span> | <span data-ttu-id="7ca4f-174">User.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="7ca4f-174">user.extensionattribute2</span></span> |
    | <span data-ttu-id="7ca4f-175">E-mail</span><span class="sxs-lookup"><span data-stu-id="7ca4f-175">email</span></span>               | <span data-ttu-id="7ca4f-176">User.mail</span><span class="sxs-lookup"><span data-stu-id="7ca4f-176">user.mail</span></span> |
    | <span data-ttu-id="7ca4f-177">gebruikers-id</span><span class="sxs-lookup"><span data-stu-id="7ca4f-177">userid</span></span>              | <span data-ttu-id="7ca4f-178">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="7ca4f-178">user.userprincipalname</span></span>|
    
    <span data-ttu-id="7ca4f-179">a.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-179">a.</span></span> <span data-ttu-id="7ca4f-180">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-180">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="7ca4f-183">b.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-183">b.</span></span> <span data-ttu-id="7ca4f-184">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="7ca4f-185">c.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-185">c.</span></span> <span data-ttu-id="7ca4f-186">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-186">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7ca4f-187">d.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-187">d.</span></span> <span data-ttu-id="7ca4f-188">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-188">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7ca4f-189">Voordat u de SAML-bevestiging configureren kunt, moet u contact op met uw [ADP Globalview ondersteuning](https://www.adp.com/contact-us/overview.aspx) en vraagt u de waarde van het kenmerk unieke id voor uw tenant.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-189">Before you can configure the SAML assertion, you need to contact your [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="7ca4f-190">U moet deze waarde voor het configureren van de aangepaste claim voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-190">You need this value to configure the custom claim for your application.</span></span> 

8. <span data-ttu-id="7ca4f-191">Op de **ADP Globalview configuratie** sectie, klikt u op **configureren ADP Globalview** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-191">On the **ADP Globalview Configuration** section, click **Configure ADP Globalview** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7ca4f-192">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="7ca4f-192">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_configure.png) 

9. <span data-ttu-id="7ca4f-194">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-194">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adglobalview-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="7ca4f-196">Eenmalige aanmelding configureren op **ADP Globalview** zijde, moet u de gedownloade verzenden **certificaat (Base64)**, **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** naar [ADP Globalview ondersteuning](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ca4f-196">To configure single sign-on on **ADP Globalview** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="7ca4f-197">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="7ca4f-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7ca4f-198">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7ca4f-199">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7ca4f-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7ca4f-200">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="7ca4f-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="7ca4f-201">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="7ca4f-203">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7ca4f-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7ca4f-204">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="7ca4f-206">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7ca4f-208">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7ca4f-210">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7ca4f-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7ca4f-212">a.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-212">a.</span></span> <span data-ttu-id="7ca4f-213">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7ca4f-214">b.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-214">b.</span></span> <span data-ttu-id="7ca4f-215">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7ca4f-216">c.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-216">c.</span></span> <span data-ttu-id="7ca4f-217">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7ca4f-218">d.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-218">d.</span></span> <span data-ttu-id="7ca4f-219">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-219">Click **Create**.</span></span>
 
### <a name="creating-an-adp-globalview-test-user"></a><span data-ttu-id="7ca4f-220">Een testgebruiker ADP Globalview maken</span><span class="sxs-lookup"><span data-stu-id="7ca4f-220">Creating an ADP Globalview test user</span></span>

<span data-ttu-id="7ca4f-221">Het doel van deze sectie is het maken van een gebruiker Britta Simon in ADP GlobalView genoemd.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-221">The objective of this section is to create a user called Britta Simon in ADP GlobalView.</span></span> <span data-ttu-id="7ca4f-222">Werken met [ADP Globalview ondersteuning](https://www.adp.com/contact-us/overview.aspx) de gebruikers in het account ADP GlobalView toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-222">Work with [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP GlobalView account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7ca4f-223">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ca4f-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7ca4f-224">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP Globalview.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="7ca4f-226">**Britta Simon om aan te wijzen ADP Globalview, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7ca4f-226">**To assign Britta Simon to ADP Globalview, perform the following steps:**</span></span>

1. <span data-ttu-id="7ca4f-227">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="7ca4f-229">Selecteer in de lijst met toepassingen **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-229">In the applications list, select **ADP Globalview**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_app.png) 

3. <span data-ttu-id="7ca4f-231">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="7ca4f-233">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-233">Click **Add** button.</span></span> <span data-ttu-id="7ca4f-234">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="7ca4f-236">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7ca4f-237">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7ca4f-238">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7ca4f-239">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7ca4f-239">Testing single sign-on</span></span>

<span data-ttu-id="7ca4f-240">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-240">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="7ca4f-241">Als u op de tegel ADP GlobalView in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="7ca4f-241">When you click the ADP GlobalView tile in the Access Panel, you should get automatically signed-on to your ADP GlobalView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7ca4f-242">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7ca4f-242">Additional resources</span></span>

* [<span data-ttu-id="7ca4f-243">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ca4f-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7ca4f-244">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7ca4f-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_203.png

