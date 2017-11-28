---
title: 'Zelfstudie: Azure Active Directory-integratie met LogicMonitor | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en LogicMonitor.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: e49960cac868f80af3e9165a9f75e49be87515f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="7a4d0-103">Zelfstudie: Azure Active Directory-integratie met LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="7a4d0-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>

<span data-ttu-id="7a4d0-104">In deze zelfstudie leert u hoe LogicMonitor integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7a4d0-104">In this tutorial, you learn how to integrate LogicMonitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7a4d0-105">LogicMonitor integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="7a4d0-105">Integrating LogicMonitor with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7a4d0-106">U kunt beheren in Azure AD die toegang tot LogicMonitor heeft</span><span class="sxs-lookup"><span data-stu-id="7a4d0-106">You can control in Azure AD who has access to LogicMonitor</span></span>
- <span data-ttu-id="7a4d0-107">U kunt uw gebruikers automatisch ophalen aangemeld bij LogicMonitor (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="7a4d0-107">You can enable your users to automatically get signed-on to LogicMonitor (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7a4d0-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="7a4d0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7a4d0-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7a4d0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a4d0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7a4d0-110">Prerequisites</span></span>

<span data-ttu-id="7a4d0-111">Voor het configureren van Azure AD-integratie met LogicMonitor, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="7a4d0-111">To configure Azure AD integration with LogicMonitor, you need the following items:</span></span>

- <span data-ttu-id="7a4d0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="7a4d0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7a4d0-113">Een LogicMonitor eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="7a4d0-113">A LogicMonitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7a4d0-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7a4d0-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="7a4d0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7a4d0-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7a4d0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a4d0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7a4d0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="7a4d0-118">Scenario description</span></span>
<span data-ttu-id="7a4d0-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7a4d0-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="7a4d0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7a4d0-121">LogicMonitor uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="7a4d0-121">Adding LogicMonitor from the gallery</span></span>
2. <span data-ttu-id="7a4d0-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7a4d0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-logicmonitor-from-the-gallery"></a><span data-ttu-id="7a4d0-123">LogicMonitor uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="7a4d0-123">Adding LogicMonitor from the gallery</span></span>
<span data-ttu-id="7a4d0-124">Voor het configureren van de integratie van LogicMonitor in Azure AD, moet u LogicMonitor uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-124">To configure the integration of LogicMonitor into Azure AD, you need to add LogicMonitor from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7a4d0-125">**Als u wilt toevoegen LogicMonitor uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7a4d0-125">**To add LogicMonitor from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7a4d0-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7a4d0-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7a4d0-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="7a4d0-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="7a4d0-133">Typ in het zoekvak **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-133">In the search box, type **LogicMonitor**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_search.png)

5. <span data-ttu-id="7a4d0-135">Selecteer in het deelvenster resultaten **LogicMonitor**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-135">In the results panel, select **LogicMonitor**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7a4d0-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7a4d0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7a4d0-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met LogicMonitor op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7a4d0-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in LogicMonitor is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LogicMonitor is to a user in Azure AD.</span></span> <span data-ttu-id="7a4d0-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in LogicMonitor tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-140">In other words, a link relationship between an Azure AD user and the related user in LogicMonitor needs to be established.</span></span>

<span data-ttu-id="7a4d0-141">Wijs in LogicMonitor, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-141">In LogicMonitor, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7a4d0-142">Om te configureren en testen van Azure AD eenmalige aanmelding met LogicMonitor, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="7a4d0-142">To configure and test Azure AD single sign-on with LogicMonitor, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7a4d0-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7a4d0-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7a4d0-145">**[Maken van een testgebruiker LogicMonitor](#creating-a-logicmonitor-test-user)**  - LogicMonitor die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - to have a counterpart of Britta Simon in LogicMonitor that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7a4d0-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7a4d0-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7a4d0-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="7a4d0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7a4d0-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing LogicMonitor configureren.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LogicMonitor application.</span></span>

<span data-ttu-id="7a4d0-150">**Voor het configureren van Azure AD eenmalige aanmelding met LogicMonitor, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7a4d0-150">**To configure Azure AD single sign-on with LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="7a4d0-151">In de Azure-portal op de **LogicMonitor** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-151">In the Azure portal, on the **LogicMonitor** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="7a4d0-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

3. <span data-ttu-id="7a4d0-155">Op de **LogicMonitor domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7a4d0-155">On the **LogicMonitor Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    <span data-ttu-id="7a4d0-157">a.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-157">a.</span></span> <span data-ttu-id="7a4d0-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="7a4d0-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    <span data-ttu-id="7a4d0-159">b.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-159">b.</span></span> <span data-ttu-id="7a4d0-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="7a4d0-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7a4d0-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-161">These values are not real.</span></span> <span data-ttu-id="7a4d0-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7a4d0-163">Neem contact op met [LogicMonitor Client ondersteuningsteam](https://www.logicmonitor.com/contact/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) to get these values.</span></span> 
 


4. <span data-ttu-id="7a4d0-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

5. <span data-ttu-id="7a4d0-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7a4d0-168">Meld u aan bij uw **LogicMonitor** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-168">Log in to your **LogicMonitor** company site as an administrator.</span></span>

7. <span data-ttu-id="7a4d0-169">Klik in het menu bovenaan op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-169">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="7a4d0-170">![Instellingen](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="7a4d0-170">![Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Settings")</span></span>

8. <span data-ttu-id="7a4d0-171">Klik in het navigatiedeelvenster bat aan de linkerkant, **eenmalige aanmelding**</span><span class="sxs-lookup"><span data-stu-id="7a4d0-171">In the navigation bat on the left side, click **Single Sign On**</span></span>
   
   <span data-ttu-id="7a4d0-172">![Eenmalige aanmelding](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="7a4d0-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span></span>

9. <span data-ttu-id="7a4d0-173">In de **instellingen voor eenmalige aanmelding (SSO)** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7a4d0-173">In the **Single Sign-on (SSO) settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="7a4d0-174">![Eenmalige aanmelding instellingen](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="7a4d0-174">![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="7a4d0-175">a.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-175">a.</span></span> <span data-ttu-id="7a4d0-176">Selecteer **eenmalige aanmelding inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-176">Select **Enable Single Sign-on**.</span></span>

   <span data-ttu-id="7a4d0-177">b.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-177">b.</span></span> <span data-ttu-id="7a4d0-178">Als **roltoewijzing standaard**, selecteer **readonly**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-178">As **Default Role Assignment**, select **readonly**.</span></span>
   
   <span data-ttu-id="7a4d0-179">c.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-179">c.</span></span> <span data-ttu-id="7a4d0-180">Open de van het gedownloade metagegevensbestand in Kladblok en plak de inhoud van het bestand naar de **identiteit Provider metagegevens** textbox.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-180">Open the downloaded metadata file in notepad, and then paste content of the file into the **Identity Provider Metadata** textbox.</span></span>
   
   <span data-ttu-id="7a4d0-181">d.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-181">d.</span></span> <span data-ttu-id="7a4d0-182">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="7a4d0-183">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="7a4d0-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7a4d0-184">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7a4d0-185">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7a4d0-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7a4d0-186">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="7a4d0-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="7a4d0-187">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="7a4d0-189">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7a4d0-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7a4d0-190">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7a4d0-192">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7a4d0-194">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7a4d0-196">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7a4d0-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7a4d0-198">a.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-198">a.</span></span> <span data-ttu-id="7a4d0-199">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7a4d0-200">b.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-200">b.</span></span> <span data-ttu-id="7a4d0-201">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7a4d0-202">c.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-202">c.</span></span> <span data-ttu-id="7a4d0-203">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7a4d0-204">d.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-204">d.</span></span> <span data-ttu-id="7a4d0-205">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-205">Click **Create**.</span></span>
 
### <a name="creating-a-logicmonitor-test-user"></a><span data-ttu-id="7a4d0-206">Een testgebruiker LogicMonitor maken</span><span class="sxs-lookup"><span data-stu-id="7a4d0-206">Creating a LogicMonitor test user</span></span>

<span data-ttu-id="7a4d0-207">AAD-gebruikers moeten kunnen aanmelden, als ze worden ingericht voor de LogicMonitor-toepassing met behulp van de namen van de Azure Active Directory-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-207">For AAD users to be able to sign in, they must be provisioned to the LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="7a4d0-208">**Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7a4d0-208">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="7a4d0-209">Meld u aan bij uw bedrijf LogicMonitor site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-209">Log in to your LogicMonitor company site as an administrator.</span></span>

2. <span data-ttu-id="7a4d0-210">Klik in het menu bovenaan op **instellingen**, en klik vervolgens op **rollen en gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-210">In the menu on the top, click **Settings**, and then click **Roles and Users**.</span></span>
   
   <span data-ttu-id="7a4d0-211">![Rollen en gebruikers](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "rollen en gebruikers")</span><span class="sxs-lookup"><span data-stu-id="7a4d0-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users")</span></span>

3. <span data-ttu-id="7a4d0-212">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-212">Click **Add**.</span></span>

4. <span data-ttu-id="7a4d0-213">In de **account toevoegen** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="7a4d0-213">In the **Add an account** section, perform the following steps:</span></span>
   
   <span data-ttu-id="7a4d0-214">![Toevoegen van een account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "account toevoegen")</span><span class="sxs-lookup"><span data-stu-id="7a4d0-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account")</span></span>
   
   <span data-ttu-id="7a4d0-215">a.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-215">a.</span></span> <span data-ttu-id="7a4d0-216">Typ de **gebruikersnaam**, **e**, **wachtwoord**, en **Typ opnieuw wachtwoord** waarden van de Azure Active Directory-gebruiker die u inrichten wilt in de bijbehorende tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-216">Type the **Username**, **Email**, **Password**, and **Retype password** values of the Azure Active Directory user you want to provision into the related textboxes.</span></span>
   
   <span data-ttu-id="7a4d0-217">b.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-217">b.</span></span> <span data-ttu-id="7a4d0-218">Selecteer **rollen**, **machtigingen weergeven**, en de **Status**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-218">Select **Roles**, **View Permissions**, and the **Status**.</span></span>
   
   <span data-ttu-id="7a4d0-219">c.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-219">c.</span></span> <span data-ttu-id="7a4d0-220">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-220">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="7a4d0-221">U kunt andere LogicMonitor gebruiker account hulpmiddelen voor het maken of API's geleverd door LogicMonitor om in te richten Azure Active Directory-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-221">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor to provision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7a4d0-222">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a4d0-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7a4d0-223">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LogicMonitor.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="7a4d0-225">**Britta Simon om aan te wijzen LogicMonitor, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="7a4d0-225">**To assign Britta Simon to LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="7a4d0-226">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="7a4d0-228">Selecteer in de lijst met toepassingen **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-228">In the applications list, select **LogicMonitor**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

3. <span data-ttu-id="7a4d0-230">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="7a4d0-232">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-232">Click **Add** button.</span></span> <span data-ttu-id="7a4d0-233">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="7a4d0-235">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7a4d0-236">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7a4d0-237">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7a4d0-238">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="7a4d0-238">Testing single sign-on</span></span>

<span data-ttu-id="7a4d0-239">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="7a4d0-240">Als u op de tegel LogicMonitor in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="7a4d0-240">When you click the LogicMonitor tile in the Access Panel, you should get automatically signed-on to your LogicMonitor application.</span></span>
<span data-ttu-id="7a4d0-241">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7a4d0-241">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7a4d0-242">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7a4d0-242">Additional resources</span></span>

* [<span data-ttu-id="7a4d0-243">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a4d0-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7a4d0-244">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7a4d0-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_203.png

