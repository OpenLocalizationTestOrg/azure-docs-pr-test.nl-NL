---
title: 'Zelfstudie: Azure Active Directory-integratie met Asset Bank | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Asset Bank.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3006ad6e-8831-41cd-94aa-7e7ae770ce7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 17bc0082e3721b50269cb4b17884c0e4a4cbcb5d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asset-bank"></a><span data-ttu-id="8bca7-103">Zelfstudie: Azure Active Directory-integratie met Asset Bank</span><span class="sxs-lookup"><span data-stu-id="8bca7-103">Tutorial: Azure Active Directory integration with Asset Bank</span></span>

<span data-ttu-id="8bca7-104">In deze zelfstudie leert u hoe Asset Bank integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8bca7-104">In this tutorial, you learn how to integrate Asset Bank with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8bca7-105">Asset Bank integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="8bca7-105">Integrating Asset Bank with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8bca7-106">U kunt beheren in Azure AD die toegang tot de Bank Asset heeft</span><span class="sxs-lookup"><span data-stu-id="8bca7-106">You can control in Azure AD who has access to Asset Bank</span></span>
- <span data-ttu-id="8bca7-107">U kunt uw gebruikers automatisch ophalen aangemeld bij de Bank Asset (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="8bca7-107">You can enable your users to automatically get signed-on to Asset Bank (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8bca7-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="8bca7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8bca7-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8bca7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8bca7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8bca7-110">Prerequisites</span></span>

<span data-ttu-id="8bca7-111">Voor het configureren van Azure AD-integratie met Asset Bank, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="8bca7-111">To configure Azure AD integration with Asset Bank, you need the following items:</span></span>

- <span data-ttu-id="8bca7-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="8bca7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8bca7-113">Een Asset Bank eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="8bca7-113">An Asset Bank single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8bca7-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="8bca7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8bca7-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="8bca7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8bca7-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="8bca7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8bca7-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8bca7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8bca7-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="8bca7-118">Scenario description</span></span>
<span data-ttu-id="8bca7-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="8bca7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8bca7-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="8bca7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8bca7-121">Adding Asset Bank uit de galerie</span><span class="sxs-lookup"><span data-stu-id="8bca7-121">Adding Asset Bank from the gallery</span></span>
2. <span data-ttu-id="8bca7-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8bca7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asset-bank-from-the-gallery"></a><span data-ttu-id="8bca7-123">Adding Asset Bank uit de galerie</span><span class="sxs-lookup"><span data-stu-id="8bca7-123">Adding Asset Bank from the gallery</span></span>
<span data-ttu-id="8bca7-124">Voor het configureren van de integratie van Asset Bank in Azure AD, moet u Asset Bank uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="8bca7-124">To configure the integration of Asset Bank into Azure AD, you need to add Asset Bank from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8bca7-125">**Als u wilt toevoegen Asset Bank uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8bca7-125">**To add Asset Bank from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8bca7-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8bca7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8bca7-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8bca7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8bca7-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8bca7-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="8bca7-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8bca7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="8bca7-133">Typ in het zoekvak **Asset Bank**.</span><span class="sxs-lookup"><span data-stu-id="8bca7-133">In the search box, type **Asset Bank**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_search.png)

5. <span data-ttu-id="8bca7-135">Selecteer in het deelvenster resultaten **Asset Bank**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="8bca7-135">In the results panel, select **Asset Bank**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8bca7-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8bca7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8bca7-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Asset Bank op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="8bca7-138">In this section, you configure and test Azure AD single sign-on with Asset Bank based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8bca7-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Asset Bank is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8bca7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Asset Bank is to a user in Azure AD.</span></span> <span data-ttu-id="8bca7-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de Asset Bank tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="8bca7-140">In other words, a link relationship between an Azure AD user and the related user in Asset Bank needs to be established.</span></span>

<span data-ttu-id="8bca7-141">In Asset Bank, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="8bca7-141">In Asset Bank, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8bca7-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Asset Bank, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="8bca7-142">To configure and test Azure AD single sign-on with Asset Bank, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8bca7-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8bca7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8bca7-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8bca7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8bca7-145">**[Maken van een testgebruiker Asset Bank](#creating-an-asset-bank-test-user)**  - Asset Bank die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="8bca7-145">**[Creating an Asset Bank test user](#creating-an-asset-bank-test-user)** - to have a counterpart of Britta Simon in Asset Bank that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8bca7-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8bca7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8bca7-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="8bca7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8bca7-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="8bca7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8bca7-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="8bca7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Asset Bank application.</span></span>

<span data-ttu-id="8bca7-150">**Voor het configureren van Azure AD eenmalige aanmelding met Asset Bank, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8bca7-150">**To configure Azure AD single sign-on with Asset Bank, perform the following steps:**</span></span>

1. <span data-ttu-id="8bca7-151">In de Azure-portal op de **Asset Bank** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="8bca7-151">In the Azure portal, on the **Asset Bank** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="8bca7-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8bca7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_samlbase.png)

3. <span data-ttu-id="8bca7-155">Op de **Asset Bank domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8bca7-155">On the **Asset Bank Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_url.png)

    <span data-ttu-id="8bca7-157">a.</span><span class="sxs-lookup"><span data-stu-id="8bca7-157">a.</span></span> <span data-ttu-id="8bca7-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.assetbank-server.com`</span><span class="sxs-lookup"><span data-stu-id="8bca7-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.assetbank-server.com`</span></span>

    <span data-ttu-id="8bca7-159">b.</span><span class="sxs-lookup"><span data-stu-id="8bca7-159">b.</span></span> <span data-ttu-id="8bca7-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.assetbank-server.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="8bca7-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.assetbank-server.com/shibboleth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8bca7-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="8bca7-161">These values are not real.</span></span> <span data-ttu-id="8bca7-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="8bca7-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8bca7-163">Neem contact op met [Asset Bank Client ondersteuningsteam](mailto:support@assetbank.co.uk) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="8bca7-163">Contact [Asset Bank Client support team](mailto:support@assetbank.co.uk) to get these values.</span></span> 
 
4. <span data-ttu-id="8bca7-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="8bca7-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_certificate.png) 

5. <span data-ttu-id="8bca7-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="8bca7-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-assetbank-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8bca7-168">Eenmalige aanmelding configureren op **Asset Bank** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Asset Bank ondersteuningsteam](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="8bca7-168">To configure single sign-on on **Asset Bank** side, you need to send the downloaded **Metadata XML** to [Asset Bank support team](mailto:support@assetbank.co.uk).</span></span> 


> [!TIP]
> <span data-ttu-id="8bca7-169">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="8bca7-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8bca7-170">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="8bca7-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8bca7-171">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8bca7-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8bca7-172">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="8bca7-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="8bca7-173">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="8bca7-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="8bca7-175">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8bca7-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8bca7-176">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8bca7-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-assetbank-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8bca7-178">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="8bca7-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-assetbank-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8bca7-180">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8bca7-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-assetbank-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8bca7-182">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8bca7-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-assetbank-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8bca7-184">a.</span><span class="sxs-lookup"><span data-stu-id="8bca7-184">a.</span></span> <span data-ttu-id="8bca7-185">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8bca7-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8bca7-186">b.</span><span class="sxs-lookup"><span data-stu-id="8bca7-186">b.</span></span> <span data-ttu-id="8bca7-187">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8bca7-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8bca7-188">c.</span><span class="sxs-lookup"><span data-stu-id="8bca7-188">c.</span></span> <span data-ttu-id="8bca7-189">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="8bca7-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8bca7-190">d.</span><span class="sxs-lookup"><span data-stu-id="8bca7-190">d.</span></span> <span data-ttu-id="8bca7-191">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8bca7-191">Click **Create**.</span></span>
 
### <a name="creating-an-asset-bank-test-user"></a><span data-ttu-id="8bca7-192">Een Asset Bank testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="8bca7-192">Creating an Asset Bank test user</span></span>

<span data-ttu-id="8bca7-193">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="8bca7-193">The objective of this section is to create a user called Britta Simon in Asset Bank.</span></span> <span data-ttu-id="8bca7-194">Asset Bank ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8bca7-194">Asset Bank supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="8bca7-195">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="8bca7-195">There is no action item for you in this section.</span></span> <span data-ttu-id="8bca7-196">Een nieuwe gebruiker is gemaakt tijdens een poging tot toegang tot de Asset Bank als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="8bca7-196">A new user is created during an attempt to access Asset Bank if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="8bca7-197">Als u een gebruiker handmatig maken wilt, moet u contact op met de [Asset Bank ondersteuningsteam](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="8bca7-197">If you need to create a user manually, you need to contact the [Asset Bank support team](mailto:support@assetbank.co.uk).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8bca7-198">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bca7-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8bca7-199">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="8bca7-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Asset Bank.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="8bca7-201">**Britta Simon om aan te wijzen Asset Bank, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8bca7-201">**To assign Britta Simon to Asset Bank, perform the following steps:**</span></span>

1. <span data-ttu-id="8bca7-202">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8bca7-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="8bca7-204">Selecteer in de lijst met toepassingen **Asset Bank**.</span><span class="sxs-lookup"><span data-stu-id="8bca7-204">In the applications list, select **Asset Bank**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_app.png) 

3. <span data-ttu-id="8bca7-206">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="8bca7-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="8bca7-208">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="8bca7-208">Click **Add** button.</span></span> <span data-ttu-id="8bca7-209">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8bca7-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="8bca7-211">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="8bca7-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8bca7-212">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8bca7-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8bca7-213">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8bca7-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8bca7-214">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8bca7-214">Testing single sign-on</span></span>

<span data-ttu-id="8bca7-215">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="8bca7-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8bca7-216">Als u op de tegel Asset Bank in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="8bca7-216">When you click the Asset Bank tile in the Access Panel, you should get automatically signed-on to your Asset Bank application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8bca7-217">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8bca7-217">Additional resources</span></span>

* [<span data-ttu-id="8bca7-218">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8bca7-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8bca7-219">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8bca7-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_203.png

