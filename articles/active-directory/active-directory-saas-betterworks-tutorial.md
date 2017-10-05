---
title: 'Zelfstudie: Azure Active Directory-integratie met BetterWorks | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en BetterWorks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: d6a5b167c0befbd0fe2c65bdd16abc35ed0a659c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="d712c-103">Zelfstudie: Azure Active Directory-integratie met BetterWorks</span><span class="sxs-lookup"><span data-stu-id="d712c-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="d712c-104">In deze zelfstudie leert u hoe BetterWorks integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d712c-104">In this tutorial, you learn how to integrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d712c-105">BetterWorks integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d712c-105">Integrating BetterWorks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d712c-106">U kunt beheren in Azure AD die toegang tot BetterWorks heeft</span><span class="sxs-lookup"><span data-stu-id="d712c-106">You can control in Azure AD who has access to BetterWorks</span></span>
- <span data-ttu-id="d712c-107">U kunt uw gebruikers automatisch ophalen aangemeld bij BetterWorks (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="d712c-107">You can enable your users to automatically get signed-on to BetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d712c-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="d712c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d712c-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d712c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d712c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d712c-110">Prerequisites</span></span>

<span data-ttu-id="d712c-111">Voor het configureren van Azure AD-integratie met BetterWorks, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="d712c-111">To configure Azure AD integration with BetterWorks, you need the following items:</span></span>

- <span data-ttu-id="d712c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="d712c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d712c-113">Een BetterWorks eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="d712c-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d712c-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d712c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d712c-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="d712c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d712c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d712c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d712c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d712c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d712c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d712c-118">Scenario description</span></span>
<span data-ttu-id="d712c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d712c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d712c-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d712c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d712c-121">BetterWorks uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d712c-121">Adding BetterWorks from the gallery</span></span>
2. <span data-ttu-id="d712c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d712c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-the-gallery"></a><span data-ttu-id="d712c-123">BetterWorks uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d712c-123">Adding BetterWorks from the gallery</span></span>
<span data-ttu-id="d712c-124">Voor het configureren van de integratie van BetterWorks in Azure AD, moet u BetterWorks uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d712c-124">To configure the integration of BetterWorks into Azure AD, you need to add BetterWorks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d712c-125">**Als u wilt toevoegen BetterWorks uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d712c-125">**To add BetterWorks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d712c-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d712c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d712c-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d712c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d712c-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d712c-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d712c-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d712c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d712c-133">Typ in het zoekvak **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="d712c-133">In the search box, type **BetterWorks**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. <span data-ttu-id="d712c-135">Selecteer in het deelvenster resultaten **BetterWorks**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d712c-135">In the results panel, select **BetterWorks**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d712c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d712c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d712c-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met BetterWorks op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="d712c-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d712c-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in BetterWorks is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d712c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BetterWorks is to a user in Azure AD.</span></span> <span data-ttu-id="d712c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in BetterWorks tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="d712c-140">In other words, a link relationship between an Azure AD user and the related user in BetterWorks needs to be established.</span></span>

<span data-ttu-id="d712c-141">Wijs in BetterWorks, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="d712c-141">In BetterWorks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d712c-142">Om te configureren en testen van Azure AD eenmalige aanmelding met BetterWorks, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="d712c-142">To configure and test Azure AD single sign-on with BetterWorks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d712c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d712c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d712c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d712c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d712c-145">**[Maken van een testgebruiker BetterWorks](#creating-a-betterworks-test-user)**  - BetterWorks die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="d712c-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - to have a counterpart of Britta Simon in BetterWorks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d712c-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d712c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d712c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d712c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d712c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d712c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d712c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing BetterWorks configureren.</span><span class="sxs-lookup"><span data-stu-id="d712c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="d712c-150">**Voor het configureren van Azure AD eenmalige aanmelding met BetterWorks, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d712c-150">**To configure Azure AD single sign-on with BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="d712c-151">In de Azure-portal op de **BetterWorks** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d712c-151">In the Azure portal, on the **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d712c-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d712c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. <span data-ttu-id="d712c-155">Op de **BetterWorks domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP geïnitieerd modus**:</span><span class="sxs-lookup"><span data-stu-id="d712c-155">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="d712c-157">a.</span><span class="sxs-lookup"><span data-stu-id="d712c-157">a.</span></span> <span data-ttu-id="d712c-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://app.betterworks.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="d712c-158">In the **Identifier** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="d712c-159">b.</span><span class="sxs-lookup"><span data-stu-id="d712c-159">b.</span></span> <span data-ttu-id="d712c-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://app.betterworks.com/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="d712c-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

4. <span data-ttu-id="d712c-161">Op de **BetterWorks domein en de URL's** sectie als u wilt configureren van de toepassing in **SP geïnitieerd modus**, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d712c-161">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="d712c-163">a.</span><span class="sxs-lookup"><span data-stu-id="d712c-163">a.</span></span> <span data-ttu-id="d712c-164">Klik op de **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="d712c-164">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="d712c-165">b.</span><span class="sxs-lookup"><span data-stu-id="d712c-165">b.</span></span> <span data-ttu-id="d712c-166">In de **aanmelding op URL** textbox, typ een URL met het volgende patroon volgen:`https://app.betterworks.com`</span><span class="sxs-lookup"><span data-stu-id="d712c-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d712c-167">Deze zijn niet echte waarden.</span><span class="sxs-lookup"><span data-stu-id="d712c-167">These are not real values.</span></span> <span data-ttu-id="d712c-168">Deze waarden bijwerken met de antwoord-URL, de id en de werkelijke aanmelding op URL.</span><span class="sxs-lookup"><span data-stu-id="d712c-168">Update these values with the Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="d712c-169">Neem contact op met [BetterWorks ondersteuningsteam](mailto:support@betterworks.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="d712c-169">Contact [BetterWorks support team](mailto:support@betterworks.com) to get these values.</span></span>
 
4. <span data-ttu-id="d712c-170">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d712c-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. <span data-ttu-id="d712c-172">De SAML-asserties verwacht BetterWorks toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="d712c-172">BetterWorks application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="d712c-173">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="d712c-173">Configure the following claims for this application.</span></span> <span data-ttu-id="d712c-174">U kunt beheren de waarden van deze kenmerken van de '**kenmerk**' tabblad van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d712c-174">You can manage the values of these attributes from the "**Attribute**" tab of the application.</span></span> <span data-ttu-id="d712c-175">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="d712c-175">The following screenshot shows an example for this.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. <span data-ttu-id="d712c-177">Op de **SAML-token kenmerken** dialoogvenster uitvoeren voor elke rij in de onderstaande tabel wordt weergegeven op de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d712c-177">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
   | <span data-ttu-id="d712c-178">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="d712c-178">Attribute Name</span></span> | <span data-ttu-id="d712c-179">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="d712c-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="d712c-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="d712c-180">saml_token</span></span>     | <span data-ttu-id="d712c-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="d712c-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="d712c-182">a.</span><span class="sxs-lookup"><span data-stu-id="d712c-182">a.</span></span> <span data-ttu-id="d712c-183">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d712c-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="d712c-186">b.</span><span class="sxs-lookup"><span data-stu-id="d712c-186">b.</span></span> <span data-ttu-id="d712c-187">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="d712c-187">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

   <span data-ttu-id="d712c-188">c.</span><span class="sxs-lookup"><span data-stu-id="d712c-188">c.</span></span> <span data-ttu-id="d712c-189">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="d712c-189">From the **Value** list, type the attribute value shown for that row.</span></span>
    
   <span data-ttu-id="d712c-190">d.</span><span class="sxs-lookup"><span data-stu-id="d712c-190">d.</span></span> <span data-ttu-id="d712c-191">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d712c-191">Click **Ok**.</span></span>

7. <span data-ttu-id="d712c-192">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d712c-192">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d712c-194">Eenmalige aanmelding configureren op **BetterWorks** zijde, moet u de gedownloade verzenden **Metadata XML** naar [BetterWorks ondersteuningsteam](mailto:support@betterworks.com).</span><span class="sxs-lookup"><span data-stu-id="d712c-194">To configure single sign-on on **BetterWorks** side, you need to send the downloaded **Metadata XML** to [BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="d712c-195">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="d712c-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d712c-196">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="d712c-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d712c-197">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d712c-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d712c-198">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d712c-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="d712c-199">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d712c-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d712c-201">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d712c-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d712c-202">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d712c-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d712c-204">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="d712c-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d712c-206">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d712c-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d712c-208">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d712c-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d712c-210">a.</span><span class="sxs-lookup"><span data-stu-id="d712c-210">a.</span></span> <span data-ttu-id="d712c-211">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d712c-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d712c-212">b.</span><span class="sxs-lookup"><span data-stu-id="d712c-212">b.</span></span> <span data-ttu-id="d712c-213">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d712c-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d712c-214">c.</span><span class="sxs-lookup"><span data-stu-id="d712c-214">c.</span></span> <span data-ttu-id="d712c-215">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d712c-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d712c-216">d.</span><span class="sxs-lookup"><span data-stu-id="d712c-216">d.</span></span> <span data-ttu-id="d712c-217">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d712c-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="d712c-218">Een testgebruiker BetterWorks maken</span><span class="sxs-lookup"><span data-stu-id="d712c-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="d712c-219">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in BetterWorks maken.</span><span class="sxs-lookup"><span data-stu-id="d712c-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="d712c-220">Werken met [BetterWorks ondersteuningsteam](mailto:support@betterworks.com) de gebruikers van het platform BetterWorks toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d712c-220">Work with [BetterWorks support team](mailto:support@betterworks.com) to add the users in the BetterWorks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d712c-221">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="d712c-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d712c-222">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="d712c-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BetterWorks.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d712c-224">**Britta Simon om aan te wijzen BetterWorks, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d712c-224">**To assign Britta Simon to BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="d712c-225">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d712c-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d712c-227">Selecteer in de lijst met toepassingen **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="d712c-227">In the applications list, select **BetterWorks**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. <span data-ttu-id="d712c-229">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d712c-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d712c-231">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d712c-231">Click **Add** button.</span></span> <span data-ttu-id="d712c-232">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d712c-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d712c-234">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d712c-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d712c-235">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d712c-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d712c-236">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d712c-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d712c-237">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d712c-237">Testing single sign-on</span></span>

<span data-ttu-id="d712c-238">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="d712c-238">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d712c-239">Als u op de tegel BetterWorks in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="d712c-239">When you click the BetterWorks tile in the Access Panel, you should get automatically signed-on to your BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d712c-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d712c-240">Additional resources</span></span>

* [<span data-ttu-id="d712c-241">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d712c-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d712c-242">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d712c-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

