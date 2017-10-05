---
title: 'Zelfstudie: Azure Active Directory-integratie met houden bestanden | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en houden bestanden.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: e02150cb27768d7b403bdca191bc1f189821def4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="bbd44-103">Zelfstudie: Azure Active Directory-integratie met houden bestanden</span><span class="sxs-lookup"><span data-stu-id="bbd44-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>

<span data-ttu-id="bbd44-104">In deze zelfstudie leert u hoe houden bestanden integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bbd44-104">In this tutorial, you learn how to integrate Flatter Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bbd44-105">Houden bestanden integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="bbd44-105">Integrating Flatter Files with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bbd44-106">U kunt beheren in Azure AD die toegang tot bestanden houden heeft</span><span class="sxs-lookup"><span data-stu-id="bbd44-106">You can control in Azure AD who has access to Flatter Files</span></span>
- <span data-ttu-id="bbd44-107">U kunt uw gebruikers automatisch ophalen aangemeld bij houden bestanden (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="bbd44-107">You can enable your users to automatically get signed-on to Flatter Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bbd44-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="bbd44-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bbd44-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bbd44-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbd44-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bbd44-110">Prerequisites</span></span>

<span data-ttu-id="bbd44-111">Voor het configureren van Azure AD-integratie met houden bestanden, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="bbd44-111">To configure Azure AD integration with Flatter Files, you need the following items:</span></span>

- <span data-ttu-id="bbd44-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="bbd44-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bbd44-113">Een houden bestanden eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="bbd44-113">A Flatter Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bbd44-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="bbd44-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bbd44-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="bbd44-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bbd44-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="bbd44-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bbd44-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bbd44-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bbd44-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="bbd44-118">Scenario description</span></span>
<span data-ttu-id="bbd44-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="bbd44-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bbd44-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="bbd44-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bbd44-121">Houden bestanden uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="bbd44-121">Adding Flatter Files from the gallery</span></span>
2. <span data-ttu-id="bbd44-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bbd44-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flatter-files-from-the-gallery"></a><span data-ttu-id="bbd44-123">Houden bestanden uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="bbd44-123">Adding Flatter Files from the gallery</span></span>
<span data-ttu-id="bbd44-124">Voor het configureren van de integratie van houden bestanden in Azure AD, moet u houden bestanden uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="bbd44-124">To configure the integration of Flatter Files into Azure AD, you need to add Flatter Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bbd44-125">**Als u wilt houden bestanden uit de galerie toevoegen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bbd44-125">**To add Flatter Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bbd44-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bbd44-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bbd44-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bbd44-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="bbd44-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bbd44-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="bbd44-133">Typ in het zoekvak **houden bestanden**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-133">In the search box, type **Flatter Files**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. <span data-ttu-id="bbd44-135">Selecteer in het deelvenster resultaten **houden bestanden**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="bbd44-135">In the results panel, select **Flatter Files**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bbd44-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bbd44-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bbd44-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met houden bestanden op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="bbd44-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bbd44-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in houden bestanden is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbd44-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Flatter Files is to a user in Azure AD.</span></span> <span data-ttu-id="bbd44-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in houden bestanden worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bbd44-140">In other words, a link relationship between an Azure AD user and the related user in Flatter Files needs to be established.</span></span>

<span data-ttu-id="bbd44-141">In houden bestanden, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="bbd44-141">In Flatter Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bbd44-142">Om te configureren en testen van Azure AD eenmalige aanmelding met houden bestanden, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="bbd44-142">To configure and test Azure AD single sign-on with Flatter Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bbd44-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bbd44-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bbd44-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbd44-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bbd44-145">**[Maken van een testgebruiker houden bestanden](#creating-a-flatter-files-test-user)**  - houden bestanden dat is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="bbd44-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - to have a counterpart of Britta Simon in Flatter Files that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bbd44-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bbd44-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bbd44-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="bbd44-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bbd44-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="bbd44-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bbd44-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing houden bestanden.</span><span class="sxs-lookup"><span data-stu-id="bbd44-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Flatter Files application.</span></span>

<span data-ttu-id="bbd44-150">**Voor het configureren van Azure AD eenmalige aanmelding met houden bestanden, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bbd44-150">**To configure Azure AD single sign-on with Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="bbd44-151">In de Azure-portal op de **houden bestanden** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-151">In the Azure portal, on the **Flatter Files** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="bbd44-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bbd44-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. <span data-ttu-id="bbd44-155">Op de **houden bestanden domein en de URL's** sectie, de gebruiker heeft geen alle stappen uitvoeren als de app al vooraf is geïntegreerd met Azure.</span><span class="sxs-lookup"><span data-stu-id="bbd44-155">On the **Flatter Files Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. <span data-ttu-id="bbd44-157">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="bbd44-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. <span data-ttu-id="bbd44-159">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="bbd44-159">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bbd44-161">Op de **houden bestanden configuratie** sectie, klikt u op **houden bestanden configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="bbd44-161">On the **Flatter Files Configuration** section, click **Configure Flatter Files** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bbd44-162">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="bbd44-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. <span data-ttu-id="bbd44-164">Eenmalige aanmelding voor uw toepassing houden bestanden als beheerder.</span><span class="sxs-lookup"><span data-stu-id="bbd44-164">Sign-on to your Flatter Files application as an administrator.</span></span>

8. <span data-ttu-id="bbd44-165">Klik op **DASHBOARD**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-165">Click **DASHBOARD**.</span></span> 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. <span data-ttu-id="bbd44-167">Klik op **instellingen**, en voer de volgende stappen uit op de **bedrijf** tabblad:</span><span class="sxs-lookup"><span data-stu-id="bbd44-167">Click **Settings**, and then perform the following steps on the **Company** tab:</span></span> 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    <span data-ttu-id="bbd44-169">a.</span><span class="sxs-lookup"><span data-stu-id="bbd44-169">a.</span></span> <span data-ttu-id="bbd44-170">Selecteer **SAML 2.0 gebruiken voor verificatie**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-170">Select **Use SAML 2.0 for Authentication**.</span></span>
    
    <span data-ttu-id="bbd44-171">b.</span><span class="sxs-lookup"><span data-stu-id="bbd44-171">b.</span></span> <span data-ttu-id="bbd44-172">Klik op **SAML configureren**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-172">Click **Configure SAML**.</span></span>

8. <span data-ttu-id="bbd44-173">Op de **SAML-configuratie** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bbd44-173">On the **SAML Configuration** dialog, perform the following steps:</span></span> 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    <span data-ttu-id="bbd44-175">a.</span><span class="sxs-lookup"><span data-stu-id="bbd44-175">a.</span></span> <span data-ttu-id="bbd44-176">In de **domein** textbox het geregistreerde domein opgeven.</span><span class="sxs-lookup"><span data-stu-id="bbd44-176">In the **Domain** textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="bbd44-177">Als u een geregistreerde domeinnaam nog contact op met hebt uw houden bestanden ondersteuningsteam via [ support@flatterfiles.com ](mailto:support@flatterfiles.com).</span><span class="sxs-lookup"><span data-stu-id="bbd44-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span> 
    
    <span data-ttu-id="bbd44-178">b.</span><span class="sxs-lookup"><span data-stu-id="bbd44-178">b.</span></span> <span data-ttu-id="bbd44-179">In **identiteit Provider URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vormen van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="bbd44-179">In **Identity Provider URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span></span>
   
    <span data-ttu-id="bbd44-180">c.</span><span class="sxs-lookup"><span data-stu-id="bbd44-180">c.</span></span>  <span data-ttu-id="bbd44-181">Open uw base-64 gecodeerde certificaat in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **Provider identiteitscertificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="bbd44-181">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="bbd44-182">d.</span><span class="sxs-lookup"><span data-stu-id="bbd44-182">d.</span></span> <span data-ttu-id="bbd44-183">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-183">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="bbd44-184">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="bbd44-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bbd44-185">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="bbd44-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bbd44-186">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bbd44-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bbd44-187">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="bbd44-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="bbd44-188">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="bbd44-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="bbd44-190">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bbd44-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bbd44-191">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bbd44-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bbd44-193">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bbd44-195">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bbd44-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bbd44-197">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bbd44-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bbd44-199">a.</span><span class="sxs-lookup"><span data-stu-id="bbd44-199">a.</span></span> <span data-ttu-id="bbd44-200">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bbd44-201">b.</span><span class="sxs-lookup"><span data-stu-id="bbd44-201">b.</span></span> <span data-ttu-id="bbd44-202">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bbd44-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bbd44-203">c.</span><span class="sxs-lookup"><span data-stu-id="bbd44-203">c.</span></span> <span data-ttu-id="bbd44-204">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bbd44-205">d.</span><span class="sxs-lookup"><span data-stu-id="bbd44-205">d.</span></span> <span data-ttu-id="bbd44-206">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-206">Click **Create**.</span></span>
 
### <a name="creating-a-flatter-files-test-user"></a><span data-ttu-id="bbd44-207">Een testgebruiker houden bestanden maken</span><span class="sxs-lookup"><span data-stu-id="bbd44-207">Creating a Flatter Files test user</span></span>

<span data-ttu-id="bbd44-208">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in houden bestanden.</span><span class="sxs-lookup"><span data-stu-id="bbd44-208">The objective of this section is to create a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="bbd44-209">**Voor het maken van een gebruiker met de naam van Britta Simon in houden bestanden, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bbd44-209">**To create a user called Britta Simon in Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="bbd44-210">Meld u aan bij uw **houden bestanden** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="bbd44-210">Sign on to your **Flatter Files** company site as administrator.</span></span>

2. <span data-ttu-id="bbd44-211">Klik in het navigatievenster aan de linkerkant op **instellingen**, en klik vervolgens op de **gebruikers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="bbd44-211">In the navigation pane on the left, click **Settings**, and then click the **Users** tab.</span></span>
   
    ![Een gebruiker met houden bestanden maken](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. <span data-ttu-id="bbd44-213">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-213">Click **Add User**.</span></span> 

4. <span data-ttu-id="bbd44-214">Op de **gebruiker toevoegen** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bbd44-214">On the **Add User** dialog, perform the following steps:</span></span>
   
    ![Een gebruiker met houden bestanden maken](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    <span data-ttu-id="bbd44-216">a.</span><span class="sxs-lookup"><span data-stu-id="bbd44-216">a.</span></span> <span data-ttu-id="bbd44-217">In de **voornaam** textbox type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-217">In the **First Name** textbox, type **Britta**.</span></span>
   
    <span data-ttu-id="bbd44-218">b.</span><span class="sxs-lookup"><span data-stu-id="bbd44-218">b.</span></span> <span data-ttu-id="bbd44-219">In de **achternaam** textbox type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-219">In the **Last Name** textbox, type **Simon**.</span></span> 
   
    <span data-ttu-id="bbd44-220">c.</span><span class="sxs-lookup"><span data-stu-id="bbd44-220">c.</span></span> <span data-ttu-id="bbd44-221">In de **e-mailadres** textbox Britta van e-mailadres typt in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="bbd44-221">In the **Email Address** textbox, type Britta's email address in the Azure portal.</span></span>
   
    <span data-ttu-id="bbd44-222">d.</span><span class="sxs-lookup"><span data-stu-id="bbd44-222">d.</span></span> <span data-ttu-id="bbd44-223">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-223">Click **Submit**.</span></span>   


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bbd44-224">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd44-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bbd44-225">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot bestanden houden.</span><span class="sxs-lookup"><span data-stu-id="bbd44-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Flatter Files.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="bbd44-227">**Britta Simon om aan te wijzen houden bestanden, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bbd44-227">**To assign Britta Simon to Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="bbd44-228">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="bbd44-230">Selecteer in de lijst met toepassingen **houden bestanden**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-230">In the applications list, select **Flatter Files**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. <span data-ttu-id="bbd44-232">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="bbd44-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="bbd44-234">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="bbd44-234">Click **Add** button.</span></span> <span data-ttu-id="bbd44-235">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bbd44-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="bbd44-237">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="bbd44-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bbd44-238">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bbd44-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bbd44-239">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bbd44-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bbd44-240">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bbd44-240">Testing single sign-on</span></span>

<span data-ttu-id="bbd44-241">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="bbd44-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bbd44-242">Als u op de tegel houden bestanden in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing houden bestanden.</span><span class="sxs-lookup"><span data-stu-id="bbd44-242">When you click the Flatter Files tile in the Access Panel, you should get automatically signed-on to your Flatter Files application.</span></span>
<span data-ttu-id="bbd44-243">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bbd44-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bbd44-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="bbd44-244">Additional resources</span></span>

* [<span data-ttu-id="bbd44-245">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbd44-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bbd44-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bbd44-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png

