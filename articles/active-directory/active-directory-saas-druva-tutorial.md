---
title: 'Zelfstudie: Azure Active Directory-integratie met Druva | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Druva.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: b23e73c47b9a00893e036b67826e4b7ead819a1d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="ac5db-103">Zelfstudie: Azure Active Directory-integratie met Druva</span><span class="sxs-lookup"><span data-stu-id="ac5db-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="ac5db-104">In deze zelfstudie leert u hoe Druva integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ac5db-104">In this tutorial, you learn how to integrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ac5db-105">Druva integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ac5db-105">Integrating Druva with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ac5db-106">U kunt beheren in Azure AD die toegang tot Druva heeft.</span><span class="sxs-lookup"><span data-stu-id="ac5db-106">You can control in Azure AD who has access to Druva.</span></span>
- <span data-ttu-id="ac5db-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Druva (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ac5db-107">You can enable your users to automatically get signed-on to Druva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ac5db-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="ac5db-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="ac5db-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ac5db-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac5db-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ac5db-110">Prerequisites</span></span>

<span data-ttu-id="ac5db-111">Voor het configureren van Azure AD-integratie met Druva, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="ac5db-111">To configure Azure AD integration with Druva, you need the following items:</span></span>

- <span data-ttu-id="ac5db-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ac5db-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ac5db-113">Een Druva eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ac5db-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ac5db-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ac5db-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ac5db-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ac5db-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ac5db-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ac5db-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ac5db-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ac5db-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ac5db-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ac5db-118">Scenario description</span></span>
<span data-ttu-id="ac5db-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ac5db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ac5db-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ac5db-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ac5db-121">Druva uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ac5db-121">Adding Druva from the gallery</span></span>
2. <span data-ttu-id="ac5db-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ac5db-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-the-gallery"></a><span data-ttu-id="ac5db-123">Druva uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ac5db-123">Adding Druva from the gallery</span></span>
<span data-ttu-id="ac5db-124">Voor het configureren van de integratie van Druva in Azure AD, moet u Druva uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ac5db-124">To configure the integration of Druva into Azure AD, you need to add Druva from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ac5db-125">**Als u wilt toevoegen Druva uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ac5db-125">**To add Druva from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ac5db-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ac5db-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="ac5db-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ac5db-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ac5db-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ac5db-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="ac5db-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac5db-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="ac5db-133">Typ in het zoekvak **Druva**, selecteer **Druva** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="ac5db-133">In the search box, type **Druva**, select **Druva** from result panel then click **Add** button to add the application.</span></span>

    ![Druva in de lijst met resultaten](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ac5db-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac5db-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ac5db-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Druva op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="ac5db-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ac5db-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Druva is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac5db-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Druva is to a user in Azure AD.</span></span> <span data-ttu-id="ac5db-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Druva tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="ac5db-138">In other words, a link relationship between an Azure AD user and the related user in Druva needs to be established.</span></span>

<span data-ttu-id="ac5db-139">Wijs in Druva, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="ac5db-139">In Druva, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ac5db-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Druva, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="ac5db-140">To configure and test Azure AD single sign-on with Druva, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ac5db-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ac5db-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ac5db-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ac5db-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ac5db-143">**[Maak een testgebruiker Druva](#create-a-druva-test-user)**  - Druva die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="ac5db-143">**[Create a Druva test user](#create-a-druva-test-user)** - to have a counterpart of Britta Simon in Druva that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ac5db-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ac5db-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ac5db-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ac5db-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ac5db-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ac5db-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ac5db-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Druva configureren.</span><span class="sxs-lookup"><span data-stu-id="ac5db-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="ac5db-148">**Voor het configureren van Azure AD eenmalige aanmelding met Druva, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ac5db-148">**To configure Azure AD single sign-on with Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="ac5db-149">In de Azure-portal op de **Druva** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ac5db-149">In the Azure portal, on the **Druva** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ac5db-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ac5db-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. <span data-ttu-id="ac5db-153">Op de **Druva domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ac5db-153">On the **Druva Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="ac5db-155">In de **aanmeldings-URL** textbox, typ de URL:`https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="ac5db-155">In the **Sign-on URL** textbox, type the URL: `https://cloud.druva.com/home`</span></span>

4. <span data-ttu-id="ac5db-156">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ac5db-156">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. <span data-ttu-id="ac5db-158">Uw toepassing Druva verwacht de SAML-asserties in een specifieke indeling waarvoor u het toevoegen van aangepast kenmerktoewijzingen aan uw **SAML-Token kenmerken** configuratie.</span><span class="sxs-lookup"><span data-stu-id="ac5db-158">Your Druva application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. <span data-ttu-id="ac5db-160">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de voorgaande afbeelding en de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ac5db-160">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>

    | <span data-ttu-id="ac5db-161">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="ac5db-161">Attribute Name</span></span>      | <span data-ttu-id="ac5db-162">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="ac5db-162">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="ac5db-163">synchroon\_auth\_token</span><span class="sxs-lookup"><span data-stu-id="ac5db-163">insync\_auth\_token</span></span> |<span data-ttu-id="ac5db-164">Voer de token gegenereerde waarde</span><span class="sxs-lookup"><span data-stu-id="ac5db-164">Enter the token generated value</span></span> |
    
    <span data-ttu-id="ac5db-165">a.</span><span class="sxs-lookup"><span data-stu-id="ac5db-165">a.</span></span> <span data-ttu-id="ac5db-166">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac5db-166">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="ac5db-169">b.</span><span class="sxs-lookup"><span data-stu-id="ac5db-169">b.</span></span> <span data-ttu-id="ac5db-170">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="ac5db-170">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="ac5db-171">c.</span><span class="sxs-lookup"><span data-stu-id="ac5db-171">c.</span></span> <span data-ttu-id="ac5db-172">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="ac5db-172">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="ac5db-173">De token gegenereerde waarde wordt verderop in de zelfstudie beschreven.</span><span class="sxs-lookup"><span data-stu-id="ac5db-173">The token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="ac5db-174">d.</span><span class="sxs-lookup"><span data-stu-id="ac5db-174">d.</span></span> <span data-ttu-id="ac5db-175">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ac5db-175">Click **Ok**.</span></span>    

7. <span data-ttu-id="ac5db-176">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ac5db-176">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ac5db-178">Op de **Druva configuratie** sectie, klikt u op **configureren Druva** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="ac5db-178">On the **Druva Configuration** section, click **Configure Druva** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ac5db-179">Kopieer de **Sign-Out URL's en SAML Single Sign-On Service** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="ac5db-179">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. <span data-ttu-id="ac5db-181">In een ander browservenster, meld u aan bij uw bedrijf Druva site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="ac5db-181">In a different web browser window, log in to your Druva company site as an administrator.</span></span>

10. <span data-ttu-id="ac5db-182">Ga naar **beheren \> instellingen**.</span><span class="sxs-lookup"><span data-stu-id="ac5db-182">Go to **Manage \> Settings**.</span></span>

    <span data-ttu-id="ac5db-183">![Instellingen](./media/active-directory-saas-druva-tutorial/ic795091.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="ac5db-183">![Settings](./media/active-directory-saas-druva-tutorial/ic795091.png "Settings")</span></span>

11. <span data-ttu-id="ac5db-184">Voer de volgende stappen uit in het dialoogvenster Instellingen voor eenmalige aanmelding:</span><span class="sxs-lookup"><span data-stu-id="ac5db-184">On the Single Sign-On Settings dialog, perform the following steps:</span></span>

    <span data-ttu-id="ac5db-185">![Eenmalige aanmelding instellingen](./media/active-directory-saas-druva-tutorial/ic795092.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="ac5db-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="ac5db-186">a.</span><span class="sxs-lookup"><span data-stu-id="ac5db-186">a.</span></span> <span data-ttu-id="ac5db-187">Plakken **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd vanuit de Azure-portal in de **ID-Provider aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="ac5db-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **ID Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="ac5db-188">b.</span><span class="sxs-lookup"><span data-stu-id="ac5db-188">b.</span></span> <span data-ttu-id="ac5db-189">Plakken **Sign-Out URL** waarde, die u hebt gekopieerd vanuit de Azure-portal in de **ID-Provider afmelding URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="ac5db-189">Paste **Sign-Out URL** value, which you have copied from the Azure portal into the **ID Provider Logout URL** textbox.</span></span>
    
     <span data-ttu-id="ac5db-190">c.</span><span class="sxs-lookup"><span data-stu-id="ac5db-190">c.</span></span> <span data-ttu-id="ac5db-191">Open uw base-64 gecodeerde certificaat in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **ID-Provider certificaat** tekstvak</span><span class="sxs-lookup"><span data-stu-id="ac5db-191">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **ID Provider Certificate** textbox</span></span>
     
     <span data-ttu-id="ac5db-192">d.</span><span class="sxs-lookup"><span data-stu-id="ac5db-192">d.</span></span> <span data-ttu-id="ac5db-193">Openen van de **instellingen** pagina, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ac5db-193">To open the **Settings** page, click **Save**.</span></span>

12. <span data-ttu-id="ac5db-194">Op de **instellingen** pagina, klikt u op **SSO-Token genereren**.</span><span class="sxs-lookup"><span data-stu-id="ac5db-194">On the **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="ac5db-195">![Instellingen](./media/active-directory-saas-druva-tutorial/ic795093.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="ac5db-195">![Settings](./media/active-directory-saas-druva-tutorial/ic795093.png "Settings")</span></span>

13. <span data-ttu-id="ac5db-196">Op de **Single Sign-on-verificatietoken** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ac5db-196">On the **Single Sign-on Authentication Token** dialog, perform the following steps:</span></span>

    <span data-ttu-id="ac5db-197">![SSO-Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO-Token")</span><span class="sxs-lookup"><span data-stu-id="ac5db-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="ac5db-198">a.</span><span class="sxs-lookup"><span data-stu-id="ac5db-198">a.</span></span> <span data-ttu-id="ac5db-199">Klik op **kopie**, plakken gekopieerd waarde in de **waarde** textbox in de **kenmerk toevoegen** sectie.</span><span class="sxs-lookup"><span data-stu-id="ac5db-199">Click **Copy**, Paste copied value in the **Value** textbox in the **Add Attribute** section.</span></span>
    
    <span data-ttu-id="ac5db-200">b.</span><span class="sxs-lookup"><span data-stu-id="ac5db-200">b.</span></span> <span data-ttu-id="ac5db-201">Klik op **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="ac5db-201">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="ac5db-202">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="ac5db-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ac5db-203">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="ac5db-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ac5db-204">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ac5db-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ac5db-205">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ac5db-205">Create an Azure AD test user</span></span>

<span data-ttu-id="ac5db-206">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ac5db-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="ac5db-208">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ac5db-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ac5db-209">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="ac5db-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ac5db-211">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ac5db-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ac5db-213">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac5db-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ac5db-215">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ac5db-215">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ac5db-217">a.</span><span class="sxs-lookup"><span data-stu-id="ac5db-217">a.</span></span> <span data-ttu-id="ac5db-218">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ac5db-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ac5db-219">b.</span><span class="sxs-lookup"><span data-stu-id="ac5db-219">b.</span></span> <span data-ttu-id="ac5db-220">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ac5db-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="ac5db-221">c.</span><span class="sxs-lookup"><span data-stu-id="ac5db-221">c.</span></span> <span data-ttu-id="ac5db-222">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="ac5db-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="ac5db-223">d.</span><span class="sxs-lookup"><span data-stu-id="ac5db-223">d.</span></span> <span data-ttu-id="ac5db-224">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ac5db-224">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="ac5db-225">Een testgebruiker Druva maken</span><span class="sxs-lookup"><span data-stu-id="ac5db-225">Create a Druva test user</span></span>

<span data-ttu-id="ac5db-226">Om Azure AD-gebruikers zich aanmelden bij Druva inschakelt, moeten ze worden ingericht in Druva.</span><span class="sxs-lookup"><span data-stu-id="ac5db-226">In order to enable Azure AD users to log in to Druva, they must be provisioned into Druva.</span></span> <span data-ttu-id="ac5db-227">In het geval van Druva is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="ac5db-227">In the case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="ac5db-228">**Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ac5db-228">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="ac5db-229">Meld u aan bij uw **Druva** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="ac5db-229">Log in to your **Druva** company site as administrator.</span></span>

2. <span data-ttu-id="ac5db-230">Ga naar **beheren \> gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ac5db-230">Go to **Manage \> Users**.</span></span>
   
   <span data-ttu-id="ac5db-231">![Gebruikers beheren](./media/active-directory-saas-druva-tutorial/ic795097.png "gebruikers beheren")</span><span class="sxs-lookup"><span data-stu-id="ac5db-231">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795097.png "Manage Users")</span></span>

3. <span data-ttu-id="ac5db-232">Klik op **maken van nieuwe**.</span><span class="sxs-lookup"><span data-stu-id="ac5db-232">Click **Create New**.</span></span>
   
   <span data-ttu-id="ac5db-233">![Gebruikers beheren](./media/active-directory-saas-druva-tutorial/ic795098.png "gebruikers beheren")</span><span class="sxs-lookup"><span data-stu-id="ac5db-233">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795098.png "Manage Users")</span></span>

4. <span data-ttu-id="ac5db-234">Voer de volgende stappen uit in het dialoogvenster Nieuwe gebruiker maken:</span><span class="sxs-lookup"><span data-stu-id="ac5db-234">On the Create New User dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="ac5db-235">![Maken van nieuwegebruiker](./media/active-directory-saas-druva-tutorial/ic795099.png "nieuwegebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="ac5db-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="ac5db-236">a.</span><span class="sxs-lookup"><span data-stu-id="ac5db-236">a.</span></span> <span data-ttu-id="ac5db-237">In de **e-mailadres** textbox, voer het e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="ac5db-237">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="ac5db-238">b.</span><span class="sxs-lookup"><span data-stu-id="ac5db-238">b.</span></span> <span data-ttu-id="ac5db-239">In de **naam** textbox, voer de naam van gebruiker zoals **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ac5db-239">In the **Name** textbox, enter the name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="ac5db-240">c.</span><span class="sxs-lookup"><span data-stu-id="ac5db-240">c.</span></span> <span data-ttu-id="ac5db-241">Klik op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="ac5db-241">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="ac5db-242">U kunt andere Druva gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Druva voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="ac5db-242">You can use any other Druva user account creation tools or APIs provided by Druva to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ac5db-243">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="ac5db-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="ac5db-244">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Druva.</span><span class="sxs-lookup"><span data-stu-id="ac5db-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Druva.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="ac5db-246">**Britta Simon om aan te wijzen Druva, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ac5db-246">**To assign Britta Simon to Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="ac5db-247">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ac5db-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ac5db-249">Selecteer in de lijst met toepassingen **Druva**.</span><span class="sxs-lookup"><span data-stu-id="ac5db-249">In the applications list, select **Druva**.</span></span>

    ![De koppeling Druva in de lijst met toepassingen](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. <span data-ttu-id="ac5db-251">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ac5db-251">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="ac5db-253">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ac5db-253">Click **Add** button.</span></span> <span data-ttu-id="ac5db-254">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac5db-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="ac5db-256">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="ac5db-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ac5db-257">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac5db-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ac5db-258">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ac5db-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ac5db-259">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ac5db-259">Test single sign-on</span></span>

<span data-ttu-id="ac5db-260">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ac5db-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ac5db-261">Als u op de tegel Druva in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Druva.</span><span class="sxs-lookup"><span data-stu-id="ac5db-261">When you click the Druva tile in the Access Panel, you should get automatically signed-on to your Druva application.</span></span>
<span data-ttu-id="ac5db-262">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ac5db-262">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ac5db-263">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ac5db-263">Additional resources</span></span>

* [<span data-ttu-id="ac5db-264">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ac5db-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ac5db-265">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ac5db-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

