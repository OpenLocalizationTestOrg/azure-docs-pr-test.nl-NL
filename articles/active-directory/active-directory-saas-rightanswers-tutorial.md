---
title: 'Zelfstudie: Azure Active Directory-integratie met RightAnswers | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en RightAnswers.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7f09e25a-a716-41e1-8ca3-fd00e3d1b8cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: e5985831598a0e5b1277d2c6cd02b03c919aad4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightanswers"></a><span data-ttu-id="34adc-103">Zelfstudie: Azure Active Directory-integratie met RightAnswers</span><span class="sxs-lookup"><span data-stu-id="34adc-103">Tutorial: Azure Active Directory integration with RightAnswers</span></span>

<span data-ttu-id="34adc-104">In deze zelfstudie leert u hoe RightAnswers integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="34adc-104">In this tutorial, you learn how to integrate RightAnswers with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="34adc-105">RightAnswers integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="34adc-105">Integrating RightAnswers with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="34adc-106">U kunt beheren in Azure AD die toegang tot RightAnswers heeft</span><span class="sxs-lookup"><span data-stu-id="34adc-106">You can control in Azure AD who has access to RightAnswers</span></span>
- <span data-ttu-id="34adc-107">U kunt uw gebruikers automatisch ophalen aangemeld bij RightAnswers (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="34adc-107">You can enable your users to automatically get signed-on to RightAnswers (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="34adc-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="34adc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="34adc-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="34adc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34adc-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="34adc-110">Prerequisites</span></span>

<span data-ttu-id="34adc-111">Voor het configureren van Azure AD-integratie met RightAnswers, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="34adc-111">To configure Azure AD integration with RightAnswers, you need the following items:</span></span>

- <span data-ttu-id="34adc-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="34adc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="34adc-113">Een RightAnswers eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="34adc-113">A RightAnswers single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="34adc-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="34adc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="34adc-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="34adc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="34adc-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="34adc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="34adc-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="34adc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="34adc-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="34adc-118">Scenario description</span></span>
<span data-ttu-id="34adc-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="34adc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="34adc-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="34adc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="34adc-121">RightAnswers uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="34adc-121">Adding RightAnswers from the gallery</span></span>
2. <span data-ttu-id="34adc-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="34adc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightanswers-from-the-gallery"></a><span data-ttu-id="34adc-123">RightAnswers uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="34adc-123">Adding RightAnswers from the gallery</span></span>
<span data-ttu-id="34adc-124">Voor het configureren van de integratie van RightAnswers in Azure AD, moet u RightAnswers uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="34adc-124">To configure the integration of RightAnswers into Azure AD, you need to add RightAnswers from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="34adc-125">**Als u wilt toevoegen RightAnswers uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="34adc-125">**To add RightAnswers from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="34adc-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="34adc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="34adc-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="34adc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="34adc-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="34adc-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="34adc-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="34adc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="34adc-133">Typ in het zoekvak **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="34adc-133">In the search box, type **RightAnswers**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_search.png)

5. <span data-ttu-id="34adc-135">Selecteer in het deelvenster resultaten **RightAnswers**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="34adc-135">In the results panel, select **RightAnswers**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="34adc-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="34adc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="34adc-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met RightAnswers op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="34adc-138">In this section, you configure and test Azure AD single sign-on with RightAnswers based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="34adc-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in RightAnswers is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34adc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RightAnswers is to a user in Azure AD.</span></span> <span data-ttu-id="34adc-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in RightAnswers tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="34adc-140">In other words, a link relationship between an Azure AD user and the related user in RightAnswers needs to be established.</span></span>

<span data-ttu-id="34adc-141">Wijs in RightAnswers, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="34adc-141">In RightAnswers, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="34adc-142">Om te configureren en testen van Azure AD eenmalige aanmelding met RightAnswers, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="34adc-142">To configure and test Azure AD single sign-on with RightAnswers, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="34adc-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34adc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="34adc-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="34adc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="34adc-145">**[Maken van een testgebruiker RightAnswers](#creating-a-rightanswers-test-user)**  - RightAnswers die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="34adc-145">**[Creating a RightAnswers test user](#creating-a-rightanswers-test-user)** - to have a counterpart of Britta Simon in RightAnswers that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="34adc-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="34adc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="34adc-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="34adc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="34adc-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="34adc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="34adc-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing RightAnswers configureren.</span><span class="sxs-lookup"><span data-stu-id="34adc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RightAnswers application.</span></span>

<span data-ttu-id="34adc-150">**Voor het configureren van Azure AD eenmalige aanmelding met RightAnswers, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="34adc-150">**To configure Azure AD single sign-on with RightAnswers, perform the following steps:**</span></span>

1. <span data-ttu-id="34adc-151">In de Azure-portal op de **RightAnswers** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="34adc-151">In the Azure portal, on the **RightAnswers** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="34adc-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="34adc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_samlbase.png)

3. <span data-ttu-id="34adc-155">Op de **RightAnswers domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="34adc-155">On the **RightAnswers Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_url.png)

    <span data-ttu-id="34adc-157">a.</span><span class="sxs-lookup"><span data-stu-id="34adc-157">a.</span></span> <span data-ttu-id="34adc-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.rightanswers.com/portal/ss/`</span><span class="sxs-lookup"><span data-stu-id="34adc-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.rightanswers.com/portal/ss/`</span></span>

    <span data-ttu-id="34adc-159">b.</span><span class="sxs-lookup"><span data-stu-id="34adc-159">b.</span></span> <span data-ttu-id="34adc-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.rightanswers.com:<identifier>/portal`</span><span class="sxs-lookup"><span data-stu-id="34adc-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.rightanswers.com:<identifier>/portal`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="34adc-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="34adc-161">These values are not real.</span></span> <span data-ttu-id="34adc-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="34adc-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="34adc-163">Neem contact op met [RightAnswers Client ondersteuningsteam](https://www.rightanswers.com/contact-us/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="34adc-163">Contact [RightAnswers Client support team](https://www.rightanswers.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="34adc-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="34adc-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_certificate.png) 

5. <span data-ttu-id="34adc-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="34adc-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rightanswers-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="34adc-168">Eenmalige aanmelding configureren op **RightAnswers** zijde, moet u de gedownloade verzenden **Metadata XML** naar [RightAnswers ondersteuningsteam](https://www.rightanswers.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="34adc-168">To configure single sign-on on **RightAnswers** side, you need to send the downloaded **Metadata XML** to [RightAnswers support team](https://www.rightanswers.com/contact-us/).</span></span>

    >[!NOTE]
    ><span data-ttu-id="34adc-169">Het ondersteuningsteam RightAnswers heeft te maken van de werkelijke SSO-configuratie.</span><span class="sxs-lookup"><span data-stu-id="34adc-169">Your RightAnswers support team has to do the actual SSO configuration.</span></span>
    ><span data-ttu-id="34adc-170">U ontvangt een melding wanneer SSO is ingeschakeld voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="34adc-170">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="34adc-171">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="34adc-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="34adc-172">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="34adc-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="34adc-173">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="34adc-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="34adc-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="34adc-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="34adc-175">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="34adc-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="34adc-177">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="34adc-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="34adc-178">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="34adc-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="34adc-180">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="34adc-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="34adc-182">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="34adc-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="34adc-184">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="34adc-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="34adc-186">a.</span><span class="sxs-lookup"><span data-stu-id="34adc-186">a.</span></span> <span data-ttu-id="34adc-187">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="34adc-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="34adc-188">b.</span><span class="sxs-lookup"><span data-stu-id="34adc-188">b.</span></span> <span data-ttu-id="34adc-189">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="34adc-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="34adc-190">c.</span><span class="sxs-lookup"><span data-stu-id="34adc-190">c.</span></span> <span data-ttu-id="34adc-191">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="34adc-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="34adc-192">d.</span><span class="sxs-lookup"><span data-stu-id="34adc-192">d.</span></span> <span data-ttu-id="34adc-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="34adc-193">Click **Create**.</span></span>
 
### <a name="creating-a-rightanswers-test-user"></a><span data-ttu-id="34adc-194">Een testgebruiker RightAnswers maken</span><span class="sxs-lookup"><span data-stu-id="34adc-194">Creating a RightAnswers test user</span></span>

<span data-ttu-id="34adc-195">Om Azure AD-gebruikers zich aanmelden bij RightAnswers, moeten ze worden ingericht in RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="34adc-195">To enable Azure AD users to log in to RightAnswers, they must be provisioned into RightAnswers.</span></span> <span data-ttu-id="34adc-196">RightAnswers, inrichting is wanneer een geautomatiseerde taak, dus er geen actie-item voor u is.</span><span class="sxs-lookup"><span data-stu-id="34adc-196">When RightAnswers, provisioning is an automated task so there is no action item for you.</span></span>

<span data-ttu-id="34adc-197">Gebruikers worden automatisch gemaakt indien nodig tijdens de eerste eenmalige aanmelding poging.</span><span class="sxs-lookup"><span data-stu-id="34adc-197">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="34adc-198">U kunt andere RightAnswers gebruiker account hulpmiddelen voor het maken of API's die is geleverd door RightAnswers aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="34adc-198">You can use any other RightAnswers user account creation tools or APIs provided by RightAnswers to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="34adc-199">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="34adc-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="34adc-200">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="34adc-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RightAnswers.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="34adc-202">**Britta Simon om aan te wijzen RightAnswers, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="34adc-202">**To assign Britta Simon to RightAnswers, perform the following steps:**</span></span>

1. <span data-ttu-id="34adc-203">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="34adc-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="34adc-205">Selecteer in de lijst met toepassingen **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="34adc-205">In the applications list, select **RightAnswers**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_app.png) 

3. <span data-ttu-id="34adc-207">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="34adc-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="34adc-209">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="34adc-209">Click **Add** button.</span></span> <span data-ttu-id="34adc-210">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="34adc-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="34adc-212">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="34adc-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="34adc-213">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="34adc-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="34adc-214">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="34adc-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="34adc-215">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="34adc-215">Testing single sign-on</span></span>

<span data-ttu-id="34adc-216">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="34adc-216">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="34adc-217">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="34adc-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>
## <a name="additional-resources"></a><span data-ttu-id="34adc-218">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="34adc-218">Additional resources</span></span>

* [<span data-ttu-id="34adc-219">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34adc-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="34adc-220">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="34adc-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_203.png

