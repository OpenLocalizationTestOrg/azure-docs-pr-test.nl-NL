---
title: 'Zelfstudie: Azure Active Directory-integratie met Schoolbord meer | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Schoolbord meer informatie.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: c2b7638e99fa46ff41a7f2202bdf0e7a2b017c19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="6d2ce-103">Zelfstudie: Azure Active Directory-integratie met Schoolbord meer</span><span class="sxs-lookup"><span data-stu-id="6d2ce-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="6d2ce-104">In deze zelfstudie leert u hoe Schoolbord meer integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6d2ce-104">In this tutorial, you learn how to integrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6d2ce-105">Schoolbord meer integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6d2ce-105">Integrating Blackboard Learn with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6d2ce-106">U kunt beheren in Azure AD die toegang tot Schoolbord meer heeft</span><span class="sxs-lookup"><span data-stu-id="6d2ce-106">You can control in Azure AD who has access to Blackboard Learn</span></span>
- <span data-ttu-id="6d2ce-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Schoolbord meer (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="6d2ce-107">You can enable your users to automatically get signed-on to Blackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6d2ce-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6d2ce-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6d2ce-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6d2ce-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d2ce-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6d2ce-110">Prerequisites</span></span>

<span data-ttu-id="6d2ce-111">Voor het configureren van Azure AD-integratie met Schoolbord meer, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="6d2ce-111">To configure Azure AD integration with Blackboard Learn, you need the following items:</span></span>

- <span data-ttu-id="6d2ce-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6d2ce-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6d2ce-113">Een Schoolbord meer eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6d2ce-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6d2ce-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6d2ce-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6d2ce-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6d2ce-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6d2ce-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6d2ce-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6d2ce-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6d2ce-118">Scenario description</span></span>
<span data-ttu-id="6d2ce-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6d2ce-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6d2ce-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6d2ce-121">Toe te voegen Schoolbord informatie uit de galerie</span><span class="sxs-lookup"><span data-stu-id="6d2ce-121">Adding Blackboard Learn from the gallery</span></span>
2. <span data-ttu-id="6d2ce-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6d2ce-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-the-gallery"></a><span data-ttu-id="6d2ce-123">Toe te voegen Schoolbord informatie uit de galerie</span><span class="sxs-lookup"><span data-stu-id="6d2ce-123">Adding Blackboard Learn from the gallery</span></span>
<span data-ttu-id="6d2ce-124">Voor het configureren van de integratie van Schoolbord meer in Azure AD, moet u Schoolbord meer toevoegen uit de galerie aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-124">To configure the integration of Blackboard Learn into Azure AD, you need to add Blackboard Learn from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6d2ce-125">**Als u wilt toevoegen Schoolbord informatie uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6d2ce-125">**To add Blackboard Learn from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6d2ce-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6d2ce-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6d2ce-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6d2ce-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6d2ce-133">Typ in het zoekvak **Schoolbord meer**.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-133">In the search box, type **Blackboard Learn**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="6d2ce-135">Selecteer in het deelvenster resultaten **Schoolbord meer**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-135">In the results panel, select **Blackboard Learn**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6d2ce-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6d2ce-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6d2ce-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Schoolbord meer op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6d2ce-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6d2ce-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Schoolbord meer is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn is to a user in Azure AD.</span></span> <span data-ttu-id="6d2ce-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Schoolbord meer tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn needs to be established.</span></span>

<span data-ttu-id="6d2ce-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Schoolbord meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="6d2ce-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Schoolbord meer, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="6d2ce-142">To configure and test Azure AD single sign-on with Blackboard Learn, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6d2ce-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6d2ce-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6d2ce-145">**[Maken van een testgebruiker Schoolbord meer](#creating-a-blackboard-learn-test-user)**  - Schoolbord informatie die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6d2ce-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6d2ce-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6d2ce-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6d2ce-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6d2ce-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Schoolbord meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="6d2ce-150">**Voor het configureren van Azure AD eenmalige aanmelding met Schoolbord meer, kunt u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6d2ce-150">**To configure Azure AD single sign-on with Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="6d2ce-151">In de Azure-portal op de **Schoolbord meer** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-151">In the Azure portal, on the **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6d2ce-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="6d2ce-155">Op de **Schoolbord meer informatie over domein- en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6d2ce-155">On the **Blackboard Learn Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="6d2ce-157">a.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-157">a.</span></span> <span data-ttu-id="6d2ce-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="6d2ce-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="6d2ce-159">b.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-159">b.</span></span> <span data-ttu-id="6d2ce-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="6d2ce-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="6d2ce-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-161">These values are not real.</span></span> <span data-ttu-id="6d2ce-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6d2ce-163">Neem contact op met [Schoolbord meer informatie over Client-ondersteuningsteam](https://www.blackboard.com/support/index.aspx) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) to get these values.</span></span> 

4. <span data-ttu-id="6d2ce-164">De SAML-asserties verwacht Schoolbord meer toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-164">Blackboard Learn application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="6d2ce-165">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-165">Configure the following claims for this application.</span></span> <span data-ttu-id="6d2ce-166">U kunt de waarden van deze kenmerken van beheren de **gebruikerskenmerken** sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-166">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="6d2ce-167">De volgende Schermafbeelding toont een voorbeeld over het.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-167">The following screenshot shows an example about it.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="6d2ce-169">In de **gebruikerskenmerken** sectie op **eenmalige aanmelding** dialoogvenster SAML-token kenmerken configureren zoals wordt weergegeven in de afbeelding en de volgende stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-169">In the **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in the image and perform the following steps.</span></span> <span data-ttu-id="6d2ce-170">We hebben de Userprincipalname toegewezen als het kenmerk unieke gebruikers hier maar kunt u deze toewijzen aan de juiste waarde die uniek is voor de gebruiker in de organisatie en die wordt toegewezen aan het veld username Schoolbord meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-170">We have mapped the Userprincipalname as the unique user attribute here but you can map it to the appropriate value, which uniquely distinguishes the user in the organization and that maps to Blackboard Learn username field.</span></span>
           
    | <span data-ttu-id="6d2ce-171">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="6d2ce-171">Attribute Name</span></span> | <span data-ttu-id="6d2ce-172">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="6d2ce-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="6d2ce-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="6d2ce-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="6d2ce-174">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="6d2ce-174">user.userprincipalname</span></span> |

    <span data-ttu-id="6d2ce-175">a.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-175">a.</span></span> <span data-ttu-id="6d2ce-176">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="6d2ce-179">b.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-179">b.</span></span> <span data-ttu-id="6d2ce-180">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="6d2ce-181">c.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-181">c.</span></span> <span data-ttu-id="6d2ce-182">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="6d2ce-183">d.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-183">d.</span></span> <span data-ttu-id="6d2ce-184">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-184">Click **Ok**.</span></span>

4. <span data-ttu-id="6d2ce-185">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="6d2ce-187">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-187">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="6d2ce-189">Op de **Schoolbord meer configuratie** sectie, klikt u op **configureren Schoolbord meer** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-189">On the **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6d2ce-190">Kopieer de **SAML entiteit-ID** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="6d2ce-190">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="6d2ce-192">Eenmalige aanmelding configureren op **Schoolbord meer** zijde, moet u de gedownloade verzenden **Metadata XML** en **SAML entiteit-ID** naar [Schoolbord meer ondersteuning](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d2ce-192">To configure single sign-on on **Blackboard Learn** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="6d2ce-193">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="6d2ce-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6d2ce-194">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6d2ce-195">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6d2ce-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6d2ce-196">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6d2ce-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="6d2ce-197">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6d2ce-199">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6d2ce-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6d2ce-200">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6d2ce-202">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6d2ce-204">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6d2ce-206">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6d2ce-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6d2ce-208">a.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-208">a.</span></span> <span data-ttu-id="6d2ce-209">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6d2ce-210">b.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-210">b.</span></span> <span data-ttu-id="6d2ce-211">In de **gebruikersnaam** textbox type de **e-mailadres** van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-211">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="6d2ce-212">c.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-212">c.</span></span> <span data-ttu-id="6d2ce-213">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6d2ce-214">d.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-214">d.</span></span> <span data-ttu-id="6d2ce-215">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="6d2ce-216">Maken van een testgebruiker Schoolbord meer</span><span class="sxs-lookup"><span data-stu-id="6d2ce-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="6d2ce-217">In deze sectie kunt u een gebruiker met de naam van Britta Simon in Schoolbord meer maken.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="6d2ce-218">Schoolbord meer toepassing ondersteunt alleen in de tijd van gebruikersinrichting.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="6d2ce-219">Zorg ervoor dat u de claims hebt geconfigureerd zoals beschreven in de sectie  **[eenmalige aanmelding configureren Azure AD](#configuring-azure-ad-single-sign-on)**</span><span class="sxs-lookup"><span data-stu-id="6d2ce-219">Make sure that you have configured the claims as described in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6d2ce-220">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d2ce-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6d2ce-221">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang te verlenen voor Schoolbord meer.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6d2ce-223">**Als u wilt toewijzen Britta Simon voor Schoolbord meer, kunt u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6d2ce-223">**To assign Britta Simon to Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="6d2ce-224">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6d2ce-226">Selecteer in de lijst met toepassingen **Schoolbord meer**.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-226">In the applications list, select **Blackboard Learn**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="6d2ce-228">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6d2ce-230">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-230">Click **Add** button.</span></span> <span data-ttu-id="6d2ce-231">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6d2ce-233">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6d2ce-234">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6d2ce-235">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6d2ce-236">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6d2ce-236">Testing single sign-on</span></span>

<span data-ttu-id="6d2ce-237">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6d2ce-238">Als u op de tegel Schoolbord meer in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Schoolbord meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6d2ce-238">When you click the Blackboard Learn tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn application.</span></span> <span data-ttu-id="6d2ce-239">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6d2ce-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6d2ce-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6d2ce-240">Additional resources</span></span>

* [<span data-ttu-id="6d2ce-241">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6d2ce-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6d2ce-242">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6d2ce-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

