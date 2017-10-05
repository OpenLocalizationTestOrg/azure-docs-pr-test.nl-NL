---
title: 'Zelfstudie: Azure Active Directory-integratie met kudo | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en kudo.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 353798fcfd4ad7ce017fc2fddf4110715db3ace2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="66828-103">Zelfstudie: Azure Active Directory-integratie met kudo</span><span class="sxs-lookup"><span data-stu-id="66828-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="66828-104">In deze zelfstudie leert u hoe kudo integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="66828-104">In this tutorial, you learn how to integrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="66828-105">Kudo integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="66828-105">Integrating Kudos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="66828-106">U kunt beheren in Azure AD die toegang tot kudo heeft</span><span class="sxs-lookup"><span data-stu-id="66828-106">You can control in Azure AD who has access to Kudos</span></span>
- <span data-ttu-id="66828-107">U kunt uw gebruikers automatisch ophalen aangemeld bij kudo (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="66828-107">You can enable your users to automatically get signed-on to Kudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="66828-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="66828-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="66828-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="66828-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66828-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="66828-110">Prerequisites</span></span>

<span data-ttu-id="66828-111">Voor het configureren van Azure AD-integratie met kudo, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="66828-111">To configure Azure AD integration with Kudos, you need the following items:</span></span>

- <span data-ttu-id="66828-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="66828-112">An Azure AD subscription</span></span>
- <span data-ttu-id="66828-113">Een kudo eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="66828-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="66828-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="66828-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="66828-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="66828-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="66828-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="66828-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="66828-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="66828-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="66828-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="66828-118">Scenario description</span></span>
<span data-ttu-id="66828-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="66828-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="66828-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="66828-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="66828-121">Kudo uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="66828-121">Adding Kudos from the gallery</span></span>
2. <span data-ttu-id="66828-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="66828-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-the-gallery"></a><span data-ttu-id="66828-123">Kudo uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="66828-123">Adding Kudos from the gallery</span></span>
<span data-ttu-id="66828-124">Voor het configureren van de integratie van kudo in Azure AD, moet u kudo uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="66828-124">To configure the integration of Kudos into Azure AD, you need to add Kudos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="66828-125">**Als u wilt toevoegen kudo uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="66828-125">**To add Kudos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="66828-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="66828-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="66828-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="66828-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="66828-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="66828-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="66828-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="66828-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="66828-133">Typ in het zoekvak **kudo**.</span><span class="sxs-lookup"><span data-stu-id="66828-133">In the search box, type **Kudos**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. <span data-ttu-id="66828-135">Selecteer in het deelvenster resultaten **kudo**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="66828-135">In the results panel, select **Kudos**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="66828-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="66828-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="66828-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met kudo op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="66828-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="66828-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in kudo is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66828-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kudos is to a user in Azure AD.</span></span> <span data-ttu-id="66828-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in kudo tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="66828-140">In other words, a link relationship between an Azure AD user and the related user in Kudos needs to be established.</span></span>

<span data-ttu-id="66828-141">Wijs in kudo, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="66828-141">In Kudos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="66828-142">Om te configureren en testen van Azure AD eenmalige aanmelding met kudo, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="66828-142">To configure and test Azure AD single sign-on with Kudos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="66828-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="66828-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="66828-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="66828-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="66828-145">**[Maken van een testgebruiker kudo](#creating-a-kudos-test-user)**  - kudo die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="66828-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - to have a counterpart of Britta Simon in Kudos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="66828-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="66828-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="66828-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="66828-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="66828-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="66828-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="66828-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing kudo configureren.</span><span class="sxs-lookup"><span data-stu-id="66828-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="66828-150">**Voor het configureren van Azure AD eenmalige aanmelding met kudo, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="66828-150">**To configure Azure AD single sign-on with Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="66828-151">In de Azure-portal op de **kudo** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="66828-151">In the Azure portal, on the **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="66828-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="66828-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. <span data-ttu-id="66828-155">Op de **kudo domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="66828-155">On the **Kudos Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="66828-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company>.kudosnow.com`</span><span class="sxs-lookup"><span data-stu-id="66828-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="66828-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="66828-158">This value is not real.</span></span> <span data-ttu-id="66828-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="66828-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="66828-160">Neem contact op met [kudo Client ondersteuningsteam](http://success.kudosnow.com/home) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="66828-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) to get this value.</span></span> 
 
4. <span data-ttu-id="66828-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="66828-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. <span data-ttu-id="66828-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="66828-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="66828-165">Op de **kudo configuratie** sectie, klikt u op **kudo configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="66828-165">On the **Kudos Configuration** section, click **Configure Kudos** to open **Configure sign-on** window.</span></span> <span data-ttu-id="66828-166">Kopieer de **Sign-Out URL's en SAML Single Sign-On Service** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="66828-166">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. <span data-ttu-id="66828-168">In een ander browservenster, meld u bij uw bedrijf kudo site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="66828-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

8. <span data-ttu-id="66828-169">Klik in het menu bovenaan op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="66828-169">In the menu on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="66828-170">![Instellingen](./media/active-directory-saas-kudos-tutorial/ic787806.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="66828-170">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

9. <span data-ttu-id="66828-171">Klik op **integraties \> SSO**.</span><span class="sxs-lookup"><span data-stu-id="66828-171">Click **Integrations \> SSO**.</span></span>

10. <span data-ttu-id="66828-172">In de **SSO** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="66828-172">In the **SSO** section, perform the following steps:</span></span>
   
    <span data-ttu-id="66828-173">![EENMALIGE AANMELDING](./media/active-directory-saas-kudos-tutorial/ic787807.png "EENMALIGE AANMELDING")</span><span class="sxs-lookup"><span data-stu-id="66828-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="66828-174">a.</span><span class="sxs-lookup"><span data-stu-id="66828-174">a.</span></span> <span data-ttu-id="66828-175">In **aanmelden URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="66828-175">In **Sign on URL** textbox, paste the value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="66828-176">b.</span><span class="sxs-lookup"><span data-stu-id="66828-176">b.</span></span> <span data-ttu-id="66828-177">Open uw base-64 gecodeerde certificaat in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **X.509-certificaat** tekstvak</span><span class="sxs-lookup"><span data-stu-id="66828-177">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="66828-178">c.</span><span class="sxs-lookup"><span data-stu-id="66828-178">c.</span></span> <span data-ttu-id="66828-179">In **afmelding naar URL**, plak de waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="66828-179">In **Logout To URL**, paste the value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="66828-180">d.</span><span class="sxs-lookup"><span data-stu-id="66828-180">d.</span></span> <span data-ttu-id="66828-181">In de **de kudo URL** textbox, typ de naam van uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="66828-181">In the **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="66828-182">e.</span><span class="sxs-lookup"><span data-stu-id="66828-182">e.</span></span> <span data-ttu-id="66828-183">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="66828-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="66828-184">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="66828-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="66828-185">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="66828-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="66828-186">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="66828-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="66828-187">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="66828-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="66828-188">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="66828-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="66828-190">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="66828-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="66828-191">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="66828-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="66828-193">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="66828-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="66828-195">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="66828-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="66828-197">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="66828-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="66828-199">a.</span><span class="sxs-lookup"><span data-stu-id="66828-199">a.</span></span> <span data-ttu-id="66828-200">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="66828-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="66828-201">b.</span><span class="sxs-lookup"><span data-stu-id="66828-201">b.</span></span> <span data-ttu-id="66828-202">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="66828-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="66828-203">c.</span><span class="sxs-lookup"><span data-stu-id="66828-203">c.</span></span> <span data-ttu-id="66828-204">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="66828-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="66828-205">d.</span><span class="sxs-lookup"><span data-stu-id="66828-205">d.</span></span> <span data-ttu-id="66828-206">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="66828-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="66828-207">Een testgebruiker kudo maken</span><span class="sxs-lookup"><span data-stu-id="66828-207">Creating a Kudos test user</span></span>

<span data-ttu-id="66828-208">Om in te schakelen gebruikers van Azure AD aan te melden bij kudo, moeten ze worden ingericht in kudo.</span><span class="sxs-lookup"><span data-stu-id="66828-208">In order to enable Azure AD users to log into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="66828-209">In het geval van kudo is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="66828-209">In the case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="66828-210">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="66828-210">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="66828-211">Meld u aan bij uw **kudo** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="66828-211">Log in to your **Kudos** company site as administrator.</span></span>

2. <span data-ttu-id="66828-212">Klik in het menu bovenaan op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="66828-212">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="66828-213">![Instellingen](./media/active-directory-saas-kudos-tutorial/ic787806.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="66828-213">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

3. <span data-ttu-id="66828-214">Klik op **Gebruikerbeheerder**.</span><span class="sxs-lookup"><span data-stu-id="66828-214">Click **User Admin**.</span></span>

4. <span data-ttu-id="66828-215">Klik op de **gebruikers** tabblad en klik vervolgens op **toevoegen van een gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="66828-215">Click the **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="66828-216">![Gebruikerbeheerder](./media/active-directory-saas-kudos-tutorial/ic787809.png "Gebruikerbeheerder")</span><span class="sxs-lookup"><span data-stu-id="66828-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span></span>

5. <span data-ttu-id="66828-217">In de **toevoegen van een gebruiker** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="66828-217">In the **Add a User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="66828-218">![Een gebruiker toevoegen](./media/active-directory-saas-kudos-tutorial/ic787810.png "een gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="66828-218">![Add a User](./media/active-directory-saas-kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="66828-219">a.</span><span class="sxs-lookup"><span data-stu-id="66828-219">a.</span></span> <span data-ttu-id="66828-220">Typ de **voornaam**, **achternaam**, **e** en andere details van een geldig Azure Active Directory-account dat u inrichten in de bijbehorende tekstvakken wilt.</span><span class="sxs-lookup"><span data-stu-id="66828-220">Type the **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="66828-221">b.</span><span class="sxs-lookup"><span data-stu-id="66828-221">b.</span></span> <span data-ttu-id="66828-222">Klik op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="66828-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="66828-223">U kunt andere kudo gebruiker account hulpmiddelen voor het maken of API's die is geleverd door kudo aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="66828-223">You can use any other Kudos user account creation tools or APIs provided by Kudos to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="66828-224">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="66828-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="66828-225">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan kudo.</span><span class="sxs-lookup"><span data-stu-id="66828-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kudos.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="66828-227">**Britta Simon om aan te wijzen kudo, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="66828-227">**To assign Britta Simon to Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="66828-228">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="66828-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="66828-230">Selecteer in de lijst met toepassingen **kudo**.</span><span class="sxs-lookup"><span data-stu-id="66828-230">In the applications list, select **Kudos**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. <span data-ttu-id="66828-232">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="66828-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="66828-234">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="66828-234">Click **Add** button.</span></span> <span data-ttu-id="66828-235">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="66828-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="66828-237">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="66828-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="66828-238">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="66828-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="66828-239">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="66828-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="66828-240">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="66828-240">Testing single sign-on</span></span>

<span data-ttu-id="66828-241">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="66828-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="66828-242">Als u op de tegel kudo in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing kudo.</span><span class="sxs-lookup"><span data-stu-id="66828-242">When you click the Kudos tile in the Access Panel, you should get automatically signed-on to your Kudos application.</span></span> <span data-ttu-id="66828-243">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="66828-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="66828-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="66828-244">Additional resources</span></span>

* [<span data-ttu-id="66828-245">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66828-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="66828-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="66828-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png

