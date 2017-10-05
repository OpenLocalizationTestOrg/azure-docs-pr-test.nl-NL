---
title: 'Zelfstudie: Azure Active Directory-integratie met Samanage | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Samanage.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c54dbe407145a29a712acc3c0fb549a38ac26bed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a><span data-ttu-id="e0545-103">Zelfstudie: Azure Active Directory-integratie met Samanage</span><span class="sxs-lookup"><span data-stu-id="e0545-103">Tutorial: Azure Active Directory integration with Samanage</span></span>

<span data-ttu-id="e0545-104">In deze zelfstudie leert u hoe Samanage integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e0545-104">In this tutorial, you learn how to integrate Samanage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e0545-105">Samanage integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e0545-105">Integrating Samanage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e0545-106">U kunt beheren in Azure AD die toegang tot Samanage heeft</span><span class="sxs-lookup"><span data-stu-id="e0545-106">You can control in Azure AD who has access to Samanage</span></span>
- <span data-ttu-id="e0545-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Samanage (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="e0545-107">You can enable your users to automatically get signed-on to Samanage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e0545-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="e0545-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e0545-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e0545-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0545-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e0545-110">Prerequisites</span></span>

<span data-ttu-id="e0545-111">Voor het configureren van Azure AD-integratie met Samanage, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="e0545-111">To configure Azure AD integration with Samanage, you need the following items:</span></span>

- <span data-ttu-id="e0545-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e0545-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e0545-113">Een Samanage eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e0545-113">A Samanage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e0545-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e0545-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e0545-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e0545-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e0545-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e0545-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e0545-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e0545-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e0545-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e0545-118">Scenario description</span></span>
<span data-ttu-id="e0545-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e0545-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e0545-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e0545-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e0545-121">Samanage uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e0545-121">Adding Samanage from the gallery</span></span>
2. <span data-ttu-id="e0545-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e0545-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-samanage-from-the-gallery"></a><span data-ttu-id="e0545-123">Samanage uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e0545-123">Adding Samanage from the gallery</span></span>
<span data-ttu-id="e0545-124">Voor het configureren van de integratie van Samanage in Azure AD, moet u Samanage uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e0545-124">To configure the integration of Samanage into Azure AD, you need to add Samanage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e0545-125">**Als u wilt toevoegen Samanage uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e0545-125">**To add Samanage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e0545-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e0545-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e0545-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e0545-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e0545-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e0545-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="e0545-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e0545-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="e0545-133">Typ in het zoekvak **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="e0545-133">In the search box, type **Samanage**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. <span data-ttu-id="e0545-135">Selecteer in het deelvenster resultaten **Samanage**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e0545-135">In the results panel, select **Samanage**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e0545-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e0545-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e0545-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Samanage op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="e0545-138">In this section, you configure and test Azure AD single sign-on with Samanage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e0545-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Samanage is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0545-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Samanage is to a user in Azure AD.</span></span> <span data-ttu-id="e0545-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Samanage tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="e0545-140">In other words, a link relationship between an Azure AD user and the related user in Samanage needs to be established.</span></span>

<span data-ttu-id="e0545-141">Wijs in Samanage, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="e0545-141">In Samanage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e0545-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Samanage, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="e0545-142">To configure and test Azure AD single sign-on with Samanage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e0545-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e0545-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e0545-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e0545-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e0545-145">**[Maken van een testgebruiker Samanage](#creating-a-samanage-test-user)**  - Samanage die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="e0545-145">**[Creating a Samanage test user](#creating-a-samanage-test-user)** - to have a counterpart of Britta Simon in Samanage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e0545-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e0545-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e0545-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e0545-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e0545-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e0545-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e0545-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Samanage configureren.</span><span class="sxs-lookup"><span data-stu-id="e0545-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Samanage application.</span></span>

<span data-ttu-id="e0545-150">**Voor het configureren van Azure AD eenmalige aanmelding met Samanage, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e0545-150">**To configure Azure AD single sign-on with Samanage, perform the following steps:**</span></span>

1. <span data-ttu-id="e0545-151">In de Azure-portal op de **Samanage** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e0545-151">In the Azure portal, on the **Samanage** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e0545-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e0545-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. <span data-ttu-id="e0545-155">Op de **Samanage domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e0545-155">On the **Samanage Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    <span data-ttu-id="e0545-157">a.</span><span class="sxs-lookup"><span data-stu-id="e0545-157">a.</span></span> <span data-ttu-id="e0545-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<Company Name>.samanage.com/saml_login/<Company Name>`</span><span class="sxs-lookup"><span data-stu-id="e0545-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span></span>

    <span data-ttu-id="e0545-159">b.</span><span class="sxs-lookup"><span data-stu-id="e0545-159">b.</span></span> <span data-ttu-id="e0545-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<Company Name>.samanage.com`</span><span class="sxs-lookup"><span data-stu-id="e0545-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e0545-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="e0545-161">These values are not real.</span></span> <span data-ttu-id="e0545-162">Deze waarden bijwerken met de werkelijke aanmeldings-URL en de id, die verderop in de zelfstudie wordt uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="e0545-162">Update these values with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span></span> <span data-ttu-id="e0545-163">Voor meer informatie contact op met [Samanage Client ondersteuningsteam](https://www.samanage.com/support).</span><span class="sxs-lookup"><span data-stu-id="e0545-163">For more details contact [Samanage Client support team](https://www.samanage.com/support).</span></span>    
 
4. <span data-ttu-id="e0545-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e0545-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. <span data-ttu-id="e0545-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e0545-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e0545-168">Op de **Samanage configuratie** sectie, klikt u op **configureren Samanage** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="e0545-168">On the **Samanage Configuration** section, click **Configure Samanage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e0545-169">Kopieer de **Sign-Out-URL en SAML entiteit-ID** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="e0545-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. <span data-ttu-id="e0545-171">In een ander browservenster, meld u bij uw bedrijf Samanage site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e0545-171">In a different web browser window, log into your Samanage company site as an administrator.</span></span>

8. <span data-ttu-id="e0545-172">Klik op **Dashboard** en selecteer **Setup** in het navigatiedeelvenster links.</span><span class="sxs-lookup"><span data-stu-id="e0545-172">Click **Dashboard** and select **Setup** in left navigation pane.</span></span>
   
    <span data-ttu-id="e0545-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span><span class="sxs-lookup"><span data-stu-id="e0545-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span></span>

9. <span data-ttu-id="e0545-174">Klik op **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="e0545-174">Click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="e0545-175">![Eenmalige aanmelding](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="e0545-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span></span>

10. <span data-ttu-id="e0545-176">Navigeer naar **aanmelding via SAML** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e0545-176">Navigate to **Login using SAML** section, perform the following steps:</span></span>
   
    <span data-ttu-id="e0545-177">![Aanmelding via SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "aanmelding via SAML")</span><span class="sxs-lookup"><span data-stu-id="e0545-177">![Login using SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span></span>
 
    <span data-ttu-id="e0545-178">a.</span><span class="sxs-lookup"><span data-stu-id="e0545-178">a.</span></span> <span data-ttu-id="e0545-179">Klik op **eenmalige aanmelding met SAML inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="e0545-179">Click **Enable Single Sign-On with SAML**.</span></span>  
 
    <span data-ttu-id="e0545-180">b.</span><span class="sxs-lookup"><span data-stu-id="e0545-180">b.</span></span> <span data-ttu-id="e0545-181">In de **identiteit Provider URL** textbox, plak de waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e0545-181">In the **Identity Provider URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>    
 
    <span data-ttu-id="e0545-182">c.</span><span class="sxs-lookup"><span data-stu-id="e0545-182">c.</span></span> <span data-ttu-id="e0545-183">Bevestig de **aanmeldings-URL** overeenkomt met de **aanmelding op URL** van **Samanage domein en de URL's** sectie in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e0545-183">Confirm the **Login URL** matches the **Sign On URL** of **Samanage Domain and URLs** section in Azure portal.</span></span>
 
    <span data-ttu-id="e0545-184">d.</span><span class="sxs-lookup"><span data-stu-id="e0545-184">d.</span></span> <span data-ttu-id="e0545-185">In de **afmelding URL** textbox, voer de waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e0545-185">In the **Logout URL** textbox, enter the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="e0545-186">e.</span><span class="sxs-lookup"><span data-stu-id="e0545-186">e.</span></span> <span data-ttu-id="e0545-187">In de **SAML verlener** textbox, type URI van de app-id moet worden ingesteld in de id-provider.</span><span class="sxs-lookup"><span data-stu-id="e0545-187">In the **SAML Issuer** textbox, type the app id URI set in your identity provider.</span></span>
 
    <span data-ttu-id="e0545-188">f.</span><span class="sxs-lookup"><span data-stu-id="e0545-188">f.</span></span> <span data-ttu-id="e0545-189">Open uw base-64 gecodeerde certificaat gedownload vanuit Azure-portal in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **plak uw id-Provider-x.509-certificaat onderstaande** textbox.</span><span class="sxs-lookup"><span data-stu-id="e0545-189">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **Paste your Identity Provider x.509 Certificate below** textbox.</span></span>
 
    <span data-ttu-id="e0545-190">g.</span><span class="sxs-lookup"><span data-stu-id="e0545-190">g.</span></span> <span data-ttu-id="e0545-191">Klik op **gebruikers maken als ze bestaan niet in Samanage**.</span><span class="sxs-lookup"><span data-stu-id="e0545-191">Click **Create users if they do not exist in Samanage**.</span></span>
 
    <span data-ttu-id="e0545-192">h.</span><span class="sxs-lookup"><span data-stu-id="e0545-192">h.</span></span> <span data-ttu-id="e0545-193">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="e0545-193">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="e0545-194">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="e0545-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e0545-195">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="e0545-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e0545-196">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e0545-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e0545-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e0545-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="e0545-198">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e0545-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="e0545-200">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e0545-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e0545-201">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e0545-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e0545-203">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e0545-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e0545-205">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e0545-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e0545-207">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e0545-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e0545-209">a.</span><span class="sxs-lookup"><span data-stu-id="e0545-209">a.</span></span> <span data-ttu-id="e0545-210">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e0545-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e0545-211">b.</span><span class="sxs-lookup"><span data-stu-id="e0545-211">b.</span></span> <span data-ttu-id="e0545-212">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e0545-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e0545-213">c.</span><span class="sxs-lookup"><span data-stu-id="e0545-213">c.</span></span> <span data-ttu-id="e0545-214">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e0545-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e0545-215">d.</span><span class="sxs-lookup"><span data-stu-id="e0545-215">d.</span></span> <span data-ttu-id="e0545-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e0545-216">Click **Create**.</span></span>
 
### <a name="creating-a-samanage-test-user"></a><span data-ttu-id="e0545-217">Een testgebruiker Samanage maken</span><span class="sxs-lookup"><span data-stu-id="e0545-217">Creating a Samanage test user</span></span>

<span data-ttu-id="e0545-218">Om Azure AD-gebruikers zich aanmelden bij Samanage, moeten ze worden ingericht in Samanage.</span><span class="sxs-lookup"><span data-stu-id="e0545-218">To enable Azure AD users to log in to Samanage, they must be provisioned into Samanage.</span></span>  
<span data-ttu-id="e0545-219">In het geval van Samanage is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="e0545-219">In the case of Samanage, provisioning is a manual task.</span></span>

<span data-ttu-id="e0545-220">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e0545-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="e0545-221">Meld u aan bij uw bedrijf Samanage site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e0545-221">Log into your Samanage company site as an administrator.</span></span>

2. <span data-ttu-id="e0545-222">Klik op **Dashboard** en selecteer **Setup** in het linkernavigatievenster pan.</span><span class="sxs-lookup"><span data-stu-id="e0545-222">Click **Dashboard** and select **Setup** in left navigation pan.</span></span>
   
    <span data-ttu-id="e0545-223">![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="e0545-223">![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span></span>

3. <span data-ttu-id="e0545-224">Klik op de **gebruikers** tabblad</span><span class="sxs-lookup"><span data-stu-id="e0545-224">Click the **Users** tab</span></span>
   
    <span data-ttu-id="e0545-225">![Gebruikers](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="e0545-225">![Users](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Users")</span></span>

4. <span data-ttu-id="e0545-226">Klik op **nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="e0545-226">Click **New User**.</span></span>
   
    <span data-ttu-id="e0545-227">![Nieuwe gebruiker](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="e0545-227">![New User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "New User")</span></span>

5. <span data-ttu-id="e0545-228">Typ de **naam** en de **e-mailadres** van een Azure Active Directory-account dat u wilt richten en klik op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="e0545-228">Type the **Name** and the **Email Address** of an Azure Active Directory account you want to provision and click **Create user**.</span></span>
   
    <span data-ttu-id="e0545-229">![Gebruiker maken](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "gebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="e0545-229">![Create User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Create User")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="e0545-230">De accounthouder Azure Active Directory wordt een e-mailbericht ontvangen en Ga als volgt een koppeling om hun account te bevestigen voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="e0545-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="e0545-231">U kunt andere Samanage gebruiker account hulpmiddelen voor het maken of API's geleverd door Samanage om in te richten Azure Active Directory-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="e0545-231">You can use any other Samanage user account creation tools or APIs provided by Samanage to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e0545-232">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0545-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e0545-233">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Samanage.</span><span class="sxs-lookup"><span data-stu-id="e0545-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Samanage.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="e0545-235">**Britta Simon om aan te wijzen Samanage, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e0545-235">**To assign Britta Simon to Samanage, perform the following steps:**</span></span>

1. <span data-ttu-id="e0545-236">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e0545-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e0545-238">Selecteer in de lijst met toepassingen **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="e0545-238">In the applications list, select **Samanage**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. <span data-ttu-id="e0545-240">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e0545-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="e0545-242">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e0545-242">Click **Add** button.</span></span> <span data-ttu-id="e0545-243">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e0545-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="e0545-245">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e0545-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e0545-246">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e0545-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e0545-247">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e0545-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e0545-248">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e0545-248">Testing single sign-on</span></span>

<span data-ttu-id="e0545-249">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="e0545-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e0545-250">Als u op de tegel Samanage in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Samanage.</span><span class="sxs-lookup"><span data-stu-id="e0545-250">When you click the Samanage tile in the Access Panel, you should get automatically signed-on to your Samanage application.</span></span>
<span data-ttu-id="e0545-251">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e0545-251">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e0545-252">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e0545-252">Additional resources</span></span>

* [<span data-ttu-id="e0545-253">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e0545-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e0545-254">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e0545-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

