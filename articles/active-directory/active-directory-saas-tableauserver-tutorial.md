---
title: 'Zelfstudie: Azure Active Directory-integratie met Tableau Server | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Tableau-Server.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 6b35609d88fbbf649e15863901d521886db2a4d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="0009a-103">Zelfstudie: Azure Active Directory-integratie met Tableau Server</span><span class="sxs-lookup"><span data-stu-id="0009a-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="0009a-104">In deze zelfstudie leert u hoe Tableau Server integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0009a-104">In this tutorial, you learn how to integrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0009a-105">Tableau Server integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="0009a-105">Integrating Tableau Server with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0009a-106">U kunt beheren in Azure AD die toegang tot de Server Tableau heeft</span><span class="sxs-lookup"><span data-stu-id="0009a-106">You can control in Azure AD who has access to Tableau Server</span></span>
- <span data-ttu-id="0009a-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Tableau Server (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="0009a-107">You can enable your users to automatically get signed-on to Tableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0009a-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="0009a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0009a-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0009a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0009a-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0009a-110">Prerequisites</span></span>

<span data-ttu-id="0009a-111">Voor het configureren van Azure AD-integratie met Tableau Server, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="0009a-111">To configure Azure AD integration with Tableau Server, you need the following items:</span></span>

- <span data-ttu-id="0009a-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="0009a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0009a-113">Een Server Tableau eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="0009a-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0009a-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="0009a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0009a-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="0009a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0009a-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="0009a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0009a-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0009a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0009a-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="0009a-118">Scenario description</span></span>
<span data-ttu-id="0009a-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="0009a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0009a-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="0009a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0009a-121">Tableau Server uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="0009a-121">Adding Tableau Server from the gallery</span></span>
2. <span data-ttu-id="0009a-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0009a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-the-gallery"></a><span data-ttu-id="0009a-123">Tableau Server uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="0009a-123">Adding Tableau Server from the gallery</span></span>
<span data-ttu-id="0009a-124">Voor het configureren van de integratie van Tableau Server in Azure AD, moet u Tableau Server uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="0009a-124">To configure the integration of Tableau Server into Azure AD, you need to add Tableau Server from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0009a-125">**Als u wilt toevoegen Tableau Server uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0009a-125">**To add Tableau Server from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0009a-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0009a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0009a-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0009a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0009a-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0009a-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="0009a-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0009a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="0009a-133">Typ in het zoekvak **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="0009a-133">In the search box, type **Tableau Server**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="0009a-135">Selecteer in het deelvenster resultaten **Tableau Server**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="0009a-135">In the results panel, select **Tableau Server**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0009a-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0009a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0009a-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Tableau-Server op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="0009a-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0009a-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Tableau Server in Azure AD voor een gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="0009a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Server is to a user in Azure AD.</span></span> <span data-ttu-id="0009a-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Tableau Server tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="0009a-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Server needs to be established.</span></span>

<span data-ttu-id="0009a-141">Wijs in Tableau-Server de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="0009a-141">In Tableau Server, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0009a-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Tableau Server, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="0009a-142">To configure and test Azure AD single sign-on with Tableau Server, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0009a-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0009a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0009a-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0009a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0009a-145">**[Maken van een testgebruiker Tableau Server](#creating-a-tableau-server-test-user)**  - Tableau-Server die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="0009a-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - to have a counterpart of Britta Simon in Tableau Server that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0009a-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0009a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0009a-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="0009a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0009a-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="0009a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0009a-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Tableau Server configureren.</span><span class="sxs-lookup"><span data-stu-id="0009a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="0009a-150">**Voor het configureren van Azure AD eenmalige aanmelding met Tableau Server, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0009a-150">**To configure Azure AD single sign-on with Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="0009a-151">In de Azure-portal op de **Tableau Server** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="0009a-151">In the Azure portal, on the **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="0009a-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0009a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="0009a-155">Op de **Tableau-serverdomein en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="0009a-155">On the **Tableau Server Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="0009a-157">a.</span><span class="sxs-lookup"><span data-stu-id="0009a-157">a.</span></span> <span data-ttu-id="0009a-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="0009a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="0009a-159">b.</span><span class="sxs-lookup"><span data-stu-id="0009a-159">b.</span></span> <span data-ttu-id="0009a-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="0009a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="0009a-161">c.</span><span class="sxs-lookup"><span data-stu-id="0009a-161">c.</span></span> <span data-ttu-id="0009a-162">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://azure.<domain name>.link/wg/saml/SSO/index.html`</span><span class="sxs-lookup"><span data-stu-id="0009a-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0009a-163">De voorgaande waarden zijn niet echte waarden.</span><span class="sxs-lookup"><span data-stu-id="0009a-163">The preceding values are not real values.</span></span> <span data-ttu-id="0009a-164">Later kunt bijwerken u de waarden met de werkelijke URL en de id van de configuratiepagina Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="0009a-164">Later, you update the values with the actual URL and identifier from the Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="0009a-165">De SAML-asserties verwacht tableau servertoepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="0009a-165">Tableau Server application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="0009a-166">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="0009a-166">Configure the following claims for this application.</span></span> <span data-ttu-id="0009a-167">U kunt de waarden van deze kenmerken van beheren de **'Gebruikerskenmerken'** sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="0009a-167">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="0009a-168">De volgende Schermafbeelding toont een voorbeeld voor dezelfde.</span><span class="sxs-lookup"><span data-stu-id="0009a-168">The following screenshot shows an example for the same.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="0009a-170">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding hierboven en voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="0009a-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="0009a-171">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="0009a-171">Attribute Name</span></span> | <span data-ttu-id="0009a-172">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="0009a-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="0009a-173">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="0009a-173">username</span></span> | <span data-ttu-id="0009a-174">*User.DisplayName*</span><span class="sxs-lookup"><span data-stu-id="0009a-174">*user.displayname*</span></span> |

    <span data-ttu-id="0009a-175">a.</span><span class="sxs-lookup"><span data-stu-id="0009a-175">a.</span></span> <span data-ttu-id="0009a-176">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0009a-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="0009a-179">b.</span><span class="sxs-lookup"><span data-stu-id="0009a-179">b.</span></span> <span data-ttu-id="0009a-180">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="0009a-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="0009a-181">c.</span><span class="sxs-lookup"><span data-stu-id="0009a-181">c.</span></span> <span data-ttu-id="0009a-182">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="0009a-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="0009a-183">d.</span><span class="sxs-lookup"><span data-stu-id="0009a-183">d.</span></span> <span data-ttu-id="0009a-184">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="0009a-184">Click **Ok**</span></span>


6. <span data-ttu-id="0009a-185">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="0009a-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="0009a-187">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="0009a-187">Click **Save** button.</span></span>

    <span data-ttu-id="0009a-188">![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="0009a-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="0009a-189">Als u eenmalige aanmelding voor uw toepassing is geconfigureerd, moet u eenmalige aanmelding voor uw tenant Tableau Server als beheerder.</span><span class="sxs-lookup"><span data-stu-id="0009a-189">To get SSO configured for your application, you need to sign-on to your Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="0009a-190">a.</span><span class="sxs-lookup"><span data-stu-id="0009a-190">a.</span></span> <span data-ttu-id="0009a-191">In de serverconfiguratie Tableau, klikt u op de **SAML** tabblad.</span><span class="sxs-lookup"><span data-stu-id="0009a-191">In the Tableau Server configuration, click the **SAML** tab.</span></span>
  
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="0009a-193">b.</span><span class="sxs-lookup"><span data-stu-id="0009a-193">b.</span></span> <span data-ttu-id="0009a-194">Schakel het selectievakje van **gebruik SAML voor eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="0009a-194">Select the checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="0009a-195">c.</span><span class="sxs-lookup"><span data-stu-id="0009a-195">c.</span></span> <span data-ttu-id="0009a-196">Tableau Server retour-URL, de URL die Tableau Server-gebruikers toegang, zoals http://tableau_server tot krijgen.</span><span class="sxs-lookup"><span data-stu-id="0009a-196">Tableau Server return URL—The URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="0009a-197">Gebruik http://localhost wordt niet aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="0009a-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="0009a-198">Via een URL met een slash (bijvoorbeeld http://tableau_server/) wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="0009a-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="0009a-199">Kopiëren **Tableau Server retour-URL** en plak deze naar Azure AD **aanmelding op URL** textbox in **Tableau-serverdomein en URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="0009a-199">Copy **Tableau Server return URL** and paste it to Azure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="0009a-200">d.</span><span class="sxs-lookup"><span data-stu-id="0009a-200">d.</span></span> <span data-ttu-id="0009a-201">SAML-entiteit-ID, de entiteit-ID is uniek voor de serverinstallatie van Tableau aan de IdP.</span><span class="sxs-lookup"><span data-stu-id="0009a-201">SAML entity ID—The entity ID uniquely identifies your Tableau Server installation to the IdP.</span></span> <span data-ttu-id="0009a-202">Hier geeft u de URL van de Server Tableau opnieuw, indien gewenst, maar deze hoeft niet te worden van de URL van de Server Tableau.</span><span class="sxs-lookup"><span data-stu-id="0009a-202">You can enter your Tableau Server URL again here, if you like, but it does not have to be your Tableau Server URL.</span></span> <span data-ttu-id="0009a-203">Kopiëren **SAML entiteit-ID** en plak deze naar Azure AD **id** textbox in **Tableau-serverdomein en URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="0009a-203">Copy **SAML entity ID** and paste it to Azure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="0009a-204">e.</span><span class="sxs-lookup"><span data-stu-id="0009a-204">e.</span></span> <span data-ttu-id="0009a-205">Klik op de **metagegevensbestand exporteren** en open het in de toepassing van de editor voor tekst.</span><span class="sxs-lookup"><span data-stu-id="0009a-205">Click the **Export Metadata File** and open it in the text editor application.</span></span> <span data-ttu-id="0009a-206">Zoek Assertion Consumer Service-URL met Http Post en 0-Index en kopieer de URL.</span><span class="sxs-lookup"><span data-stu-id="0009a-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy the URL.</span></span> <span data-ttu-id="0009a-207">Plak nu naar Azure AD **antwoord-URL** textbox in **Tableau-serverdomein en URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="0009a-207">Now paste it to Azure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="0009a-208">f.</span><span class="sxs-lookup"><span data-stu-id="0009a-208">f.</span></span> <span data-ttu-id="0009a-209">Zoek uw Federatiemetagegevens bestand gedownload van Azure-portal en uploadt u dit in de **SAML Idp metagegevensbestand**.</span><span class="sxs-lookup"><span data-stu-id="0009a-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in the **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="0009a-210">g.</span><span class="sxs-lookup"><span data-stu-id="0009a-210">g.</span></span> <span data-ttu-id="0009a-211">Klik op de **OK** knop op de pagina serverconfiguratie Tableau.</span><span class="sxs-lookup"><span data-stu-id="0009a-211">Click the **OK** button in the Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="0009a-212">Klant hebben voor het uploaden van een certificaat in de SSO-Tableau Server SAML-configuratie en het in de SSO-stroom ophalen genegeerd.</span><span class="sxs-lookup"><span data-stu-id="0009a-212">Customer have to upload any certificate in the Tableau Server SAML SSO configuration and it will get ignored in the SSO flow.</span></span>
    ><span data-ttu-id="0009a-213">Als u moet helpen SAML configureren op de Server Tableau Raadpleeg dit artikel [SAML configureren](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span><span class="sxs-lookup"><span data-stu-id="0009a-213">If you need help configuring SAML on Tableau Server then please refer to this article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="0009a-214">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="0009a-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0009a-215">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="0009a-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0009a-216">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0009a-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0009a-217">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="0009a-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="0009a-218">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0009a-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="0009a-220">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0009a-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0009a-221">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0009a-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0009a-223">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="0009a-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0009a-225">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0009a-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0009a-227">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="0009a-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0009a-229">a.</span><span class="sxs-lookup"><span data-stu-id="0009a-229">a.</span></span> <span data-ttu-id="0009a-230">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0009a-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0009a-231">b.</span><span class="sxs-lookup"><span data-stu-id="0009a-231">b.</span></span> <span data-ttu-id="0009a-232">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0009a-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0009a-233">c.</span><span class="sxs-lookup"><span data-stu-id="0009a-233">c.</span></span> <span data-ttu-id="0009a-234">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="0009a-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0009a-235">d.</span><span class="sxs-lookup"><span data-stu-id="0009a-235">d.</span></span> <span data-ttu-id="0009a-236">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0009a-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="0009a-237">Een testgebruiker Tableau Server maken</span><span class="sxs-lookup"><span data-stu-id="0009a-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="0009a-238">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in Tableau-Server.</span><span class="sxs-lookup"><span data-stu-id="0009a-238">The objective of this section is to create a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="0009a-239">U moet alle gebruikers in de server Tableau inrichten.</span><span class="sxs-lookup"><span data-stu-id="0009a-239">You need to provision all the users in the Tableau server.</span></span> 

<span data-ttu-id="0009a-240">Deze gebruikersnaam van de gebruiker moet overeenkomen met de waarde die u hebt geconfigureerd in het aangepaste kenmerk Azure AD van **gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="0009a-240">That username of the user should match the value which you have configured in the Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="0009a-241">Met de juiste toewijzing de integratie moet werken [eenmalige aanmelding configureren Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="0009a-241">With the correct mapping the integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="0009a-242">Als u een gebruiker handmatig maken wilt, moet u contact op met de serverbeheerder Tableau in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="0009a-242">If you need to create a user manually, you need to contact the Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0009a-243">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="0009a-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0009a-244">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="0009a-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Server.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="0009a-246">**Britta Simon om aan te wijzen Tableau Server, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0009a-246">**To assign Britta Simon to Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="0009a-247">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0009a-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="0009a-249">Selecteer in de lijst met toepassingen **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="0009a-249">In the applications list, select **Tableau Server**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="0009a-251">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="0009a-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="0009a-253">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="0009a-253">Click **Add** button.</span></span> <span data-ttu-id="0009a-254">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0009a-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="0009a-256">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="0009a-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0009a-257">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0009a-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0009a-258">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0009a-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0009a-259">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0009a-259">Testing single sign-on</span></span>

<span data-ttu-id="0009a-260">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="0009a-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0009a-261">Als u op de tegel Tableau Server in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Tableau-Server.</span><span class="sxs-lookup"><span data-stu-id="0009a-261">When you click the Tableau Server tile in the Access Panel, you should get automatically signed-on to your Tableau Server application.</span></span>
<span data-ttu-id="0009a-262">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="0009a-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0009a-263">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="0009a-263">Additional resources</span></span>

* [<span data-ttu-id="0009a-264">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0009a-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0009a-265">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0009a-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

