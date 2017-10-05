---
title: 'Zelfstudie: Azure Active Directory-integratie met SmarterU | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en SmarterU.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 129d08c8a7b4228d4d5f1a3b7938ab649b2747a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a><span data-ttu-id="6f3c4-103">Zelfstudie: Azure Active Directory-integratie met SmarterU</span><span class="sxs-lookup"><span data-stu-id="6f3c4-103">Tutorial: Azure Active Directory integration with SmarterU</span></span>

<span data-ttu-id="6f3c4-104">In deze zelfstudie leert u hoe SmarterU integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6f3c4-104">In this tutorial, you learn how to integrate SmarterU with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6f3c4-105">SmarterU integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6f3c4-105">Integrating SmarterU with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6f3c4-106">U kunt beheren in Azure AD die toegang tot SmarterU heeft</span><span class="sxs-lookup"><span data-stu-id="6f3c4-106">You can control in Azure AD who has access to SmarterU</span></span>
- <span data-ttu-id="6f3c4-107">U kunt uw gebruikers automatisch ophalen aangemeld bij SmarterU (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="6f3c4-107">You can enable your users to automatically get signed-on to SmarterU (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6f3c4-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6f3c4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6f3c4-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6f3c4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f3c4-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6f3c4-110">Prerequisites</span></span>

<span data-ttu-id="6f3c4-111">Voor het configureren van Azure AD-integratie met SmarterU, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="6f3c4-111">To configure Azure AD integration with SmarterU, you need the following items:</span></span>

- <span data-ttu-id="6f3c4-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6f3c4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6f3c4-113">Een SmarterU eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6f3c4-113">A SmarterU single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6f3c4-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6f3c4-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6f3c4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6f3c4-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6f3c4-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6f3c4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6f3c4-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6f3c4-118">Scenario description</span></span>
<span data-ttu-id="6f3c4-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6f3c4-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6f3c4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6f3c4-121">SmarterU uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6f3c4-121">Adding SmarterU from the gallery</span></span>
2. <span data-ttu-id="6f3c4-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6f3c4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smarteru-from-the-gallery"></a><span data-ttu-id="6f3c4-123">SmarterU uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6f3c4-123">Adding SmarterU from the gallery</span></span>
<span data-ttu-id="6f3c4-124">Voor het configureren van de integratie van SmarterU in Azure AD, moet u SmarterU uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-124">To configure the integration of SmarterU into Azure AD, you need to add SmarterU from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6f3c4-125">**Als u wilt toevoegen SmarterU uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6f3c4-125">**To add SmarterU from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6f3c4-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6f3c4-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6f3c4-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6f3c4-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6f3c4-133">Typ in het zoekvak **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-133">In the search box, type **SmarterU**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_search.png)

5. <span data-ttu-id="6f3c4-135">Selecteer in het deelvenster resultaten **SmarterU**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-135">In the results panel, select **SmarterU**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6f3c4-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6f3c4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6f3c4-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met SmarterU op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6f3c4-138">In this section, you configure and test Azure AD single sign-on with SmarterU based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6f3c4-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in SmarterU is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SmarterU is to a user in Azure AD.</span></span> <span data-ttu-id="6f3c4-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in SmarterU tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-140">In other words, a link relationship between an Azure AD user and the related user in SmarterU needs to be established.</span></span>

<span data-ttu-id="6f3c4-141">Wijs in SmarterU, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-141">In SmarterU, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6f3c4-142">Om te configureren en testen van Azure AD eenmalige aanmelding met SmarterU, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="6f3c4-142">To configure and test Azure AD single sign-on with SmarterU, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6f3c4-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6f3c4-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6f3c4-145">**[Maken van een testgebruiker SmarterU](#creating-a-smarteru-test-user)**  - SmarterU die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-145">**[Creating a SmarterU test user](#creating-a-smarteru-test-user)** - to have a counterpart of Britta Simon in SmarterU that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6f3c4-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6f3c4-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6f3c4-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6f3c4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6f3c4-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing SmarterU configureren.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SmarterU application.</span></span>

<span data-ttu-id="6f3c4-150">**Voor het configureren van Azure AD eenmalige aanmelding met SmarterU, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6f3c4-150">**To configure Azure AD single sign-on with SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="6f3c4-151">In de Azure-portal op de **SmarterU** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-151">In the Azure portal, on the **SmarterU** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6f3c4-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_samlbase.png)

3. <span data-ttu-id="6f3c4-155">Op de **SmarterU domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6f3c4-155">On the **SmarterU Domain and URLs** section, perform the following steps:</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_url.png)

    <span data-ttu-id="6f3c4-157">In de **id** textbox, typ de URL:`https://www.smarteru.com/`</span><span class="sxs-lookup"><span data-stu-id="6f3c4-157">In the **Identifier** textbox, type the URL: `https://www.smarteru.com/`</span></span>

4. <span data-ttu-id="6f3c4-158">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_certificate.png) 

5. <span data-ttu-id="6f3c4-160">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-160">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smarteru-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6f3c4-162">In een ander browservenster, meld u aan bij uw bedrijf SmarterU site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-162">In a different web browser window, log in to your SmarterU company site as an administrator.</span></span>

7. <span data-ttu-id="6f3c4-163">Klik in de werkbalk bovenaan op **Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-163">In the toolbar on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="6f3c4-164">![Instellingen account](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Accountinstellingen")</span><span class="sxs-lookup"><span data-stu-id="6f3c4-164">![Account Settings](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")</span></span>

8. <span data-ttu-id="6f3c4-165">Voer de volgende stappen uit op de configuratiepagina van account:</span><span class="sxs-lookup"><span data-stu-id="6f3c4-165">On the account configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="6f3c4-166">![Externe autorisatie](./media/active-directory-saas-smarteru-tutorial/IC777327.png "externe autorisatie")</span><span class="sxs-lookup"><span data-stu-id="6f3c4-166">![External Authorization](./media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization")</span></span> 
 
      <span data-ttu-id="6f3c4-167">a.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-167">a.</span></span> <span data-ttu-id="6f3c4-168">Selecteer **inschakelen van externe autorisatie**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-168">Select **Enable External Authorization**.</span></span>
  
      <span data-ttu-id="6f3c4-169">b.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-169">b.</span></span> <span data-ttu-id="6f3c4-170">In de **Master aanmelding besturingselement** sectie, selecteer de **SmarterU** tabblad.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-170">In the **Master Login Control** section, select the **SmarterU** tab.</span></span>
  
      <span data-ttu-id="6f3c4-171">c.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-171">c.</span></span> <span data-ttu-id="6f3c4-172">In de **standaard gebruikersaanmelding** sectie, selecteer de **SmarterU** tabblad.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-172">In the **User Default Login** section, select the **SmarterU** tab.</span></span>
  
      <span data-ttu-id="6f3c4-173">d.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-173">d.</span></span> <span data-ttu-id="6f3c4-174">Selecteer **inschakelen, Okta**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-174">Select **Enable Okta**.</span></span>
  
      <span data-ttu-id="6f3c4-175">e.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-175">e.</span></span> <span data-ttu-id="6f3c4-176">Kopieer de inhoud van het metagegevensbestand van de gedownloade en plakt u deze in de **Okta Metadata** textbox.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-176">Copy the content of the downloaded metadata file, and then paste it into the **Okta Metadata** textbox.</span></span>
  
      <span data-ttu-id="6f3c4-177">f.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-177">f.</span></span> <span data-ttu-id="6f3c4-178">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-178">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6f3c4-179">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="6f3c4-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6f3c4-180">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6f3c4-181">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6f3c4-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6f3c4-182">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6f3c4-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="6f3c4-183">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6f3c4-185">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6f3c4-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6f3c4-186">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smarteru-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6f3c4-188">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smarteru-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6f3c4-190">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smarteru-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6f3c4-192">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6f3c4-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-smarteru-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6f3c4-194">a.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-194">a.</span></span> <span data-ttu-id="6f3c4-195">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6f3c4-196">b.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-196">b.</span></span> <span data-ttu-id="6f3c4-197">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6f3c4-198">c.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-198">c.</span></span> <span data-ttu-id="6f3c4-199">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6f3c4-200">d.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-200">d.</span></span> <span data-ttu-id="6f3c4-201">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-201">Click **Create**.</span></span>
 
### <a name="creating-a-smarteru-test-user"></a><span data-ttu-id="6f3c4-202">Een testgebruiker SmarterU maken</span><span class="sxs-lookup"><span data-stu-id="6f3c4-202">Creating a SmarterU test user</span></span>

<span data-ttu-id="6f3c4-203">Om Azure AD-gebruikers zich aanmelden bij SmarterU, moeten ze worden ingericht in SmarterU.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-203">To enable Azure AD users to log in to SmarterU, they must be provisioned into SmarterU.</span></span>

<span data-ttu-id="6f3c4-204">SmarterU, inrichting wanneer een handmatige taak is.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-204">When SmarterU, provisioning is a manual task.</span></span>

<span data-ttu-id="6f3c4-205">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6f3c4-205">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="6f3c4-206">Meld u aan bij uw **SmarterU** tenant.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-206">Log in to your **SmarterU** tenant.</span></span>

2. <span data-ttu-id="6f3c4-207">Ga naar **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-207">Go to **Users**.</span></span>

3. <span data-ttu-id="6f3c4-208">Voer de volgende stappen uit in de sectie gebruiker:</span><span class="sxs-lookup"><span data-stu-id="6f3c4-208">In the user section, perform the following steps:</span></span>
   
    <span data-ttu-id="6f3c4-209">![Nieuwe gebruiker](./media/active-directory-saas-smarteru-tutorial/IC777329.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="6f3c4-209">![New User](./media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")</span></span>  

    <span data-ttu-id="6f3c4-210">a.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-210">a.</span></span> <span data-ttu-id="6f3c4-211">Klik op **+ User**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-211">Click **+User**.</span></span>
    
    <span data-ttu-id="6f3c4-212">b.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-212">b.</span></span> <span data-ttu-id="6f3c4-213">Typ de waarden van het gerelateerde kenmerk van het Azure AD-gebruikersaccount in de volgende tekstvakken: **primaire e**, **werknemer-ID**, **wachtwoord**, **controleren Wachtwoord**, **voornaam**, **achternaam**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-213">Type the related attribute values of the Azure AD user account into the following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span></span>
    
    <span data-ttu-id="6f3c4-214">c.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-214">c.</span></span> <span data-ttu-id="6f3c4-215">Klik op **Active**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-215">Click **Active**.</span></span> 
    
    <span data-ttu-id="6f3c4-216">d.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-216">d.</span></span> <span data-ttu-id="6f3c4-217">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-217">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="6f3c4-218">U kunt andere SmarterU gebruiker account hulpmiddelen voor het maken of API's die is geleverd door SmarterU aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-218">You can use any other SmarterU user account creation tools or APIs provided by SmarterU to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6f3c4-219">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f3c4-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6f3c4-220">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan SmarterU.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SmarterU.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6f3c4-222">**Britta Simon om aan te wijzen SmarterU, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6f3c4-222">**To assign Britta Simon to SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="6f3c4-223">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6f3c4-225">Selecteer in de lijst met toepassingen **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-225">In the applications list, select **SmarterU**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_app.png) 

3. <span data-ttu-id="6f3c4-227">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6f3c4-229">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-229">Click **Add** button.</span></span> <span data-ttu-id="6f3c4-230">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6f3c4-232">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6f3c4-233">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6f3c4-234">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6f3c4-235">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6f3c4-235">Testing single sign-on</span></span>

<span data-ttu-id="6f3c4-236">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="6f3c4-237">Als u op de tegel SmarterU in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing SmarterU.</span><span class="sxs-lookup"><span data-stu-id="6f3c4-237">When you click the SmarterU tile in the Access Panel, you should get automatically signed-on to your SmarterU application.</span></span>
<span data-ttu-id="6f3c4-238">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6f3c4-238">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 


## <a name="additional-resources"></a><span data-ttu-id="6f3c4-239">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6f3c4-239">Additional resources</span></span>

* [<span data-ttu-id="6f3c4-240">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6f3c4-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6f3c4-241">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6f3c4-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_203.png

