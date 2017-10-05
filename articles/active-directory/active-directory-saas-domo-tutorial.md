---
title: 'Zelfstudie: Azure Active Directory-integratie met Domo | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Domo.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 058626e4-73b3-4dc2-86ca-b060d002d70a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: 919d2262cf9f14159a13370037301005b5b69da2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-domo"></a><span data-ttu-id="55fbc-103">Zelfstudie: Azure Active Directory-integratie met Domo</span><span class="sxs-lookup"><span data-stu-id="55fbc-103">Tutorial: Azure Active Directory integration with Domo</span></span>

<span data-ttu-id="55fbc-104">In deze zelfstudie leert u hoe Domo integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="55fbc-104">In this tutorial, you learn how to integrate Domo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="55fbc-105">Domo integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="55fbc-105">Integrating Domo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="55fbc-106">U kunt beheren in Azure AD die toegang tot Domo heeft</span><span class="sxs-lookup"><span data-stu-id="55fbc-106">You can control in Azure AD who has access to Domo</span></span>
- <span data-ttu-id="55fbc-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Domo (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="55fbc-107">You can enable your users to automatically get signed-on to Domo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="55fbc-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="55fbc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="55fbc-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="55fbc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55fbc-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="55fbc-110">Prerequisites</span></span>

<span data-ttu-id="55fbc-111">Voor het configureren van Azure AD-integratie met Domo, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="55fbc-111">To configure Azure AD integration with Domo, you need the following items:</span></span>

- <span data-ttu-id="55fbc-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="55fbc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="55fbc-113">Een Domo eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="55fbc-113">A Domo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="55fbc-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="55fbc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="55fbc-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="55fbc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="55fbc-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="55fbc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="55fbc-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="55fbc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="55fbc-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="55fbc-118">Scenario description</span></span>
<span data-ttu-id="55fbc-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="55fbc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="55fbc-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="55fbc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="55fbc-121">Domo uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="55fbc-121">Adding Domo from the gallery</span></span>
2. <span data-ttu-id="55fbc-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="55fbc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-domo-from-the-gallery"></a><span data-ttu-id="55fbc-123">Domo uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="55fbc-123">Adding Domo from the gallery</span></span>
<span data-ttu-id="55fbc-124">Voor het configureren van de integratie van Domo in Azure AD, moet u Domo uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="55fbc-124">To configure the integration of Domo into Azure AD, you need to add Domo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="55fbc-125">**Als u wilt toevoegen Domo uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="55fbc-125">**To add Domo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="55fbc-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="55fbc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="55fbc-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="55fbc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="55fbc-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="55fbc-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="55fbc-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="55fbc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="55fbc-133">Typ in het zoekvak **Domo**.</span><span class="sxs-lookup"><span data-stu-id="55fbc-133">In the search box, type **Domo**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-domo-tutorial/tutorial_domo_search.png)

5. <span data-ttu-id="55fbc-135">Selecteer in het deelvenster resultaten **Domo**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="55fbc-135">In the results panel, select **Domo**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-domo-tutorial/tutorial_domo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="55fbc-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="55fbc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="55fbc-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Domo op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="55fbc-138">In this section, you configure and test Azure AD single sign-on with Domo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="55fbc-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Domo is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55fbc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Domo is to a user in Azure AD.</span></span> <span data-ttu-id="55fbc-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Domo tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="55fbc-140">In other words, a link relationship between an Azure AD user and the related user in Domo needs to be established.</span></span>

<span data-ttu-id="55fbc-141">Wijs in Domo, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="55fbc-141">In Domo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="55fbc-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Domo, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="55fbc-142">To configure and test Azure AD single sign-on with Domo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="55fbc-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="55fbc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="55fbc-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="55fbc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="55fbc-145">**[Maken van een testgebruiker Domo](#creating-a-domo-test-user)**  - Domo die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="55fbc-145">**[Creating a Domo test user](#creating-a-domo-test-user)** - to have a counterpart of Britta Simon in Domo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="55fbc-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="55fbc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="55fbc-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="55fbc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="55fbc-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="55fbc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="55fbc-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Domo configureren.</span><span class="sxs-lookup"><span data-stu-id="55fbc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Domo application.</span></span>

<span data-ttu-id="55fbc-150">**Voor het configureren van Azure AD eenmalige aanmelding met Domo, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="55fbc-150">**To configure Azure AD single sign-on with Domo, perform the following steps:**</span></span>

1. <span data-ttu-id="55fbc-151">In de Azure-portal op de **Domo** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="55fbc-151">In the Azure portal, on the **Domo** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="55fbc-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="55fbc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-domo-tutorial/tutorial_domo_samlbase.png)

3. <span data-ttu-id="55fbc-155">Op de **Domo domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="55fbc-155">On the **Domo Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-domo-tutorial/tutorial_domo_url.png)

    <span data-ttu-id="55fbc-157">a.</span><span class="sxs-lookup"><span data-stu-id="55fbc-157">a.</span></span> <span data-ttu-id="55fbc-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.domo.com`</span><span class="sxs-lookup"><span data-stu-id="55fbc-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.domo.com`</span></span>

    <span data-ttu-id="55fbc-159">b.</span><span class="sxs-lookup"><span data-stu-id="55fbc-159">b.</span></span> <span data-ttu-id="55fbc-160">In de **id** textbox, typ een URL met de volgende patronen:</span><span class="sxs-lookup"><span data-stu-id="55fbc-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span>     

    | |
    |--|    
    | `https://<companyname>.domo.com` |
    | `https://<companyname>.beta.domo.com` |
    | `https://<companyname>.demo.domo.com` |
    | `https://<companyname>.dev.domo.com` | 
    | `https://<companyname>.fastage1.domo.com` |       
    | `https://<companyname>.frdev.domo.com` |       
    | `https://<companyname>.gastage.domo.com` |       
    | `https://<companyname>.load.domo.com` |       
    | `https://<companyname>.local.domo.com` |       
    | `https://<companyname>.qa.domo.com` |
    | `https://<companyname>.stage.domo.com` |
    
    > [!NOTE] 
    > <span data-ttu-id="55fbc-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="55fbc-161">These values are not real.</span></span> <span data-ttu-id="55fbc-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="55fbc-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="55fbc-163">Neem contact op met [Domo Client ondersteuningsteam](mailto:support@domo.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="55fbc-163">Contact [Domo Client support team](mailto:support@domo.com) to get these values.</span></span>

4. <span data-ttu-id="55fbc-164">De SAML-asserties verwacht Domo toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="55fbc-164">Domo application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="55fbc-165">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="55fbc-165">Configure the following claims for this application.</span></span> <span data-ttu-id="55fbc-166">U kunt beheren de waarden van deze kenmerken van de '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="55fbc-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="55fbc-167">De volgende Schermafbeelding toont een voorbeeld voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="55fbc-167">The following screenshot shows an example for this configuration.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-domo-tutorial/tutorial_domo_attributes.png)
    
5. <span data-ttu-id="55fbc-169">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding en de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="55fbc-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="55fbc-170">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="55fbc-170">Attribute Name</span></span> | <span data-ttu-id="55fbc-171">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="55fbc-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="55fbc-172">naam</span><span class="sxs-lookup"><span data-stu-id="55fbc-172">name</span></span> | <span data-ttu-id="55fbc-173">User.DisplayName</span><span class="sxs-lookup"><span data-stu-id="55fbc-173">user.displayname</span></span> |
    | <span data-ttu-id="55fbc-174">E-mail</span><span class="sxs-lookup"><span data-stu-id="55fbc-174">email</span></span> | <span data-ttu-id="55fbc-175">User.mail</span><span class="sxs-lookup"><span data-stu-id="55fbc-175">user.mail</span></span> |
    
    <span data-ttu-id="55fbc-176">a.</span><span class="sxs-lookup"><span data-stu-id="55fbc-176">a.</span></span> <span data-ttu-id="55fbc-177">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="55fbc-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-domo-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-domo-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="55fbc-180">b.</span><span class="sxs-lookup"><span data-stu-id="55fbc-180">b.</span></span> <span data-ttu-id="55fbc-181">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="55fbc-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="55fbc-182">c.</span><span class="sxs-lookup"><span data-stu-id="55fbc-182">c.</span></span> <span data-ttu-id="55fbc-183">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="55fbc-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="55fbc-184">d.</span><span class="sxs-lookup"><span data-stu-id="55fbc-184">d.</span></span> <span data-ttu-id="55fbc-185">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="55fbc-185">Click **Ok**.</span></span> 
 
6. <span data-ttu-id="55fbc-186">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="55fbc-186">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-domo-tutorial/tutorial_domo_certificate.png) 

7. <span data-ttu-id="55fbc-188">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="55fbc-188">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-domo-tutorial/tutorial_general_400.png)


8. <span data-ttu-id="55fbc-190">Op de **Domo configuratie** sectie, klikt u op **configureren Domo** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="55fbc-190">On the **Domo Configuration** section, click **Configure Domo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="55fbc-191">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="55fbc-191">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>   

   ![Eenmalige aanmelding configureren](./media/active-directory-saas-domo-tutorial/tutorial_domo_configure.png) 

9. <span data-ttu-id="55fbc-193">Eenmalige aanmelding configureren op **Domo** zijde, moet u de gedownloade verzenden **certificaat**, **SAML entiteit-ID**, wordt de **SAML Single Sign-On Service-URL** en de **Sign-Out URL** naar [Domo ondersteuningsteam](mailto:support@domo.com).</span><span class="sxs-lookup"><span data-stu-id="55fbc-193">To configure single sign-on on **Domo** side, you need to send the downloaded **Certificate**, **SAML Entity ID**, the **SAML Single Sign-On Service URL** and the **Sign-Out URL** to [Domo support team](mailto:support@domo.com).</span></span> <span data-ttu-id="55fbc-194">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="55fbc-194">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="55fbc-195">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="55fbc-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="55fbc-196">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="55fbc-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="55fbc-197">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="55fbc-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="55fbc-198">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="55fbc-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="55fbc-199">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="55fbc-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="55fbc-201">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="55fbc-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="55fbc-202">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="55fbc-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-domo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="55fbc-204">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="55fbc-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-domo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="55fbc-206">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="55fbc-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-domo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="55fbc-208">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="55fbc-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-domo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="55fbc-210">a.</span><span class="sxs-lookup"><span data-stu-id="55fbc-210">a.</span></span> <span data-ttu-id="55fbc-211">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="55fbc-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="55fbc-212">b.</span><span class="sxs-lookup"><span data-stu-id="55fbc-212">b.</span></span> <span data-ttu-id="55fbc-213">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="55fbc-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="55fbc-214">c.</span><span class="sxs-lookup"><span data-stu-id="55fbc-214">c.</span></span> <span data-ttu-id="55fbc-215">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="55fbc-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="55fbc-216">d.</span><span class="sxs-lookup"><span data-stu-id="55fbc-216">d.</span></span> <span data-ttu-id="55fbc-217">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="55fbc-217">Click **Create**.</span></span>
 
### <a name="creating-a-domo-test-user"></a><span data-ttu-id="55fbc-218">Een testgebruiker Domo maken</span><span class="sxs-lookup"><span data-stu-id="55fbc-218">Creating a Domo test user</span></span>

<span data-ttu-id="55fbc-219">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Domo genoemd.</span><span class="sxs-lookup"><span data-stu-id="55fbc-219">The objective of this section is to create a user called Britta Simon in Domo.</span></span> <span data-ttu-id="55fbc-220">Domo ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="55fbc-220">Domo supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="55fbc-221">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="55fbc-221">There is no action item for you in this section.</span></span> <span data-ttu-id="55fbc-222">Een nieuwe gebruiker is gemaakt tijdens een poging tot toegang tot Domo als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="55fbc-222">A new user is created during an attempt to access Domo if it doesn't exist yet.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="55fbc-223">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="55fbc-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="55fbc-224">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Domo.</span><span class="sxs-lookup"><span data-stu-id="55fbc-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Domo.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="55fbc-226">**Britta Simon om aan te wijzen Domo, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="55fbc-226">**To assign Britta Simon to Domo, perform the following steps:**</span></span>

1. <span data-ttu-id="55fbc-227">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="55fbc-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="55fbc-229">Selecteer in de lijst met toepassingen **Domo**.</span><span class="sxs-lookup"><span data-stu-id="55fbc-229">In the applications list, select **Domo**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-domo-tutorial/tutorial_domo_app.png) 

3. <span data-ttu-id="55fbc-231">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="55fbc-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="55fbc-233">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="55fbc-233">Click **Add** button.</span></span> <span data-ttu-id="55fbc-234">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="55fbc-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="55fbc-236">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="55fbc-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="55fbc-237">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="55fbc-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="55fbc-238">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="55fbc-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="55fbc-239">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="55fbc-239">Testing single sign-on</span></span>

<span data-ttu-id="55fbc-240">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="55fbc-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="55fbc-241">Als u op de tegel Domo in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Domo.</span><span class="sxs-lookup"><span data-stu-id="55fbc-241">When you click the Domo tile in the Access Panel, you should get automatically signed-on to your Domo application.</span></span>

<span data-ttu-id="55fbc-242">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="55fbc-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="55fbc-243">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="55fbc-243">Additional resources</span></span>

* [<span data-ttu-id="55fbc-244">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="55fbc-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="55fbc-245">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="55fbc-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-domo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-domo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-domo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-domo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-domo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-domo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-domo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-domo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-domo-tutorial/tutorial_general_203.png

