---
title: 'Zelfstudie: Azure Active Directory-integratie met Bridge | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Bridge.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dbb6499-80c1-4d00-a0b4-e0ad5522cf0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d2b7fd6f73f1b782cfe6337d13f9f22f9c70d389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bridge"></a><span data-ttu-id="5056e-103">Zelfstudie: Azure Active Directory-integratie met brug</span><span class="sxs-lookup"><span data-stu-id="5056e-103">Tutorial: Azure Active Directory integration with Bridge</span></span>

<span data-ttu-id="5056e-104">In deze zelfstudie leert u hoe Bridge integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5056e-104">In this tutorial, you learn how to integrate Bridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5056e-105">Bridge integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="5056e-105">Integrating Bridge with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5056e-106">U kunt beheren in Azure AD die toegang tot de brug heeft</span><span class="sxs-lookup"><span data-stu-id="5056e-106">You can control in Azure AD who has access to Bridge</span></span>
- <span data-ttu-id="5056e-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Bridge (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="5056e-107">You can enable your users to automatically get signed-on to Bridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5056e-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="5056e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5056e-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5056e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5056e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5056e-110">Prerequisites</span></span>

<span data-ttu-id="5056e-111">Voor het configureren van Azure AD-integratie met Bridge, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="5056e-111">To configure Azure AD integration with Bridge, you need the following items:</span></span>

- <span data-ttu-id="5056e-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="5056e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5056e-113">Een brug eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="5056e-113">A Bridge single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5056e-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="5056e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5056e-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="5056e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5056e-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="5056e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5056e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5056e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5056e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="5056e-118">Scenario description</span></span>
<span data-ttu-id="5056e-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="5056e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5056e-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="5056e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5056e-121">Bridge uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="5056e-121">Adding Bridge from the gallery</span></span>
2. <span data-ttu-id="5056e-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5056e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bridge-from-the-gallery"></a><span data-ttu-id="5056e-123">Bridge uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="5056e-123">Adding Bridge from the gallery</span></span>
<span data-ttu-id="5056e-124">Voor het configureren van de integratie van Bridge in Azure AD, moet u Bridge uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="5056e-124">To configure the integration of Bridge into Azure AD, you need to add Bridge from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5056e-125">**Als u wilt toevoegen Bridge uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5056e-125">**To add Bridge from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5056e-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="5056e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5056e-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5056e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5056e-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5056e-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="5056e-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5056e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="5056e-133">Typ in het zoekvak **Bridge**.</span><span class="sxs-lookup"><span data-stu-id="5056e-133">In the search box, type **Bridge**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_search.png)

5. <span data-ttu-id="5056e-135">Selecteer in het deelvenster resultaten **Bridge**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5056e-135">In the results panel, select **Bridge**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5056e-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5056e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5056e-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Bridge op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="5056e-138">In this section, you configure and test Azure AD single sign-on with Bridge based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5056e-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Bridge is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5056e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bridge is to a user in Azure AD.</span></span> <span data-ttu-id="5056e-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Bridge tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="5056e-140">In other words, a link relationship between an Azure AD user and the related user in Bridge needs to be established.</span></span>

<span data-ttu-id="5056e-141">Wijs in Bridge de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="5056e-141">In Bridge, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5056e-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Bridge, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="5056e-142">To configure and test Azure AD single sign-on with Bridge, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5056e-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5056e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5056e-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5056e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5056e-145">**[Maken van een testgebruiker Bridge](#creating-a-bridge-test-user)**  - Bridge die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="5056e-145">**[Creating a Bridge test user](#creating-a-bridge-test-user)** - to have a counterpart of Britta Simon in Bridge that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5056e-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="5056e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5056e-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="5056e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5056e-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="5056e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5056e-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Bridge configureren.</span><span class="sxs-lookup"><span data-stu-id="5056e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bridge application.</span></span>

<span data-ttu-id="5056e-150">**Voor het configureren van Azure AD eenmalige aanmelding met Bridge, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5056e-150">**To configure Azure AD single sign-on with Bridge, perform the following steps:**</span></span>

1. <span data-ttu-id="5056e-151">In de Azure-portal op de **Bridge** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="5056e-151">In the Azure portal, on the **Bridge** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="5056e-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="5056e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_samlbase.png)

3. <span data-ttu-id="5056e-155">Op de **Bridge domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="5056e-155">On the **Bridge Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_url.png)

    <span data-ttu-id="5056e-157">a.</span><span class="sxs-lookup"><span data-stu-id="5056e-157">a.</span></span> <span data-ttu-id="5056e-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.bridgeapp.com`</span><span class="sxs-lookup"><span data-stu-id="5056e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.bridgeapp.com`</span></span>

    <span data-ttu-id="5056e-159">b.</span><span class="sxs-lookup"><span data-stu-id="5056e-159">b.</span></span> <span data-ttu-id="5056e-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.bridgeapp.com`</span><span class="sxs-lookup"><span data-stu-id="5056e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.bridgeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5056e-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="5056e-161">These values are not real.</span></span> <span data-ttu-id="5056e-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="5056e-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5056e-163">Neem contact op met [Bridge Client ondersteuningsteam](https://community.bridgeapp.com/community/help) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="5056e-163">Contact [Bridge Client support team](https://community.bridgeapp.com/community/help) to get these values.</span></span> 
 
4. <span data-ttu-id="5056e-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Raw)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="5056e-164">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_certificate.png) 

5. <span data-ttu-id="5056e-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="5056e-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5056e-168">Op de **Bridge configuratie** sectie, klikt u op **configureren Bridge** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="5056e-168">On the **Bridge Configuration** section, click **Configure Bridge** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5056e-169">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="5056e-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_configure.png) 

7. <span data-ttu-id="5056e-171">Eenmalige aanmelding configureren op **Bridge** zijde, moet u de gedownloade verzenden **Certificate(Raw)** en **SAML entiteit-ID, SAML Single Sign-On Service-URL en de URL Sign-Out** naar [Bridge ondersteuningsteam](https://community.bridgeapp.com/community/help).</span><span class="sxs-lookup"><span data-stu-id="5056e-171">To configure single sign-on on **Bridge** side, you need to send the downloaded **Certificate(Raw)** and **SAML Entity ID, SAML Single Sign-On Service URL, and Sign-Out URL** to [Bridge support team](https://community.bridgeapp.com/community/help).</span></span> 

> [!TIP]
> <span data-ttu-id="5056e-172">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="5056e-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5056e-173">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="5056e-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5056e-174">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5056e-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5056e-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="5056e-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="5056e-176">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="5056e-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="5056e-178">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5056e-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5056e-179">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="5056e-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5056e-181">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="5056e-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5056e-183">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5056e-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5056e-185">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="5056e-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5056e-187">a.</span><span class="sxs-lookup"><span data-stu-id="5056e-187">a.</span></span> <span data-ttu-id="5056e-188">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5056e-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5056e-189">b.</span><span class="sxs-lookup"><span data-stu-id="5056e-189">b.</span></span> <span data-ttu-id="5056e-190">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5056e-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5056e-191">c.</span><span class="sxs-lookup"><span data-stu-id="5056e-191">c.</span></span> <span data-ttu-id="5056e-192">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="5056e-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5056e-193">d.</span><span class="sxs-lookup"><span data-stu-id="5056e-193">d.</span></span> <span data-ttu-id="5056e-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="5056e-194">Click **Create**.</span></span>
 
### <a name="creating-a-bridge-test-user"></a><span data-ttu-id="5056e-195">Maken van een testgebruiker brug</span><span class="sxs-lookup"><span data-stu-id="5056e-195">Creating a Bridge test user</span></span>

<span data-ttu-id="5056e-196">In deze sectie kunt u een gebruiker met de naam van Britta Simon in Bridge maken.</span><span class="sxs-lookup"><span data-stu-id="5056e-196">In this section, you create a user called Britta Simon in Bridge.</span></span> <span data-ttu-id="5056e-197">Werken met [Bridge Client ondersteuningsteam](https://community.bridgeapp.com/community/help) een gebruiker te maken van het platform.</span><span class="sxs-lookup"><span data-stu-id="5056e-197">Work with [Bridge Client support team](https://community.bridgeapp.com/community/help) to create a user in the platform.</span></span> <span data-ttu-id="5056e-198">U kunt de ondersteuningsticket met Bridge van verhogen <a href="https://community.bridgeapp.com/community/help">hier</a> de gebruikers van het platform brug toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5056e-198">You can raise the support ticket with Bridge from <a href="https://community.bridgeapp.com/community/help">here</a> to add the users in the Bridge platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5056e-199">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="5056e-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5056e-200">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan brug.</span><span class="sxs-lookup"><span data-stu-id="5056e-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bridge.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="5056e-202">**Britta Simon om aan te wijzen Bridge, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5056e-202">**To assign Britta Simon to Bridge, perform the following steps:**</span></span>

1. <span data-ttu-id="5056e-203">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5056e-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="5056e-205">Selecteer in de lijst met toepassingen **Bridge**.</span><span class="sxs-lookup"><span data-stu-id="5056e-205">In the applications list, select **Bridge**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_app.png) 

3. <span data-ttu-id="5056e-207">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="5056e-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="5056e-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="5056e-209">Click **Add** button.</span></span> <span data-ttu-id="5056e-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5056e-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="5056e-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5056e-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5056e-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5056e-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5056e-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5056e-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5056e-215">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5056e-215">Testing single sign-on</span></span>

<span data-ttu-id="5056e-216">In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="5056e-216">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="5056e-217">Als u op de tegel Bridge in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Bridge.</span><span class="sxs-lookup"><span data-stu-id="5056e-217">When you click the Bridge tile in the Access Panel, you should get automatically signed-on to your Bridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5056e-218">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="5056e-218">Additional resources</span></span>

* [<span data-ttu-id="5056e-219">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5056e-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5056e-220">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5056e-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_203.png

