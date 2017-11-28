---
title: 'Zelfstudie: Azure Active Directory-integratie met Kronos | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Kronos.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: eb61ec0a7d3e992a285b1af3d4a7fbe1feb8d991
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a><span data-ttu-id="ae9e0-103">Zelfstudie: Azure Active Directory-integratie met Kronos</span><span class="sxs-lookup"><span data-stu-id="ae9e0-103">Tutorial: Azure Active Directory integration with Kronos</span></span>

<span data-ttu-id="ae9e0-104">In deze zelfstudie leert u hoe Kronos integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae9e0-104">In this tutorial, you learn how to integrate Kronos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae9e0-105">Kronos integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ae9e0-105">Integrating Kronos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ae9e0-106">U kunt beheren in Azure AD die toegang tot Kronos heeft</span><span class="sxs-lookup"><span data-stu-id="ae9e0-106">You can control in Azure AD who has access to Kronos</span></span>
- <span data-ttu-id="ae9e0-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Kronos (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="ae9e0-107">You can enable your users to automatically get signed-on to Kronos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae9e0-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ae9e0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ae9e0-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ae9e0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae9e0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ae9e0-110">Prerequisites</span></span>

<span data-ttu-id="ae9e0-111">Voor het configureren van Azure AD-integratie met Kronos, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="ae9e0-111">To configure Azure AD integration with Kronos, you need the following items:</span></span>

- <span data-ttu-id="ae9e0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ae9e0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae9e0-113">Een **Kronos medewerkers centrale** SSO abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="ae9e0-113">A **Kronos Workforce Central** SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae9e0-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae9e0-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ae9e0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae9e0-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae9e0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae9e0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae9e0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ae9e0-118">Scenario description</span></span>
<span data-ttu-id="ae9e0-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae9e0-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ae9e0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae9e0-121">Kronos uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ae9e0-121">Adding Kronos from the gallery</span></span>
2. <span data-ttu-id="ae9e0-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ae9e0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kronos-from-the-gallery"></a><span data-ttu-id="ae9e0-123">Kronos uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ae9e0-123">Adding Kronos from the gallery</span></span>
<span data-ttu-id="ae9e0-124">Voor het configureren van de integratie van Kronos in Azure AD, moet u Kronos uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-124">To configure the integration of Kronos into Azure AD, you need to add Kronos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ae9e0-125">**Als u wilt toevoegen Kronos uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ae9e0-125">**To add Kronos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ae9e0-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ae9e0-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ae9e0-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ae9e0-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ae9e0-133">Typ in het zoekvak **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-133">In the search box, type **Kronos**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_search.png)

5. <span data-ttu-id="ae9e0-135">Selecteer in het deelvenster resultaten **Kronos**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-135">In the results panel, select **Kronos**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae9e0-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ae9e0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae9e0-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Kronos op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="ae9e0-138">In this section, you configure and test Azure AD single sign-on with Kronos based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ae9e0-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Kronos is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kronos is to a user in Azure AD.</span></span> <span data-ttu-id="ae9e0-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Kronos tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-140">In other words, a link relationship between an Azure AD user and the related user in Kronos needs to be established.</span></span>

<span data-ttu-id="ae9e0-141">Wijs in Kronos, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-141">In Kronos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ae9e0-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Kronos, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="ae9e0-142">To configure and test Azure AD single sign-on with Kronos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ae9e0-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ae9e0-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae9e0-145">**[Maken van een testgebruiker Kronos](#creating-a-kronos-test-user)**  - Kronos die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-145">**[Creating a Kronos test user](#creating-a-kronos-test-user)** - to have a counterpart of Britta Simon in Kronos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ae9e0-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae9e0-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae9e0-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ae9e0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae9e0-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Kronos configureren.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kronos application.</span></span>

<span data-ttu-id="ae9e0-150">**Voor het configureren van Azure AD eenmalige aanmelding met Kronos, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ae9e0-150">**To configure Azure AD single sign-on with Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="ae9e0-151">In de Azure-portal op de **Kronos** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-151">In the Azure portal, on the **Kronos** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ae9e0-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_samlbase.png)

3. <span data-ttu-id="ae9e0-155">Op de **Kronos domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ae9e0-155">On the **Kronos Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_url.png)

    <span data-ttu-id="ae9e0-157">a.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-157">a.</span></span> <span data-ttu-id="ae9e0-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.kronos.net/`</span><span class="sxs-lookup"><span data-stu-id="ae9e0-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/`</span></span>

    <span data-ttu-id="ae9e0-159">b.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-159">b.</span></span> <span data-ttu-id="ae9e0-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span><span class="sxs-lookup"><span data-stu-id="ae9e0-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ae9e0-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-161">These values are not real.</span></span> <span data-ttu-id="ae9e0-162">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="ae9e0-163">Neem contact op met [Kronos ondersteuningsteam](https://www.kronos.in/contact/en-in/form) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-163">Contact [Kronos support team](https://www.kronos.in/contact/en-in/form) to get these values.</span></span>
 
4. <span data-ttu-id="ae9e0-164">Uw toepassing Kronos verwacht de SAML-asserties in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-164">Your Kronos application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="ae9e0-165">Werken met [Kronos ondersteuningsteam](https://www.kronos.in/contact/en-in/form) eerst naar de juiste gebruikers-id, die is toegewezen in de toepassing te identificeren.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-165">Work with [Kronos support team](https://www.kronos.in/contact/en-in/form) first to identify the correct user identifier, which is mapped into the application.</span></span> <span data-ttu-id="ae9e0-166">Neem ook de informatie over het kenmerk moet worden gebruikt voor deze toewijzing.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-166">Also please take the guidance about the attribute, which they want to use for this mapping.</span></span>
 
     <span data-ttu-id="ae9e0-167">Microsoft raadt u aan met behulp van de **'NameIdentifier'** kenmerk als gebruikers-id.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-167">Microsoft recommends using the **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="ae9e0-168">U kunt de waarden van deze kenmerken van beheren de **'Gebruikerskenmerken'** sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-168">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span>
     
     <span data-ttu-id="ae9e0-169">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="ae9e0-170">We hebben hier toegewezen de **gebruikers-id (nameid)** met **ExtractMailPrefix()** functie van **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-170">Here we have mapped the **User Identifier (nameid)** with **ExtractMailPrefix()** function of **user.userprincipalname**.</span></span> <span data-ttu-id="ae9e0-171">Dit geeft de waarde van het voorvoegsel van e-mailadres van de gebruiker die de unieke gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-171">This gives the prefix value of email of the user which is the unique User ID.</span></span> <span data-ttu-id="ae9e0-172">Dit wordt verzonden naar de toepassing Kronos in elke geslaagde reactie.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-172">This is sent to the Kronos application in every successful response.</span></span> 
     
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_attribute.png)

5. <span data-ttu-id="ae9e0-174">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="ae9e0-174">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="ae9e0-175">a.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-175">a.</span></span> <span data-ttu-id="ae9e0-176">Selecteer in de vervolgkeuzelijst van de gebruikers-id **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-176">In the User Identifier dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="ae9e0-177">b.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-177">b.</span></span> <span data-ttu-id="ae9e0-178">In de **Mail** vervolgkeuzelijst, selecteer **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-178">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

6. <span data-ttu-id="ae9e0-179">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_certificate.png) 

7. <span data-ttu-id="ae9e0-181">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-181">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kronos-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ae9e0-183">Eenmalige aanmelding configureren op **Kronos** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Kronos ondersteuningsteam](https://www.kronos.in/contact/en-in/form).</span><span class="sxs-lookup"><span data-stu-id="ae9e0-183">To configure single sign-on on **Kronos** side, you need to send the downloaded **Metadata XML** to [Kronos support team](https://www.kronos.in/contact/en-in/form).</span></span> 

> [!TIP]
> <span data-ttu-id="ae9e0-184">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="ae9e0-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ae9e0-185">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ae9e0-186">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ae9e0-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae9e0-187">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ae9e0-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae9e0-188">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ae9e0-190">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ae9e0-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ae9e0-191">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kronos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae9e0-193">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kronos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae9e0-195">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kronos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae9e0-197">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ae9e0-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kronos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae9e0-199">a.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-199">a.</span></span> <span data-ttu-id="ae9e0-200">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae9e0-201">b.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-201">b.</span></span> <span data-ttu-id="ae9e0-202">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae9e0-203">c.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-203">c.</span></span> <span data-ttu-id="ae9e0-204">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ae9e0-205">d.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-205">d.</span></span> <span data-ttu-id="ae9e0-206">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-206">Click **Create**.</span></span>
 
### <a name="creating-a-kronos-test-user"></a><span data-ttu-id="ae9e0-207">Een testgebruiker Kronos maken</span><span class="sxs-lookup"><span data-stu-id="ae9e0-207">Creating a Kronos test user</span></span>

<span data-ttu-id="ae9e0-208">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Kronos maken.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-208">In this section, you create a user called Britta Simon in Kronos.</span></span> <span data-ttu-id="ae9e0-209">Kronos toepassing moet de gebruikers moeten worden ingericht in de toepassing voordat u eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-209">Kronos application needs all the users to be provisioned in the application before doing SSO.</span></span> 

<span data-ttu-id="ae9e0-210">Werken met de [Kronos ondersteuningsteam](https://www.kronos.in/contact/en-in/form) voor het inrichten van al deze gebruikers in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-210">Work with the [Kronos support team](https://www.kronos.in/contact/en-in/form) to provision all these users into the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ae9e0-211">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae9e0-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ae9e0-212">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Kronos.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kronos.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ae9e0-214">**Britta Simon om aan te wijzen Kronos, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ae9e0-214">**To assign Britta Simon to Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="ae9e0-215">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ae9e0-217">Selecteer in de lijst met toepassingen **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-217">In the applications list, select **Kronos**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_app.png) 

3. <span data-ttu-id="ae9e0-219">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ae9e0-221">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-221">Click **Add** button.</span></span> <span data-ttu-id="ae9e0-222">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ae9e0-224">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ae9e0-225">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ae9e0-226">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ae9e0-227">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ae9e0-227">Testing single sign-on</span></span>

<span data-ttu-id="ae9e0-228">In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-228">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="ae9e0-229">Als u op de tegel Kronos in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Kronos.</span><span class="sxs-lookup"><span data-stu-id="ae9e0-229">When you click the Kronos tile in the Access Panel, you should get automatically signed-on to your Kronos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae9e0-230">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ae9e0-230">Additional resources</span></span>

* [<span data-ttu-id="ae9e0-231">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae9e0-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae9e0-232">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ae9e0-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_203.png

