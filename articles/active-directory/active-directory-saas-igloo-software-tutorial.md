---
title: 'Zelfstudie: Azure Active Directory-integratie met Igloo Software | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Igloo Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ab3891e11eb33b4d233e4fc967a40c7df06e4f4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="3c602-103">Zelfstudie: Azure Active Directory-integratie met Igloo Software</span><span class="sxs-lookup"><span data-stu-id="3c602-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="3c602-104">In deze zelfstudie leert u hoe Igloo Software integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3c602-104">In this tutorial, you learn how to integrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3c602-105">Igloo Software integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="3c602-105">Integrating Igloo Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3c602-106">U kunt beheren in Azure AD die toegang tot Igloo Software heeft</span><span class="sxs-lookup"><span data-stu-id="3c602-106">You can control in Azure AD who has access to Igloo Software</span></span>
- <span data-ttu-id="3c602-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Igloo Software (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="3c602-107">You can enable your users to automatically get signed-on to Igloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3c602-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="3c602-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3c602-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3c602-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c602-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3c602-110">Prerequisites</span></span>

<span data-ttu-id="3c602-111">Voor het configureren van Azure AD-integratie met Igloo Software, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="3c602-111">To configure Azure AD integration with Igloo Software, you need the following items:</span></span>

- <span data-ttu-id="3c602-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="3c602-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3c602-113">Een Igloo Software eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="3c602-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3c602-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3c602-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3c602-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="3c602-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3c602-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="3c602-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3c602-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3c602-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3c602-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="3c602-118">Scenario description</span></span>
<span data-ttu-id="3c602-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="3c602-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3c602-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="3c602-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3c602-121">Igloo Software uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3c602-121">Adding Igloo Software from the gallery</span></span>
2. <span data-ttu-id="3c602-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3c602-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-the-gallery"></a><span data-ttu-id="3c602-123">Igloo Software uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3c602-123">Adding Igloo Software from the gallery</span></span>
<span data-ttu-id="3c602-124">Voor het configureren van de integratie van Igloo Software in Azure AD, moet u Igloo Software uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="3c602-124">To configure the integration of Igloo Software into Azure AD, you need to add Igloo Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3c602-125">**Als u wilt toevoegen Igloo Software uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3c602-125">**To add Igloo Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3c602-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3c602-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3c602-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3c602-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3c602-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3c602-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="3c602-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3c602-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="3c602-133">Typ in het zoekvak **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="3c602-133">In the search box, type **Igloo Software**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="3c602-135">Selecteer in het deelvenster resultaten **Igloo Software**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="3c602-135">In the results panel, select **Igloo Software**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3c602-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3c602-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3c602-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Igloo Software op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="3c602-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3c602-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Igloo Software is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c602-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Igloo Software is to a user in Azure AD.</span></span> <span data-ttu-id="3c602-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Igloo Software worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3c602-140">In other words, a link relationship between an Azure AD user and the related user in Igloo Software needs to be established.</span></span>

<span data-ttu-id="3c602-141">Wijs in Igloo Software, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="3c602-141">In Igloo Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3c602-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Igloo Software, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="3c602-142">To configure and test Azure AD single sign-on with Igloo Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3c602-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3c602-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3c602-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3c602-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3c602-145">**[Maken van een testgebruiker Igloo Software](#creating-an-igloo-software-test-user)**  - Igloo-Software die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="3c602-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - to have a counterpart of Britta Simon in Igloo Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3c602-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3c602-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3c602-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="3c602-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3c602-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="3c602-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3c602-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="3c602-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="3c602-150">**Voor het configureren van Azure AD eenmalige aanmelding met Igloo Software, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3c602-150">**To configure Azure AD single sign-on with Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="3c602-151">In de Azure-portal op de **Igloo Software** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="3c602-151">In the Azure portal, on the **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="3c602-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3c602-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="3c602-155">Op de **Igloo Software domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3c602-155">On the **Igloo Software Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="3c602-157">a.</span><span class="sxs-lookup"><span data-stu-id="3c602-157">a.</span></span> <span data-ttu-id="3c602-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="3c602-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="3c602-159">b.</span><span class="sxs-lookup"><span data-stu-id="3c602-159">b.</span></span> <span data-ttu-id="3c602-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="3c602-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="3c602-161">c.</span><span class="sxs-lookup"><span data-stu-id="3c602-161">c.</span></span> <span data-ttu-id="3c602-162">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="3c602-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3c602-163">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="3c602-163">These values are not real.</span></span> <span data-ttu-id="3c602-164">Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="3c602-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="3c602-165">Neem contact op met [Igloo Software Client ondersteuningsteam](https://www.igloosoftware.com/services/support) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="3c602-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) to get these values.</span></span> 

4. <span data-ttu-id="3c602-166">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3c602-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="3c602-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="3c602-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="3c602-170">Op de **Igloo softwareconfiguratie** sectie, klikt u op **Igloo Software configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="3c602-170">On the **Igloo Software Configuration** section, click **Configure Igloo Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3c602-171">Kopieer de **Sign-Out URL's en SAML Single Sign-On Service** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="3c602-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="3c602-173">In een ander browservenster, meld u aan bij uw bedrijf Software Igloo site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="3c602-173">In a different web browser window, log in to your Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="3c602-174">Ga naar de **Configuratiescherm**.</span><span class="sxs-lookup"><span data-stu-id="3c602-174">Go to the **Control Panel**.</span></span>
   
     <span data-ttu-id="3c602-175">![Het Configuratiescherm](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Configuratiescherm")</span><span class="sxs-lookup"><span data-stu-id="3c602-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="3c602-176">In de **lidmaatschap** tabblad **aanmelding In instellingen**.</span><span class="sxs-lookup"><span data-stu-id="3c602-176">In the **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="3c602-177">![Meld u aan instellingen](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "instellingen aanmelden")</span><span class="sxs-lookup"><span data-stu-id="3c602-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="3c602-178">Klik in de sectie SAML-configuratie op **SAML-verificatie configureren**.</span><span class="sxs-lookup"><span data-stu-id="3c602-178">In the SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="3c602-179">![De SAML-configuratie](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML-configuratie")</span><span class="sxs-lookup"><span data-stu-id="3c602-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="3c602-180">In de **algemene configuratie** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3c602-180">In the **General Configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="3c602-181">![Algemene configuratie](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "algemene configuratie")</span><span class="sxs-lookup"><span data-stu-id="3c602-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="3c602-182">a.</span><span class="sxs-lookup"><span data-stu-id="3c602-182">a.</span></span> <span data-ttu-id="3c602-183">In de **verbindingsnaam** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="3c602-183">In the **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="3c602-184">b.</span><span class="sxs-lookup"><span data-stu-id="3c602-184">b.</span></span> <span data-ttu-id="3c602-185">In de **IdP aanmeldings-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3c602-185">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="3c602-186">c.</span><span class="sxs-lookup"><span data-stu-id="3c602-186">c.</span></span> <span data-ttu-id="3c602-187">In de **IdP afmelding URL** textbox, plak de waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3c602-187">In the **IdP Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="3c602-188">d.</span><span class="sxs-lookup"><span data-stu-id="3c602-188">d.</span></span> <span data-ttu-id="3c602-189">Selecteer **afmelding antwoord en Type van de HTTP-aanvraag** als **POST**.</span><span class="sxs-lookup"><span data-stu-id="3c602-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="3c602-190">e.</span><span class="sxs-lookup"><span data-stu-id="3c602-190">e.</span></span> <span data-ttu-id="3c602-191">Open uw **base 64-** in Kladblok een gecodeerd certificaat gedownload vanuit Azure-portal, de inhoud van het kopiëren naar het Klembord en plakt u deze naar de **openbaar certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="3c602-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="3c602-192">In de **respons en de configuratie van verificatie**, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3c602-192">In the **Response and Authentication Configuration**, perform the following steps:</span></span>
    
    <span data-ttu-id="3c602-193">![Respons en de configuratie van verificatie](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "respons en de configuratie van verificatie")</span><span class="sxs-lookup"><span data-stu-id="3c602-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="3c602-194">a.</span><span class="sxs-lookup"><span data-stu-id="3c602-194">a.</span></span> <span data-ttu-id="3c602-195">Als **identiteitsprovider**, selecteer **Microsoft ADFS**.</span><span class="sxs-lookup"><span data-stu-id="3c602-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="3c602-196">b.</span><span class="sxs-lookup"><span data-stu-id="3c602-196">b.</span></span> <span data-ttu-id="3c602-197">Als **id van het Type**, selecteer **e-mailadres**.</span><span class="sxs-lookup"><span data-stu-id="3c602-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="3c602-198">c.</span><span class="sxs-lookup"><span data-stu-id="3c602-198">c.</span></span> <span data-ttu-id="3c602-199">In de **e kenmerk** textbox type **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="3c602-199">In the **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="3c602-200">d.</span><span class="sxs-lookup"><span data-stu-id="3c602-200">d.</span></span> <span data-ttu-id="3c602-201">In de **voornaam kenmerk** textbox type **givenname**.</span><span class="sxs-lookup"><span data-stu-id="3c602-201">In the **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="3c602-202">e.</span><span class="sxs-lookup"><span data-stu-id="3c602-202">e.</span></span> <span data-ttu-id="3c602-203">In de **laatste naamkenmerk** textbox type **achternaam**.</span><span class="sxs-lookup"><span data-stu-id="3c602-203">In the **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="3c602-204">Voer de volgende stappen uit om de configuratie te voltooien:</span><span class="sxs-lookup"><span data-stu-id="3c602-204">Perform the following steps to complete the configuration:</span></span>
    
    <span data-ttu-id="3c602-205">![Het maken van de gebruiker op aanmelden](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "aanmaken op aanmelding gebruiker")</span><span class="sxs-lookup"><span data-stu-id="3c602-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="3c602-206">a.</span><span class="sxs-lookup"><span data-stu-id="3c602-206">a.</span></span> <span data-ttu-id="3c602-207">Als **aanmaken op aanmelding gebruiker**, selecteer **Maak een nieuwe gebruiker in uw site wanneer ze zich aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="3c602-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="3c602-208">b.</span><span class="sxs-lookup"><span data-stu-id="3c602-208">b.</span></span> <span data-ttu-id="3c602-209">Als **aanmelden instellingen**, selecteer **gebruik SAML-knop op het scherm 'Aanmelden'**.</span><span class="sxs-lookup"><span data-stu-id="3c602-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="3c602-210">c.</span><span class="sxs-lookup"><span data-stu-id="3c602-210">c.</span></span> <span data-ttu-id="3c602-211">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3c602-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3c602-212">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="3c602-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3c602-213">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="3c602-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3c602-214">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3c602-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3c602-215">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3c602-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="3c602-216">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3c602-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="3c602-218">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3c602-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3c602-219">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3c602-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3c602-221">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3c602-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3c602-223">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3c602-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3c602-225">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3c602-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3c602-227">a.</span><span class="sxs-lookup"><span data-stu-id="3c602-227">a.</span></span> <span data-ttu-id="3c602-228">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3c602-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3c602-229">b.</span><span class="sxs-lookup"><span data-stu-id="3c602-229">b.</span></span> <span data-ttu-id="3c602-230">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3c602-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3c602-231">c.</span><span class="sxs-lookup"><span data-stu-id="3c602-231">c.</span></span> <span data-ttu-id="3c602-232">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="3c602-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3c602-233">d.</span><span class="sxs-lookup"><span data-stu-id="3c602-233">d.</span></span> <span data-ttu-id="3c602-234">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3c602-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="3c602-235">Een testgebruiker Igloo Software maken</span><span class="sxs-lookup"><span data-stu-id="3c602-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="3c602-236">Er is geen actie-item voor gebruikers inrichten op Igloo Software configuratie.</span><span class="sxs-lookup"><span data-stu-id="3c602-236">There is no action item for you to configure user provisioning to Igloo Software.</span></span>  

<span data-ttu-id="3c602-237">Wanneer een toegewezen gebruiker probeert zich aanmelden bij Igloo Software in het deelvenster toegang, wordt er Igloo Software controleert of de gebruiker bestaat.</span><span class="sxs-lookup"><span data-stu-id="3c602-237">When an assigned user tries to log in to Igloo Software using the access panel, Igloo Software checks whether the user exists.</span></span>  <span data-ttu-id="3c602-238">Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="3c602-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3c602-239">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c602-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3c602-240">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="3c602-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Igloo Software.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="3c602-242">**Britta Simon om aan te wijzen Igloo Software, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3c602-242">**To assign Britta Simon to Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="3c602-243">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3c602-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="3c602-245">Selecteer in de lijst met toepassingen **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="3c602-245">In the applications list, select **Igloo Software**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="3c602-247">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="3c602-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="3c602-249">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="3c602-249">Click **Add** button.</span></span> <span data-ttu-id="3c602-250">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3c602-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="3c602-252">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="3c602-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3c602-253">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3c602-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3c602-254">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3c602-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3c602-255">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3c602-255">Testing single sign-on</span></span>

<span data-ttu-id="3c602-256">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="3c602-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3c602-257">Als u op de tegel Igloo Software in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="3c602-257">When you click the Igloo Software tile in the Access Panel, you should get automatically signed-on to your Igloo Software application.</span></span>
<span data-ttu-id="3c602-258">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3c602-258">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3c602-259">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3c602-259">Additional resources</span></span>

* [<span data-ttu-id="3c602-260">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3c602-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3c602-261">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3c602-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

