---
title: 'Zelfstudie: Azure Active Directory-integratie met Tableau Online | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding van Azure Active Directory en Tableau Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 443fab1198a91a4d5749e6421f7b8603fc75a81e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="c3c36-103">Zelfstudie: Azure Active Directory-integratie met Tableau Online</span><span class="sxs-lookup"><span data-stu-id="c3c36-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="c3c36-104">In deze zelfstudie leert u hoe Tableau Online integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3c36-104">In this tutorial, you learn how to integrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c3c36-105">Online Tableau integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="c3c36-105">Integrating Tableau Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c3c36-106">U kunt beheren in Azure AD die toegang tot Tableau Online heeft</span><span class="sxs-lookup"><span data-stu-id="c3c36-106">You can control in Azure AD who has access to Tableau Online</span></span>
- <span data-ttu-id="c3c36-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Tableau Online (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="c3c36-107">You can enable your users to automatically get signed-on to Tableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c3c36-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="c3c36-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c3c36-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c3c36-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3c36-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c3c36-110">Prerequisites</span></span>

<span data-ttu-id="c3c36-111">Voor het configureren van Azure AD-integratie met Tableau Online, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="c3c36-111">To configure Azure AD integration with Tableau Online, you need the following items:</span></span>

- <span data-ttu-id="c3c36-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="c3c36-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c3c36-113">Een Tableau Online eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="c3c36-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c3c36-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="c3c36-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c3c36-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="c3c36-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c3c36-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="c3c36-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c3c36-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c3c36-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c3c36-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="c3c36-118">Scenario description</span></span>
<span data-ttu-id="c3c36-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="c3c36-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c3c36-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="c3c36-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c3c36-121">Toevoegen van Online Tableau uit de galerie</span><span class="sxs-lookup"><span data-stu-id="c3c36-121">Adding Tableau Online from the gallery</span></span>
2. <span data-ttu-id="c3c36-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c3c36-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-the-gallery"></a><span data-ttu-id="c3c36-123">Toevoegen van Online Tableau uit de galerie</span><span class="sxs-lookup"><span data-stu-id="c3c36-123">Adding Tableau Online from the gallery</span></span>
<span data-ttu-id="c3c36-124">Voor het configureren van de integratie van Tableau Online in Azure AD, moet u Tableau Online uit de galerie toevoegt aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="c3c36-124">To configure the integration of Tableau Online into Azure AD, you need to add Tableau Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c3c36-125">**Als u wilt toevoegen in de galerie Tableau Online, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c3c36-125">**To add Tableau Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c3c36-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c3c36-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c3c36-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c3c36-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c3c36-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c3c36-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="c3c36-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c3c36-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="c3c36-133">Typ in het zoekvak **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="c3c36-133">In the search box, type **Tableau Online**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="c3c36-135">Selecteer in het deelvenster resultaten **Tableau Online**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c3c36-135">In the results panel, select **Tableau Online**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c3c36-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c3c36-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c3c36-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Tableau Online op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="c3c36-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c3c36-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Tableau Online is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3c36-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Online is to a user in Azure AD.</span></span> <span data-ttu-id="c3c36-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Tableau online worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c3c36-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Online needs to be established.</span></span>

<span data-ttu-id="c3c36-141">In Online Tableau, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="c3c36-141">In Tableau Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c3c36-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Tableau Online, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="c3c36-142">To configure and test Azure AD single sign-on with Tableau Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c3c36-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c3c36-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c3c36-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3c36-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c3c36-145">**[Maken van een Online Tableau testgebruiker](#creating-a-tableau-online-test-user)**  - bevatten een equivalent van Britta Simon Tableau Online die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c3c36-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - to have a counterpart of Britta Simon in Tableau Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c3c36-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c3c36-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c3c36-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="c3c36-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c3c36-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="c3c36-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c3c36-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Tableau Online configureren.</span><span class="sxs-lookup"><span data-stu-id="c3c36-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="c3c36-150">**Voor het configureren van Azure AD eenmalige aanmelding met Tableau Online, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c3c36-150">**To configure Azure AD single sign-on with Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="c3c36-151">In de Azure-portal op de **Tableau Online** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="c3c36-151">In the Azure portal, on the **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="c3c36-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c3c36-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="c3c36-155">Op de **Tableau Online domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c3c36-155">On the **Tableau Online Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="c3c36-157">a.</span><span class="sxs-lookup"><span data-stu-id="c3c36-157">a.</span></span> <span data-ttu-id="c3c36-158">In de **aanmeldings-URL** textbox, typ de URL:`https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="c3c36-158">In the **Sign-on URL** textbox, type the URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="c3c36-159">b.</span><span class="sxs-lookup"><span data-stu-id="c3c36-159">b.</span></span> <span data-ttu-id="c3c36-160">In de **id** textbox, typ de URL:`https://sso.online.tableau.com/public/sp/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="c3c36-160">In the **Identifier** textbox, type the URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="c3c36-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c3c36-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="c3c36-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="c3c36-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c3c36-165">In een ander browservenster aanmelding bij uw Tableau Online-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c3c36-165">In a different browser window, sign-on to your Tableau Online application.</span></span> <span data-ttu-id="c3c36-166">Ga naar **instellingen** en vervolgens **verificatie**.</span><span class="sxs-lookup"><span data-stu-id="c3c36-166">Go to **Settings** and then **Authentication**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="c3c36-168">Om in te schakelen SAML, onder **verificatietypen** sectie.</span><span class="sxs-lookup"><span data-stu-id="c3c36-168">To enable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="c3c36-169">Controleer de **eenmalige aanmelding met SAML** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="c3c36-169">Check the **Single sign-on with SAML** checkbox.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="c3c36-171">Schuif omlaag totdat **metagegevensbestand importeren in Tableau Online** sectie.</span><span class="sxs-lookup"><span data-stu-id="c3c36-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="c3c36-172">Klik op Bladeren en importeer het metagegevensbestand die u hebt gedownload van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3c36-172">Click Browse and import the metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="c3c36-173">Klik vervolgens op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="c3c36-173">Then, click **Apply**.</span></span>
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="c3c36-175">In de **overeen met asserties** sectie, voert u de bijbehorende naam van de verklaring id-Provider voor **e-mailadres**, **voornaam**, en **achternaam**.</span><span class="sxs-lookup"><span data-stu-id="c3c36-175">In the **Match assertions** section, insert the corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="c3c36-176">Deze gegevens ophalen uit Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c3c36-176">To get this information from Azure AD:</span></span> 
  
    <span data-ttu-id="c3c36-177">a.</span><span class="sxs-lookup"><span data-stu-id="c3c36-177">a.</span></span> <span data-ttu-id="c3c36-178">Ga in de Azure-portal op de **Tableau Online** pagina van de integratie van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c3c36-178">In the Azure portal, go on the **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="c3c36-179">b.</span><span class="sxs-lookup"><span data-stu-id="c3c36-179">b.</span></span> <span data-ttu-id="c3c36-180">Selecteer in de kenmerkensectie de **'weergeven en bewerken van alle andere gebruikerskenmerken '** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="c3c36-180">In the attributes section, Select the **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="c3c36-182">c.</span><span class="sxs-lookup"><span data-stu-id="c3c36-182">c.</span></span> <span data-ttu-id="c3c36-183">Kopieer de naamruimtewaarde voor deze kenmerken: givenname, e-mail- en achternaam met behulp van de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c3c36-183">Copy the namespace value for these attributes: givenname, email and surname by using the following steps:</span></span>

   ![Azure AD voor eenmalige aanmelding](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="c3c36-185">d.</span><span class="sxs-lookup"><span data-stu-id="c3c36-185">d.</span></span> <span data-ttu-id="c3c36-186">Klik op **user.givenname** waarde</span><span class="sxs-lookup"><span data-stu-id="c3c36-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="c3c36-187">e.</span><span class="sxs-lookup"><span data-stu-id="c3c36-187">e.</span></span> <span data-ttu-id="c3c36-188">Kopieer de waarde van de **naamruimte** textbox.</span><span class="sxs-lookup"><span data-stu-id="c3c36-188">Copy the value from the **namespace** textbox.</span></span>

   ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="c3c36-190">f.</span><span class="sxs-lookup"><span data-stu-id="c3c36-190">f.</span></span> <span data-ttu-id="c3c36-191">Als u wilt kopiëren van de namesapce stappen waarden voor de e-mail- en achternaam de voorgaande.</span><span class="sxs-lookup"><span data-stu-id="c3c36-191">To copy the namesapce values for the email and surname follow the preceding steps.</span></span>

    <span data-ttu-id="c3c36-192">g.</span><span class="sxs-lookup"><span data-stu-id="c3c36-192">g.</span></span> <span data-ttu-id="c3c36-193">Overschakelen naar de Tableau on line toepassing en stel vervolgens de **Tableau Online kenmerken** sectie als volgt:</span><span class="sxs-lookup"><span data-stu-id="c3c36-193">Switch to the Tableau Online application, then set the **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="c3c36-194">E-mailadres: **mail** of **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="c3c36-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="c3c36-195">Voornaam: **givenname**</span><span class="sxs-lookup"><span data-stu-id="c3c36-195">First name: **givenname**</span></span>
     * <span data-ttu-id="c3c36-196">Achternaam: **achternaam**</span><span class="sxs-lookup"><span data-stu-id="c3c36-196">Last name: **surname**</span></span>
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="c3c36-198">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="c3c36-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c3c36-199">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="c3c36-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c3c36-200">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c3c36-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c3c36-201">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="c3c36-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="c3c36-202">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c3c36-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="c3c36-204">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c3c36-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c3c36-205">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c3c36-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c3c36-207">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="c3c36-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c3c36-209">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c3c36-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c3c36-211">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c3c36-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c3c36-213">a.</span><span class="sxs-lookup"><span data-stu-id="c3c36-213">a.</span></span> <span data-ttu-id="c3c36-214">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c3c36-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c3c36-215">b.</span><span class="sxs-lookup"><span data-stu-id="c3c36-215">b.</span></span> <span data-ttu-id="c3c36-216">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c3c36-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c3c36-217">c.</span><span class="sxs-lookup"><span data-stu-id="c3c36-217">c.</span></span> <span data-ttu-id="c3c36-218">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="c3c36-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c3c36-219">d.</span><span class="sxs-lookup"><span data-stu-id="c3c36-219">d.</span></span> <span data-ttu-id="c3c36-220">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c3c36-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="c3c36-221">Maken van een Online Tableau testgebruiker</span><span class="sxs-lookup"><span data-stu-id="c3c36-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="c3c36-222">In deze sectie maakt maken u een gebruiker die is aangeroepen terwijl Britta Simon Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="c3c36-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="c3c36-223">Op **Tableau Online**, klikt u op **instellingen** en vervolgens **verificatie** sectie.</span><span class="sxs-lookup"><span data-stu-id="c3c36-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="c3c36-224">Schuif omlaag naar **gebruikers selecteren** sectie.</span><span class="sxs-lookup"><span data-stu-id="c3c36-224">Scroll down to **Select Users** section.</span></span> <span data-ttu-id="c3c36-225">Klik op **gebruikers toevoegen** en vervolgens **Voer e-mailadressen**.</span><span class="sxs-lookup"><span data-stu-id="c3c36-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="c3c36-227">Selecteer **toevoegen van gebruikers voor eenmalige aanmelding (SSO) verificatie**.</span><span class="sxs-lookup"><span data-stu-id="c3c36-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="c3c36-228">In de **e-mailadressen opgeven** textbox toevoegenbritta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="c3c36-228">In the **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="c3c36-230">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c3c36-230">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c3c36-231">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3c36-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c3c36-232">In deze sectie maakt inschakelen u Britta Simon gebruiken Azure eenmalige aanmelding toegang verleent tot Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="c3c36-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Online.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="c3c36-234">**Britta Simon om aan te wijzen Tableau Online, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="c3c36-234">**To assign Britta Simon to Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="c3c36-235">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c3c36-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="c3c36-237">Selecteer in de lijst met toepassingen **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="c3c36-237">In the applications list, select **Tableau Online**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="c3c36-239">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c3c36-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="c3c36-241">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="c3c36-241">Click **Add** button.</span></span> <span data-ttu-id="c3c36-242">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c3c36-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="c3c36-244">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c3c36-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c3c36-245">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c3c36-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c3c36-246">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="c3c36-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c3c36-247">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="c3c36-247">Testing single sign-on</span></span>

<span data-ttu-id="c3c36-248">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="c3c36-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="c3c36-249">Als u op de tegel Tableau Online in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw Tableau Online-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c3c36-249">When you click the Tableau Online tile in the Access Panel, you should get automatically signed-on to your Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c3c36-250">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c3c36-250">Additional resources</span></span>

* [<span data-ttu-id="c3c36-251">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3c36-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c3c36-252">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c3c36-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

