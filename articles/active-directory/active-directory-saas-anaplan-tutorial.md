---
title: 'Zelfstudie: Azure Active Directory-integratie met Anaplan | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Anaplan.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a9c2914-6c8c-4a88-93e3-3753afb40e6b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jeedes
ms.openlocfilehash: c2ecfd5f066ed3bd10f74f935de2f2b80057329f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-anaplan"></a><span data-ttu-id="d0003-103">Zelfstudie: Azure Active Directory-integratie met Anaplan</span><span class="sxs-lookup"><span data-stu-id="d0003-103">Tutorial: Azure Active Directory integration with Anaplan</span></span>

<span data-ttu-id="d0003-104">In deze zelfstudie leert u hoe Anaplan integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0003-104">In this tutorial, you learn how to integrate Anaplan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d0003-105">Anaplan integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d0003-105">Integrating Anaplan with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d0003-106">U kunt beheren in Azure AD die toegang tot Anaplan heeft</span><span class="sxs-lookup"><span data-stu-id="d0003-106">You can control in Azure AD who has access to Anaplan</span></span>
- <span data-ttu-id="d0003-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Anaplan (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="d0003-107">You can enable your users to automatically get signed-on to Anaplan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d0003-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="d0003-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d0003-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d0003-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0003-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d0003-110">Prerequisites</span></span>

<span data-ttu-id="d0003-111">Voor het configureren van Azure AD-integratie met Anaplan, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="d0003-111">To configure Azure AD integration with Anaplan, you need the following items:</span></span>

- <span data-ttu-id="d0003-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="d0003-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d0003-113">Een Anaplan eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="d0003-113">An Anaplan single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d0003-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d0003-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d0003-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="d0003-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d0003-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d0003-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d0003-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0003-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d0003-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d0003-118">Scenario description</span></span>
<span data-ttu-id="d0003-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d0003-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d0003-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d0003-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d0003-121">Anaplan uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d0003-121">Adding Anaplan from the gallery</span></span>
2. <span data-ttu-id="d0003-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d0003-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-anaplan-from-the-gallery"></a><span data-ttu-id="d0003-123">Anaplan uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d0003-123">Adding Anaplan from the gallery</span></span>
<span data-ttu-id="d0003-124">Voor het configureren van de integratie van Anaplan in Azure AD, moet u Anaplan uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d0003-124">To configure the integration of Anaplan into Azure AD, you need to add Anaplan from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d0003-125">**Als u wilt toevoegen Anaplan uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d0003-125">**To add Anaplan from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d0003-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d0003-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d0003-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d0003-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d0003-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d0003-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d0003-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d0003-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d0003-133">Typ in het zoekvak **Anaplan**.</span><span class="sxs-lookup"><span data-stu-id="d0003-133">In the search box, type **Anaplan**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_search.png)

5. <span data-ttu-id="d0003-135">Selecteer in het deelvenster resultaten **Anaplan**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d0003-135">In the results panel, select **Anaplan**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d0003-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d0003-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d0003-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Anaplan op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="d0003-138">In this section, you configure and test Azure AD single sign-on with Anaplan based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d0003-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Anaplan is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0003-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Anaplan is to a user in Azure AD.</span></span> <span data-ttu-id="d0003-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Anaplan tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="d0003-140">In other words, a link relationship between an Azure AD user and the related user in Anaplan needs to be established.</span></span>

<span data-ttu-id="d0003-141">Wijs in Anaplan, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="d0003-141">In Anaplan, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d0003-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Anaplan, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="d0003-142">To configure and test Azure AD single sign-on with Anaplan, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d0003-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d0003-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d0003-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0003-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d0003-145">**[Maken van een testgebruiker Anaplan](#creating-an-anaplan-test-user)**  - Anaplan die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="d0003-145">**[Creating an Anaplan test user](#creating-an-anaplan-test-user)** - to have a counterpart of Britta Simon in Anaplan that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d0003-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d0003-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d0003-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d0003-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d0003-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d0003-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d0003-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Anaplan configureren.</span><span class="sxs-lookup"><span data-stu-id="d0003-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Anaplan application.</span></span>

<span data-ttu-id="d0003-150">**Voor het configureren van Azure AD eenmalige aanmelding met Anaplan, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d0003-150">**To configure Azure AD single sign-on with Anaplan, perform the following steps:**</span></span>

1. <span data-ttu-id="d0003-151">In de Azure-portal op de **Anaplan** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d0003-151">In the Azure portal, on the **Anaplan** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d0003-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d0003-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_samlbase.png)

3. <span data-ttu-id="d0003-155">Op de **Anaplan domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d0003-155">On the **Anaplan Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_url.png)

    <span data-ttu-id="d0003-157">a.</span><span class="sxs-lookup"><span data-stu-id="d0003-157">a.</span></span> <span data-ttu-id="d0003-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://sdp.anaplan.com/frontdoor/saml/<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="d0003-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sdp.anaplan.com/frontdoor/saml/<tenant name>`</span></span>

    <span data-ttu-id="d0003-159">b.</span><span class="sxs-lookup"><span data-stu-id="d0003-159">b.</span></span> <span data-ttu-id="d0003-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.anaplan.com`</span><span class="sxs-lookup"><span data-stu-id="d0003-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.anaplan.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d0003-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="d0003-161">These values are not real.</span></span> <span data-ttu-id="d0003-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="d0003-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d0003-163">Neem contact op met [Anaplan Client ondersteuningsteam](mailto:support@anaplan.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="d0003-163">Contact [Anaplan Client support team](mailto:support@anaplan.com) to get these values.</span></span> 
 
4. <span data-ttu-id="d0003-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d0003-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_certificate.png) 

5. <span data-ttu-id="d0003-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d0003-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-anaplan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d0003-168">Op de **Anaplan configuratie** sectie, klikt u op **configureren Anaplan** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="d0003-168">On the **Anaplan Configuration** section, click **Configure Anaplan** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d0003-169">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="d0003-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_configure.png) 

7. <span data-ttu-id="d0003-171">Eenmalige aanmelding configureren op **Anaplan** zijde, moet u de gedownloade verzenden **Metadata XML**, **SAML entiteit-ID**, **SAML Single Sign-On Service-URL** en **Sign-Out URL** naar [Anaplan ondersteuningsteam](mailto:support@anaplan.com).</span><span class="sxs-lookup"><span data-stu-id="d0003-171">To configure single sign-on on **Anaplan** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL**   to [Anaplan support team](mailto:support@anaplan.com).</span></span> <span data-ttu-id="d0003-172">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="d0003-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d0003-173">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="d0003-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d0003-174">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="d0003-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d0003-175">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d0003-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d0003-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d0003-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="d0003-177">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d0003-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d0003-179">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d0003-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d0003-180">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d0003-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-anaplan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d0003-182">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="d0003-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-anaplan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d0003-184">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d0003-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-anaplan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d0003-186">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d0003-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-anaplan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d0003-188">a.</span><span class="sxs-lookup"><span data-stu-id="d0003-188">a.</span></span> <span data-ttu-id="d0003-189">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d0003-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d0003-190">b.</span><span class="sxs-lookup"><span data-stu-id="d0003-190">b.</span></span> <span data-ttu-id="d0003-191">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d0003-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d0003-192">c.</span><span class="sxs-lookup"><span data-stu-id="d0003-192">c.</span></span> <span data-ttu-id="d0003-193">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d0003-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d0003-194">d.</span><span class="sxs-lookup"><span data-stu-id="d0003-194">d.</span></span> <span data-ttu-id="d0003-195">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d0003-195">Click **Create**.</span></span>
 
### <a name="creating-an-anaplan-test-user"></a><span data-ttu-id="d0003-196">Een testgebruiker Anaplan maken</span><span class="sxs-lookup"><span data-stu-id="d0003-196">Creating an Anaplan test user</span></span>

<span data-ttu-id="d0003-197">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Anaplan maken.</span><span class="sxs-lookup"><span data-stu-id="d0003-197">In this section, you create a user called Britta Simon in Anaplan.</span></span> <span data-ttu-id="d0003-198">Neem contact op met [Anaplan ondersteuningsteam](mailto:support@anaplan.com) de gebruikers van het platform Anaplan toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d0003-198">Please work with [Anaplan support team](mailto:support@anaplan.com) to add the users in the Anaplan platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d0003-199">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0003-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d0003-200">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Anaplan.</span><span class="sxs-lookup"><span data-stu-id="d0003-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Anaplan.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d0003-202">**Britta Simon om aan te wijzen Anaplan, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d0003-202">**To assign Britta Simon to Anaplan, perform the following steps:**</span></span>

1. <span data-ttu-id="d0003-203">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d0003-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d0003-205">Selecteer in de lijst met toepassingen **Anaplan**.</span><span class="sxs-lookup"><span data-stu-id="d0003-205">In the applications list, select **Anaplan**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_app.png) 

3. <span data-ttu-id="d0003-207">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d0003-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d0003-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d0003-209">Click **Add** button.</span></span> <span data-ttu-id="d0003-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d0003-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d0003-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d0003-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d0003-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d0003-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d0003-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d0003-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d0003-215">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d0003-215">Testing single sign-on</span></span>

<span data-ttu-id="d0003-216">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="d0003-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d0003-217">Als u op de tegel Anaplan in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Anaplan.</span><span class="sxs-lookup"><span data-stu-id="d0003-217">When you click the Anaplan tile in the Access Panel, you should get automatically signed-on to your Anaplan application.</span></span>

<span data-ttu-id="d0003-218">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d0003-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d0003-219">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d0003-219">Additional resources</span></span>

* [<span data-ttu-id="d0003-220">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0003-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d0003-221">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d0003-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_203.png

