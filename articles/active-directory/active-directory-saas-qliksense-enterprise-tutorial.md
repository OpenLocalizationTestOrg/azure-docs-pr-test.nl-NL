---
title: 'Zelfstudie: Azure Active Directory-integratie met Qlik zin Enterprise | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Qlik zin Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 4964634cd5aaf0dbb98c766f5e12700c4d118750
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="63fb0-103">Zelfstudie: Azure Active Directory-integratie met Qlik zin Enterprise</span><span class="sxs-lookup"><span data-stu-id="63fb0-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="63fb0-104">In deze zelfstudie leert u hoe Qlik zin Enterprise integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="63fb0-104">In this tutorial, you learn how to integrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="63fb0-105">Qlik zin Enterprise integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="63fb0-105">Integrating Qlik Sense Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="63fb0-106">U kunt beheren in Azure AD die toegang tot Qlik zin Enterprise heeft.</span><span class="sxs-lookup"><span data-stu-id="63fb0-106">You can control in Azure AD who has access to Qlik Sense Enterprise.</span></span>
- <span data-ttu-id="63fb0-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Qlik zin Enterprise (Single Sign-On) inschakelen met hun Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="63fb0-107">You can enable your users to automatically get signed-on to Qlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="63fb0-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="63fb0-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="63fb0-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="63fb0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63fb0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="63fb0-110">Prerequisites</span></span>

<span data-ttu-id="63fb0-111">Voor het configureren van Azure AD-integratie met Qlik zin voor ondernemingen, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="63fb0-111">To configure Azure AD integration with Qlik Sense Enterprise, you need the following items:</span></span>

- <span data-ttu-id="63fb0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="63fb0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="63fb0-113">Een Qlik zin Enterprise eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="63fb0-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="63fb0-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="63fb0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="63fb0-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="63fb0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="63fb0-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="63fb0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="63fb0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="63fb0-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="63fb0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="63fb0-118">Scenario description</span></span>
<span data-ttu-id="63fb0-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="63fb0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="63fb0-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="63fb0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="63fb0-121">Qlik zin Enterprise uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="63fb0-121">Adding Qlik Sense Enterprise from the gallery</span></span>
2. <span data-ttu-id="63fb0-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="63fb0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-the-gallery"></a><span data-ttu-id="63fb0-123">Qlik zin Enterprise uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="63fb0-123">Adding Qlik Sense Enterprise from the gallery</span></span>
<span data-ttu-id="63fb0-124">Voor het configureren van de integratie van Qlik zin Enterprise in Azure AD, moet u Qlik zin Enterprise uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="63fb0-124">To configure the integration of Qlik Sense Enterprise into Azure AD, you need to add Qlik Sense Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="63fb0-125">**Als u wilt toevoegen Qlik zin Enterprise uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="63fb0-125">**To add Qlik Sense Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="63fb0-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="63fb0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="63fb0-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="63fb0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="63fb0-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="63fb0-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="63fb0-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="63fb0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="63fb0-133">Typ in het zoekvak **Qlik zin Enterprise**, selecteer **Qlik zin Enterprise** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="63fb0-133">In the search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button to add the application.</span></span>

    ![Qlik zin onderneming in de lijst met resultaten](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="63fb0-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="63fb0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="63fb0-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Qlik zin Enterprise op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="63fb0-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="63fb0-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Qlik zin onderneming is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63fb0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Qlik Sense Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="63fb0-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Qlik zin onderneming tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="63fb0-138">In other words, a link relationship between an Azure AD user and the related user in Qlik Sense Enterprise needs to be established.</span></span>

<span data-ttu-id="63fb0-139">Wijs in Qlik zin Enterprise, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="63fb0-139">In Qlik Sense Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="63fb0-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Qlik zin voor ondernemingen, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="63fb0-140">To configure and test Azure AD single sign-on with Qlik Sense Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="63fb0-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="63fb0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="63fb0-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="63fb0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="63fb0-143">**[Maak een testgebruiker Qlik zin Enterprise](#create-a-qlik-sense-enterprise-test-user)**  - Qlik zin Enterprise die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="63fb0-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - to have a counterpart of Britta Simon in Qlik Sense Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="63fb0-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="63fb0-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="63fb0-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="63fb0-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="63fb0-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="63fb0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="63fb0-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Qlik zin Enterprise.</span><span class="sxs-lookup"><span data-stu-id="63fb0-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="63fb0-148">**Voor het configureren van Azure AD eenmalige aanmelding met Qlik zin voor ondernemingen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="63fb0-148">**To configure Azure AD single sign-on with Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="63fb0-149">In de Azure-portal op de **Qlik zin Enterprise** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="63fb0-149">In the Azure portal, on the **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="63fb0-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="63fb0-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="63fb0-153">Op de **Qlik zin Enterprise domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="63fb0-153">On the **Qlik Sense Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![URL's en Qlik zin Enterprise domein eenmalige aanmelding informatie](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="63fb0-155">a.</span><span class="sxs-lookup"><span data-stu-id="63fb0-155">a.</span></span> <span data-ttu-id="63fb0-156">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span><span class="sxs-lookup"><span data-stu-id="63fb0-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="63fb0-157">Noteer de afsluitende slash aan het einde van deze URI.</span><span class="sxs-lookup"><span data-stu-id="63fb0-157">Note the trailing slash at the end of this URI.</span></span> <span data-ttu-id="63fb0-158">Dit is vereist.</span><span class="sxs-lookup"><span data-stu-id="63fb0-158">It is required.</span></span>
    
    <span data-ttu-id="63fb0-159">b.</span><span class="sxs-lookup"><span data-stu-id="63fb0-159">b.</span></span> <span data-ttu-id="63fb0-160">In de **id** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="63fb0-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > <span data-ttu-id="63fb0-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="63fb0-161">These values are not real.</span></span> <span data-ttu-id="63fb0-162">Bijwerken van deze waarden met de werkelijke aanmeldings-URL en de id, die worden beschreven verderop in deze zelfstudie of neem contact op met [Qlik zin Enterprise Client ondersteuningsteam](https://www.qlik.com/us/services/support) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="63fb0-162">Update these values with the actual Sign-On URL and Identifier, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to get these values.</span></span> 

4. <span data-ttu-id="63fb0-163">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="63fb0-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. <span data-ttu-id="63fb0-165">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="63fb0-165">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="63fb0-167">Bereid het federatieve metagegevens-XML-bestand zodat u die naar Qlik zin-server uploaden kunt.</span><span class="sxs-lookup"><span data-stu-id="63fb0-167">Prepare the Federation Metadata XML file so that you can upload that to Qlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="63fb0-168">Voordat u de metagegevens van de IdP uploadt naar de server Qlik zin, het bestand moet worden bewerkt om informatie om te controleren of de juiste werking tussen Azure AD te verwijderen en Qlik zin-server.</span><span class="sxs-lookup"><span data-stu-id="63fb0-168">Before uploading the IdP metadata to the Qlik Sense server, the file needs to be edited to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>
    
    ![QlikSense][qs24]
   
    <span data-ttu-id="63fb0-170">a.</span><span class="sxs-lookup"><span data-stu-id="63fb0-170">a.</span></span> <span data-ttu-id="63fb0-171">Open het bestand FederationMetaData.xml, dat u hebt gedownload vanuit Azure-portal in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="63fb0-171">Open the FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>
   
    <span data-ttu-id="63fb0-172">b.</span><span class="sxs-lookup"><span data-stu-id="63fb0-172">b.</span></span> <span data-ttu-id="63fb0-173">Zoeken naar de waarde **RoleDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="63fb0-173">Search for the value **RoleDescriptor**.</span></span>  <span data-ttu-id="63fb0-174">Er zijn vier gegevens (twee paren openen en sluiten elementlabels).</span><span class="sxs-lookup"><span data-stu-id="63fb0-174">There are four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="63fb0-175">c.</span><span class="sxs-lookup"><span data-stu-id="63fb0-175">c.</span></span> <span data-ttu-id="63fb0-176">De codes RoleDescriptor en alle informatie daartussen uit het bestand verwijderen.</span><span class="sxs-lookup"><span data-stu-id="63fb0-176">Delete the RoleDescriptor tags and all information in between from the file.</span></span>
   
    <span data-ttu-id="63fb0-177">d.</span><span class="sxs-lookup"><span data-stu-id="63fb0-177">d.</span></span> <span data-ttu-id="63fb0-178">Sla het bestand en het in de buurt te houden voor gebruik verderop in dit document.</span><span class="sxs-lookup"><span data-stu-id="63fb0-178">Save the file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="63fb0-179">Navigeer naar de Qlik zin Qlik Management Console (QMC) als een gebruiker die virtuele proxyconfiguraties kunt maken.</span><span class="sxs-lookup"><span data-stu-id="63fb0-179">Navigate to the Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="63fb0-180">Klik in de QMC op de **virtuele proxy's** menu-item.</span><span class="sxs-lookup"><span data-stu-id="63fb0-180">In the QMC, click on the **Virtual Proxies** menu item.</span></span>
   
    ![QlikSense][qs6] 

9. <span data-ttu-id="63fb0-182">Aan de onderkant van het scherm, klikt u op de **nieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="63fb0-182">At the bottom of the screen, click the **Create new** button.</span></span>
   
    ![QlikSense][qs7]

10. <span data-ttu-id="63fb0-184">Het scherm virtuele proxy bewerken wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="63fb0-184">The Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="63fb0-185">Aan de rechterkant van het scherm wordt een menu voor het zichtbaar maken van configuratie-opties.</span><span class="sxs-lookup"><span data-stu-id="63fb0-185">On the right side of the screen is a menu for making configuration options visible.</span></span>
   
    ![QlikSense][qs9]

11. <span data-ttu-id="63fb0-187">Voer de gegevens voor de virtuele Azure-proxy-configuratie met de id-menuoptie gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="63fb0-187">With the Identification menu option checked, enter the identifying information for the Azure virtual proxy configuration.</span></span>
    
    ![QlikSense][qs8]  
    
    <span data-ttu-id="63fb0-189">a.</span><span class="sxs-lookup"><span data-stu-id="63fb0-189">a.</span></span> <span data-ttu-id="63fb0-190">De **beschrijving** veld is een beschrijvende naam voor de virtuele-proxyconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="63fb0-190">The **Description** field is a friendly name for the virtual proxy configuration.</span></span>  <span data-ttu-id="63fb0-191">Voer een waarde voor een beschrijving.</span><span class="sxs-lookup"><span data-stu-id="63fb0-191">Enter a value for a description.</span></span>
    
    <span data-ttu-id="63fb0-192">b.</span><span class="sxs-lookup"><span data-stu-id="63fb0-192">b.</span></span> <span data-ttu-id="63fb0-193">De **voorvoegsel** veld identificeert het eindpunt van de virtuele proxy voor het verbinden met Qlik zin met Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="63fb0-193">The **Prefix** field identifies the virtual proxy endpoint for connecting to Qlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="63fb0-194">Voer een naam uniek voorvoegsel voor deze virtuele proxy.</span><span class="sxs-lookup"><span data-stu-id="63fb0-194">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="63fb0-195">c.</span><span class="sxs-lookup"><span data-stu-id="63fb0-195">c.</span></span> <span data-ttu-id="63fb0-196">**Time-out voor inactiviteit sessie (minuten)** is de time-out voor verbindingen via deze virtuele proxy.</span><span class="sxs-lookup"><span data-stu-id="63fb0-196">**Session inactivity timeout (minutes)** is the timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="63fb0-197">d.</span><span class="sxs-lookup"><span data-stu-id="63fb0-197">d.</span></span> <span data-ttu-id="63fb0-198">De **cookie-kop sessienaam** is de naam van de cookie voor het opslaan van de sessie-id voor de sessie Qlik zin is een gebruiker na een geslaagde authenticatie ontvangt.</span><span class="sxs-lookup"><span data-stu-id="63fb0-198">The **Session cookie header name** is the cookie name storing the session identifier for the Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="63fb0-199">Deze naam moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="63fb0-199">This name must be unique.</span></span>

12. <span data-ttu-id="63fb0-200">Klik op de menuoptie verificatie zichtbaar te maken.</span><span class="sxs-lookup"><span data-stu-id="63fb0-200">Click on the Authentication menu option to make it visible.</span></span>  <span data-ttu-id="63fb0-201">De verificatie-scherm wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="63fb0-201">The Authentication screen appears.</span></span>
    
    ![QlikSense][qs10]
    
    <span data-ttu-id="63fb0-203">a.</span><span class="sxs-lookup"><span data-stu-id="63fb0-203">a.</span></span> <span data-ttu-id="63fb0-204">De **anonieme toegangsmodus** vervolgkeuzelijst bepaalt als anonieme gebruikers toegang Qlik zin via de virtuele-proxy tot mogelijk.</span><span class="sxs-lookup"><span data-stu-id="63fb0-204">The **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through the virtual proxy.</span></span>  <span data-ttu-id="63fb0-205">De standaardoptie is geen anonieme gebruiker.</span><span class="sxs-lookup"><span data-stu-id="63fb0-205">The default option is No anonymous user.</span></span>
    
    <span data-ttu-id="63fb0-206">b.</span><span class="sxs-lookup"><span data-stu-id="63fb0-206">b.</span></span> <span data-ttu-id="63fb0-207">De **verificatiemethode** vervolgkeuzelijst bepaalt het verificatieschema dat de virtuele-proxy wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="63fb0-207">The **Authentication method** drop-down determines the authentication scheme the virtual proxy will use.</span></span>  <span data-ttu-id="63fb0-208">Selecteer SAML in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="63fb0-208">Select SAML from the drop-down list.</span></span>  <span data-ttu-id="63fb0-209">Meer opties als gevolg hiervan worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="63fb0-209">More options appear as a result.</span></span>
    
    <span data-ttu-id="63fb0-210">c.</span><span class="sxs-lookup"><span data-stu-id="63fb0-210">c.</span></span> <span data-ttu-id="63fb0-211">In de **SAML host URI veld**, voer de gebruikers van de hostnaam invoeren voor toegang tot Qlik zin via deze virtuele SAML-proxy.</span><span class="sxs-lookup"><span data-stu-id="63fb0-211">In the **SAML host URI field**, input the hostname users enter to access Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="63fb0-212">De hostnaam is de uri van de server Qlik zin.</span><span class="sxs-lookup"><span data-stu-id="63fb0-212">The hostname is the uri of the Qlik Sense server.</span></span>
    
    <span data-ttu-id="63fb0-213">d.</span><span class="sxs-lookup"><span data-stu-id="63fb0-213">d.</span></span> <span data-ttu-id="63fb0-214">In de **SAML entiteit-ID**, voert u de dezelfde waarde die is ingevoerd voor het veld SAML host URI.</span><span class="sxs-lookup"><span data-stu-id="63fb0-214">In the **SAML entity ID**, enter the same value entered for the SAML host URI field.</span></span>
    
    <span data-ttu-id="63fb0-215">e.</span><span class="sxs-lookup"><span data-stu-id="63fb0-215">e.</span></span> <span data-ttu-id="63fb0-216">De **SAML IdP metagegevens** is het bestand bewerkt eerder in de **Federatiemetagegevens van Azure AD-configuratie bewerken** sectie.</span><span class="sxs-lookup"><span data-stu-id="63fb0-216">The **SAML IdP metadata** is the file edited earlier in the **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="63fb0-217">**Voordat u uploadt de IdP-metagegevens, het bestand moet worden bewerkt** gegevens om te controleren of de juiste werking tussen Azure AD te verwijderen en Qlik zin-server.</span><span class="sxs-lookup"><span data-stu-id="63fb0-217">**Before uploading the IdP metadata, the file needs to be edited** to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="63fb0-218">**Raadpleeg de bovenstaande instructies als het bestand nog heeft moeten worden bewerkt.**</span><span class="sxs-lookup"><span data-stu-id="63fb0-218">**Please refer to the instructions above if the file has yet to be edited.**</span></span>  <span data-ttu-id="63fb0-219">Klik op de knop Bladeren en selecteer vervolgens het bewerkte metagegevensbestand te uploaden naar de virtuele-proxyconfiguratie als het bestand is bewerkt.</span><span class="sxs-lookup"><span data-stu-id="63fb0-219">If the file has been edited click on the Browse button and select the edited metadata file to upload it to the virtual proxy configuration.</span></span>
    
    <span data-ttu-id="63fb0-220">f.</span><span class="sxs-lookup"><span data-stu-id="63fb0-220">f.</span></span> <span data-ttu-id="63fb0-221">Voer in de kenmerkverwijzing naam of het schema voor de SAML-kenmerk voor de **UserID** Azure AD naar de server Qlik zin verzendt.</span><span class="sxs-lookup"><span data-stu-id="63fb0-221">Enter the attribute name or schema reference for the SAML attribute representing the **UserID** Azure AD sends to the Qlik Sense server.</span></span>  <span data-ttu-id="63fb0-222">Schema referentie-informatie is beschikbaar in de configuratie van Azure app schermen post.</span><span class="sxs-lookup"><span data-stu-id="63fb0-222">Schema reference information is available in the Azure app screens post configuration.</span></span>  <span data-ttu-id="63fb0-223">Voer voor het gebruik van het kenmerk name `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="63fb0-223">To use the name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="63fb0-224">g.</span><span class="sxs-lookup"><span data-stu-id="63fb0-224">g.</span></span> <span data-ttu-id="63fb0-225">Voer de waarde voor de **gebruikerslijst** die wordt gekoppeld aan gebruikers wanneer ze zich met Qlik zin server via Azure AD verifiëren.</span><span class="sxs-lookup"><span data-stu-id="63fb0-225">Enter the value for the **user directory** that will be attached to users when they authenticate to Qlik Sense server through Azure AD.</span></span>  <span data-ttu-id="63fb0-226">Hardcoded waarden moeten worden omgeven door **vierkante haakjes []**.</span><span class="sxs-lookup"><span data-stu-id="63fb0-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="63fb0-227">Voor het gebruik van een kenmerk in de Azure AD SAML-bevestiging verzonden, voert u de naam van het kenmerk in dit tekstvak **zonder** vierkante haken.</span><span class="sxs-lookup"><span data-stu-id="63fb0-227">To use an attribute sent in the Azure AD SAML assertion, enter the name of the attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="63fb0-228">h.</span><span class="sxs-lookup"><span data-stu-id="63fb0-228">h.</span></span> <span data-ttu-id="63fb0-229">De **SAML-ondertekeningsalgoritme** Hiermee stelt u de serviceprovider (in dit geval Qlik zin server) voor Certificaatondertekening voor de virtuele-proxyconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="63fb0-229">The **SAML signing algorithm** sets the service provider (in this case Qlik Sense server) certificate signing for the virtual proxy configuration.</span></span>  <span data-ttu-id="63fb0-230">Als Qlik zin server gebruikmaakt van een vertrouwd certificaat gegenereerd met behulp van de Microsoft Enhanced RSA and AES Cryptographic Provider, wijzigt u de SAML-ondertekeningsalgoritme naar **SHA-256**.</span><span class="sxs-lookup"><span data-stu-id="63fb0-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change the SAML signing algorithm to **SHA-256**.</span></span>
    
    <span data-ttu-id="63fb0-231">ik.</span><span class="sxs-lookup"><span data-stu-id="63fb0-231">i.</span></span> <span data-ttu-id="63fb0-232">De SAML-kenmerk toewijzing sectie kan extra kenmerken zoals groepen worden verzonden naar Qlik zin voor gebruik in regels.</span><span class="sxs-lookup"><span data-stu-id="63fb0-232">The SAML attribute mapping section allows for additional attributes like groups to be sent to Qlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="63fb0-233">Klik op de **LOAD BALANCING** menuoptie zichtbaar te maken.</span><span class="sxs-lookup"><span data-stu-id="63fb0-233">Click on the **LOAD BALANCING** menu option to make it visible.</span></span>  <span data-ttu-id="63fb0-234">Het scherm Load Balancing wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="63fb0-234">The Load Balancing screen appears.</span></span>
    
    ![QlikSense][qs11]

14. <span data-ttu-id="63fb0-236">Klik op de **toevoegen nieuwe serverknooppunt** knop, selecteer engine knooppunt of knooppunten Qlik zin stuurt sessies laden voor taakverdeling doeleinden, en klik op de **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="63fb0-236">Click on the **Add new server node** button, select engine node or nodes Qlik Sense will send sessions to for load balancing purposes, and click the **Add** button.</span></span>
    
    ![QlikSense][qs12]

15. <span data-ttu-id="63fb0-238">Klik op de geavanceerde optie zichtbaar te maken.</span><span class="sxs-lookup"><span data-stu-id="63fb0-238">Click on the Advanced menu option to make it visible.</span></span> <span data-ttu-id="63fb0-239">Het geavanceerde scherm wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="63fb0-239">The Advanced screen appears.</span></span>
    
    ![QlikSense][qs13]
    
    <span data-ttu-id="63fb0-241">De Host witte lijst identificeert hostnamen die worden geaccepteerd wanneer ze verbinden met de server Qlik zin.</span><span class="sxs-lookup"><span data-stu-id="63fb0-241">The Host white list identifies hostnames that are accepted when connecting to the Qlik Sense server.</span></span>  <span data-ttu-id="63fb0-242">**Geef de hostnaam van de gebruikers wordt opgeven bij het verbinden met server Qlik zin.**</span><span class="sxs-lookup"><span data-stu-id="63fb0-242">**Enter the hostname users will specify when connecting to Qlik Sense server.**</span></span> <span data-ttu-id="63fb0-243">De hostnaam is dezelfde waarde als het SAML-uri die host zonder de https://.</span><span class="sxs-lookup"><span data-stu-id="63fb0-243">The hostname is the same value as the SAML host uri without the https://.</span></span>

16. <span data-ttu-id="63fb0-244">Klik op de **toepassen** knop.</span><span class="sxs-lookup"><span data-stu-id="63fb0-244">Click the **Apply** button.</span></span>
    
    ![QlikSense][qs14]

17. <span data-ttu-id="63fb0-246">Klik op OK accepteer het waarschuwingsbericht dat aangeeft proxy's die zijn gekoppeld aan de virtuele-proxy wordt opnieuw gestart.</span><span class="sxs-lookup"><span data-stu-id="63fb0-246">Click OK to accept the warning message that states proxies linked to the virtual proxy will be restarted.</span></span>
    
    ![QlikSense][qs15]

18. <span data-ttu-id="63fb0-248">Klik aan de rechterkant van het scherm de gekoppelde items menu wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="63fb0-248">On the right side of the screen, the Associated items menu appears.</span></span>  <span data-ttu-id="63fb0-249">Klik op de **proxy's** menuoptie.</span><span class="sxs-lookup"><span data-stu-id="63fb0-249">Click on the **Proxies** menu option.</span></span>
    
    ![QlikSense][qs16]

19. <span data-ttu-id="63fb0-251">De proxy-scherm wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="63fb0-251">The proxy screen appears.</span></span>  <span data-ttu-id="63fb0-252">Klik op de **koppeling** knop onder een proxy te koppelen aan de virtuele-proxy.</span><span class="sxs-lookup"><span data-stu-id="63fb0-252">Click the **Link** button at the bottom to link a proxy to the virtual proxy.</span></span>
    
    ![QlikSense][qs17]

20. <span data-ttu-id="63fb0-254">Selecteer de proxyknooppunt dat ondersteuning biedt voor deze virtuele proxyverbinding en klikt u op de **koppeling** knop.</span><span class="sxs-lookup"><span data-stu-id="63fb0-254">Select the proxy node that will support this virtual proxy connection and click the **Link** button.</span></span>  <span data-ttu-id="63fb0-255">Na het koppelen, wordt de proxy wordt vermeld onder de bijbehorende proxy's.</span><span class="sxs-lookup"><span data-stu-id="63fb0-255">After linking, the proxy will be listed under associated proxies.</span></span>
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. <span data-ttu-id="63fb0-258">Na ongeveer vijf tot tien seconden verschijnt het bericht QMC vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="63fb0-258">After about five to ten seconds, the Refresh QMC message will appear.</span></span>  <span data-ttu-id="63fb0-259">Klik op de **QMC vernieuwen** knop.</span><span class="sxs-lookup"><span data-stu-id="63fb0-259">Click the **Refresh QMC** button.</span></span>
    
    ![QlikSense][qs20]

22. <span data-ttu-id="63fb0-261">Wanneer de QMC is vernieuwd, klikt u op de **virtuele proxy's** menu-item.</span><span class="sxs-lookup"><span data-stu-id="63fb0-261">When the QMC refreshes, click on the **Virtual proxies** menu item.</span></span> <span data-ttu-id="63fb0-262">De nieuwe SAML virtuele proxy invoer wordt vermeld in de tabel op het scherm.</span><span class="sxs-lookup"><span data-stu-id="63fb0-262">The new SAML virtual proxy entry is listed in the table on the screen.</span></span>  <span data-ttu-id="63fb0-263">Één klik op de vermelding virtuele proxy.</span><span class="sxs-lookup"><span data-stu-id="63fb0-263">Single click on the virtual proxy entry.</span></span>
    
    ![QlikSense][qs51]

23. <span data-ttu-id="63fb0-265">Aan de onderkant van het scherm wordt de metagegevens-knop downloaden SP geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="63fb0-265">At the bottom of the screen, the Download SP metadata button will activate.</span></span>  <span data-ttu-id="63fb0-266">Klik op de **downloaden SP metagegevens** om op te slaan van de metagegevens naar een bestand.</span><span class="sxs-lookup"><span data-stu-id="63fb0-266">Click the **Download SP metadata** button to save the metadata to a file.</span></span>
    
    ![QlikSense][qs52]

24. <span data-ttu-id="63fb0-268">Open het metagegevensbestand van de serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="63fb0-268">Open the sp metadata file.</span></span>  <span data-ttu-id="63fb0-269">Houd rekening met de **id van de entiteit** vermelding en de **AssertionConsumerService** vermelding.</span><span class="sxs-lookup"><span data-stu-id="63fb0-269">Observe the **entityID** entry and the **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="63fb0-270">Deze waarden gelijk zijn aan de **id** en de **aanmelden URL** in de configuratie van de Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="63fb0-270">These values are equivalent to the **Identifier** and the **Sign on URL** in the Azure AD application configuration.</span></span> <span data-ttu-id="63fb0-271">Plak deze waarden in de **Qlik zin Enterprise domein en de URL's** sectie in de configuratie van de toepassing Azure AD als ze niet overeen komen en vervolgens u deze in de configuratiewizard van Azure AD-App vervangen moet.</span><span class="sxs-lookup"><span data-stu-id="63fb0-271">Paste these values in the **Qlik Sense Enterprise Domain and URLs** section in the Azure AD application configuration if they are not matching, then you should replace them in the Azure AD App configuration wizard.</span></span>
    
    ![QlikSense][qs53]

> [!TIP]
> <span data-ttu-id="63fb0-273">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="63fb0-273">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="63fb0-274">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="63fb0-274">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="63fb0-275">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="63fb0-275">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="63fb0-276">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="63fb0-276">Create an Azure AD test user</span></span>
<span data-ttu-id="63fb0-277">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="63fb0-277">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="63fb0-279">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="63fb0-279">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="63fb0-280">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="63fb0-280">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

   ![De Azure Active Directory-knop](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="63fb0-282">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="63fb0-282">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

   !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="63fb0-284">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="63fb0-284">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

   ![De knop toevoegen](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="63fb0-286">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="63fb0-286">In the **User** dialog box, perform the following steps:</span></span>

   ![Het dialoogvenster gebruiker](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="63fb0-288">a.</span><span class="sxs-lookup"><span data-stu-id="63fb0-288">a.</span></span> <span data-ttu-id="63fb0-289">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="63fb0-289">In the **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="63fb0-290">b.</span><span class="sxs-lookup"><span data-stu-id="63fb0-290">b.</span></span> <span data-ttu-id="63fb0-291">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="63fb0-291">In the **User name** box, type the email address of user Britta Simon.</span></span>

   <span data-ttu-id="63fb0-292">c.</span><span class="sxs-lookup"><span data-stu-id="63fb0-292">c.</span></span> <span data-ttu-id="63fb0-293">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="63fb0-293">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

   <span data-ttu-id="63fb0-294">d.</span><span class="sxs-lookup"><span data-stu-id="63fb0-294">d.</span></span> <span data-ttu-id="63fb0-295">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="63fb0-295">Click **Create**.</span></span>
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="63fb0-296">Maak een testgebruiker Qlik zin Enterprise</span><span class="sxs-lookup"><span data-stu-id="63fb0-296">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="63fb0-297">In deze sectie kunt u een gebruiker met de naam van Britta Simon in Qlik zin onderneming maken.</span><span class="sxs-lookup"><span data-stu-id="63fb0-297">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="63fb0-298">Werken met [Qlik zin Enterprise Client ondersteuningsteam](https://www.qlik.com/us/services/support) om toe te voegen de gebruikers van het platform Qlik zin Enterprise.</span><span class="sxs-lookup"><span data-stu-id="63fb0-298">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add the users in the Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="63fb0-299">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="63fb0-299">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="63fb0-300">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="63fb0-300">Assign the Azure AD test user</span></span>

<span data-ttu-id="63fb0-301">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding toegang verleent tot Qlik zin onderneming gebruiken.</span><span class="sxs-lookup"><span data-stu-id="63fb0-301">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Qlik Sense Enterprise.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="63fb0-303">**Britta Simon om aan te wijzen Qlik zin Enterprise, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="63fb0-303">**To assign Britta Simon to Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="63fb0-304">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="63fb0-304">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="63fb0-306">Selecteer in de lijst met toepassingen **Qlik zin Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="63fb0-306">In the applications list, select **Qlik Sense Enterprise**.</span></span>

    ![De koppeling Qlik zin Enterprise in de lijst met toepassingen](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="63fb0-308">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="63fb0-308">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="63fb0-310">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="63fb0-310">Click **Add** button.</span></span> <span data-ttu-id="63fb0-311">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="63fb0-311">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="63fb0-313">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="63fb0-313">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="63fb0-314">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="63fb0-314">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="63fb0-315">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="63fb0-315">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="63fb0-316">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="63fb0-316">Test single sign-on</span></span>

<span data-ttu-id="63fb0-317">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="63fb0-317">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="63fb0-318">Als u op de tegel Qlik zin Enterprise in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Qlik zin Enterprise.</span><span class="sxs-lookup"><span data-stu-id="63fb0-318">When you click the Qlik Sense Enterprise tile in the Access Panel, you should get automatically signed-on to your Qlik Sense Enterprise application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="63fb0-319">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="63fb0-319">Additional resources</span></span>

* [<span data-ttu-id="63fb0-320">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="63fb0-320">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="63fb0-321">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="63fb0-321">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

