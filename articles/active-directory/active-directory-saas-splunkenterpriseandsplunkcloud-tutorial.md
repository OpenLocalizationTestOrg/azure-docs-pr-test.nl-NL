---
title: 'Zelfstudie: Azure Active Directory-integratie met Splunk Enterprise en Splunk Cloud | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Splunk Enterprise en Splunk Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 181d0f33245f0811c15c1e7945c797502ef71eba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="80fa3-103">Zelfstudie: Azure Active Directory-integratie met Splunk Enterprise en Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="80fa3-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="80fa3-104">In deze zelfstudie leert u hoe Splunk Enterprise en Splunk Cloud integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="80fa3-104">In this tutorial, you learn how to integrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="80fa3-105">Splunk Enterprise en Splunk Cloud integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="80fa3-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="80fa3-106">U kunt beheren in Azure AD die toegang tot Splunk Enterprise en Splunk Cloud heeft</span><span class="sxs-lookup"><span data-stu-id="80fa3-106">You can control in Azure AD who has access to Splunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="80fa3-107">U kunt uw gebruikers automatisch ophalen aangemelde Splunk Enterprise-en Splunk (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="80fa3-107">You can enable your users to automatically get signed-on to Splunk Enterprise and Splunk Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="80fa3-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="80fa3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="80fa3-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="80fa3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80fa3-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="80fa3-110">Prerequisites</span></span>

<span data-ttu-id="80fa3-111">Voor het configureren van Azure AD-integratie met Splunk Enterprise en Splunk Cloud, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="80fa3-111">To configure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need the following items:</span></span>

- <span data-ttu-id="80fa3-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="80fa3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="80fa3-113">Een Splunk Enterprise en Splunk Cloud eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="80fa3-113">A Splunk Enterprise and Splunk Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="80fa3-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="80fa3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="80fa3-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="80fa3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="80fa3-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="80fa3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="80fa3-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="80fa3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="80fa3-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="80fa3-118">Scenario description</span></span>
<span data-ttu-id="80fa3-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="80fa3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="80fa3-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="80fa3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="80fa3-121">Splunk Enterprise en Splunk Cloud uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="80fa3-121">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
2. <span data-ttu-id="80fa3-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="80fa3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-splunk-enterprise-and-splunk-cloud-from-the-gallery"></a><span data-ttu-id="80fa3-123">Splunk Enterprise en Splunk Cloud uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="80fa3-123">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
<span data-ttu-id="80fa3-124">Voor het configureren van de integratie van Splunk Enterprise en Splunk Cloud met Azure AD, moet u Splunk Enterprise en Splunk Cloud uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="80fa3-124">To configure the integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need to add Splunk Enterprise and Splunk Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="80fa3-125">**Als u wilt toevoegen Splunk Enterprise en Splunk Cloud uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="80fa3-125">**To add Splunk Enterprise and Splunk Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="80fa3-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="80fa3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="80fa3-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="80fa3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="80fa3-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="80fa3-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="80fa3-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="80fa3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="80fa3-133">Typ in het zoekvak **Splunk Enterprise en Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="80fa3-133">In the search box, type **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_search.png)

5. <span data-ttu-id="80fa3-135">Selecteer in het deelvenster resultaten **Splunk Enterprise en Splunk Cloud**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="80fa3-135">In the results panel, select **Splunk Enterprise and Splunk Cloud**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="80fa3-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="80fa3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="80fa3-138">In deze sectie maakt u configureren en testen Azure AD eenmalige aanmelding met Splunk voor ondernemingen en Splunk Cloud op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="80fa3-138">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="80fa3-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Splunk Enterprise en Splunk Cloud is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80fa3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Splunk Enterprise and Splunk Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="80fa3-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Splunk Enterprise en Splunk Cloud worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="80fa3-140">In other words, a link relationship between an Azure AD user and the related user in Splunk Enterprise and Splunk Cloud needs to be established.</span></span>

<span data-ttu-id="80fa3-141">Wijs in Splunk Enterprise en Splunk Cloud, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="80fa3-141">In Splunk Enterprise and Splunk Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="80fa3-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Splunk Enterprise en Splunk Cloud, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="80fa3-142">To configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="80fa3-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="80fa3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="80fa3-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="80fa3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="80fa3-145">**[Maken van een testgebruiker Splunk Enterprise en Splunk Cloud](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  - hebben een equivalent van Britta Simon in de onderneming Splunk en Splunk Cloud die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="80fa3-145">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - to have a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="80fa3-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="80fa3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="80fa3-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="80fa3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="80fa3-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="80fa3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="80fa3-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Splunk Enterprise en Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="80fa3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Splunk Enterprise and Splunk Cloud application.</span></span>

<span data-ttu-id="80fa3-150">**Voor het configureren van Azure AD eenmalige aanmelding met Splunk Enterprise en Splunk Cloud, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="80fa3-150">**To configure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="80fa3-151">In de Azure-portal op de **Splunk Enterprise en Splunk Cloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="80fa3-151">In the Azure portal, on the **Splunk Enterprise and Splunk Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="80fa3-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="80fa3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_samlbase.png)

3. <span data-ttu-id="80fa3-155">Op de **Splunk Enterprise en Splunk Cloud-domein en URL's** sectie als u wilt configureren van de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="80fa3-155">On the **Splunk Enterprise and Splunk Cloud Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_url.png)

    <span data-ttu-id="80fa3-157">a.</span><span class="sxs-lookup"><span data-stu-id="80fa3-157">a.</span></span> <span data-ttu-id="80fa3-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="80fa3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
    
    <span data-ttu-id="80fa3-159">b.</span><span class="sxs-lookup"><span data-stu-id="80fa3-159">b.</span></span> <span data-ttu-id="80fa3-160">In de **id** textbox, typ de URL van uw Splunk Server.</span><span class="sxs-lookup"><span data-stu-id="80fa3-160">In the **Identifier** textbox, type the URL of your Splunk Server.</span></span>

    <span data-ttu-id="80fa3-161">c.</span><span class="sxs-lookup"><span data-stu-id="80fa3-161">c.</span></span> <span data-ttu-id="80fa3-162">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="80fa3-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<splunkserver>/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="80fa3-163">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="80fa3-163">These values are not real.</span></span> <span data-ttu-id="80fa3-164">Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="80fa3-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="80fa3-165">Hier raden we u voor het gebruik van de unieke waarde van een tekenreeks in de id.</span><span class="sxs-lookup"><span data-stu-id="80fa3-165">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="80fa3-166">Neem contact op met [Splunk Enterprise- en Cloud-Client Splunk ondersteuningsteam](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="80fa3-166">Contact [Splunk Enterprise and Splunk Cloud Client support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) to get these values.</span></span> 

4. <span data-ttu-id="80fa3-167">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="80fa3-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_certificate.png) 

5. <span data-ttu-id="80fa3-169">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="80fa3-169">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="80fa3-171">Eenmalige aanmelding configureren op **Splunk Enterprise en Splunk Cloud** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Splunk Enterprise en Splunk Cloud ondersteuningsteam](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span><span class="sxs-lookup"><span data-stu-id="80fa3-171">To configure single sign-on on **Splunk Enterprise and Splunk Cloud** side, you need to send the downloaded **Metadata XML** to [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span></span>

> [!TIP]
> <span data-ttu-id="80fa3-172">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="80fa3-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="80fa3-173">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="80fa3-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="80fa3-174">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="80fa3-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="80fa3-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="80fa3-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="80fa3-176">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="80fa3-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="80fa3-178">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="80fa3-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="80fa3-179">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="80fa3-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="80fa3-181">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="80fa3-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="80fa3-183">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="80fa3-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="80fa3-185">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="80fa3-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="80fa3-187">a.</span><span class="sxs-lookup"><span data-stu-id="80fa3-187">a.</span></span> <span data-ttu-id="80fa3-188">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="80fa3-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="80fa3-189">b.</span><span class="sxs-lookup"><span data-stu-id="80fa3-189">b.</span></span> <span data-ttu-id="80fa3-190">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="80fa3-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="80fa3-191">c.</span><span class="sxs-lookup"><span data-stu-id="80fa3-191">c.</span></span> <span data-ttu-id="80fa3-192">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="80fa3-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="80fa3-193">d.</span><span class="sxs-lookup"><span data-stu-id="80fa3-193">d.</span></span> <span data-ttu-id="80fa3-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="80fa3-194">Click **Create**.</span></span>
 
### <a name="creating-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="80fa3-195">Een testgebruiker Splunk Enterprise en Splunk Cloud maken</span><span class="sxs-lookup"><span data-stu-id="80fa3-195">Creating a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="80fa3-196">In deze sectie maakt u een gebruiker met de naam Britta Simon in de onderneming Splunk en Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="80fa3-196">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="80fa3-197">Werken met [Splunk Enterprise en Splunk Cloud ondersteuningsteam](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) toevoegen van de gebruikers in het Splunk Enterprise en Splunk Cloud-platform.</span><span class="sxs-lookup"><span data-stu-id="80fa3-197">Work with  [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) to add the users in the Splunk Enterprise and Splunk Cloud platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="80fa3-198">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="80fa3-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="80fa3-199">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Splunk Enterprise en Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="80fa3-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Splunk Enterprise and Splunk Cloud.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="80fa3-201">**Als u Britta Simon naar de onderneming Splunk en Splunk Cloud toewijzen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="80fa3-201">**To assign Britta Simon to Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="80fa3-202">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="80fa3-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="80fa3-204">Selecteer in de lijst met toepassingen **Splunk Enterprise en Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="80fa3-204">In the applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_app.png) 

3. <span data-ttu-id="80fa3-206">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="80fa3-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="80fa3-208">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="80fa3-208">Click **Add** button.</span></span> <span data-ttu-id="80fa3-209">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="80fa3-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="80fa3-211">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="80fa3-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="80fa3-212">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="80fa3-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="80fa3-213">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="80fa3-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="80fa3-214">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="80fa3-214">Testing single sign-on</span></span>

<span data-ttu-id="80fa3-215">In deze sectie kunt u uw Azure AD-SSOonfiguration met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="80fa3-215">In this section, you test your Azure AD SSOonfiguration using the Access Panel.</span></span>

<span data-ttu-id="80fa3-216">Wanneer u klikt op de onderneming Splunk en Splunk Cloud-tegel in het toegangsvenster, u moet ophalen automatisch aangemeld bij uw toepassing Splunk Enterprise en Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="80fa3-216">When you click the Splunk Enterprise and Splunk Cloud tile in the Access Panel, you should get automatically signed-on to your Splunk Enterprise and Splunk Cloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="80fa3-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="80fa3-217">Additional resources</span></span>

* [<span data-ttu-id="80fa3-218">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80fa3-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="80fa3-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="80fa3-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_203.png

