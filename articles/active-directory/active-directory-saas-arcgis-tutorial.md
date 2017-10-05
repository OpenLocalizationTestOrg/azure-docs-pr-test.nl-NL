---
title: 'Zelfstudie: Azure Active Directory-integratie met ArcGIS Online | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding van Azure Active Directory en ArcGIS Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: df72270ca6443b456c079b22425f1660aa522389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="b5397-103">Zelfstudie: Azure Active Directory-integratie met ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="b5397-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="b5397-104">In deze zelfstudie leert u hoe ArcGIS Online integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b5397-104">In this tutorial, you learn how to integrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b5397-105">Online ArcGIS integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b5397-105">Integrating ArcGIS Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b5397-106">U kunt beheren in Azure AD die toegang tot ArcGIS Online heeft</span><span class="sxs-lookup"><span data-stu-id="b5397-106">You can control in Azure AD who has access to ArcGIS Online</span></span>
- <span data-ttu-id="b5397-107">U kunt uw gebruikers automatisch ophalen aangemeld bij ArcGIS Online (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="b5397-107">You can enable your users to automatically get signed-on to ArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b5397-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b5397-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b5397-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b5397-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with ArcGIS Online, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="b5397-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b5397-110">Prerequisites</span></span>

<span data-ttu-id="b5397-111">Voor het configureren van Azure AD-integratie met ArcGIS Online, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b5397-111">To configure Azure AD integration with ArcGIS Online, you need the following items:</span></span>

- <span data-ttu-id="b5397-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b5397-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b5397-113">Een ArcGIS Online eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b5397-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b5397-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b5397-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b5397-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b5397-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b5397-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b5397-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b5397-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b5397-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b5397-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b5397-118">Scenario description</span></span>
<span data-ttu-id="b5397-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b5397-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b5397-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b5397-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b5397-121">Toevoegen van Online ArcGIS uit de galerie</span><span class="sxs-lookup"><span data-stu-id="b5397-121">Adding ArcGIS Online from the gallery</span></span>
2. <span data-ttu-id="b5397-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b5397-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-the-gallery"></a><span data-ttu-id="b5397-123">Toevoegen van Online ArcGIS uit de galerie</span><span class="sxs-lookup"><span data-stu-id="b5397-123">Adding ArcGIS Online from the gallery</span></span>
<span data-ttu-id="b5397-124">Voor het configureren van de integratie van ArcGIS Online in Azure AD, moet u ArcGIS Online uit de galerie toevoegt aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b5397-124">To configure the integration of ArcGIS Online into Azure AD, you need to add ArcGIS Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b5397-125">**Als u wilt toevoegen in de galerie ArcGIS Online, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b5397-125">**To add ArcGIS Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b5397-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b5397-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b5397-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b5397-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b5397-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b5397-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="b5397-131">Klik op **nieuwe toepassing** knop boven aan het dialoogvenster nieuwe toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b5397-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="b5397-133">Typ in het zoekvak **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="b5397-133">In the search box, type **ArcGIS Online**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="b5397-135">Selecteer in het deelvenster resultaten **ArcGIS Online**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b5397-135">In the results panel, select **ArcGIS Online**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b5397-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b5397-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b5397-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met ArcGIS Online op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="b5397-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b5397-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in ArcGIS Online is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5397-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ArcGIS Online is to a user in Azure AD.</span></span> <span data-ttu-id="b5397-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker ArcGIS online worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b5397-140">In other words, a link relationship between an Azure AD user and the related user in ArcGIS Online needs to be established.</span></span>

<span data-ttu-id="b5397-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="b5397-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="b5397-142">Om te configureren en testen van Azure AD eenmalige aanmelding met ArcGIS Online, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="b5397-142">To configure and test Azure AD single sign-on with ArcGIS Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b5397-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b5397-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b5397-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b5397-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b5397-145">**[Maken van een Online ArcGIS testgebruiker](#creating-an-arcgis-online-test-user)**  - bevatten een equivalent van Britta Simon ArcGIS Online die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b5397-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - to have a counterpart of Britta Simon in ArcGIS Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b5397-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b5397-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b5397-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b5397-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b5397-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b5397-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b5397-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing ArcGIS Online configureren.</span><span class="sxs-lookup"><span data-stu-id="b5397-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="b5397-150">**Voor het configureren van Azure AD eenmalige aanmelding met ArcGIS Online, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b5397-150">**To configure Azure AD single sign-on with ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="b5397-151">In de Azure-portal op de **ArcGIS Online** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b5397-151">In the Azure portal, on the **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b5397-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b5397-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="b5397-155">Op de **ArcGIS Online domein en de URL's** sectie, voert u de volgende stap:</span><span class="sxs-lookup"><span data-stu-id="b5397-155">On the **ArcGIS Online Domain and URLs** section, perform the following step:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="b5397-157">In de **aanmeldings-URL** textbox, typ de waarde met het volgende patroon volgen:`https://<company>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="b5397-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b5397-158">Deze waarde is niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="b5397-158">This value is not the real.</span></span> <span data-ttu-id="b5397-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b5397-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="b5397-160">Neem contact op met [ArcGIS Online Client ondersteuningsteam](http://support.esri.com/) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="b5397-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) to get this value.</span></span> 

4. <span data-ttu-id="b5397-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b5397-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="b5397-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b5397-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b5397-165">In een ander browservenster, meld u bij uw bedrijf ArcGIS site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b5397-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="b5397-166">Klik op **bewerken van instellingen**.</span><span class="sxs-lookup"><span data-stu-id="b5397-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="b5397-167">![Instellingen bewerken](./media/active-directory-saas-arcgis-tutorial/ic784742.png "instellingen bewerken")</span><span class="sxs-lookup"><span data-stu-id="b5397-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="b5397-168">Klik op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="b5397-168">Click **Security**.</span></span>

    <span data-ttu-id="b5397-169">![Beveiliging](./media/active-directory-saas-arcgis-tutorial/ic784743.png "beveiliging")</span><span class="sxs-lookup"><span data-stu-id="b5397-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="b5397-170">Onder **Enterprise aanmeldingen**, klikt u op **IDENTITEITSPROVIDER ingesteld**.</span><span class="sxs-lookup"><span data-stu-id="b5397-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="b5397-171">![Enterprise-aanmeldingen](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise-aanmeldingen")</span><span class="sxs-lookup"><span data-stu-id="b5397-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="b5397-172">Op de **identiteitsprovider ingesteld** configuratie pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b5397-172">On the **Set Identity Provider** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="b5397-173">![Instellen van de identiteitsprovider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "identiteitsprovider instellen")</span><span class="sxs-lookup"><span data-stu-id="b5397-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="b5397-174">a.</span><span class="sxs-lookup"><span data-stu-id="b5397-174">a.</span></span> <span data-ttu-id="b5397-175">In de **naam** textbox, typ de naam van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="b5397-175">In the **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="b5397-176">b.</span><span class="sxs-lookup"><span data-stu-id="b5397-176">b.</span></span> <span data-ttu-id="b5397-177">Voor **metagegevens voor de Enterprise-id-Provider worden opgegeven met behulp van**, selecteer **een bestand**.</span><span class="sxs-lookup"><span data-stu-id="b5397-177">For **Metadata for the Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="b5397-178">c.</span><span class="sxs-lookup"><span data-stu-id="b5397-178">c.</span></span> <span data-ttu-id="b5397-179">Als u wilt uw van het gedownloade metagegevensbestand uploadt, klikt u op **bestand kiezen**.</span><span class="sxs-lookup"><span data-stu-id="b5397-179">To upload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="b5397-180">d.</span><span class="sxs-lookup"><span data-stu-id="b5397-180">d.</span></span> <span data-ttu-id="b5397-181">Klik op **SET IDENTITEITSPROVIDER**.</span><span class="sxs-lookup"><span data-stu-id="b5397-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="b5397-182">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="b5397-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b5397-183">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="b5397-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b5397-184">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b5397-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b5397-185">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b5397-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="b5397-186">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b5397-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="b5397-188">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b5397-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b5397-189">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b5397-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b5397-191">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="b5397-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b5397-193">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b5397-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b5397-195">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b5397-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b5397-197">a.</span><span class="sxs-lookup"><span data-stu-id="b5397-197">a.</span></span> <span data-ttu-id="b5397-198">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b5397-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b5397-199">b.</span><span class="sxs-lookup"><span data-stu-id="b5397-199">b.</span></span> <span data-ttu-id="b5397-200">In de **gebruikersnaam** textbox type de **e-mailadres** van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b5397-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="b5397-201">c.</span><span class="sxs-lookup"><span data-stu-id="b5397-201">c.</span></span> <span data-ttu-id="b5397-202">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b5397-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b5397-203">d.</span><span class="sxs-lookup"><span data-stu-id="b5397-203">d.</span></span> <span data-ttu-id="b5397-204">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b5397-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="b5397-205">Maken van een Online ArcGIS testgebruiker</span><span class="sxs-lookup"><span data-stu-id="b5397-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="b5397-206">Om in te schakelen gebruikers van Azure AD aan te melden bij ArcGIS Online, moeten ze worden ingericht in ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="b5397-206">In order to enable Azure AD users to log into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="b5397-207">In het geval van Online ArcGIS is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="b5397-207">In the case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="b5397-208">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b5397-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="b5397-209">Meld u aan bij uw **ArcGIS** tenant.</span><span class="sxs-lookup"><span data-stu-id="b5397-209">Log in to your **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="b5397-210">Klik op **leden UITNODIGEN**.</span><span class="sxs-lookup"><span data-stu-id="b5397-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="b5397-211">![Leden uitnodigen](./media/active-directory-saas-arcgis-tutorial/ic784747.png "leden uit te nodigen")</span><span class="sxs-lookup"><span data-stu-id="b5397-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="b5397-212">Selecteer **automatisch leden toevoegen zonder een e-mailbericht te verzenden**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b5397-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="b5397-213">![Automatisch toevoegen van leden](./media/active-directory-saas-arcgis-tutorial/ic784748.png "automatisch toevoegen van leden")</span><span class="sxs-lookup"><span data-stu-id="b5397-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="b5397-214">Op de **leden** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b5397-214">On the **Members** dialog page, perform the following steps:</span></span>
   
     <span data-ttu-id="b5397-215">![Toevoegen en controleren](./media/active-directory-saas-arcgis-tutorial/ic784749.png "toevoegen en controleren")</span><span class="sxs-lookup"><span data-stu-id="b5397-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="b5397-216">a.</span><span class="sxs-lookup"><span data-stu-id="b5397-216">a.</span></span> <span data-ttu-id="b5397-217">Voer de **e**, **voornaam**, en **achternaam** van een geldige AAD-account dat u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="b5397-217">Enter the **Email**, **First Name**, and **Last Name** of a valid AAD account you want to provision.</span></span>
  
     <span data-ttu-id="b5397-218">b.</span><span class="sxs-lookup"><span data-stu-id="b5397-218">b.</span></span> <span data-ttu-id="b5397-219">Klik op **toevoegen en bekijk**.</span><span class="sxs-lookup"><span data-stu-id="b5397-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="b5397-220">Controleer de gegevens die u hebt ingevoerd, en klik vervolgens op **leden toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b5397-220">Review the data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="b5397-221">![Lid toevoegen](./media/active-directory-saas-arcgis-tutorial/ic784750.png "lid toevoegen")</span><span class="sxs-lookup"><span data-stu-id="b5397-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="b5397-222">De accounthouder Azure Active Directory wordt een e-mailbericht ontvangen en Ga als volgt een koppeling om hun account te bevestigen voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="b5397-222">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b5397-223">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5397-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b5397-224">In deze sectie maakt inschakelen u Britta Simon gebruiken Azure eenmalige aanmelding toegang verleent tot ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="b5397-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ArcGIS Online.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b5397-226">**Britta Simon om aan te wijzen ArcGIS Online, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b5397-226">**To assign Britta Simon to ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="b5397-227">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b5397-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b5397-229">Selecteer in de lijst met toepassingen **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="b5397-229">In the applications list, select **ArcGIS Online**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="b5397-231">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b5397-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="b5397-233">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b5397-233">Click **Add** button.</span></span> <span data-ttu-id="b5397-234">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b5397-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="b5397-236">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b5397-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b5397-237">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b5397-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b5397-238">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b5397-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b5397-239">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b5397-239">Testing single sign-on</span></span>

<span data-ttu-id="b5397-240">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b5397-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b5397-241">Als u op de tegel ArcGIS Online in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw ArcGIS Online-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b5397-241">When you click the ArcGIS Online tile in the Access Panel, you should get automatically signed-on to your ArcGIS Online application.</span></span>
<span data-ttu-id="b5397-242">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b5397-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b5397-243">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b5397-243">Additional resources</span></span>

* [<span data-ttu-id="b5397-244">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b5397-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b5397-245">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b5397-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

