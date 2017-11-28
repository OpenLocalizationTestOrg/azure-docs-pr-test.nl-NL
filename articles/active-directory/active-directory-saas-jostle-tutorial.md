---
title: 'Zelfstudie: Azure Active Directory-integratie met Jostle | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Jostle.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ca4ca1f-8f68-4225-81a6-1666b486d6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 0ca8aca1446a38643ce9f6751b6fe9cae1eaa5b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jostle"></a><span data-ttu-id="d6eeb-103">Zelfstudie: Azure Active Directory-integratie met Jostle</span><span class="sxs-lookup"><span data-stu-id="d6eeb-103">Tutorial: Azure Active Directory integration with Jostle</span></span>

<span data-ttu-id="d6eeb-104">In deze zelfstudie leert u hoe Jostle integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d6eeb-104">In this tutorial, you learn how to integrate Jostle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d6eeb-105">Jostle integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d6eeb-105">Integrating Jostle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d6eeb-106">U kunt beheren in Azure AD die toegang tot Jostle heeft</span><span class="sxs-lookup"><span data-stu-id="d6eeb-106">You can control in Azure AD who has access to Jostle</span></span>
- <span data-ttu-id="d6eeb-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Jostle (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="d6eeb-107">You can enable your users to automatically get signed-on to Jostle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d6eeb-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="d6eeb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d6eeb-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d6eeb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6eeb-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d6eeb-110">Prerequisites</span></span>

<span data-ttu-id="d6eeb-111">Voor het configureren van Azure AD-integratie met Jostle, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="d6eeb-111">To configure Azure AD integration with Jostle, you need the following items:</span></span>

- <span data-ttu-id="d6eeb-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="d6eeb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d6eeb-113">Een Jostle eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="d6eeb-113">A Jostle single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d6eeb-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d6eeb-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="d6eeb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d6eeb-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d6eeb-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6eeb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d6eeb-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d6eeb-118">Scenario description</span></span>
<span data-ttu-id="d6eeb-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d6eeb-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d6eeb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d6eeb-121">Jostle uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d6eeb-121">Adding Jostle from the gallery</span></span>
2. <span data-ttu-id="d6eeb-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d6eeb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jostle-from-the-gallery"></a><span data-ttu-id="d6eeb-123">Jostle uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d6eeb-123">Adding Jostle from the gallery</span></span>
<span data-ttu-id="d6eeb-124">Voor het configureren van de integratie van Jostle in Azure AD, moet u Jostle uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-124">To configure the integration of Jostle into Azure AD, you need to add Jostle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d6eeb-125">**Als u wilt toevoegen Jostle uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d6eeb-125">**To add Jostle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d6eeb-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d6eeb-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d6eeb-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d6eeb-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d6eeb-133">Typ in het zoekvak **Jostle**.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-133">In the search box, type **Jostle**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_search.png)

5. <span data-ttu-id="d6eeb-135">Selecteer in het deelvenster resultaten **Jostle**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-135">In the results panel, select **Jostle**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d6eeb-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d6eeb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d6eeb-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Jostle op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="d6eeb-138">In this section, you configure and test Azure AD single sign-on with Jostle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d6eeb-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Jostle is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jostle is to a user in Azure AD.</span></span> <span data-ttu-id="d6eeb-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Jostle tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-140">In other words, a link relationship between an Azure AD user and the related user in Jostle needs to be established.</span></span>

<span data-ttu-id="d6eeb-141">Wijs in Jostle, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-141">In Jostle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d6eeb-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Jostle, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="d6eeb-142">To configure and test Azure AD single sign-on with Jostle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d6eeb-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d6eeb-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d6eeb-145">**[Maken van een testgebruiker Jostle](#creating-a-jostle-test-user)**  - Jostle die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-145">**[Creating a Jostle test user](#creating-a-jostle-test-user)** - to have a counterpart of Britta Simon in Jostle that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d6eeb-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d6eeb-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d6eeb-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d6eeb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d6eeb-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Jostle configureren.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jostle application.</span></span>

<span data-ttu-id="d6eeb-150">**Voor het configureren van Azure AD eenmalige aanmelding met Jostle, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d6eeb-150">**To configure Azure AD single sign-on with Jostle, perform the following steps:**</span></span>

1. <span data-ttu-id="d6eeb-151">In de Azure-portal op de **Jostle** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-151">In the Azure portal, on the **Jostle** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d6eeb-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_samlbase.png)

3. <span data-ttu-id="d6eeb-155">Op de **Jostle domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d6eeb-155">On the **Jostle Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_url.png)

    <span data-ttu-id="d6eeb-157">a.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-157">a.</span></span> <span data-ttu-id="d6eeb-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<tanent name>.jostle.us/jostle-prod/`</span><span class="sxs-lookup"><span data-stu-id="d6eeb-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tanent name>.jostle.us/jostle-prod/`</span></span>

    <span data-ttu-id="d6eeb-159">b.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-159">b.</span></span> <span data-ttu-id="d6eeb-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<tanent name>.jostle.us`</span><span class="sxs-lookup"><span data-stu-id="d6eeb-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tanent name>.jostle.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d6eeb-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-161">These values are not real.</span></span> <span data-ttu-id="d6eeb-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d6eeb-163">Neem contact op met [Jostle ondersteuningsteam](mailto:support@jostle.me) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-163">Contact [Jostle support team](mailto:support@jostle.me) to get these values.</span></span> 
 


4. <span data-ttu-id="d6eeb-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_certificate.png) 

5. <span data-ttu-id="d6eeb-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jostle-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d6eeb-168">Voor het configureren van eenmalige aanmelding Jostle zijde, moet u de gedownloade XML met metagegevens verzenden naar [Jostle ondersteuningsteam](mailto:support@jostle.me).</span><span class="sxs-lookup"><span data-stu-id="d6eeb-168">To configure single sign-on on Jostle side, you need to send the downloaded metadata XML to [Jostle support team](mailto:support@jostle.me).</span></span> <span data-ttu-id="d6eeb-169">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span> 

> [!TIP]
> <span data-ttu-id="d6eeb-170">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="d6eeb-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d6eeb-171">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d6eeb-172">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d6eeb-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d6eeb-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d6eeb-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="d6eeb-174">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d6eeb-176">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d6eeb-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d6eeb-177">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jostle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d6eeb-179">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jostle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d6eeb-181">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jostle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d6eeb-183">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d6eeb-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jostle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d6eeb-185">a.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-185">a.</span></span> <span data-ttu-id="d6eeb-186">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d6eeb-187">b.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-187">b.</span></span> <span data-ttu-id="d6eeb-188">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d6eeb-189">c.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-189">c.</span></span> <span data-ttu-id="d6eeb-190">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d6eeb-191">d.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-191">d.</span></span> <span data-ttu-id="d6eeb-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-192">Click **Create**.</span></span>
 
### <a name="creating-a-jostle-test-user"></a><span data-ttu-id="d6eeb-193">Een testgebruiker Jostle maken</span><span class="sxs-lookup"><span data-stu-id="d6eeb-193">Creating a Jostle test user</span></span>

<span data-ttu-id="d6eeb-194">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Jostle maken.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-194">In this section, you create a user called Britta Simon in Jostle.</span></span> <span data-ttu-id="d6eeb-195">Als u niet hoe Britta Simon toevoegen in Jostle weet, neem contact op met [Jostle ondersteuningsteam](mailto:support@jostle.me) toe te voegen van de testgebruiker en eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-195">If you don't know how to add Britta Simon in Jostle, please contact with [Jostle support team](mailto:support@jostle.me) to add the test user and enable SSO.</span></span>

> [!NOTE]
> <span data-ttu-id="d6eeb-196">De houder van Azure Active Directory-account ontvangt een e-mailbericht en volgt een koppeling om hun account te bevestigen voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-196">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d6eeb-197">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6eeb-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d6eeb-198">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Jostle.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jostle.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d6eeb-200">**Britta Simon om aan te wijzen Jostle, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d6eeb-200">**To assign Britta Simon to Jostle, perform the following steps:**</span></span>

1. <span data-ttu-id="d6eeb-201">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d6eeb-203">Selecteer in de lijst met toepassingen **Jostle**.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-203">In the applications list, select **Jostle**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_app.png) 

3. <span data-ttu-id="d6eeb-205">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d6eeb-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-207">Click **Add** button.</span></span> <span data-ttu-id="d6eeb-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d6eeb-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d6eeb-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d6eeb-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d6eeb-213">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d6eeb-213">Testing single sign-on</span></span>

<span data-ttu-id="d6eeb-214">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d6eeb-215">Als u op de tegel Jostle in het deelvenster toegang, moet u de aanmeldingspagina van Jostle toepassing automatisch ophalen.</span><span class="sxs-lookup"><span data-stu-id="d6eeb-215">When you click the Jostle tile in the Access Panel, you should get automatically login page of Jostle application.</span></span>
<span data-ttu-id="d6eeb-216">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d6eeb-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d6eeb-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d6eeb-217">Additional resources</span></span>

* [<span data-ttu-id="d6eeb-218">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6eeb-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d6eeb-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d6eeb-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_203.png

