---
title: 'Zelfstudie: Azure Active Directory-integratie met Bambu door sociale Sprout | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Bambu door sociale Sprout.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 985966d26f6ed0dcd4db47589abf94260ce62bf0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="8e306-103">Zelfstudie: Azure Active Directory-integratie met Bambu door sociale Sprout</span><span class="sxs-lookup"><span data-stu-id="8e306-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="8e306-104">In deze zelfstudie leert u hoe Bambu door sociale Sprout integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8e306-104">In this tutorial, you learn how to integrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8e306-105">Bambu door sociale Sprout integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="8e306-105">Integrating Bambu by Sprout Social with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8e306-106">U kunt beheren in Azure AD die toegang tot Bambu door sociale Sprout heeft</span><span class="sxs-lookup"><span data-stu-id="8e306-106">You can control in Azure AD who has access to Bambu by Sprout Social</span></span>
- <span data-ttu-id="8e306-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Bambu door sociale Sprout (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="8e306-107">You can enable your users to automatically get signed-on to Bambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8e306-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="8e306-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8e306-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8e306-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Bambu by Sprout Social, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="8e306-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8e306-110">Prerequisites</span></span>

<span data-ttu-id="8e306-111">Voor het configureren van Azure AD-integratie met Bambu door sociale Sprout, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="8e306-111">To configure Azure AD integration with Bambu by Sprout Social, you need the following items:</span></span>

- <span data-ttu-id="8e306-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="8e306-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8e306-113">Een Bambu door sociale Sprout eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="8e306-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8e306-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="8e306-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8e306-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="8e306-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8e306-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="8e306-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="8e306-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8e306-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8e306-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="8e306-118">Scenario description</span></span>
<span data-ttu-id="8e306-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="8e306-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8e306-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="8e306-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8e306-121">Bambu door sociale Sprout uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="8e306-121">Adding Bambu by Sprout Social from the gallery</span></span>
2. <span data-ttu-id="8e306-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8e306-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-the-gallery"></a><span data-ttu-id="8e306-123">Bambu door sociale Sprout uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="8e306-123">Adding Bambu by Sprout Social from the gallery</span></span>
<span data-ttu-id="8e306-124">Voor het configureren van de integratie van Bambu door sociale Sprout in Azure AD, moet u Bambu door sociale Sprout uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="8e306-124">To configure the integration of Bambu by Sprout Social into Azure AD, you need to add Bambu by Sprout Social from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8e306-125">**Als u wilt toevoegen Bambu door sociale Sprout uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8e306-125">**To add Bambu by Sprout Social from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8e306-126">In de  **[Azure Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8e306-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8e306-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8e306-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8e306-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8e306-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="8e306-131">Klik op **nieuwe toepassing** knop boven aan het dialoogvenster nieuwe toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8e306-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="8e306-133">Typ in het zoekvak **Bambu door sociale Sprout**.</span><span class="sxs-lookup"><span data-stu-id="8e306-133">In the search box, type **Bambu by Sprout Social**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. <span data-ttu-id="8e306-135">Selecteer in het deelvenster resultaten **Bambu door sociale Sprout**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="8e306-135">In the results panel, select **Bambu by Sprout Social**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8e306-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8e306-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8e306-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Bambu door sociale Sprout op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="8e306-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8e306-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Bambu door sociale Sprout is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e306-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bambu by Sprout Social is to a user in Azure AD.</span></span> <span data-ttu-id="8e306-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Bambu door sociale Sprout tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="8e306-140">In other words, a link relationship between an Azure AD user and the related user in Bambu by Sprout Social needs to be established.</span></span>

<span data-ttu-id="8e306-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Bambu door sociale Sprout.</span><span class="sxs-lookup"><span data-stu-id="8e306-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="8e306-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Bambu door sociale Sprout, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="8e306-142">To configure and test Azure AD single sign-on with Bambu by Sprout Social, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8e306-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8e306-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8e306-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e306-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8e306-145">**[Maken van een Bambu door sociale Sprout testgebruiker](#creating-a-bambu-by-sprout-social-test-user)**  - Bambu door Sprout sociale die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="8e306-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - to have a counterpart of Britta Simon in Bambu by Sprout Social that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="8e306-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8e306-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8e306-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="8e306-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8e306-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="8e306-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8e306-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw Bambu configureren door sociale Sprout toepassing.</span><span class="sxs-lookup"><span data-stu-id="8e306-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="8e306-150">**Voor het configureren van Azure AD eenmalige aanmelding met Bambu door sociale Sprout, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8e306-150">**To configure Azure AD single sign-on with Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="8e306-151">In de Azure-portal op de **Bambu door sociale Sprout** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="8e306-151">In the Azure portal, on the **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="8e306-153">Op de **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** eenmalige aanmelding inschakelen op.</span><span class="sxs-lookup"><span data-stu-id="8e306-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. <span data-ttu-id="8e306-155">Op de **Bambu door de URL's en sociale domein Sprout** sectie, de gebruiker heeft geen alle stappen uitvoeren als de app al vooraf is geïntegreerd met Azure.</span><span class="sxs-lookup"><span data-stu-id="8e306-155">On the **Bambu by Sprout Social Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. <span data-ttu-id="8e306-157">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="8e306-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. <span data-ttu-id="8e306-159">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="8e306-159">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="8e306-161">Op de **Bambu door sociale configuratie Sprout** sectie, klikt u op **Bambu configureren door sociale Sprout** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="8e306-161">On the **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8e306-162">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="8e306-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. <span data-ttu-id="8e306-164">Eenmalige aanmelding configureren op **Bambu door sociale Sprout** zijde, moet u de gedownloade verzenden **Metadata XML** en **SAML Single Sign-On Service-URL** naar [Bambu sociale Sprout Support](mailto:support@getbambu.com).</span><span class="sxs-lookup"><span data-stu-id="8e306-164">To configure single sign-on on **Bambu by Sprout Social** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="8e306-165">Ze zullen dit instellen om de SAML SSO-verbinding juist is ingesteld op beide zijden.</span><span class="sxs-lookup"><span data-stu-id="8e306-165">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8e306-166">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="8e306-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8e306-167">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u gewoon op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="8e306-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click on the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8e306-168">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8e306-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

To ensure users can sign-in to Bambu by Sprout Social after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Bambu by Sprout Social in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8e306-169">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="8e306-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="8e306-170">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="8e306-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="8e306-172">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8e306-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8e306-173">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8e306-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8e306-175">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="8e306-175">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8e306-177">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8e306-177">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8e306-179">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8e306-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8e306-181">a.</span><span class="sxs-lookup"><span data-stu-id="8e306-181">a.</span></span> <span data-ttu-id="8e306-182">In de **naam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8e306-182">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="8e306-183">b.</span><span class="sxs-lookup"><span data-stu-id="8e306-183">b.</span></span> <span data-ttu-id="8e306-184">In de **gebruikersnaam** textbox type de **e-mailadres** van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e306-184">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="8e306-185">c.</span><span class="sxs-lookup"><span data-stu-id="8e306-185">c.</span></span> <span data-ttu-id="8e306-186">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="8e306-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8e306-187">d.</span><span class="sxs-lookup"><span data-stu-id="8e306-187">d.</span></span> <span data-ttu-id="8e306-188">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8e306-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="8e306-189">Een Bambu door sociale Sprout testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="8e306-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="8e306-190">Toepassing ondersteunt Just in tijd gebruikers inrichten en na verificatie gebruikers wordt in de toepassing automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8e306-190">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8e306-191">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e306-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8e306-192">In deze sectie maakt inschakelen u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan Bambu door sociale Sprout.</span><span class="sxs-lookup"><span data-stu-id="8e306-192">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Bambu by Sprout Social.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="8e306-194">**Britta Simon om aan te wijzen Bambu door sociale Sprout, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8e306-194">**To assign Britta Simon to Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="8e306-195">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8e306-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="8e306-197">Selecteer in de lijst met toepassingen **Bambu door sociale Sprout**.</span><span class="sxs-lookup"><span data-stu-id="8e306-197">In the applications list, select **Bambu by Sprout Social**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. <span data-ttu-id="8e306-199">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="8e306-199">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="8e306-201">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="8e306-201">Click **Add** button.</span></span> <span data-ttu-id="8e306-202">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8e306-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="8e306-204">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="8e306-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8e306-205">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8e306-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8e306-206">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8e306-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8e306-207">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8e306-207">Testing single sign-on</span></span>

<span data-ttu-id="8e306-208">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="8e306-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8e306-209">Als u op de Bambu door sociale Sprout tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw Bambu door sociale Sprout toepassing.</span><span class="sxs-lookup"><span data-stu-id="8e306-209">When you click the Bambu by Sprout Social tile in the Access Panel, you should get automatically signed-on to your Bambu by Sprout Social application.</span></span> <span data-ttu-id="8e306-210">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="8e306-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8e306-211">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8e306-211">Additional resources</span></span>

* [<span data-ttu-id="8e306-212">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e306-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8e306-213">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8e306-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png

