---
title: 'Zelfstudie: Azure Active Directory-integratie met InsideView | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en InsideView.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c489a7ab-6b1f-4efb-8a66-8bc13bca78c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: f2b0a1d4bc44f8d0cd57c61e2d78950cb6a99854
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a><span data-ttu-id="0e7db-103">Zelfstudie: Azure Active Directory-integratie met InsideView</span><span class="sxs-lookup"><span data-stu-id="0e7db-103">Tutorial: Azure Active Directory integration with InsideView</span></span>

<span data-ttu-id="0e7db-104">In deze zelfstudie leert u hoe InsideView integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0e7db-104">In this tutorial, you learn how to integrate InsideView with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0e7db-105">InsideView integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="0e7db-105">Integrating InsideView with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0e7db-106">U kunt beheren in Azure AD die toegang tot InsideView heeft</span><span class="sxs-lookup"><span data-stu-id="0e7db-106">You can control in Azure AD who has access to InsideView</span></span>
- <span data-ttu-id="0e7db-107">U kunt uw gebruikers automatisch ophalen aangemeld bij InsideView (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="0e7db-107">You can enable your users to automatically get signed-on to InsideView (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0e7db-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="0e7db-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0e7db-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0e7db-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e7db-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0e7db-110">Prerequisites</span></span>

<span data-ttu-id="0e7db-111">Voor het configureren van Azure AD-integratie met InsideView, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="0e7db-111">To configure Azure AD integration with InsideView, you need the following items:</span></span>

- <span data-ttu-id="0e7db-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="0e7db-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0e7db-113">Een InsideView eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="0e7db-113">A InsideView single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0e7db-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="0e7db-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0e7db-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="0e7db-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e7db-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="0e7db-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0e7db-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e7db-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e7db-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="0e7db-118">Scenario description</span></span>
<span data-ttu-id="0e7db-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="0e7db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0e7db-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="0e7db-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e7db-121">InsideView uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="0e7db-121">Adding InsideView from the gallery</span></span>
2. <span data-ttu-id="0e7db-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0e7db-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insideview-from-the-gallery"></a><span data-ttu-id="0e7db-123">InsideView uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="0e7db-123">Adding InsideView from the gallery</span></span>
<span data-ttu-id="0e7db-124">Voor het configureren van de integratie van InsideView in naar Azure AD, moet u InsideView uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="0e7db-124">To configure the integration of InsideView in to Azure AD, you need to add InsideView from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0e7db-125">**Als u wilt toevoegen InsideView uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0e7db-125">**To add InsideView from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0e7db-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0e7db-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0e7db-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0e7db-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0e7db-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0e7db-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="0e7db-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0e7db-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="0e7db-133">Typ in het zoekvak **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="0e7db-133">In the search box, type **InsideView**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_search.png)

5. <span data-ttu-id="0e7db-135">Selecteer in het deelvenster resultaten **InsideView**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="0e7db-135">In the results panel, select **InsideView**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0e7db-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0e7db-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0e7db-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met InsideView op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="0e7db-138">In this section, you configure and test Azure AD single sign-on with InsideView based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0e7db-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in InsideView is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e7db-139">For single sign-on to work, Azure AD needs to know what the counterpart user in InsideView is to a user in Azure AD.</span></span> <span data-ttu-id="0e7db-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in InsideView tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="0e7db-140">In other words, a link relationship between an Azure AD user and the related user in InsideView needs to be established.</span></span>

<span data-ttu-id="0e7db-141">Wijs in InsideView, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="0e7db-141">In InsideView, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0e7db-142">Om te configureren en testen van Azure AD eenmalige aanmelding met InsideView, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="0e7db-142">To configure and test Azure AD single sign-on with InsideView, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0e7db-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0e7db-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0e7db-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0e7db-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0e7db-145">**[Maken van een testgebruiker InsideView](#creating-a-insideview-test-user)**  - InsideView die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="0e7db-145">**[Creating a InsideView test user](#creating-a-insideview-test-user)** - to have a counterpart of Britta Simon in InsideView that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0e7db-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0e7db-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0e7db-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="0e7db-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0e7db-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="0e7db-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0e7db-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing InsideView configureren.</span><span class="sxs-lookup"><span data-stu-id="0e7db-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your InsideView application.</span></span>

<span data-ttu-id="0e7db-150">**Voor het configureren van Azure AD eenmalige aanmelding met InsideView, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0e7db-150">**To configure Azure AD single sign-on with InsideView, perform the following steps:**</span></span>

1. <span data-ttu-id="0e7db-151">In de Azure-portal op de **InsideView** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="0e7db-151">In the Azure portal, on the **InsideView** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="0e7db-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0e7db-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_samlbase.png)

3. <span data-ttu-id="0e7db-155">Op de **InsideView domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="0e7db-155">On the **InsideView Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_url.png)
    
    <span data-ttu-id="0e7db-157">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://my.insideview.com/iv/<STS Name>/login.iv`</span><span class="sxs-lookup"><span data-stu-id="0e7db-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://my.insideview.com/iv/<STS Name>/login.iv`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0e7db-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="0e7db-158">This value is not real.</span></span> <span data-ttu-id="0e7db-159">Deze waarde bijwerken met de werkelijke antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="0e7db-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="0e7db-160">Neem contact op met [InsideView ondersteuningsteam ](mailto:support@insideview.com) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="0e7db-160">Contact [InsideView support team ](mailto:support@insideview.com) to get this value.</span></span>
 
4. <span data-ttu-id="0e7db-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Raw)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="0e7db-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_certificate.png) 

5. <span data-ttu-id="0e7db-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="0e7db-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-insideview-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0e7db-165">Op de **InsideView configuratie** sectie, klikt u op **configureren InsideView** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="0e7db-165">On the **InsideView Configuration** section, click **Configure InsideView** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0e7db-166">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="0e7db-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_configure.png) 

7. <span data-ttu-id="0e7db-168">In een ander browservenster, meld u aan bij uw bedrijf InsideView site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="0e7db-168">In a different web browser window, log in to your InsideView company site as an administrator.</span></span>

8. <span data-ttu-id="0e7db-169">Klik in de werkbalk bovenaan op **Admin**, **SingleSignOn instellingen**, en klik vervolgens op **SAML toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="0e7db-169">In the toolbar on the top, click **Admin**, **SingleSignOn Settings**, and then click **Add SAML**.</span></span>
   
   <span data-ttu-id="0e7db-170">![SAML voor eenmalige aanmelding instellingen](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML voor eenmalige aanmelding instellingen")</span><span class="sxs-lookup"><span data-stu-id="0e7db-170">![SAML Single Sign On Settings](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML Single Sign On Settings")</span></span>

9. <span data-ttu-id="0e7db-171">In de **toevoegen van een nieuwe SAML** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="0e7db-171">In the **Add a New SAML** section, perform the following steps:</span></span>

    <span data-ttu-id="0e7db-172">![Voeg een nieuwe SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "toevoegen van een nieuwe SAML")</span><span class="sxs-lookup"><span data-stu-id="0e7db-172">![Add a New SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Add a New SAML")</span></span>
   
    <span data-ttu-id="0e7db-173">a.</span><span class="sxs-lookup"><span data-stu-id="0e7db-173">a.</span></span> <span data-ttu-id="0e7db-174">In de **STS Name** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="0e7db-174">In the **STS Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="0e7db-175">b.</span><span class="sxs-lookup"><span data-stu-id="0e7db-175">b.</span></span> <span data-ttu-id="0e7db-176">In **WS-SamlP-Fed ongevraagde eindpunt** textbox, plak de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0e7db-176">In **SamlP/WS-Fed Unsolicited EndPoint** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="0e7db-177">c.</span><span class="sxs-lookup"><span data-stu-id="0e7db-177">c.</span></span> <span data-ttu-id="0e7db-178">Open uw base-64 gecodeerde certificaat dat u vanuit Azure-portal hebt gedownload, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **STS Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="0e7db-178">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **STS Certificate** textbox.</span></span>

    <span data-ttu-id="0e7db-179">d.</span><span class="sxs-lookup"><span data-stu-id="0e7db-179">d.</span></span> <span data-ttu-id="0e7db-180">In de **Crm-Id Gebruikerskoppeling** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="0e7db-180">In the **Crm User Id Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
        
    <span data-ttu-id="0e7db-181">e.</span><span class="sxs-lookup"><span data-stu-id="0e7db-181">e.</span></span> <span data-ttu-id="0e7db-182">In de **Crm e toewijzing** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="0e7db-182">In the **Crm Email Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="0e7db-183">f.</span><span class="sxs-lookup"><span data-stu-id="0e7db-183">f.</span></span> <span data-ttu-id="0e7db-184">In de **Crm voornaam toewijzing** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="0e7db-184">In the **Crm First Name Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="0e7db-185">g.</span><span class="sxs-lookup"><span data-stu-id="0e7db-185">g.</span></span> <span data-ttu-id="0e7db-186">In de **Crm lastName toewijzing** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="0e7db-186">In the **Crm lastName Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>  

    <span data-ttu-id="0e7db-187">h.</span><span class="sxs-lookup"><span data-stu-id="0e7db-187">h.</span></span> <span data-ttu-id="0e7db-188">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="0e7db-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0e7db-189">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="0e7db-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0e7db-190">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="0e7db-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0e7db-191">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0e7db-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0e7db-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="0e7db-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="0e7db-193">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0e7db-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="0e7db-195">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0e7db-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0e7db-196">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0e7db-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-insideview-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0e7db-198">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="0e7db-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-insideview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0e7db-200">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0e7db-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-insideview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0e7db-202">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="0e7db-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-insideview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0e7db-204">a.</span><span class="sxs-lookup"><span data-stu-id="0e7db-204">a.</span></span> <span data-ttu-id="0e7db-205">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0e7db-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0e7db-206">b.</span><span class="sxs-lookup"><span data-stu-id="0e7db-206">b.</span></span> <span data-ttu-id="0e7db-207">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0e7db-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0e7db-208">c.</span><span class="sxs-lookup"><span data-stu-id="0e7db-208">c.</span></span> <span data-ttu-id="0e7db-209">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="0e7db-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0e7db-210">d.</span><span class="sxs-lookup"><span data-stu-id="0e7db-210">d.</span></span> <span data-ttu-id="0e7db-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0e7db-211">Click **Create**.</span></span>
 
### <a name="creating-a-insideview-test-user"></a><span data-ttu-id="0e7db-212">Een testgebruiker InsideView maken</span><span class="sxs-lookup"><span data-stu-id="0e7db-212">Creating a InsideView test user</span></span>

<span data-ttu-id="0e7db-213">Om Azure AD-gebruikers zich aanmelden bij InsideView, moeten ze worden ingericht op InsideView.</span><span class="sxs-lookup"><span data-stu-id="0e7db-213">To enable Azure AD users to log in to InsideView, they must be provisioned in to InsideView.</span></span> <span data-ttu-id="0e7db-214">In het geval van InsideView is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="0e7db-214">In the case of InsideView, provisioning is a manual task.</span></span>

<span data-ttu-id="0e7db-215">Als u gebruikers of contactpersonen in InsideView hebt gemaakt, neem contact op met [InsideView ondersteuningsteam](mailto:support@insideview.com).</span><span class="sxs-lookup"><span data-stu-id="0e7db-215">To get users or contacts created in InsideView, Contact [InsideView support team](mailto:support@insideview.com).</span></span>

>[!NOTE]
><span data-ttu-id="0e7db-216">U kunt andere InsideView gebruiker account hulpmiddelen voor het maken of API's die is geleverd door InsideView voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="0e7db-216">You can use any other InsideView user account creation tools or APIs provided by InsideView to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0e7db-217">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e7db-217">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0e7db-218">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan InsideView.</span><span class="sxs-lookup"><span data-stu-id="0e7db-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to InsideView.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="0e7db-220">**Britta Simon om aan te wijzen InsideView, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0e7db-220">**To assign Britta Simon to InsideView, perform the following steps:**</span></span>

1. <span data-ttu-id="0e7db-221">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0e7db-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="0e7db-223">Selecteer in de lijst met toepassingen **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="0e7db-223">In the applications list, select **InsideView**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_app.png) 

3. <span data-ttu-id="0e7db-225">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="0e7db-225">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="0e7db-227">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="0e7db-227">Click **Add** button.</span></span> <span data-ttu-id="0e7db-228">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0e7db-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="0e7db-230">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="0e7db-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0e7db-231">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0e7db-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0e7db-232">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0e7db-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0e7db-233">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0e7db-233">Testing single sign-on</span></span>

<span data-ttu-id="0e7db-234">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="0e7db-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0e7db-235">Als u op de tegel InsideView in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing InsideView.</span><span class="sxs-lookup"><span data-stu-id="0e7db-235">When you click the InsideView tile in the Access Panel, you should get automatically signed-on to your InsideView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0e7db-236">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="0e7db-236">Additional resources</span></span>

* [<span data-ttu-id="0e7db-237">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e7db-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0e7db-238">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0e7db-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_203.png

