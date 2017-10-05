---
title: 'Zelfstudie: Azure Active Directory-integratie met SpringCM | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en SpringCM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: edfd06a06c730597fee4569ca1ce29092b45244a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="e976c-103">Zelfstudie: Azure Active Directory-integratie met SpringCM</span><span class="sxs-lookup"><span data-stu-id="e976c-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="e976c-104">In deze zelfstudie leert u hoe SpringCM integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e976c-104">In this tutorial, you learn how to integrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e976c-105">SpringCM integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e976c-105">Integrating SpringCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e976c-106">U kunt beheren in Azure AD die toegang tot SpringCM heeft</span><span class="sxs-lookup"><span data-stu-id="e976c-106">You can control in Azure AD who has access to SpringCM</span></span>
- <span data-ttu-id="e976c-107">U kunt uw gebruikers automatisch ophalen aangemeld bij SpringCM (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="e976c-107">You can enable your users to automatically get signed-on to SpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e976c-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="e976c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e976c-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e976c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e976c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e976c-110">Prerequisites</span></span>

<span data-ttu-id="e976c-111">Voor het configureren van Azure AD-integratie met SpringCM, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="e976c-111">To configure Azure AD integration with SpringCM, you need the following items:</span></span>

- <span data-ttu-id="e976c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e976c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e976c-113">Een SpringCM eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e976c-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e976c-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e976c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e976c-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e976c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e976c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e976c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e976c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e976c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e976c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e976c-118">Scenario description</span></span>
<span data-ttu-id="e976c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e976c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e976c-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e976c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e976c-121">SpringCM uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e976c-121">Adding SpringCM from the gallery</span></span>
2. <span data-ttu-id="e976c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e976c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-the-gallery"></a><span data-ttu-id="e976c-123">SpringCM uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e976c-123">Adding SpringCM from the gallery</span></span>
<span data-ttu-id="e976c-124">Voor het configureren van de integratie van SpringCM in Azure AD, moet u SpringCM uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e976c-124">To configure the integration of SpringCM into Azure AD, you need to add SpringCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e976c-125">**Als u wilt toevoegen SpringCM uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e976c-125">**To add SpringCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e976c-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e976c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e976c-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e976c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e976c-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e976c-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="e976c-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e976c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="e976c-133">Typ in het zoekvak **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="e976c-133">In the search box, type **SpringCM**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. <span data-ttu-id="e976c-135">Selecteer in het deelvenster resultaten **SpringCM**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e976c-135">In the results panel, select **SpringCM**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e976c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e976c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e976c-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met SpringCM op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="e976c-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e976c-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in SpringCM is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e976c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SpringCM is to a user in Azure AD.</span></span> <span data-ttu-id="e976c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in SpringCM tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="e976c-140">In other words, a link relationship between an Azure AD user and the related user in SpringCM needs to be established.</span></span>

<span data-ttu-id="e976c-141">Wijs in SpringCM, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="e976c-141">In SpringCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e976c-142">Om te configureren en testen van Azure AD eenmalige aanmelding met SpringCM, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="e976c-142">To configure and test Azure AD single sign-on with SpringCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e976c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e976c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e976c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e976c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e976c-145">**[Maken van een testgebruiker SpringCM](#creating-a-springcm-test-user)**  - SpringCM die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="e976c-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - to have a counterpart of Britta Simon in SpringCM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e976c-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e976c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e976c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e976c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e976c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e976c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e976c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing SpringCM configureren.</span><span class="sxs-lookup"><span data-stu-id="e976c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="e976c-150">**Voor het configureren van Azure AD eenmalige aanmelding met SpringCM, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e976c-150">**To configure Azure AD single sign-on with SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="e976c-151">In de Azure-portal op de **SpringCM** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e976c-151">In the Azure portal, on the **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e976c-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e976c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. <span data-ttu-id="e976c-155">Op de **SpringCM domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e976c-155">On the **SpringCM Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="e976c-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="e976c-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e976c-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="e976c-158">This value is not real.</span></span> <span data-ttu-id="e976c-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e976c-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="e976c-160">Neem contact op met [SpringCM Client ondersteuningsteam](https://knowledge.springcm.com/support) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="e976c-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) to get this value.</span></span> 
 
4. <span data-ttu-id="e976c-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Raw)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e976c-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. <span data-ttu-id="e976c-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e976c-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e976c-165">Op de **SpringCM configuratie** sectie, klikt u op **configureren SpringCM** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="e976c-165">On the **SpringCM Configuration** section, click **Configure SpringCM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e976c-166">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="e976c-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. <span data-ttu-id="e976c-168">In een ander browservenster, meld u aan bij uw **SpringCM** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="e976c-168">In a different web browser window, sign on to your **SpringCM** company site as administrator.</span></span>

8. <span data-ttu-id="e976c-169">Klik in het menu bovenaan op **Ga naar**, klikt u op **voorkeuren**, en klikt u op de **accountvoorkeuren** sectie, klikt u op **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="e976c-169">In the menu on the top, click **GO TO**, click **Preferences**, and then, in the **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="e976c-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML EENMALIGE AANMELDING")</span><span class="sxs-lookup"><span data-stu-id="e976c-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

9. <span data-ttu-id="e976c-171">In de configuratiesectie van identiteit Provider de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e976c-171">In the Identity Provider Configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="e976c-172">![Configuratie van de Provider identiteit](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "providerconfiguratie identiteit")</span><span class="sxs-lookup"><span data-stu-id="e976c-172">![Identity Provider Configuration](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="e976c-173">a.</span><span class="sxs-lookup"><span data-stu-id="e976c-173">a.</span></span> <span data-ttu-id="e976c-174">Als u wilt uw gedownloade Azure Active Directory-certificaat uploaden, klikt u op **uitgeverscertificaat Selecteer** of **wijziging uitgeverscertificaat**.</span><span class="sxs-lookup"><span data-stu-id="e976c-174">To upload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="e976c-175">b.</span><span class="sxs-lookup"><span data-stu-id="e976c-175">b.</span></span> <span data-ttu-id="e976c-176">Plakken **SAML entiteit-ID** waarde, die u hebt gekopieerd vanuit Azure-portal in de **verlener** textbox.</span><span class="sxs-lookup"><span data-stu-id="e976c-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into the **Issuer** textbox.</span></span>
    
    <span data-ttu-id="e976c-177">c.</span><span class="sxs-lookup"><span data-stu-id="e976c-177">c.</span></span> <span data-ttu-id="e976c-178">Plakken **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd vanuit de Azure-portal in de **Service Provider (SP) geïnitieerd eindpunt** textbox.</span><span class="sxs-lookup"><span data-stu-id="e976c-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="e976c-179">d.</span><span class="sxs-lookup"><span data-stu-id="e976c-179">d.</span></span> <span data-ttu-id="e976c-180">Selecteer **SAML ingeschakeld** als **inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="e976c-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="e976c-181">e.</span><span class="sxs-lookup"><span data-stu-id="e976c-181">e.</span></span> <span data-ttu-id="e976c-182">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e976c-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="e976c-183">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="e976c-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e976c-184">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="e976c-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e976c-185">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e976c-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e976c-186">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e976c-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="e976c-187">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e976c-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="e976c-189">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e976c-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e976c-190">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e976c-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e976c-192">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e976c-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e976c-194">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e976c-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e976c-196">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e976c-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e976c-198">a.</span><span class="sxs-lookup"><span data-stu-id="e976c-198">a.</span></span> <span data-ttu-id="e976c-199">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e976c-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e976c-200">b.</span><span class="sxs-lookup"><span data-stu-id="e976c-200">b.</span></span> <span data-ttu-id="e976c-201">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e976c-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e976c-202">c.</span><span class="sxs-lookup"><span data-stu-id="e976c-202">c.</span></span> <span data-ttu-id="e976c-203">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e976c-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e976c-204">d.</span><span class="sxs-lookup"><span data-stu-id="e976c-204">d.</span></span> <span data-ttu-id="e976c-205">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e976c-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="e976c-206">Een testgebruiker SpringCM maken</span><span class="sxs-lookup"><span data-stu-id="e976c-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="e976c-207">Om Azure Active Directory-gebruikers zich aanmelden bij SpringCM, moeten ze worden ingericht in SpringCM.</span><span class="sxs-lookup"><span data-stu-id="e976c-207">To enable Azure Active Directory users to log in to SpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="e976c-208">In het geval van SpringCM is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="e976c-208">In the case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="e976c-209">Zie voor meer informatie [maken en bewerken van een gebruiker SpringCM](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span><span class="sxs-lookup"><span data-stu-id="e976c-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="e976c-210">**Voor het inrichten van een gebruikersaccount aan SpringCM, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e976c-210">**To provision a user account to SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="e976c-211">Meld u aan bij uw **SpringCM** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="e976c-211">Log in to your **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="e976c-212">Klik op **GOTO**, en klik vervolgens op **ADRESBOEK**.</span><span class="sxs-lookup"><span data-stu-id="e976c-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="e976c-213">![Gebruiker maken](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "gebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="e976c-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span></span>

3. <span data-ttu-id="e976c-214">Klik op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="e976c-214">Click **Create User**.</span></span>

4. <span data-ttu-id="e976c-215">Selecteer een **gebruikersrol**.</span><span class="sxs-lookup"><span data-stu-id="e976c-215">Select a **User Role**.</span></span>

5. <span data-ttu-id="e976c-216">Selecteer **activering E-mail verzenden**.</span><span class="sxs-lookup"><span data-stu-id="e976c-216">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="e976c-217">Typ de voornaam, de achternaam en het e-mailadres van een geldige Azure Active Directory-gebruikersaccount die u inrichten in de bijbehorende tekstvakken wilt.</span><span class="sxs-lookup"><span data-stu-id="e976c-217">Type the first name, last name, and email address of a valid Azure Active Directory user account you want to provision into the related textboxes.</span></span>

7. <span data-ttu-id="e976c-218">De gebruiker toevoegen aan een **beveiligingsgroep**.</span><span class="sxs-lookup"><span data-stu-id="e976c-218">Add the user to a **Security group**.</span></span>

8. <span data-ttu-id="e976c-219">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e976c-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="e976c-220">U kunt andere SpringCM gebruiker account hulpmiddelen voor het maken of API's die is geleverd door SpringCM aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="e976c-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM to provision AAD user accounts.</span></span>  
  > 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e976c-221">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="e976c-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e976c-222">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan SpringCM.</span><span class="sxs-lookup"><span data-stu-id="e976c-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SpringCM.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="e976c-224">**Britta Simon om aan te wijzen SpringCM, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e976c-224">**To assign Britta Simon to SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="e976c-225">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e976c-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e976c-227">Selecteer in de lijst met toepassingen **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="e976c-227">In the applications list, select **SpringCM**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. <span data-ttu-id="e976c-229">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e976c-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="e976c-231">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e976c-231">Click **Add** button.</span></span> <span data-ttu-id="e976c-232">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e976c-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="e976c-234">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e976c-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e976c-235">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e976c-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e976c-236">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e976c-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e976c-237">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e976c-237">Testing single sign-on</span></span>

<span data-ttu-id="e976c-238">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="e976c-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="e976c-239">Als u op de tegel SpringCM in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing SpringCM.</span><span class="sxs-lookup"><span data-stu-id="e976c-239">When you click the SpringCM tile in the Access Panel, you should get automatically signed-on to your SpringCM application.</span></span>

<span data-ttu-id="e976c-240">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e976c-240">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e976c-241">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e976c-241">Additional resources</span></span>

* [<span data-ttu-id="e976c-242">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e976c-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e976c-243">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e976c-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png

