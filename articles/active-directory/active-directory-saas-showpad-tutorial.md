---
title: 'Zelfstudie: Azure Active Directory-integratie met Showpad | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Showpad.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48b6bee0-dbc5-4863-964d-75b25e517741
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: c8b39c9215675d8073f896f934339e7cd55334cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-showpad"></a><span data-ttu-id="9d219-103">Zelfstudie: Azure Active Directory-integratie met Showpad</span><span class="sxs-lookup"><span data-stu-id="9d219-103">Tutorial: Azure Active Directory integration with Showpad</span></span>

<span data-ttu-id="9d219-104">In deze zelfstudie leert u hoe Showpad integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9d219-104">In this tutorial, you learn how to integrate Showpad with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d219-105">Showpad integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="9d219-105">Integrating Showpad with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9d219-106">U kunt beheren in Azure AD die toegang tot Showpad heeft</span><span class="sxs-lookup"><span data-stu-id="9d219-106">You can control in Azure AD who has access to Showpad</span></span>
- <span data-ttu-id="9d219-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Showpad (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="9d219-107">You can enable your users to automatically get signed-on to Showpad (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9d219-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="9d219-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9d219-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9d219-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d219-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9d219-110">Prerequisites</span></span>

<span data-ttu-id="9d219-111">Voor het configureren van Azure AD-integratie met Showpad, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="9d219-111">To configure Azure AD integration with Showpad, you need the following items:</span></span>

- <span data-ttu-id="9d219-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="9d219-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9d219-113">Een Showpad eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="9d219-113">A Showpad single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d219-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="9d219-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9d219-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="9d219-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9d219-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="9d219-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9d219-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d219-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d219-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="9d219-118">Scenario description</span></span>
<span data-ttu-id="9d219-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="9d219-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9d219-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="9d219-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9d219-121">Showpad uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9d219-121">Adding Showpad from the gallery</span></span>
2. <span data-ttu-id="9d219-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9d219-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-showpad-from-the-gallery"></a><span data-ttu-id="9d219-123">Showpad uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9d219-123">Adding Showpad from the gallery</span></span>

<span data-ttu-id="9d219-124">Voor het configureren van de integratie van Showpad in Azure AD, moet u Showpad uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="9d219-124">To configure the integration of Showpad into Azure AD, you need to add Showpad from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9d219-125">**Als u wilt toevoegen Showpad uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9d219-125">**To add Showpad from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9d219-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9d219-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9d219-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9d219-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9d219-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9d219-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="9d219-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d219-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="9d219-133">Typ in het zoekvak **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="9d219-133">In the search box, type **Showpad**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_search.png)

5. <span data-ttu-id="9d219-135">Selecteer in het deelvenster resultaten **Showpad**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9d219-135">In the results panel, select **Showpad**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9d219-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9d219-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="9d219-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Showpad op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="9d219-138">In this section, you configure and test Azure AD single sign-on with Showpad based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9d219-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Showpad is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d219-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Showpad is to a user in Azure AD.</span></span> <span data-ttu-id="9d219-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Showpad tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="9d219-140">In other words, a link relationship between an Azure AD user and the related user in Showpad needs to be established.</span></span>

<span data-ttu-id="9d219-141">Wijs in Showpad, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="9d219-141">In Showpad, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9d219-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Showpad, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="9d219-142">To configure and test Azure AD single sign-on with Showpad, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9d219-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9d219-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9d219-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d219-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9d219-145">**[Maken van een testgebruiker Showpad](#creating-a-showpad-test-user)**  - Showpad die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="9d219-145">**[Creating a Showpad test user](#creating-a-showpad-test-user)** - to have a counterpart of Britta Simon in Showpad that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9d219-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9d219-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9d219-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="9d219-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9d219-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="9d219-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9d219-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Showpad configureren.</span><span class="sxs-lookup"><span data-stu-id="9d219-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Showpad application.</span></span>

<span data-ttu-id="9d219-150">**Voor het configureren van Azure AD eenmalige aanmelding met Showpad, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9d219-150">**To configure Azure AD single sign-on with Showpad, perform the following steps:**</span></span>

1. <span data-ttu-id="9d219-151">In de Azure-portal op de **Showpad** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="9d219-151">In the Azure portal, on the **Showpad** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="9d219-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9d219-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_samlbase.png)

3. <span data-ttu-id="9d219-155">Op de **Showpad domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9d219-155">On the **Showpad Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_url.png)

    <span data-ttu-id="9d219-157">a.</span><span class="sxs-lookup"><span data-stu-id="9d219-157">a.</span></span> <span data-ttu-id="9d219-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<comapany-name>.showpad.biz/login`</span><span class="sxs-lookup"><span data-stu-id="9d219-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<comapany-name>.showpad.biz/login`</span></span>

    <span data-ttu-id="9d219-159">b.</span><span class="sxs-lookup"><span data-stu-id="9d219-159">b.</span></span> <span data-ttu-id="9d219-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<company-name>.showpad.biz`</span><span class="sxs-lookup"><span data-stu-id="9d219-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company-name>.showpad.biz`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9d219-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="9d219-161">These values are not real.</span></span> <span data-ttu-id="9d219-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="9d219-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9d219-163">Neem contact op met [Showpad ondersteuningsteam](https://help.showpad.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="9d219-163">Contact [Showpad support team](https://help.showpad.com) to get these values.</span></span> 
 


4. <span data-ttu-id="9d219-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9d219-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_certificate.png) 

5. <span data-ttu-id="9d219-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="9d219-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-showpad-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9d219-168">Eenmalige aanmelding voor uw tenant Showpad als beheerder.</span><span class="sxs-lookup"><span data-stu-id="9d219-168">Sign-on to your Showpad tenant as an administrator.</span></span>

7. <span data-ttu-id="9d219-169">Klik in het menu bovenaan op de **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="9d219-169">In the menu on the top, click the **Settings**.</span></span>
   
    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_001.png) 

8. <span data-ttu-id="9d219-171">Navigeer naar '**Single Sign-On**'en klik op'**inschakelen**. "</span><span class="sxs-lookup"><span data-stu-id="9d219-171">Navigate to "**Single Sign-On**" and click "**Enable**."</span></span>
   
    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_002.png)

9. <span data-ttu-id="9d219-173">Op de **een SAML 2.0-Service toevoegen** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9d219-173">On the **Add a SAML 2.0 Service** dialog, perform the following steps:</span></span>
   
    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_003.png) 
   
    <span data-ttu-id="9d219-175">a.</span><span class="sxs-lookup"><span data-stu-id="9d219-175">a.</span></span> <span data-ttu-id="9d219-176">In de **naam** textbox, typ de naam van de id-Provider (bijvoorbeeld: naam van uw bedrijf).</span><span class="sxs-lookup"><span data-stu-id="9d219-176">In the **Name** textbox, type the name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="9d219-177">b.</span><span class="sxs-lookup"><span data-stu-id="9d219-177">b.</span></span> <span data-ttu-id="9d219-178">Als **metagegevensbron**, selecteer **XML**.</span><span class="sxs-lookup"><span data-stu-id="9d219-178">As **Metadata Source**, select **XML**.</span></span>
   
    <span data-ttu-id="9d219-179">c.</span><span class="sxs-lookup"><span data-stu-id="9d219-179">c.</span></span> <span data-ttu-id="9d219-180">De inhoud van metagegevens van XML-bestand, die u vanuit de Azure-portal hebt gedownload, kopieert en plakt u deze in de **Metadata XML** textbox.</span><span class="sxs-lookup"><span data-stu-id="9d219-180">Copy the content of metadata XML file, which you have downloaded from the Azure portal, and then paste it into the **Metadata XML** textbox.</span></span>
   
    <span data-ttu-id="9d219-181">d.</span><span class="sxs-lookup"><span data-stu-id="9d219-181">d.</span></span> <span data-ttu-id="9d219-182">Selecteer **automatisch inrichten van nieuwe gebruikers gebruikersaccounts wanneer deze zich aanmeldt**.</span><span class="sxs-lookup"><span data-stu-id="9d219-182">Select **Auto-provision accounts for new users when they log in**.</span></span>
   
    <span data-ttu-id="9d219-183">e.</span><span class="sxs-lookup"><span data-stu-id="9d219-183">e.</span></span> <span data-ttu-id="9d219-184">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="9d219-184">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="9d219-185">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="9d219-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9d219-186">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="9d219-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9d219-187">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9d219-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9d219-188">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="9d219-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="9d219-189">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9d219-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="9d219-191">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9d219-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9d219-192">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9d219-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-showpad-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9d219-194">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="9d219-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-showpad-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9d219-196">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d219-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-showpad-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9d219-198">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9d219-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-showpad-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9d219-200">a.</span><span class="sxs-lookup"><span data-stu-id="9d219-200">a.</span></span> <span data-ttu-id="9d219-201">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9d219-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d219-202">b.</span><span class="sxs-lookup"><span data-stu-id="9d219-202">b.</span></span> <span data-ttu-id="9d219-203">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9d219-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9d219-204">c.</span><span class="sxs-lookup"><span data-stu-id="9d219-204">c.</span></span> <span data-ttu-id="9d219-205">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="9d219-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9d219-206">d.</span><span class="sxs-lookup"><span data-stu-id="9d219-206">d.</span></span> <span data-ttu-id="9d219-207">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="9d219-207">Click **Create**.</span></span>
 
### <a name="creating-a-showpad-test-user"></a><span data-ttu-id="9d219-208">Een testgebruiker Showpad maken</span><span class="sxs-lookup"><span data-stu-id="9d219-208">Creating a Showpad test user</span></span>

<span data-ttu-id="9d219-209">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Showpad genoemd.</span><span class="sxs-lookup"><span data-stu-id="9d219-209">The objective of this section is to create a user called Britta Simon in Showpad.</span></span> 

<span data-ttu-id="9d219-210">Showpad ondersteuning biedt voor just-in-time-inrichting.</span><span class="sxs-lookup"><span data-stu-id="9d219-210">Showpad supports just-in-time provisioning.</span></span> <span data-ttu-id="9d219-211">U hebt ingeschakeld in inrichting  **[eenmalige aanmelding configureren Azure AD](#configuring-azure-ad-single-sign-on)**.</span><span class="sxs-lookup"><span data-stu-id="9d219-211">You have enabled provisioning in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**.</span></span> 

<span data-ttu-id="9d219-212">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="9d219-212">There is no action item for you in this section.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9d219-213">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d219-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9d219-214">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Showpad.</span><span class="sxs-lookup"><span data-stu-id="9d219-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Showpad.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="9d219-216">**Britta Simon om aan te wijzen Showpad, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9d219-216">**To assign Britta Simon to Showpad, perform the following steps:**</span></span>

1. <span data-ttu-id="9d219-217">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9d219-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="9d219-219">Selecteer in de lijst met toepassingen **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="9d219-219">In the applications list, select **Showpad**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_app.png) 

3. <span data-ttu-id="9d219-221">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="9d219-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="9d219-223">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="9d219-223">Click **Add** button.</span></span> <span data-ttu-id="9d219-224">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d219-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="9d219-226">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="9d219-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9d219-227">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d219-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9d219-228">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d219-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9d219-229">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9d219-229">Testing single sign-on</span></span>

<span data-ttu-id="9d219-230">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="9d219-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9d219-231">Als u op de tegel Showpad in het deelvenster toegang, u moet ophalen automatisch aangemeld bij Showpad toepassing.</span><span class="sxs-lookup"><span data-stu-id="9d219-231">When you click the Showpad tile in the Access Panel, you should get automatically signed-on to Showpad application.</span></span>
<span data-ttu-id="9d219-232">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9d219-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9d219-233">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="9d219-233">Additional resources</span></span>

* [<span data-ttu-id="9d219-234">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d219-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d219-235">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9d219-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_203.png

