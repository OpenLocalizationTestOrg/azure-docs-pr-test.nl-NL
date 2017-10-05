---
title: 'Zelfstudie: Azure Active Directory-integratie met Lucidchart | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Lucidchart.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2dea669f03c893632c08d30feeb3173efc2d8243
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="d1b07-103">Zelfstudie: Azure Active Directory-integratie met Lucidchart</span><span class="sxs-lookup"><span data-stu-id="d1b07-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>

<span data-ttu-id="d1b07-104">In deze zelfstudie leert u hoe Lucidchart integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d1b07-104">In this tutorial, you learn how to integrate Lucidchart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d1b07-105">Lucidchart integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d1b07-105">Integrating Lucidchart with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d1b07-106">U kunt beheren in Azure AD die toegang tot Lucidchart heeft</span><span class="sxs-lookup"><span data-stu-id="d1b07-106">You can control in Azure AD who has access to Lucidchart</span></span>
- <span data-ttu-id="d1b07-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Lucidchart (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="d1b07-107">You can enable your users to automatically get signed-on to Lucidchart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d1b07-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="d1b07-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d1b07-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d1b07-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1b07-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d1b07-110">Prerequisites</span></span>

<span data-ttu-id="d1b07-111">Voor het configureren van Azure AD-integratie met Lucidchart, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="d1b07-111">To configure Azure AD integration with Lucidchart, you need the following items:</span></span>

- <span data-ttu-id="d1b07-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="d1b07-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d1b07-113">Een Lucidchart eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="d1b07-113">A Lucidchart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d1b07-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d1b07-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d1b07-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="d1b07-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d1b07-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d1b07-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d1b07-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d1b07-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d1b07-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d1b07-118">Scenario description</span></span>
<span data-ttu-id="d1b07-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d1b07-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d1b07-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d1b07-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d1b07-121">Lucidchart uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d1b07-121">Adding Lucidchart from the gallery</span></span>
2. <span data-ttu-id="d1b07-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d1b07-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lucidchart-from-the-gallery"></a><span data-ttu-id="d1b07-123">Lucidchart uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d1b07-123">Adding Lucidchart from the gallery</span></span>
<span data-ttu-id="d1b07-124">Voor het configureren van de integratie van Lucidchart in Azure AD, moet u Lucidchart uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d1b07-124">To configure the integration of Lucidchart into Azure AD, you need to add Lucidchart from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d1b07-125">**Als u wilt toevoegen Lucidchart uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d1b07-125">**To add Lucidchart from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d1b07-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d1b07-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d1b07-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d1b07-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d1b07-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d1b07-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d1b07-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d1b07-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d1b07-133">Typ in het zoekvak **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="d1b07-133">In the search box, type **Lucidchart**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. <span data-ttu-id="d1b07-135">Selecteer in het deelvenster resultaten **Lucidchart**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d1b07-135">In the results panel, select **Lucidchart**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d1b07-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d1b07-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d1b07-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Lucidchart op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="d1b07-138">In this section, you configure and test Azure AD single sign-on with Lucidchart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d1b07-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Lucidchart is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1b07-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lucidchart is to a user in Azure AD.</span></span> <span data-ttu-id="d1b07-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Lucidchart tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="d1b07-140">In other words, a link relationship between an Azure AD user and the related user in Lucidchart needs to be established.</span></span>

<span data-ttu-id="d1b07-141">Wijs in Lucidchart, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="d1b07-141">In Lucidchart, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d1b07-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Lucidchart, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="d1b07-142">To configure and test Azure AD single sign-on with Lucidchart, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d1b07-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d1b07-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d1b07-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d1b07-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d1b07-145">**[Maken van een testgebruiker Lucidchart](#creating-a-lucidchart-test-user)**  - Lucidchart die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="d1b07-145">**[Creating a Lucidchart test user](#creating-a-lucidchart-test-user)** - to have a counterpart of Britta Simon in Lucidchart that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d1b07-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d1b07-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d1b07-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d1b07-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d1b07-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d1b07-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d1b07-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Lucidchart configureren.</span><span class="sxs-lookup"><span data-stu-id="d1b07-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lucidchart application.</span></span>

<span data-ttu-id="d1b07-150">**Voor het configureren van Azure AD eenmalige aanmelding met Lucidchart, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d1b07-150">**To configure Azure AD single sign-on with Lucidchart, perform the following steps:**</span></span>

1. <span data-ttu-id="d1b07-151">In de Azure-portal op de **Lucidchart** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d1b07-151">In the Azure portal, on the **Lucidchart** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d1b07-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d1b07-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. <span data-ttu-id="d1b07-155">Op de **Lucidchart domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d1b07-155">On the **Lucidchart Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    <span data-ttu-id="d1b07-157">In de **aanmeldings-URL** textbox, typ een URL als:`https://chart2.office.lucidchart.com/saml/sso/azure`</span><span class="sxs-lookup"><span data-stu-id="d1b07-157">In the **Sign-on URL** textbox, type a URL as: `https://chart2.office.lucidchart.com/saml/sso/azure`</span></span>

4. <span data-ttu-id="d1b07-158">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d1b07-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. <span data-ttu-id="d1b07-160">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d1b07-160">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d1b07-162">In een ander browservenster, meld u bij uw bedrijf Lucidchart site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="d1b07-162">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>

7. <span data-ttu-id="d1b07-163">Klik in het menu bovenaan op **Team**.</span><span class="sxs-lookup"><span data-stu-id="d1b07-163">In the menu on the top, click **Team**.</span></span>
   
    <span data-ttu-id="d1b07-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span><span class="sxs-lookup"><span data-stu-id="d1b07-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span></span>

8. <span data-ttu-id="d1b07-165">Klik op **toepassingen \> SAML beheren**.</span><span class="sxs-lookup"><span data-stu-id="d1b07-165">Click **Applications \> Manage SAML**.</span></span>
   
    <span data-ttu-id="d1b07-166">![Beheren van SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "SAML beheren")</span><span class="sxs-lookup"><span data-stu-id="d1b07-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML")</span></span>

9. <span data-ttu-id="d1b07-167">Op de **SAML-verificatie-instellingen** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d1b07-167">On the **SAML Authentication Settings** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="d1b07-168">a.</span><span class="sxs-lookup"><span data-stu-id="d1b07-168">a.</span></span> <span data-ttu-id="d1b07-169">Selecteer **SAML-verificatie inschakelen**, en klik vervolgens op **optioneel**.</span><span class="sxs-lookup"><span data-stu-id="d1b07-169">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

    <span data-ttu-id="d1b07-170">![Verificatie-instellingen van SAML](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML-verificatie-instellingen")</span><span class="sxs-lookup"><span data-stu-id="d1b07-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings")</span></span>
 
    <span data-ttu-id="d1b07-171">b.</span><span class="sxs-lookup"><span data-stu-id="d1b07-171">b.</span></span> <span data-ttu-id="d1b07-172">In de **domein** textbox, typt u uw domein en klik vervolgens op **wijziging certificaat**.</span><span class="sxs-lookup"><span data-stu-id="d1b07-172">In the **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

    <span data-ttu-id="d1b07-173">![Certificaat wijzigen](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "-certificaat wijzigen")</span><span class="sxs-lookup"><span data-stu-id="d1b07-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate")</span></span>
 
    <span data-ttu-id="d1b07-174">c.</span><span class="sxs-lookup"><span data-stu-id="d1b07-174">c.</span></span> <span data-ttu-id="d1b07-175">Uw gedownloade metagegevensbestand openen, de inhoud kopieert en plakt u deze in de **metagegevens uploaden** textbox.</span><span class="sxs-lookup"><span data-stu-id="d1b07-175">Open your downloaded metadata file, copy the content, and then paste it into the **Upload Metadata** textbox.</span></span>

    <span data-ttu-id="d1b07-176">![Uploaden van metagegevens](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "metagegevens uploaden")</span><span class="sxs-lookup"><span data-stu-id="d1b07-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata")</span></span>
 
    <span data-ttu-id="d1b07-177">d.</span><span class="sxs-lookup"><span data-stu-id="d1b07-177">d.</span></span> <span data-ttu-id="d1b07-178">Selecteer **nieuwe gebruikers automatisch toevoegen aan het team**, en klik vervolgens op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d1b07-178">Select **Automatically Add new users to the team**, and then click **Save changes**.</span></span>

    <span data-ttu-id="d1b07-179">![Wijzigingen opslaan](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "wijzigingen opslaan")</span><span class="sxs-lookup"><span data-stu-id="d1b07-179">![Save Changes](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Save Changes")</span></span>

> [!TIP]
> <span data-ttu-id="d1b07-180">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="d1b07-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d1b07-181">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="d1b07-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d1b07-182">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d1b07-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d1b07-183">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d1b07-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="d1b07-184">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d1b07-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d1b07-186">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d1b07-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d1b07-187">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d1b07-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d1b07-189">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="d1b07-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d1b07-191">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d1b07-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d1b07-193">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d1b07-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d1b07-195">a.</span><span class="sxs-lookup"><span data-stu-id="d1b07-195">a.</span></span> <span data-ttu-id="d1b07-196">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d1b07-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d1b07-197">b.</span><span class="sxs-lookup"><span data-stu-id="d1b07-197">b.</span></span> <span data-ttu-id="d1b07-198">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d1b07-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d1b07-199">c.</span><span class="sxs-lookup"><span data-stu-id="d1b07-199">c.</span></span> <span data-ttu-id="d1b07-200">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d1b07-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d1b07-201">d.</span><span class="sxs-lookup"><span data-stu-id="d1b07-201">d.</span></span> <span data-ttu-id="d1b07-202">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d1b07-202">Click **Create**.</span></span>
 
### <a name="creating-a-lucidchart-test-user"></a><span data-ttu-id="d1b07-203">Een testgebruiker Lucidchart maken</span><span class="sxs-lookup"><span data-stu-id="d1b07-203">Creating a Lucidchart test user</span></span>

<span data-ttu-id="d1b07-204">Er is geen actie-item voor gebruikers inrichten voor Lucidchart configuratie.</span><span class="sxs-lookup"><span data-stu-id="d1b07-204">There is no action item for you to configure user provisioning to Lucidchart.</span></span>  <span data-ttu-id="d1b07-205">Wanneer een toegewezen gebruiker probeert aan te melden bij met het toegangsvenster Lucidchart, Lucidchart u controleert of de gebruiker bestaat.</span><span class="sxs-lookup"><span data-stu-id="d1b07-205">When an assigned user tries to log into Lucidchart using the access panel, Lucidchart checks whether the user exists.</span></span>  

<span data-ttu-id="d1b07-206">Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="d1b07-206">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d1b07-207">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1b07-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d1b07-208">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="d1b07-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lucidchart.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d1b07-210">**Britta Simon om aan te wijzen Lucidchart, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d1b07-210">**To assign Britta Simon to Lucidchart, perform the following steps:**</span></span>

1. <span data-ttu-id="d1b07-211">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d1b07-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d1b07-213">Selecteer in de lijst met toepassingen **Lucidchart**.</span><span class="sxs-lookup"><span data-stu-id="d1b07-213">In the applications list, select **Lucidchart**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. <span data-ttu-id="d1b07-215">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d1b07-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d1b07-217">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d1b07-217">Click **Add** button.</span></span> <span data-ttu-id="d1b07-218">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d1b07-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d1b07-220">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d1b07-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d1b07-221">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d1b07-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d1b07-222">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d1b07-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d1b07-223">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d1b07-223">Testing single sign-on</span></span>

<span data-ttu-id="d1b07-224">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="d1b07-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d1b07-225">Als u op de tegel Lucidchart in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Lucidchart.</span><span class="sxs-lookup"><span data-stu-id="d1b07-225">When you click the Lucidchart tile in the Access Panel, you should get automatically signed-on to your Lucidchart application.</span></span>
<span data-ttu-id="d1b07-226">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d1b07-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d1b07-227">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d1b07-227">Additional resources</span></span>

* [<span data-ttu-id="d1b07-228">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d1b07-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d1b07-229">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d1b07-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png

