---
title: 'Zelfstudie: Azure Active Directory-integratie met RunMyProcess | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en RunMyProcess.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f8a08ef4f90d5cb98e7648ae6001055a3f4696e8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="5aee8-103">Zelfstudie: Azure Active Directory-integratie met RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="5aee8-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="5aee8-104">In deze zelfstudie leert u hoe RunMyProcess integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5aee8-104">In this tutorial, you learn how to integrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5aee8-105">RunMyProcess integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="5aee8-105">Integrating RunMyProcess with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5aee8-106">U kunt beheren in Azure AD die toegang tot RunMyProcess heeft</span><span class="sxs-lookup"><span data-stu-id="5aee8-106">You can control in Azure AD who has access to RunMyProcess</span></span>
- <span data-ttu-id="5aee8-107">U kunt uw gebruikers automatisch ophalen aangemeld bij RunMyProcess (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="5aee8-107">You can enable your users to automatically get signed-on to RunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5aee8-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="5aee8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5aee8-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5aee8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5aee8-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5aee8-110">Prerequisites</span></span>

<span data-ttu-id="5aee8-111">Voor het configureren van Azure AD-integratie met RunMyProcess, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="5aee8-111">To configure Azure AD integration with RunMyProcess, you need the following items:</span></span>

- <span data-ttu-id="5aee8-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="5aee8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5aee8-113">Een RunMyProcess eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="5aee8-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5aee8-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="5aee8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5aee8-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="5aee8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5aee8-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="5aee8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5aee8-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden:[proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5aee8-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5aee8-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="5aee8-118">Scenario description</span></span>
<span data-ttu-id="5aee8-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="5aee8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5aee8-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="5aee8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5aee8-121">RunMyProcess uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="5aee8-121">Adding RunMyProcess from the gallery</span></span>
2. <span data-ttu-id="5aee8-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5aee8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-the-gallery"></a><span data-ttu-id="5aee8-123">RunMyProcess uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="5aee8-123">Adding RunMyProcess from the gallery</span></span>
<span data-ttu-id="5aee8-124">Voor het configureren van de integratie van RunMyProcess in Azure AD, moet u RunMyProcess uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="5aee8-124">To configure the integration of RunMyProcess into Azure AD, you need to add RunMyProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5aee8-125">**Als u wilt toevoegen RunMyProcess uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5aee8-125">**To add RunMyProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5aee8-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="5aee8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5aee8-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5aee8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5aee8-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5aee8-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="5aee8-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5aee8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="5aee8-133">Typ in het zoekvak **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="5aee8-133">In the search box, type **RunMyProcess**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. <span data-ttu-id="5aee8-135">Selecteer in het deelvenster resultaten **RunMyProcess**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5aee8-135">In the results panel, select **RunMyProcess**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5aee8-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5aee8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5aee8-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met RunMyProcess op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="5aee8-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5aee8-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in RunMyProcess is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5aee8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RunMyProcess is to a user in Azure AD.</span></span> <span data-ttu-id="5aee8-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in RunMyProcess tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="5aee8-140">In other words, a link relationship between an Azure AD user and the related user in RunMyProcess needs to be established.</span></span>

<span data-ttu-id="5aee8-141">Wijs in RunMyProcess, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="5aee8-141">In RunMyProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5aee8-142">Om te configureren en testen van Azure AD eenmalige aanmelding met RunMyProcess, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="5aee8-142">To configure and test Azure AD single sign-on with RunMyProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5aee8-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5aee8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5aee8-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5aee8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5aee8-145">**[Maken van een testgebruiker RunMyProcess](#creating-a-runmyprocess-test-user)**  - RunMyProcess die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="5aee8-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - to have a counterpart of Britta Simon in RunMyProcess that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5aee8-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="5aee8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5aee8-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="5aee8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5aee8-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="5aee8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5aee8-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing RunMyProcess configureren.</span><span class="sxs-lookup"><span data-stu-id="5aee8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="5aee8-150">**Voor het configureren van Azure AD eenmalige aanmelding met RunMyProcess, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5aee8-150">**To configure Azure AD single sign-on with RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="5aee8-151">In de Azure-portal op de **RunMyProcess** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="5aee8-151">In the Azure portal, on the **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="5aee8-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="5aee8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. <span data-ttu-id="5aee8-155">Op de **RunMyProcess domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="5aee8-155">On the **RunMyProcess Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="5aee8-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://live.runmyprocess.com/live/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="5aee8-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5aee8-158">De waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="5aee8-158">The value is not real.</span></span> <span data-ttu-id="5aee8-159">Werk de waarde met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="5aee8-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="5aee8-160">Neem contact op met [RunMyProcess Client ondersteuningsteam](mailto:support@runmyprocess.com) de waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="5aee8-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) to get the value.</span></span> 

4. <span data-ttu-id="5aee8-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="5aee8-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. <span data-ttu-id="5aee8-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="5aee8-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5aee8-165">Op de **RunMyProcess configuratie** sectie, klikt u op **configureren RunMyProcess** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="5aee8-165">On the **RunMyProcess Configuration** section, click **Configure RunMyProcess** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5aee8-166">Kopieer de **Sign-Out URL's, en SAML Single Sign-On Service** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="5aee8-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. <span data-ttu-id="5aee8-168">In een ander browservenster aanmelding bij uw tenant RunMyProcess als beheerder.</span><span class="sxs-lookup"><span data-stu-id="5aee8-168">In a different web browser window, sign-on to your RunMyProcess tenant as an administrator.</span></span>

8. <span data-ttu-id="5aee8-169">Klik in het linkernavigatievenster, **Account** en selecteer **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="5aee8-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. <span data-ttu-id="5aee8-171">Ga naar **verificatiemethode** sectie en Voer onderstaande stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5aee8-171">Go to **Authentication method** section and perform below steps:</span></span>
   
    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="5aee8-173">a.</span><span class="sxs-lookup"><span data-stu-id="5aee8-173">a.</span></span> <span data-ttu-id="5aee8-174">Als **methode**, selecteer **-SSO met Samlv2**.</span><span class="sxs-lookup"><span data-stu-id="5aee8-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="5aee8-175">b.</span><span class="sxs-lookup"><span data-stu-id="5aee8-175">b.</span></span> <span data-ttu-id="5aee8-176">In de **SSO omleiding** textbox, plak de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5aee8-176">In the **SSO redirect** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5aee8-177">c.</span><span class="sxs-lookup"><span data-stu-id="5aee8-177">c.</span></span> <span data-ttu-id="5aee8-178">In de **afmelding omleiding** textbox, plak de waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5aee8-178">In the **Logout redirect** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5aee8-179">d.</span><span class="sxs-lookup"><span data-stu-id="5aee8-179">d.</span></span> <span data-ttu-id="5aee8-180">In de **indeling naam-Id** textbox, typ de waarde van **indeling van de id** als **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="5aee8-180">In the **Name Id Format** textbox, type the value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="5aee8-181">e.</span><span class="sxs-lookup"><span data-stu-id="5aee8-181">e.</span></span> <span data-ttu-id="5aee8-182">Kopieer de inhoud van het gedownloade certificaatbestand en plakt u deze in de **certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="5aee8-182">Copy the content of the downloaded certificate file and then paste it into the **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="5aee8-183">f.</span><span class="sxs-lookup"><span data-stu-id="5aee8-183">f.</span></span> <span data-ttu-id="5aee8-184">Klik op **opslaan** pictogram.</span><span class="sxs-lookup"><span data-stu-id="5aee8-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="5aee8-185">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="5aee8-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5aee8-186">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="5aee8-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5aee8-187">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5aee8-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5aee8-188">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="5aee8-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="5aee8-189">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="5aee8-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="5aee8-191">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5aee8-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5aee8-192">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="5aee8-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5aee8-194">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="5aee8-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5aee8-196">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5aee8-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5aee8-198">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="5aee8-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5aee8-200">a.</span><span class="sxs-lookup"><span data-stu-id="5aee8-200">a.</span></span> <span data-ttu-id="5aee8-201">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5aee8-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5aee8-202">b.</span><span class="sxs-lookup"><span data-stu-id="5aee8-202">b.</span></span> <span data-ttu-id="5aee8-203">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5aee8-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5aee8-204">c.</span><span class="sxs-lookup"><span data-stu-id="5aee8-204">c.</span></span> <span data-ttu-id="5aee8-205">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="5aee8-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5aee8-206">d.</span><span class="sxs-lookup"><span data-stu-id="5aee8-206">d.</span></span> <span data-ttu-id="5aee8-207">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="5aee8-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="5aee8-208">Een testgebruiker RunMyProcess maken</span><span class="sxs-lookup"><span data-stu-id="5aee8-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="5aee8-209">Om Azure AD-gebruikers zich aanmelden bij RunMyProcess inschakelt, moeten ze worden ingericht in RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="5aee8-209">In order to enable Azure AD users to log in to RunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="5aee8-210">In het geval van RunMyProcess is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="5aee8-210">In the case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="5aee8-211">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5aee8-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="5aee8-212">Meld u aan bij uw bedrijf RunMyProcess site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="5aee8-212">Log in to your RunMyProcess company site as an administrator.</span></span>

2. <span data-ttu-id="5aee8-213">Klik op **Account** en selecteer **gebruikers** in het linkernavigatievenster, klik vervolgens op **nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="5aee8-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="5aee8-214">![Nieuwe gebruiker](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="5aee8-214">![New User](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

3. <span data-ttu-id="5aee8-215">In de **gebruikersinstellingen** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="5aee8-215">In the **User Settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="5aee8-216">![Profiel](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "profiel")</span><span class="sxs-lookup"><span data-stu-id="5aee8-216">![Profile](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="5aee8-217">a.</span><span class="sxs-lookup"><span data-stu-id="5aee8-217">a.</span></span> <span data-ttu-id="5aee8-218">Typ de **naam** en **e** van een geldig Azure AD-account die u inrichten in de bijbehorende tekstvakken wilt.</span><span class="sxs-lookup"><span data-stu-id="5aee8-218">Type the **Name** and **E-mail** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="5aee8-219">b.</span><span class="sxs-lookup"><span data-stu-id="5aee8-219">b.</span></span> <span data-ttu-id="5aee8-220">Selecteer een **IDE taal**, **taal**, en **profiel**.</span><span class="sxs-lookup"><span data-stu-id="5aee8-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="5aee8-221">c.</span><span class="sxs-lookup"><span data-stu-id="5aee8-221">c.</span></span> <span data-ttu-id="5aee8-222">Selecteer **Stuur mij e-mail voor het maken van account**.</span><span class="sxs-lookup"><span data-stu-id="5aee8-222">Select **Send account creation e-mail to me**.</span></span> 

    <span data-ttu-id="5aee8-223">d.</span><span class="sxs-lookup"><span data-stu-id="5aee8-223">d.</span></span> <span data-ttu-id="5aee8-224">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5aee8-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="5aee8-225">U kunt andere RunMyProcess gebruiker account hulpmiddelen voor het maken of API's geleverd door RunMyProcess om in te richten Azure Active Directory-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="5aee8-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess to provision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5aee8-226">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="5aee8-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5aee8-227">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="5aee8-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RunMyProcess.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="5aee8-229">**Britta Simon om aan te wijzen RunMyProcess, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="5aee8-229">**To assign Britta Simon to RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="5aee8-230">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="5aee8-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="5aee8-232">Selecteer in de lijst met toepassingen **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="5aee8-232">In the applications list, select **RunMyProcess**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. <span data-ttu-id="5aee8-234">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="5aee8-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="5aee8-236">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="5aee8-236">Click **Add** button.</span></span> <span data-ttu-id="5aee8-237">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5aee8-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="5aee8-239">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5aee8-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5aee8-240">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5aee8-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5aee8-241">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5aee8-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5aee8-242">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="5aee8-242">Testing single sign-on</span></span>

<span data-ttu-id="5aee8-243">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="5aee8-243">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="5aee8-244">Als u op de tegel RunMyProcess in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="5aee8-244">When you click the RunMyProcess tile in the Access Panel, you should get automatically signed-on to your RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5aee8-245">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="5aee8-245">Additional resources</span></span>

* [<span data-ttu-id="5aee8-246">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5aee8-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5aee8-247">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5aee8-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

