---
title: 'Zelfstudie: Azure Active Directory-integratie met BenSelect | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en BenSelect.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: f8caa023da05863372b7ef92b47a92168445d741
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="9df24-103">Zelfstudie: Azure Active Directory-integratie met BenSelect</span><span class="sxs-lookup"><span data-stu-id="9df24-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>

<span data-ttu-id="9df24-104">In deze zelfstudie leert u hoe BenSelect integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9df24-104">In this tutorial, you learn how to integrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9df24-105">BenSelect integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="9df24-105">Integrating BenSelect with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9df24-106">U kunt beheren in Azure AD die toegang tot BenSelect heeft</span><span class="sxs-lookup"><span data-stu-id="9df24-106">You can control in Azure AD who has access to BenSelect</span></span>
- <span data-ttu-id="9df24-107">U kunt uw gebruikers automatisch ophalen aangemeld bij BenSelect (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="9df24-107">You can enable your users to automatically get signed-on to BenSelect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9df24-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="9df24-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9df24-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9df24-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9df24-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9df24-110">Prerequisites</span></span>

<span data-ttu-id="9df24-111">Voor het configureren van Azure AD-integratie met BenSelect, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="9df24-111">To configure Azure AD integration with BenSelect, you need the following items:</span></span>

- <span data-ttu-id="9df24-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="9df24-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9df24-113">Een BenSelect eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="9df24-113">A BenSelect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9df24-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="9df24-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9df24-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="9df24-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9df24-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="9df24-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9df24-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9df24-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9df24-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="9df24-118">Scenario description</span></span>
<span data-ttu-id="9df24-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="9df24-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9df24-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="9df24-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9df24-121">BenSelect uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9df24-121">Adding BenSelect from the gallery</span></span>
2. <span data-ttu-id="9df24-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9df24-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benselect-from-the-gallery"></a><span data-ttu-id="9df24-123">BenSelect uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9df24-123">Adding BenSelect from the gallery</span></span>
<span data-ttu-id="9df24-124">Voor het configureren van de integratie van BenSelect in Azure AD, moet u BenSelect uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="9df24-124">To configure the integration of BenSelect into Azure AD, you need to add BenSelect from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9df24-125">**Als u wilt toevoegen BenSelect uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9df24-125">**To add BenSelect from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9df24-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9df24-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9df24-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9df24-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9df24-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9df24-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="9df24-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9df24-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="9df24-133">Typ in het zoekvak **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="9df24-133">In the search box, type **BenSelect**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_search.png)

5. <span data-ttu-id="9df24-135">Selecteer in het deelvenster resultaten **BenSelect**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9df24-135">In the results panel, select **BenSelect**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9df24-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9df24-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9df24-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met BenSelect op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="9df24-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9df24-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in BenSelect is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9df24-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenSelect is to a user in Azure AD.</span></span> <span data-ttu-id="9df24-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in BenSelect tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="9df24-140">In other words, a link relationship between an Azure AD user and the related user in BenSelect needs to be established.</span></span>

<span data-ttu-id="9df24-141">Wijs in BenSelect, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="9df24-141">In BenSelect, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9df24-142">Om te configureren en testen van Azure AD eenmalige aanmelding met BenSelect, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="9df24-142">To configure and test Azure AD single sign-on with BenSelect, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9df24-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9df24-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9df24-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9df24-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9df24-145">**[Maken van een testgebruiker BenSelect](#creating-a-benselect-test-user)**  - BenSelect die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="9df24-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - to have a counterpart of Britta Simon in BenSelect that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9df24-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9df24-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9df24-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="9df24-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9df24-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="9df24-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9df24-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing BenSelect configureren.</span><span class="sxs-lookup"><span data-stu-id="9df24-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenSelect application.</span></span>

<span data-ttu-id="9df24-150">**Voor het configureren van Azure AD eenmalige aanmelding met BenSelect, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9df24-150">**To configure Azure AD single sign-on with BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="9df24-151">In de Azure-portal op de **BenSelect** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="9df24-151">In the Azure portal, on the **BenSelect** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="9df24-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9df24-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_samlbase.png)

3. <span data-ttu-id="9df24-155">Op de **BenSelect domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9df24-155">On the **BenSelect Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_url.png)

    <span data-ttu-id="9df24-157">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="9df24-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9df24-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="9df24-158">This value is not real.</span></span> <span data-ttu-id="9df24-159">Deze waarde bijwerken met de werkelijke antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="9df24-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="9df24-160">Neem contact op met [BenSelect ondersteuningsteam](mailto:support@selerix.com) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="9df24-160">Contact [BenSelect support team](mailto:support@selerix.com) to get this value.</span></span>
 
4. <span data-ttu-id="9df24-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Raw)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9df24-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_certificate.png) 

5. <span data-ttu-id="9df24-163">De SAML-asserties verwacht BenSelect toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="9df24-163">BenSelect application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="9df24-164">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="9df24-164">Configure the following claims for this application.</span></span> <span data-ttu-id="9df24-165">U kunt de waarden van deze kenmerken van beheren de **gebruikerskenmerken** sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="9df24-165">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="9df24-166">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="9df24-166">The following screenshot shows an example for this.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

6. <span data-ttu-id="9df24-168">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="9df24-168">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="9df24-169">a.</span><span class="sxs-lookup"><span data-stu-id="9df24-169">a.</span></span> <span data-ttu-id="9df24-170">In de **gebruikers-id** vervolgkeuzelijst, selecteer **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="9df24-170">In the **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="9df24-171">b.</span><span class="sxs-lookup"><span data-stu-id="9df24-171">b.</span></span> <span data-ttu-id="9df24-172">In de **Mail** vervolgkeuzelijst, selecteer **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="9df24-172">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

7. <span data-ttu-id="9df24-173">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="9df24-173">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benselect-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9df24-175">Op de **BenSelect configuratie** sectie, klikt u op **configureren BenSelect** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="9df24-175">On the **BenSelect Configuration** section, click **Configure BenSelect** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9df24-176">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="9df24-176">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_configure.png) 

9. <span data-ttu-id="9df24-178">Eenmalige aanmelding configureren op **BenSelect** zijde, moet u de gedownloade verzenden **Certificate(Raw)** en **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** naar [BenSelect ondersteuningsteam](mailto:support@selerix.com).</span><span class="sxs-lookup"><span data-stu-id="9df24-178">To configure single sign-on on **BenSelect** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [BenSelect support team](mailto:support@selerix.com).</span></span>

   >[!NOTE]
   ><span data-ttu-id="9df24-179">U moet aangeven dat deze integratie het algoritme SHA256 vereist (SHA1 wordt niet ondersteund) de eenmalige aanmelding instellen op de juiste server zoals app2101 enzovoort.</span><span class="sxs-lookup"><span data-stu-id="9df24-179">You need to mention that this integration requires the SHA256 algorithm (SHA1 is not supported) to set the SSO on the appropriate server like app2101 etc.</span></span> 
   
> [!TIP]
> <span data-ttu-id="9df24-180">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="9df24-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9df24-181">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="9df24-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9df24-182">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9df24-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9df24-183">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="9df24-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="9df24-184">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9df24-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="9df24-186">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9df24-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9df24-187">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9df24-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benselect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9df24-189">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="9df24-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benselect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9df24-191">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9df24-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9df24-193">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9df24-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9df24-195">a.</span><span class="sxs-lookup"><span data-stu-id="9df24-195">a.</span></span> <span data-ttu-id="9df24-196">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9df24-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9df24-197">b.</span><span class="sxs-lookup"><span data-stu-id="9df24-197">b.</span></span> <span data-ttu-id="9df24-198">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9df24-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9df24-199">c.</span><span class="sxs-lookup"><span data-stu-id="9df24-199">c.</span></span> <span data-ttu-id="9df24-200">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="9df24-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9df24-201">d.</span><span class="sxs-lookup"><span data-stu-id="9df24-201">d.</span></span> <span data-ttu-id="9df24-202">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="9df24-202">Click **Create**.</span></span>
 
### <a name="creating-a-benselect-test-user"></a><span data-ttu-id="9df24-203">Een testgebruiker BenSelect maken</span><span class="sxs-lookup"><span data-stu-id="9df24-203">Creating a BenSelect test user</span></span>

<span data-ttu-id="9df24-204">Het doel van deze sectie is het maken van een gebruiker Britta Simon in BenSelect genoemd.</span><span class="sxs-lookup"><span data-stu-id="9df24-204">The objective of this section is to create a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="9df24-205">Werken met [BenSelect ondersteuningsteam](mailto:support@selerix.com) de gebruikers in het account BenSelect toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9df24-205">Work with [BenSelect support team](mailto:support@selerix.com) to add the users in the BenSelect account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9df24-206">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="9df24-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9df24-207">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan BenSelect.</span><span class="sxs-lookup"><span data-stu-id="9df24-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenSelect.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="9df24-209">**Britta Simon om aan te wijzen BenSelect, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9df24-209">**To assign Britta Simon to BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="9df24-210">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9df24-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="9df24-212">Selecteer in de lijst met toepassingen **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="9df24-212">In the applications list, select **BenSelect**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_app.png) 

3. <span data-ttu-id="9df24-214">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="9df24-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="9df24-216">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="9df24-216">Click **Add** button.</span></span> <span data-ttu-id="9df24-217">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9df24-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="9df24-219">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="9df24-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9df24-220">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9df24-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9df24-221">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9df24-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9df24-222">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9df24-222">Testing single sign-on</span></span>

<span data-ttu-id="9df24-223">In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="9df24-223">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="9df24-224">Als u op de tegel BenSelect in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing BenSelect.</span><span class="sxs-lookup"><span data-stu-id="9df24-224">When you click the BenSelect tile in the Access Panel, you should get automatically signed-on to your BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9df24-225">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="9df24-225">Additional resources</span></span>

* [<span data-ttu-id="9df24-226">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9df24-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9df24-227">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9df24-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_203.png

