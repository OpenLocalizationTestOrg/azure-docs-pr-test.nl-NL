---
title: 'Zelfstudie: Azure Active Directory-integratie met BenefitHub | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en BenefitHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 8df9c0d8443d6685253207ed1915c780275014fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a><span data-ttu-id="38858-103">Zelfstudie: Azure Active Directory-integratie met BenefitHub</span><span class="sxs-lookup"><span data-stu-id="38858-103">Tutorial: Azure Active Directory integration with BenefitHub</span></span>

<span data-ttu-id="38858-104">In deze zelfstudie leert u hoe BenefitHub integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="38858-104">In this tutorial, you learn how to integrate BenefitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="38858-105">BenefitHub integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="38858-105">Integrating BenefitHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="38858-106">U kunt beheren in Azure AD die toegang tot BenefitHub heeft</span><span class="sxs-lookup"><span data-stu-id="38858-106">You can control in Azure AD who has access to BenefitHub</span></span>
- <span data-ttu-id="38858-107">U kunt uw gebruikers automatisch ophalen aangemeld bij BenefitHub (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="38858-107">You can enable your users to automatically get signed-on to BenefitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="38858-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="38858-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="38858-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="38858-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38858-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="38858-110">Prerequisites</span></span>

<span data-ttu-id="38858-111">Voor het configureren van Azure AD-integratie met BenefitHub, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="38858-111">To configure Azure AD integration with BenefitHub, you need the following items:</span></span>

- <span data-ttu-id="38858-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="38858-112">An Azure AD subscription</span></span>
- <span data-ttu-id="38858-113">Een BenefitHub eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="38858-113">A BenefitHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="38858-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="38858-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="38858-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="38858-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="38858-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="38858-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="38858-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="38858-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="38858-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="38858-118">Scenario description</span></span>
<span data-ttu-id="38858-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="38858-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="38858-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="38858-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="38858-121">BenefitHub uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="38858-121">Adding BenefitHub from the gallery</span></span>
2. <span data-ttu-id="38858-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="38858-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefithub-from-the-gallery"></a><span data-ttu-id="38858-123">BenefitHub uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="38858-123">Adding BenefitHub from the gallery</span></span>
<span data-ttu-id="38858-124">Voor het configureren van de integratie van BenefitHub in Azure AD, moet u BenefitHub uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="38858-124">To configure the integration of BenefitHub into Azure AD, you need to add BenefitHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="38858-125">**Als u wilt toevoegen BenefitHub uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="38858-125">**To add BenefitHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="38858-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="38858-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="38858-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="38858-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="38858-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="38858-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="38858-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="38858-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="38858-133">Typ in het zoekvak **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="38858-133">In the search box, type **BenefitHub**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_search.png)

5. <span data-ttu-id="38858-135">Selecteer in het deelvenster resultaten **BenefitHub**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="38858-135">In the results panel, select **BenefitHub**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="38858-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="38858-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="38858-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met BenefitHub op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="38858-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="38858-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in BenefitHub is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38858-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenefitHub is to a user in Azure AD.</span></span> <span data-ttu-id="38858-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in BenefitHub tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="38858-140">In other words, a link relationship between an Azure AD user and the related user in BenefitHub needs to be established.</span></span>

<span data-ttu-id="38858-141">Wijs in BenefitHub, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="38858-141">In BenefitHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="38858-142">Om te configureren en testen van Azure AD eenmalige aanmelding met BenefitHub, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="38858-142">To configure and test Azure AD single sign-on with BenefitHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="38858-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="38858-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="38858-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="38858-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="38858-145">**[Maken van een testgebruiker BenefitHub](#creating-a-benefithub-test-user)**  - BenefitHub die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="38858-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - to have a counterpart of Britta Simon in BenefitHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="38858-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="38858-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="38858-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="38858-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="38858-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="38858-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="38858-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing BenefitHub configureren.</span><span class="sxs-lookup"><span data-stu-id="38858-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenefitHub application.</span></span>

<span data-ttu-id="38858-150">**Voor het configureren van Azure AD eenmalige aanmelding met BenefitHub, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="38858-150">**To configure Azure AD single sign-on with BenefitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="38858-151">In de Azure-portal op de **BenefitHub** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="38858-151">In the Azure portal, on the **BenefitHub** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="38858-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="38858-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_samlbase.png)

3. <span data-ttu-id="38858-155">Op de **BenefitHub domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="38858-155">On the **BenefitHub Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_url1.png)
  
    <span data-ttu-id="38858-157">a.</span><span class="sxs-lookup"><span data-stu-id="38858-157">a.</span></span> <span data-ttu-id="38858-158">In de **id** textbox, type:`urn:benefithub:passport`</span><span class="sxs-lookup"><span data-stu-id="38858-158">In the **Identifier** textbox, type: `urn:benefithub:passport`</span></span>
    
    <span data-ttu-id="38858-159">b.</span><span class="sxs-lookup"><span data-stu-id="38858-159">b.</span></span> <span data-ttu-id="38858-160">In de **antwoord-URL** textbox, type:`https://passport.benefithub.info/saml/post/ac`</span><span class="sxs-lookup"><span data-stu-id="38858-160">In the **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span></span>

4. <span data-ttu-id="38858-161">De toepassing BenefitHub verwacht de SAML-asserties in een specifieke indeling waarvoor u aangepaste kenmerktoewijzingen toevoegen aan uw configuratie van SAML-token kenmerken.</span><span class="sxs-lookup"><span data-stu-id="38858-161">The BenefitHub application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="38858-162">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="38858-162">Configure the following claims for this application.</span></span> <span data-ttu-id="38858-163">U kunt beheren de waarden van deze kenmerken van de '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="38858-163">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_attribute.png)

5. <span data-ttu-id="38858-165">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de voorgaande afbeelding en de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="38858-165">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="38858-166">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="38858-166">Attribute Name</span></span> | <span data-ttu-id="38858-167">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="38858-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="38858-168">OrganizationId</span><span class="sxs-lookup"><span data-stu-id="38858-168">organizationid</span></span> | <span data-ttu-id="38858-169">< organizationid ></span><span class="sxs-lookup"><span data-stu-id="38858-169">< organizationid ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="38858-170">De waarde van dit kenmerk is niet echt.</span><span class="sxs-lookup"><span data-stu-id="38858-170">This attribute value is not real.</span></span> <span data-ttu-id="38858-171">Deze waarde met de werkelijke organizationid bijwerken.</span><span class="sxs-lookup"><span data-stu-id="38858-171">Update this value with actual organizationid.</span></span> <span data-ttu-id="38858-172">Neem contact op met [BenefitHub ondersteuningsteam](https://www.benefithub.com/Home/ContactUs) ophalen van de werkelijke organizationid.</span><span class="sxs-lookup"><span data-stu-id="38858-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to get the actual organizationid.</span></span>
    
    <span data-ttu-id="38858-173">a.</span><span class="sxs-lookup"><span data-stu-id="38858-173">a.</span></span> <span data-ttu-id="38858-174">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="38858-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="38858-177">b.</span><span class="sxs-lookup"><span data-stu-id="38858-177">b.</span></span> <span data-ttu-id="38858-178">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="38858-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="38858-179">c.</span><span class="sxs-lookup"><span data-stu-id="38858-179">c.</span></span> <span data-ttu-id="38858-180">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="38858-180">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="38858-181">d.</span><span class="sxs-lookup"><span data-stu-id="38858-181">d.</span></span> <span data-ttu-id="38858-182">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="38858-182">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="38858-183">Voordat u de SAML-bevestiging configureren kunt, moet u contact op met uw [BenefitHub ondersteuning](https://www.benefithub.com/Home/ContactUs) en vraagt u de waarde van het kenmerk unieke id voor uw tenant.</span><span class="sxs-lookup"><span data-stu-id="38858-183">Before you can configure the SAML assertion, you need to contact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="38858-184">U moet deze waarde voor het configureren van de aangepaste claim voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="38858-184">You need this value to configure the custom claim for your application.</span></span>

6. <span data-ttu-id="38858-185">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="38858-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_certificate.png) 

7. <span data-ttu-id="38858-187">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="38858-187">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefithub-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="38858-189">Eenmalige aanmelding configureren op **BenefitHub** zijde, moet u de gedownloade verzenden **Metadata XML** naar [BenefitHub ondersteuningsteam](https://www.benefithub.com/Home/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="38858-189">To configure single sign-on on **BenefitHub** side, you need to send the downloaded **Metadata XML** to [BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span></span> <span data-ttu-id="38858-190">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="38858-190">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="38858-191">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="38858-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="38858-192">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="38858-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="38858-193">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="38858-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="38858-194">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="38858-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="38858-195">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="38858-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="38858-197">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="38858-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="38858-198">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="38858-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benefithub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="38858-200">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="38858-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benefithub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="38858-202">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="38858-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benefithub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="38858-204">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="38858-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benefithub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="38858-206">a.</span><span class="sxs-lookup"><span data-stu-id="38858-206">a.</span></span> <span data-ttu-id="38858-207">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="38858-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="38858-208">b.</span><span class="sxs-lookup"><span data-stu-id="38858-208">b.</span></span> <span data-ttu-id="38858-209">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="38858-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="38858-210">c.</span><span class="sxs-lookup"><span data-stu-id="38858-210">c.</span></span> <span data-ttu-id="38858-211">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="38858-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="38858-212">d.</span><span class="sxs-lookup"><span data-stu-id="38858-212">d.</span></span> <span data-ttu-id="38858-213">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="38858-213">Click **Create**.</span></span>
 
### <a name="creating-a-benefithub-test-user"></a><span data-ttu-id="38858-214">Een testgebruiker BenefitHub maken</span><span class="sxs-lookup"><span data-stu-id="38858-214">Creating a BenefitHub test user</span></span>

<span data-ttu-id="38858-215">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in BenefitHub maken.</span><span class="sxs-lookup"><span data-stu-id="38858-215">In this section, you create a user called Britta Simon in BenefitHub.</span></span> <span data-ttu-id="38858-216">Werken met [BenefitHub ondersteuningsteam](https://www.benefithub.com/Home/ContactUs) de gebruikers van het platform BenefitHub toevoegen.</span><span class="sxs-lookup"><span data-stu-id="38858-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add the users in the BenefitHub platform.</span></span> <span data-ttu-id="38858-217">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="38858-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="38858-218">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="38858-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="38858-219">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="38858-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenefitHub.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="38858-221">**Britta Simon om aan te wijzen BenefitHub, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="38858-221">**To assign Britta Simon to BenefitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="38858-222">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="38858-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="38858-224">Selecteer in de lijst met toepassingen **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="38858-224">In the applications list, select **BenefitHub**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_app.png) 

3. <span data-ttu-id="38858-226">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="38858-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="38858-228">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="38858-228">Click **Add** button.</span></span> <span data-ttu-id="38858-229">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="38858-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="38858-231">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="38858-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="38858-232">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="38858-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="38858-233">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="38858-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="38858-234">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="38858-234">Testing single sign-on</span></span>

<span data-ttu-id="38858-235">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="38858-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="38858-236">Als u op de tegel BenefitHub in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="38858-236">When you click the BenefitHub tile in the Access Panel, you should get automatically signed-on to your BenefitHub application.</span></span>
<span data-ttu-id="38858-237">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="38858-237">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="38858-238">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="38858-238">Additional resources</span></span>

* [<span data-ttu-id="38858-239">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="38858-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="38858-240">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="38858-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_203.png

