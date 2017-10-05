---
title: 'Zelfstudie: Azure Active Directory-integratie met Printix | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Printix.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 97dbb3fa0531f2f679badb6bb9752f2e42fc9cb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="494db-103">Zelfstudie: Azure Active Directory-integratie met Printix</span><span class="sxs-lookup"><span data-stu-id="494db-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="494db-104">In deze zelfstudie leert u hoe Printix integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="494db-104">In this tutorial, you learn how to integrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="494db-105">Printix integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="494db-105">Integrating Printix with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="494db-106">U kunt beheren in Azure AD die toegang tot Printix heeft</span><span class="sxs-lookup"><span data-stu-id="494db-106">You can control in Azure AD who has access to Printix</span></span>
- <span data-ttu-id="494db-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Printix (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="494db-107">You can enable your users to automatically get signed-on to Printix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="494db-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="494db-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="494db-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="494db-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="494db-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="494db-110">Prerequisites</span></span>

<span data-ttu-id="494db-111">Voor het configureren van Azure AD-integratie met Printix, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="494db-111">To configure Azure AD integration with Printix, you need the following items:</span></span>

- <span data-ttu-id="494db-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="494db-112">An Azure AD subscription</span></span>
- <span data-ttu-id="494db-113">Een Printix eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="494db-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="494db-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="494db-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="494db-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="494db-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="494db-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="494db-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="494db-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="494db-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="494db-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="494db-118">Scenario description</span></span>
<span data-ttu-id="494db-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="494db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="494db-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="494db-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="494db-121">Printix uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="494db-121">Adding Printix from the gallery</span></span>
2. <span data-ttu-id="494db-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="494db-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-the-gallery"></a><span data-ttu-id="494db-123">Printix uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="494db-123">Adding Printix from the gallery</span></span>
<span data-ttu-id="494db-124">Voor het configureren van de integratie van Printix in Azure AD, moet u Printix uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="494db-124">To configure the integration of Printix into Azure AD, you need to add Printix from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="494db-125">**Als u wilt toevoegen Printix uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="494db-125">**To add Printix from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="494db-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="494db-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="494db-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="494db-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="494db-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="494db-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="494db-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="494db-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="494db-133">Typ in het zoekvak **Printix**.</span><span class="sxs-lookup"><span data-stu-id="494db-133">In the search box, type **Printix**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="494db-135">Selecteer in het deelvenster resultaten **Printix**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="494db-135">In the results panel, select **Printix**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="494db-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="494db-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="494db-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Printix op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="494db-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="494db-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Printix is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="494db-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Printix is to a user in Azure AD.</span></span> <span data-ttu-id="494db-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Printix tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="494db-140">In other words, a link relationship between an Azure AD user and the related user in Printix needs to be established.</span></span>

<span data-ttu-id="494db-141">Wijs in Printix, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="494db-141">In Printix, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="494db-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Printix, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="494db-142">To configure and test Azure AD single sign-on with Printix, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="494db-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="494db-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="494db-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="494db-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="494db-145">**[Maken van een testgebruiker Printix](#creating-a-printix-test-user)**  - Printix die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="494db-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - to have a counterpart of Britta Simon in Printix that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="494db-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="494db-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="494db-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="494db-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="494db-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="494db-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="494db-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Printix configureren.</span><span class="sxs-lookup"><span data-stu-id="494db-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="494db-150">**Voor het configureren van Azure AD eenmalige aanmelding met Printix, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="494db-150">**To configure Azure AD single sign-on with Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="494db-151">In de Azure-portal op de **Printix** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="494db-151">In the Azure portal, on the **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="494db-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="494db-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="494db-155">Op de **Printix domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="494db-155">On the **Printix Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="494db-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="494db-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="494db-158">De waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="494db-158">The value is not real.</span></span> <span data-ttu-id="494db-159">Werk de waarde met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="494db-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="494db-160">Neem contact op met [Printix Client ondersteuningsteam](mailto:support@printix.net) de waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="494db-160">Contact [Printix Client support team](mailto:support@printix.net) to get the value.</span></span> 
 
4. <span data-ttu-id="494db-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="494db-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="494db-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="494db-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="494db-165">Eenmalige aanmelding voor uw tenant Printix als beheerder.</span><span class="sxs-lookup"><span data-stu-id="494db-165">Sign-on to your Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="494db-166">In het menu bovenaan, klik op het pictogram in de rechterbovenhoek en selecteer '**verificatie**'.</span><span class="sxs-lookup"><span data-stu-id="494db-166">In the menu on the top, click the icon at the upper right corner and select "**Authentication**".</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="494db-168">Op de **Setup** tabblad **inschakelen Azure/Office 365-verificatie**</span><span class="sxs-lookup"><span data-stu-id="494db-168">On the **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="494db-170">Op de **Azure** tabblad, invoer-URL voor federatieve metagegevens aan het textbox van '**document met federatieve metagegevens**'.</span><span class="sxs-lookup"><span data-stu-id="494db-170">On the **Azure** tab, input federation metadata URL to the textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="494db-171">Koppel de metagegevens-XML-bestand dat u hebt gedownload van Azure AD [Printix ondersteuningsteam](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="494db-171">Attach the metadata xml file which you downloaded from Azure AD to [Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="494db-172">Vervolgens het xml-bestand uploaden en een federation-metagegevens-URL opgeven.</span><span class="sxs-lookup"><span data-stu-id="494db-172">Then they upload the xml file and provide a federation metadata URL.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="494db-174">Klik op de '**testen**'knop en klik op'**OK**' knop als de test geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="494db-174">Click the "**Test**" button and click "**OK**" button if the test was successful.</span></span>
   
     <span data-ttu-id="494db-175">Azure active directory-pagina wordt weergegeven wanneer u op de **testen** knop.</span><span class="sxs-lookup"><span data-stu-id="494db-175">Azure active directory page will show after clicking the **test** button.</span></span> <span data-ttu-id="494db-176">"De test is geslaagd" betekent hier na het invoeren van de referenties van uw Azure testaccount die er verschijnt een bericht met 'instellingen getest OK'. Klik vervolgens op de **OK** knop.</span><span class="sxs-lookup"><span data-stu-id="494db-176">"The test was successful" here means after entering the credentials of your Azure test account it will pop up a message "Settings tested OK".Then click the **OK** button.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="494db-178">Klik op de **opslaan** op knop '**verificatie**' pagina.</span><span class="sxs-lookup"><span data-stu-id="494db-178">Click the **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="494db-179">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="494db-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="494db-180">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="494db-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="494db-181">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="494db-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="494db-182">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="494db-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="494db-183">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="494db-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="494db-185">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="494db-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="494db-186">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="494db-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="494db-188">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="494db-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="494db-190">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="494db-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="494db-192">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="494db-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="494db-194">a.</span><span class="sxs-lookup"><span data-stu-id="494db-194">a.</span></span> <span data-ttu-id="494db-195">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="494db-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="494db-196">b.</span><span class="sxs-lookup"><span data-stu-id="494db-196">b.</span></span> <span data-ttu-id="494db-197">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="494db-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="494db-198">c.</span><span class="sxs-lookup"><span data-stu-id="494db-198">c.</span></span> <span data-ttu-id="494db-199">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="494db-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="494db-200">d.</span><span class="sxs-lookup"><span data-stu-id="494db-200">d.</span></span> <span data-ttu-id="494db-201">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="494db-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="494db-202">Een testgebruiker Printix maken</span><span class="sxs-lookup"><span data-stu-id="494db-202">Creating a Printix test user</span></span>

<span data-ttu-id="494db-203">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Printix genoemd.</span><span class="sxs-lookup"><span data-stu-id="494db-203">The objective of this section is to create a user called Britta Simon in Printix.</span></span> <span data-ttu-id="494db-204">Printix ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="494db-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="494db-205">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="494db-205">There is no action item for you in this section.</span></span> <span data-ttu-id="494db-206">Een nieuwe gebruiker is gemaakt tijdens een poging tot toegang tot Printix als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="494db-206">A new user is created during an attempt to access Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="494db-207">Als u een gebruiker handmatig maken wilt, moet u contact op met de [Printix ondersteuningsteam](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="494db-207">If you need to create a user manually, you need to contact the [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="494db-208">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="494db-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="494db-209">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Printix.</span><span class="sxs-lookup"><span data-stu-id="494db-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Printix.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="494db-211">**Britta Simon om aan te wijzen Printix, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="494db-211">**To assign Britta Simon to Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="494db-212">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="494db-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="494db-214">Selecteer in de lijst met toepassingen **Printix**.</span><span class="sxs-lookup"><span data-stu-id="494db-214">In the applications list, select **Printix**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="494db-216">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="494db-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="494db-218">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="494db-218">Click **Add** button.</span></span> <span data-ttu-id="494db-219">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="494db-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="494db-221">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="494db-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="494db-222">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="494db-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="494db-223">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="494db-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="494db-224">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="494db-224">Testing single sign-on</span></span>

<span data-ttu-id="494db-225">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="494db-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="494db-226">Als u op de tegel Printix in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Printix.</span><span class="sxs-lookup"><span data-stu-id="494db-226">When you click the Printix tile in the Access Panel, you should get automatically signed-on to your Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="494db-227">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="494db-227">Additional resources</span></span>

* [<span data-ttu-id="494db-228">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="494db-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="494db-229">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="494db-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

