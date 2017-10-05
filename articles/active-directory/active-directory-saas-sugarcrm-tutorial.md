---
title: 'Zelfstudie: Azure Active Directory-integratie met suiker CRM | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en suiker CRM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: c27aef24e859522b8001ecb747906abdca14d87a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a><span data-ttu-id="f79b9-103">Zelfstudie: Azure Active Directory-integratie met suiker CRM</span><span class="sxs-lookup"><span data-stu-id="f79b9-103">Tutorial: Azure Active Directory integration with Sugar CRM</span></span>

<span data-ttu-id="f79b9-104">In deze zelfstudie leert u hoe suiker CRM integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f79b9-104">In this tutorial, you learn how to integrate Sugar CRM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f79b9-105">Suiker CRM integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f79b9-105">Integrating Sugar CRM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f79b9-106">U kunt beheren in Azure AD die toegang tot de CRM suiker heeft</span><span class="sxs-lookup"><span data-stu-id="f79b9-106">You can control in Azure AD who has access to Sugar CRM</span></span>
- <span data-ttu-id="f79b9-107">U kunt uw gebruikers automatisch ophalen aangemeld bij suiker CRM (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="f79b9-107">You can enable your users to automatically get signed-on to Sugar CRM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f79b9-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f79b9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f79b9-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f79b9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f79b9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f79b9-110">Prerequisites</span></span>

<span data-ttu-id="f79b9-111">Voor het configureren van Azure AD-integratie met suiker CRM, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="f79b9-111">To configure Azure AD integration with Sugar CRM, you need the following items:</span></span>

- <span data-ttu-id="f79b9-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f79b9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f79b9-113">Een CRM suiker eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f79b9-113">A Sugar CRM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f79b9-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f79b9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f79b9-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f79b9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f79b9-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f79b9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f79b9-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f79b9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f79b9-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f79b9-118">Scenario description</span></span>
<span data-ttu-id="f79b9-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f79b9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f79b9-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f79b9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f79b9-121">Suiker CRM uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f79b9-121">Adding Sugar CRM from the gallery</span></span>
2. <span data-ttu-id="f79b9-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f79b9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sugar-crm-from-the-gallery"></a><span data-ttu-id="f79b9-123">Suiker CRM uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f79b9-123">Adding Sugar CRM from the gallery</span></span>
<span data-ttu-id="f79b9-124">Voor het configureren van de integratie van suiker CRM in Azure AD, moet u suiker CRM uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f79b9-124">To configure the integration of Sugar CRM into Azure AD, you need to add Sugar CRM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f79b9-125">**Als u wilt toevoegen suiker CRM uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f79b9-125">**To add Sugar CRM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f79b9-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f79b9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f79b9-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f79b9-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f79b9-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f79b9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f79b9-133">Typ in het zoekvak **suiker CRM**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-133">In the search box, type **Sugar CRM**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. <span data-ttu-id="f79b9-135">Selecteer in het deelvenster resultaten **suiker CRM**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f79b9-135">In the results panel, select **Sugar CRM**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f79b9-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f79b9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f79b9-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met suiker CRM op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f79b9-138">In this section, you configure and test Azure AD single sign-on with Sugar CRM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f79b9-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in suiker CRM is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f79b9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sugar CRM is to a user in Azure AD.</span></span> <span data-ttu-id="f79b9-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante suiker CRM-gebruiker worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f79b9-140">In other words, a link relationship between an Azure AD user and the related user in Sugar CRM needs to be established.</span></span>

<span data-ttu-id="f79b9-141">Wijs in suiker CRM, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="f79b9-141">In Sugar CRM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f79b9-142">Om te configureren en testen van Azure AD eenmalige aanmelding met suiker CRM, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="f79b9-142">To configure and test Azure AD single sign-on with Sugar CRM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f79b9-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f79b9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f79b9-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f79b9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f79b9-145">**[Maken van een testgebruiker suiker CRM](#creating-a-sugar-crm-test-user)**  - suiker CRM die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="f79b9-145">**[Creating a Sugar CRM test user](#creating-a-sugar-crm-test-user)** - to have a counterpart of Britta Simon in Sugar CRM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f79b9-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f79b9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f79b9-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f79b9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f79b9-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f79b9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f79b9-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing suiker CRM.</span><span class="sxs-lookup"><span data-stu-id="f79b9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sugar CRM application.</span></span>

<span data-ttu-id="f79b9-150">**Voor het configureren van Azure AD eenmalige aanmelding met suiker CRM, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f79b9-150">**To configure Azure AD single sign-on with Sugar CRM, perform the following steps:**</span></span>

1. <span data-ttu-id="f79b9-151">In de Azure-portal op de **suiker CRM** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-151">In the Azure portal, on the **Sugar CRM** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f79b9-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f79b9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. <span data-ttu-id="f79b9-155">Op de **suiker CRM-domein en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f79b9-155">On the **Sugar CRM Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    <span data-ttu-id="f79b9-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="f79b9-157">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > <span data-ttu-id="f79b9-158">De waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="f79b9-158">The value is not real.</span></span> <span data-ttu-id="f79b9-159">Werk de waarde met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f79b9-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="f79b9-160">Neem contact op met [suiker CRM-Client-ondersteuningsteam](https://support.sugarcrm.com/) de waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="f79b9-160">Contact [Sugar CRM Client support team](https://support.sugarcrm.com/) to get the value.</span></span> 
 
4. <span data-ttu-id="f79b9-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f79b9-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. <span data-ttu-id="f79b9-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f79b9-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f79b9-165">Op de **suiker CRM configuratie** sectie, klikt u op **configureren suiker CRM** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="f79b9-165">On the **Sugar CRM Configuration** section, click **Configure Sugar CRM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f79b9-166">Kopieer de **Sign-Out URL's, en SAML Single Sign-On Service** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="f79b9-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. <span data-ttu-id="f79b9-168">In een ander browservenster, meld u aan bij uw bedrijf suiker CRM site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f79b9-168">In a different web browser window, log in to your Sugar CRM company site as an administrator.</span></span>

8. <span data-ttu-id="f79b9-169">Ga naar **Admin**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-169">Go to **Admin**.</span></span>
   
    <span data-ttu-id="f79b9-170">![Beheerder](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="f79b9-170">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

9. <span data-ttu-id="f79b9-171">In de **beheer** sectie, klikt u op **wachtwoordbeheer**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-171">In the **Administration** section, click **Password Management**.</span></span>
   
    <span data-ttu-id="f79b9-172">![Beheer](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="f79b9-172">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administration")</span></span>

10. <span data-ttu-id="f79b9-173">Selecteer **SAML-verificatie inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-173">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="f79b9-174">![Beheer](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="f79b9-174">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administration")</span></span>

11. <span data-ttu-id="f79b9-175">In de **SAML-verificatie** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f79b9-175">In the **SAML Authentication** section, perform the following steps:</span></span>
   
    <span data-ttu-id="f79b9-176">![SAML-verificatie](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML-verificatie")</span><span class="sxs-lookup"><span data-stu-id="f79b9-176">![SAML Authentication](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML Authentication")</span></span>  
 
    <span data-ttu-id="f79b9-177">a.</span><span class="sxs-lookup"><span data-stu-id="f79b9-177">a.</span></span> <span data-ttu-id="f79b9-178">In de **aanmeldings-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f79b9-178">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="f79b9-179">b.</span><span class="sxs-lookup"><span data-stu-id="f79b9-179">b.</span></span> <span data-ttu-id="f79b9-180">In de **SLO URL** textbox, plak de waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f79b9-180">In the **SLO URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="f79b9-181">c.</span><span class="sxs-lookup"><span data-stu-id="f79b9-181">c.</span></span> <span data-ttu-id="f79b9-182">Open uw base-64 gecodeerde certificaat in Kladblok, Kopieer de inhoud ervan naar het Klembord en plak het gehele certificaat in **X.509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="f79b9-182">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="f79b9-183">d.</span><span class="sxs-lookup"><span data-stu-id="f79b9-183">d.</span></span> <span data-ttu-id="f79b9-184">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f79b9-185">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="f79b9-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f79b9-186">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="f79b9-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f79b9-187">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f79b9-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f79b9-188">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f79b9-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="f79b9-189">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f79b9-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f79b9-191">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f79b9-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f79b9-192">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f79b9-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f79b9-194">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f79b9-196">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f79b9-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f79b9-198">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f79b9-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f79b9-200">a.</span><span class="sxs-lookup"><span data-stu-id="f79b9-200">a.</span></span> <span data-ttu-id="f79b9-201">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f79b9-202">b.</span><span class="sxs-lookup"><span data-stu-id="f79b9-202">b.</span></span> <span data-ttu-id="f79b9-203">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f79b9-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f79b9-204">c.</span><span class="sxs-lookup"><span data-stu-id="f79b9-204">c.</span></span> <span data-ttu-id="f79b9-205">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f79b9-206">d.</span><span class="sxs-lookup"><span data-stu-id="f79b9-206">d.</span></span> <span data-ttu-id="f79b9-207">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-207">Click **Create**.</span></span>
 
### <a name="creating-a-sugar-crm-test-user"></a><span data-ttu-id="f79b9-208">Een testgebruiker suiker CRM maken</span><span class="sxs-lookup"><span data-stu-id="f79b9-208">Creating a Sugar CRM test user</span></span>

<span data-ttu-id="f79b9-209">Om in te schakelen Azure AD-gebruikers zich aanmelden bij suiker CRM, moeten ze worden ingericht op suiker CRM.</span><span class="sxs-lookup"><span data-stu-id="f79b9-209">In order to enable Azure AD users to log in to Sugar CRM, they must be provisioned to Sugar CRM.</span></span>

<span data-ttu-id="f79b9-210">In het geval van suiker CRM is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="f79b9-210">In the case of Sugar CRM, provisioning is a manual task.</span></span>

<span data-ttu-id="f79b9-211">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f79b9-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="f79b9-212">Meld u aan bij uw **suiker CRM** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="f79b9-212">Log in to your **Sugar CRM** company site as administrator.</span></span>

2. <span data-ttu-id="f79b9-213">Ga naar **Admin**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-213">Go to **Admin**.</span></span>
   
    <span data-ttu-id="f79b9-214">![Beheerder](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="f79b9-214">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

3. <span data-ttu-id="f79b9-215">In de **beheer** sectie, klikt u op **Gebruikersbeheer**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-215">In the **Administration** section, click **User Management**.</span></span>
   
    <span data-ttu-id="f79b9-216">![Beheer](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="f79b9-216">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administration")</span></span>

4. <span data-ttu-id="f79b9-217">Ga naar **gebruikers \> nieuwe gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-217">Go to **Users \> Create New User**.</span></span>
   
    <span data-ttu-id="f79b9-218">![Nieuwe gebruiker maken](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "nieuwe gebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="f79b9-218">![Create New User](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Create New User")</span></span>

5. <span data-ttu-id="f79b9-219">Op de **gebruikersprofiel** tabblad, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f79b9-219">On the **User Profile** tab, perform the following steps:</span></span>
   
    <span data-ttu-id="f79b9-220">![Nieuwe gebruiker](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="f79b9-220">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "New User")</span></span>

    <span data-ttu-id="f79b9-221">a.</span><span class="sxs-lookup"><span data-stu-id="f79b9-221">a.</span></span> <span data-ttu-id="f79b9-222">Typ de **gebruikersnaam**, **achternaam**, en **e-mailadres** van een geldige Azure Active Directory-gebruiker in de bijbehorende tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="f79b9-222">Type the **user name**, **last name**, and **email address** of a valid Azure Active Directory user into the related textboxes.</span></span>
  
6. <span data-ttu-id="f79b9-223">Als **Status**, selecteer **Active**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-223">As **Status**, select **Active**.</span></span>

7. <span data-ttu-id="f79b9-224">Voer de volgende stappen uit op het tabblad wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="f79b9-224">On the Password tab, perform the following steps:</span></span>
   
    <span data-ttu-id="f79b9-225">![Nieuwe gebruiker](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="f79b9-225">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "New User")</span></span>

    <span data-ttu-id="f79b9-226">a.</span><span class="sxs-lookup"><span data-stu-id="f79b9-226">a.</span></span> <span data-ttu-id="f79b9-227">Typ het wachtwoord in het bijbehorende tekstvak.</span><span class="sxs-lookup"><span data-stu-id="f79b9-227">Type the password into the related textbox.</span></span>

    <span data-ttu-id="f79b9-228">b.</span><span class="sxs-lookup"><span data-stu-id="f79b9-228">b.</span></span> <span data-ttu-id="f79b9-229">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-229">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="f79b9-230">U kunt andere suiker CRM gebruiker account hulpmiddelen voor het maken of API's die is geleverd door suiker CRM aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="f79b9-230">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f79b9-231">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="f79b9-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f79b9-232">In deze sectie maakt inschakelen u Britta Simon gebruiken Azure eenmalige aanmelding toegang verleent tot suiker CRM.</span><span class="sxs-lookup"><span data-stu-id="f79b9-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sugar CRM.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f79b9-234">**Britta Simon om aan te wijzen suiker CRM, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f79b9-234">**To assign Britta Simon to Sugar CRM, perform the following steps:**</span></span>

1. <span data-ttu-id="f79b9-235">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f79b9-237">Selecteer in de lijst met toepassingen **suiker CRM**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-237">In the applications list, select **Sugar CRM**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. <span data-ttu-id="f79b9-239">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f79b9-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f79b9-241">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f79b9-241">Click **Add** button.</span></span> <span data-ttu-id="f79b9-242">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f79b9-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f79b9-244">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="f79b9-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f79b9-245">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f79b9-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f79b9-246">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f79b9-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f79b9-247">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f79b9-247">Testing single sign-on</span></span>

<span data-ttu-id="f79b9-248">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="f79b9-248">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f79b9-249">Als u op de tegel suiker CRM in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw suiker CRM-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f79b9-249">When you click the Sugar CRM tile in the Access Panel, you should get automatically signed-on to your Sugar CRM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f79b9-250">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f79b9-250">Additional resources</span></span>

* [<span data-ttu-id="f79b9-251">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f79b9-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f79b9-252">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f79b9-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

