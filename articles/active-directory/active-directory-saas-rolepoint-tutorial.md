---
title: 'Zelfstudie: Azure Active Directory-integratie met RolePoint | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en RolePoint.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68d37f40-15da-45f5-a9e1-d53f78e786d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: jeedes
ms.openlocfilehash: fcde562484f4401e9f936614b9978f839f4aa290
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rolepoint"></a><span data-ttu-id="b825c-103">Zelfstudie: Azure Active Directory-integratie met RolePoint</span><span class="sxs-lookup"><span data-stu-id="b825c-103">Tutorial: Azure Active Directory integration with RolePoint</span></span>

<span data-ttu-id="b825c-104">In deze zelfstudie leert u hoe RolePoint integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b825c-104">In this tutorial, you learn how to integrate RolePoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b825c-105">RolePoint integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b825c-105">Integrating RolePoint with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b825c-106">U kunt beheren in Azure AD die toegang tot RolePoint heeft</span><span class="sxs-lookup"><span data-stu-id="b825c-106">You can control in Azure AD who has access to RolePoint</span></span>
- <span data-ttu-id="b825c-107">U kunt uw gebruikers automatisch ophalen aangemeld bij RolePoint (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="b825c-107">You can enable your users to automatically get signed-on to RolePoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b825c-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b825c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b825c-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b825c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b825c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b825c-110">Prerequisites</span></span>

<span data-ttu-id="b825c-111">Voor het configureren van Azure AD-integratie met RolePoint, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b825c-111">To configure Azure AD integration with RolePoint, you need the following items:</span></span>

- <span data-ttu-id="b825c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b825c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b825c-113">Een RolePoint eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b825c-113">A RolePoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b825c-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b825c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b825c-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b825c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b825c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b825c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b825c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b825c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b825c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b825c-118">Scenario description</span></span>
<span data-ttu-id="b825c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b825c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b825c-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b825c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b825c-121">RolePoint uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b825c-121">Adding RolePoint from the gallery</span></span>
2. <span data-ttu-id="b825c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b825c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rolepoint-from-the-gallery"></a><span data-ttu-id="b825c-123">RolePoint uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b825c-123">Adding RolePoint from the gallery</span></span>
<span data-ttu-id="b825c-124">Voor het configureren van de integratie van RolePoint in Azure AD, moet u RolePoint uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b825c-124">To configure the integration of RolePoint into Azure AD, you need to add RolePoint from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b825c-125">**Als u wilt toevoegen RolePoint uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b825c-125">**To add RolePoint from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b825c-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b825c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b825c-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b825c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b825c-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b825c-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="b825c-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b825c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="b825c-133">Typ in het zoekvak **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="b825c-133">In the search box, type **RolePoint**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_search.png)

5. <span data-ttu-id="b825c-135">Selecteer in het deelvenster resultaten **RolePoint**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b825c-135">In the results panel, select **RolePoint**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b825c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b825c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b825c-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met RolePoint op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="b825c-138">In this section, you configure and test Azure AD single sign-on with RolePoint based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b825c-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in RolePoint is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b825c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RolePoint is to a user in Azure AD.</span></span> <span data-ttu-id="b825c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in RolePoint tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="b825c-140">In other words, a link relationship between an Azure AD user and the related user in RolePoint needs to be established.</span></span>

<span data-ttu-id="b825c-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in RolePoint.</span><span class="sxs-lookup"><span data-stu-id="b825c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in RolePoint.</span></span>

<span data-ttu-id="b825c-142">Om te configureren en testen van Azure AD eenmalige aanmelding met RolePoint, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="b825c-142">To configure and test Azure AD single sign-on with RolePoint, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b825c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b825c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b825c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b825c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b825c-145">**[Maken van een testgebruiker RolePoint](#creating-a-rolepoint-test-user)**  - RolePoint die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="b825c-145">**[Creating a RolePoint test user](#creating-a-rolepoint-test-user)** - to have a counterpart of Britta Simon in RolePoint that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b825c-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b825c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b825c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b825c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b825c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b825c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b825c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing RolePoint configureren.</span><span class="sxs-lookup"><span data-stu-id="b825c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RolePoint application.</span></span>

<span data-ttu-id="b825c-150">**Voor het configureren van Azure AD eenmalige aanmelding met RolePoint, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b825c-150">**To configure Azure AD single sign-on with RolePoint, perform the following steps:**</span></span>

1. <span data-ttu-id="b825c-151">In de Azure-portal op de **RolePoint** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b825c-151">In the Azure portal, on the **RolePoint** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b825c-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b825c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_samlbase.png)

3. <span data-ttu-id="b825c-155">Op de **RolePoint domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b825c-155">On the **RolePoint Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_url.png)

    <span data-ttu-id="b825c-157">a.</span><span class="sxs-lookup"><span data-stu-id="b825c-157">a.</span></span> <span data-ttu-id="b825c-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.rolepoint.com/login`</span><span class="sxs-lookup"><span data-stu-id="b825c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.rolepoint.com/login`</span></span>
    
    <span data-ttu-id="b825c-159">b.</span><span class="sxs-lookup"><span data-stu-id="b825c-159">b.</span></span> <span data-ttu-id="b825c-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://app.rolepoint.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="b825c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://app.rolepoint.com/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b825c-161">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="b825c-161">These values are not the real.</span></span> <span data-ttu-id="b825c-162">Deze waarden bijwerken met de werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="b825c-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="b825c-163">Hier we raden u voor het gebruik van de unieke waarde van een tekenreeks in de Identifier.Contact [RolePoint ondersteuningsteam](mailto:info@rolepoint.com) de waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="b825c-163">Here we suggest you to use the unique value of string in the Identifier.Contact [RolePoint support team](mailto:info@rolepoint.com) to get the value.</span></span> 
 
4. <span data-ttu-id="b825c-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b825c-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_certificate.png) 

5. <span data-ttu-id="b825c-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b825c-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rolepoint-tutorial/tutorial_general_400.png)


6. <span data-ttu-id="b825c-168">Eenmalige aanmelding configureren op **RolePoint** zijde, moet u de gedownloade verzenden **Metadata XML** naar [RolePoint ondersteuningsteam](mailto:info@rolepoint.com).</span><span class="sxs-lookup"><span data-stu-id="b825c-168">To configure single sign-on on **RolePoint** side, you need to send the downloaded **Metadata XML** to [RolePoint support team](mailto:info@rolepoint.com).</span></span>

> [!TIP]
> <span data-ttu-id="b825c-169">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="b825c-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b825c-170">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="b825c-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b825c-171">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b825c-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b825c-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b825c-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="b825c-173">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b825c-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="b825c-175">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b825c-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b825c-176">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b825c-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b825c-178">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b825c-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b825c-180">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b825c-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b825c-182">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b825c-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b825c-184">a.</span><span class="sxs-lookup"><span data-stu-id="b825c-184">a.</span></span> <span data-ttu-id="b825c-185">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b825c-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b825c-186">b.</span><span class="sxs-lookup"><span data-stu-id="b825c-186">b.</span></span> <span data-ttu-id="b825c-187">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b825c-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b825c-188">c.</span><span class="sxs-lookup"><span data-stu-id="b825c-188">c.</span></span> <span data-ttu-id="b825c-189">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b825c-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b825c-190">d.</span><span class="sxs-lookup"><span data-stu-id="b825c-190">d.</span></span> <span data-ttu-id="b825c-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b825c-191">Click **Create**.</span></span>
 
### <a name="creating-a-rolepoint-test-user"></a><span data-ttu-id="b825c-192">Een testgebruiker RolePoint maken</span><span class="sxs-lookup"><span data-stu-id="b825c-192">Creating a RolePoint test user</span></span>

<span data-ttu-id="b825c-193">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in RolePoint maken.</span><span class="sxs-lookup"><span data-stu-id="b825c-193">In this section, you create a user called Britta Simon in RolePoint.</span></span> <span data-ttu-id="b825c-194">Werken met [RolePoint ondersteuningsteam](mailto:info@rolepoint.com) de gebruikers van het platform RolePoint toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b825c-194">Work with [RolePoint support team](mailto:info@rolepoint.com) to add the users in the RolePoint platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b825c-195">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="b825c-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b825c-196">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan RolePoint.</span><span class="sxs-lookup"><span data-stu-id="b825c-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RolePoint.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b825c-198">**Britta Simon om aan te wijzen RolePoint, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b825c-198">**To assign Britta Simon to RolePoint, perform the following steps:**</span></span>

1. <span data-ttu-id="b825c-199">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b825c-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b825c-201">Selecteer in de lijst met toepassingen **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="b825c-201">In the applications list, select **RolePoint**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_app.png) 

3. <span data-ttu-id="b825c-203">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b825c-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="b825c-205">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b825c-205">Click **Add** button.</span></span> <span data-ttu-id="b825c-206">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b825c-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="b825c-208">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b825c-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b825c-209">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b825c-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b825c-210">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b825c-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b825c-211">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b825c-211">Testing single sign-on</span></span>

<span data-ttu-id="b825c-212">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b825c-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b825c-213">Als u op de tegel RolePoint in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing RolePoint.</span><span class="sxs-lookup"><span data-stu-id="b825c-213">When you click the RolePoint tile in the Access Panel, you should get automatically signed-on to your RolePoint application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b825c-214">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b825c-214">Additional resources</span></span>

* [<span data-ttu-id="b825c-215">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b825c-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b825c-216">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b825c-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_203.png

