---
title: 'Zelfstudie: Azure Active Directory-integratie met Teamphoria | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Teamphoria.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 2a35efb04d7fe22abc6894c149caf090666ce016
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="46a8c-103">Zelfstudie: Azure Active Directory-integratie met Teamphoria</span><span class="sxs-lookup"><span data-stu-id="46a8c-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="46a8c-104">In deze zelfstudie leert u hoe Teamphoria integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="46a8c-104">In this tutorial, you learn how to integrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="46a8c-105">Teamphoria integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="46a8c-105">Integrating Teamphoria with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="46a8c-106">U kunt beheren in Azure AD die toegang tot Teamphoria heeft</span><span class="sxs-lookup"><span data-stu-id="46a8c-106">You can control in Azure AD who has access to Teamphoria</span></span>
- <span data-ttu-id="46a8c-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Teamphoria (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="46a8c-107">You can enable your users to automatically get signed-on to Teamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="46a8c-108">U kunt uw accounts op één centrale locatie - en de Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="46a8c-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="46a8c-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="46a8c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Teamphoria, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="46a8c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="46a8c-110">Prerequisites</span></span>

<span data-ttu-id="46a8c-111">Voor het configureren van Azure AD-integratie met Teamphoria, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="46a8c-111">To configure Azure AD integration with Teamphoria, you need the following items:</span></span>

- <span data-ttu-id="46a8c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="46a8c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="46a8c-113">Een Teamphoria eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="46a8c-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="46a8c-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="46a8c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="46a8c-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="46a8c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="46a8c-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="46a8c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="46a8c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="46a8c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="46a8c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="46a8c-118">Scenario description</span></span>
<span data-ttu-id="46a8c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="46a8c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="46a8c-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="46a8c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="46a8c-121">Teamphoria uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="46a8c-121">Adding Teamphoria from the gallery</span></span>
2. <span data-ttu-id="46a8c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="46a8c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-the-gallery"></a><span data-ttu-id="46a8c-123">Teamphoria uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="46a8c-123">Adding Teamphoria from the gallery</span></span>
<span data-ttu-id="46a8c-124">Voor het configureren van de integratie van Teamphoria in Azure AD, moet u Teamphoria uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="46a8c-124">To configure the integration of Teamphoria into Azure AD, you need to add Teamphoria from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="46a8c-125">**Als u wilt toevoegen Teamphoria uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="46a8c-125">**To add Teamphoria from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="46a8c-126">In de  **[Azure Management Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="46a8c-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="46a8c-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="46a8c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="46a8c-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="46a8c-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="46a8c-131">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="46a8c-131">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="46a8c-133">Typ in het zoekvak **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="46a8c-133">In the search box, type **Teamphoria**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="46a8c-135">Selecteer in het deelvenster resultaten **Teamphoria**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="46a8c-135">In the results panel, select **Teamphoria**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="46a8c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="46a8c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="46a8c-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Teamphoria op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="46a8c-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="46a8c-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Teamphoria is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46a8c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamphoria is to a user in Azure AD.</span></span> <span data-ttu-id="46a8c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Teamphoria tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="46a8c-140">In other words, a link relationship between an Azure AD user and the related user in Teamphoria needs to be established.</span></span>

<span data-ttu-id="46a8c-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="46a8c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamphoria.</span></span>

<span data-ttu-id="46a8c-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Teamphoria, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="46a8c-142">To configure and test Azure AD single sign-on with Teamphoria, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="46a8c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="46a8c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="46a8c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="46a8c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="46a8c-145">**[Maken van een testgebruiker Teamphoria](#creating-a-teamphoria-test-user)**  - Teamphoria die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="46a8c-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - to have a counterpart of Britta Simon in Teamphoria that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="46a8c-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="46a8c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="46a8c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="46a8c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="46a8c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="46a8c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="46a8c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure-beheerportal en eenmalige aanmelding in uw toepassing Teamphoria configureren.</span><span class="sxs-lookup"><span data-stu-id="46a8c-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="46a8c-150">**Voor het configureren van Azure AD eenmalige aanmelding met Teamphoria, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="46a8c-150">**To configure Azure AD single sign-on with Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="46a8c-151">In de Azure-beheerportal op de **Teamphoria** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="46a8c-151">In the Azure Management portal, on the **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="46a8c-153">Op de **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** eenmalige aanmelding inschakelen op.</span><span class="sxs-lookup"><span data-stu-id="46a8c-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="46a8c-155">Op de **Teamphoria domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="46a8c-155">On the **Teamphoria Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="46a8c-157">a.</span><span class="sxs-lookup"><span data-stu-id="46a8c-157">a.</span></span> <span data-ttu-id="46a8c-158">In de **aanmeldings-URL** textbox, typ de URL die met het volgende patroon volgen:`https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="46a8c-158">In the **Sign-on URL** textbox, type the URL using the following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="46a8c-159">Houd er rekening mee dat deze niet de werkelijke waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="46a8c-159">Please note that these are not the real values.</span></span> <span data-ttu-id="46a8c-160">U hebt deze waarden bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="46a8c-160">You have to update these values with the actual Sign-On URL.</span></span> <span data-ttu-id="46a8c-161">Neem contact op met [Teamphoria Client ondersteuningsteam](https://www.teamphoria.com/) ophalen van de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="46a8c-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) to get the Sign-on URL.</span></span> 

4. <span data-ttu-id="46a8c-162">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaat op uw computer.</span><span class="sxs-lookup"><span data-stu-id="46a8c-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="46a8c-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="46a8c-164">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="46a8c-166">Op de **Teamphoria configuratie** sectie, klikt u op **configureren Teamphoria** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="46a8c-166">On the **Teamphoria Configuration** section, click **Configure Teamphoria** to open **Configure sign-on** window.</span></span> <span data-ttu-id="46a8c-167">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="46a8c-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="46a8c-169">Eenmalige aanmelding configureren op **Teamphoria** aan clientzijde, meld u aan bij uw toepassing Teamphoria als beheerder.</span><span class="sxs-lookup"><span data-stu-id="46a8c-169">To configure single sign-on on **Teamphoria** side, Login to your Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="46a8c-170">Ga naar **BEHEERDERSINSTELLINGEN** optie in de werkbalk links en klikt u onder de het tabblad configureren, klikt u op **SINGLE SIGN-ON** om de configuratie van SSO-venster te openen.</span><span class="sxs-lookup"><span data-stu-id="46a8c-170">Go to **ADMIN SETTINGS** option in the left toolbar and under the the Configure Tab click on **SINGLE SIGN-ON** to open the SSO configuration window.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="46a8c-172">Klik op **IDENTITEITSPROVIDER toevoegen** optie in de rechterbovenhoek om het formulier voor het toevoegen van de instellingen voor eenmalige aanmelding te openen.</span><span class="sxs-lookup"><span data-stu-id="46a8c-172">Click on **ADD NEW IDENTITY PROVIDER** option in the top right corner to open the form for adding the settings for SSO.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="46a8c-174">Voer de gegevens in de velden in zoals beschreven onderstaande-</span><span class="sxs-lookup"><span data-stu-id="46a8c-174">Enter the details in the fields as described below-</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="46a8c-176">a.</span><span class="sxs-lookup"><span data-stu-id="46a8c-176">a.</span></span> <span data-ttu-id="46a8c-177">**WEERGAVENAAM** : Geef de weergavenaam van de invoegtoepassing op de beheerpagina.</span><span class="sxs-lookup"><span data-stu-id="46a8c-177">**DISPLAY NAME** : Enter the display name of the plugin on the admin page.</span></span>

    <span data-ttu-id="46a8c-178">b.</span><span class="sxs-lookup"><span data-stu-id="46a8c-178">b.</span></span> <span data-ttu-id="46a8c-179">**NAAM van de knop** : de naam van het tabblad dat wordt weergegeven op de aanmeldingspagina voor logboekregistratie in via eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="46a8c-179">**BUTTON NAME** : The name of the tab which will display on the login page for logging in via SSO.</span></span>

    <span data-ttu-id="46a8c-180">c.</span><span class="sxs-lookup"><span data-stu-id="46a8c-180">c.</span></span> <span data-ttu-id="46a8c-181">**CERTIFICAAT** : Open het certificaat eerder hebt gedownload vanuit de Azure-portal in Kladblok, Kopieer de inhoud van dezelfde en plakt u deze hier in het vak.</span><span class="sxs-lookup"><span data-stu-id="46a8c-181">**CERTIFICATE** : Open the Certificate downloaded earlier from the Azure portal in notepad, copy the contents of the same and paste it here in the box.</span></span>

    <span data-ttu-id="46a8c-182">d.</span><span class="sxs-lookup"><span data-stu-id="46a8c-182">d.</span></span> <span data-ttu-id="46a8c-183">**TOEGANGSPUNT** : plak de **SAML Single Sign-On Service-URL** gekopieerd eerdere formulier de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="46a8c-183">**ENTRY POINT** : Paste the **SAML Single Sign-On Service URL** copied earlier form the Azure portal.</span></span>

    <span data-ttu-id="46a8c-184">e.</span><span class="sxs-lookup"><span data-stu-id="46a8c-184">e.</span></span> <span data-ttu-id="46a8c-185">De optie voor het overschakelen **ON** en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="46a8c-185">Switch the option to **ON** and click on **SAVE**.</span></span>   

<!--### Next steps

To ensure users can sign-in to Teamphoria after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Teamphoria in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="46a8c-186">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="46a8c-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="46a8c-187">Het doel van deze sectie is het een testgebruiker maken in Azure Management portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="46a8c-187">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="46a8c-189">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="46a8c-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="46a8c-190">In de **Azure Management portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="46a8c-190">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="46a8c-192">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="46a8c-192">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="46a8c-194">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="46a8c-194">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="46a8c-196">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="46a8c-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="46a8c-198">a.</span><span class="sxs-lookup"><span data-stu-id="46a8c-198">a.</span></span> <span data-ttu-id="46a8c-199">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="46a8c-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="46a8c-200">b.</span><span class="sxs-lookup"><span data-stu-id="46a8c-200">b.</span></span> <span data-ttu-id="46a8c-201">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="46a8c-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="46a8c-202">c.</span><span class="sxs-lookup"><span data-stu-id="46a8c-202">c.</span></span> <span data-ttu-id="46a8c-203">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="46a8c-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="46a8c-204">d.</span><span class="sxs-lookup"><span data-stu-id="46a8c-204">d.</span></span> <span data-ttu-id="46a8c-205">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="46a8c-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="46a8c-206">Een testgebruiker Teamphoria maken</span><span class="sxs-lookup"><span data-stu-id="46a8c-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="46a8c-207">Om in te schakelen gebruikers van Azure AD aan te melden bij Teamphoria, moeten ze worden ingericht in Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="46a8c-207">In order to enable Azure AD users to log into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="46a8c-208">In het geval van Teamphoria is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="46a8c-208">In the case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="46a8c-209">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="46a8c-209">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="46a8c-210">Meld u aan bij uw bedrijf Teamphoria site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="46a8c-210">Log in to your Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="46a8c-211">Klik op **ADMIN** instellingen op de werkbalk links en onder de **beheren** Klik op tabblad **gebruikers** openen de beheerpagina voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="46a8c-211">Click on **ADMIN** settings on the left toolbar and under the **MANAGE** tab Click on **USERS** to open the admin page for users.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="46a8c-213">Klik op de **handmatig uit te NODIGEN** optie.</span><span class="sxs-lookup"><span data-stu-id="46a8c-213">Click on the **MANUAL INVITE** option.</span></span>

    ![Personen uitnodigen](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="46a8c-215">Uitvoeren na de actie op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="46a8c-215">On this page, perform following action.</span></span> 
    
    ![Personen uitnodigen](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="46a8c-217">a.</span><span class="sxs-lookup"><span data-stu-id="46a8c-217">a.</span></span> <span data-ttu-id="46a8c-218">In de **e-MAILADRES** tekstvak de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="46a8c-218">In the **EMAIL ADDRESS** textbox, the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="46a8c-219">b.</span><span class="sxs-lookup"><span data-stu-id="46a8c-219">b.</span></span> <span data-ttu-id="46a8c-220">In de **VOORNAAM** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="46a8c-220">In the **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="46a8c-221">c.</span><span class="sxs-lookup"><span data-stu-id="46a8c-221">c.</span></span> <span data-ttu-id="46a8c-222">In de **ACHTERNAAM** textbox type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="46a8c-222">In the **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="46a8c-223">d.</span><span class="sxs-lookup"><span data-stu-id="46a8c-223">d.</span></span> <span data-ttu-id="46a8c-224">Klik op **uitnodiging 1 gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="46a8c-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="46a8c-225">Gebruiker moet de uitnodiging accepteren farmherstelpunten gemaakt in het systeem.</span><span class="sxs-lookup"><span data-stu-id="46a8c-225">User needs to accept the invite to get created in the system.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="46a8c-226">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="46a8c-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="46a8c-227">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="46a8c-227">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamphoria.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="46a8c-229">**Britta Simon om aan te wijzen Teamphoria, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="46a8c-229">**To assign Britta Simon to Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="46a8c-230">In de Azure-beheerportal, opent u de weergave toepassingen en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="46a8c-230">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="46a8c-232">Selecteer in de lijst met toepassingen **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="46a8c-232">In the applications list, select **Teamphoria**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="46a8c-234">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="46a8c-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="46a8c-236">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="46a8c-236">Click **Add** button.</span></span> <span data-ttu-id="46a8c-237">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="46a8c-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="46a8c-239">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="46a8c-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="46a8c-240">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="46a8c-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="46a8c-241">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="46a8c-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="46a8c-242">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="46a8c-242">Testing single sign-on</span></span>

<span data-ttu-id="46a8c-243">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="46a8c-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="46a8c-244">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="46a8c-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="46a8c-245">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="46a8c-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="46a8c-246">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="46a8c-246">Additional resources</span></span>

* [<span data-ttu-id="46a8c-247">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46a8c-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="46a8c-248">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="46a8c-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

