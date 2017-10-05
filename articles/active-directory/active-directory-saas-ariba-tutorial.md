---
title: 'Zelfstudie: Azure Active Directory-integratie met Ariba | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Ariba.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 45a8364c-55d1-4dc7-b079-9eb2a701842d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 214367847055ba38ee03a28d0afdcc58f68333cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ariba"></a><span data-ttu-id="246d4-103">Zelfstudie: Azure Active Directory-integratie met Ariba</span><span class="sxs-lookup"><span data-stu-id="246d4-103">Tutorial: Azure Active Directory integration with Ariba</span></span>

<span data-ttu-id="246d4-104">In deze zelfstudie leert u hoe Ariba integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="246d4-104">In this tutorial, you learn how to integrate Ariba with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="246d4-105">Ariba integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="246d4-105">Integrating Ariba with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="246d4-106">U kunt beheren in Azure AD die toegang tot Ariba heeft</span><span class="sxs-lookup"><span data-stu-id="246d4-106">You can control in Azure AD who has access to Ariba</span></span>
- <span data-ttu-id="246d4-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Ariba (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="246d4-107">You can enable your users to automatically get signed-on to Ariba (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="246d4-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="246d4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="246d4-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="246d4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="246d4-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="246d4-110">Prerequisites</span></span>

<span data-ttu-id="246d4-111">Voor het configureren van Azure AD-integratie met Ariba, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="246d4-111">To configure Azure AD integration with Ariba, you need the following items:</span></span>

- <span data-ttu-id="246d4-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="246d4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="246d4-113">Een Ariba eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="246d4-113">An Ariba single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="246d4-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="246d4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="246d4-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="246d4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="246d4-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="246d4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="246d4-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="246d4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="246d4-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="246d4-118">Scenario description</span></span>
<span data-ttu-id="246d4-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="246d4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="246d4-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="246d4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="246d4-121">Ariba uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="246d4-121">Adding Ariba from the gallery</span></span>
2. <span data-ttu-id="246d4-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="246d4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ariba-from-the-gallery"></a><span data-ttu-id="246d4-123">Ariba uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="246d4-123">Adding Ariba from the gallery</span></span>
<span data-ttu-id="246d4-124">Voor het configureren van de integratie van Ariba in Azure AD, moet u Ariba uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="246d4-124">To configure the integration of Ariba into Azure AD, you need to add Ariba from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="246d4-125">**Als u wilt toevoegen Ariba uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="246d4-125">**To add Ariba from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="246d4-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="246d4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="246d4-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="246d4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="246d4-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="246d4-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="246d4-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="246d4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="246d4-133">Typ in het zoekvak **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="246d4-133">In the search box, type **Ariba**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_search.png)

5. <span data-ttu-id="246d4-135">Selecteer in het deelvenster resultaten **Ariba**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="246d4-135">In the results panel, select **Ariba**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="246d4-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="246d4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="246d4-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Ariba op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="246d4-138">In this section, you configure and test Azure AD single sign-on with Ariba based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="246d4-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Ariba is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="246d4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Ariba is to a user in Azure AD.</span></span> <span data-ttu-id="246d4-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Ariba tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="246d4-140">In other words, a link relationship between an Azure AD user and the related user in Ariba needs to be established.</span></span>

<span data-ttu-id="246d4-141">Wijs in Ariba, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="246d4-141">In Ariba, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="246d4-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Ariba, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="246d4-142">To configure and test Azure AD single sign-on with Ariba, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="246d4-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="246d4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="246d4-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="246d4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="246d4-145">**[Maken van een testgebruiker Ariba](#creating-an-ariba-test-user)**  - Ariba die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="246d4-145">**[Creating an Ariba test user](#creating-an-ariba-test-user)** - to have a counterpart of Britta Simon in Ariba that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="246d4-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="246d4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="246d4-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="246d4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="246d4-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="246d4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="246d4-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Ariba configureren.</span><span class="sxs-lookup"><span data-stu-id="246d4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ariba application.</span></span>

<span data-ttu-id="246d4-150">**Voor het configureren van Azure AD eenmalige aanmelding met Ariba, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="246d4-150">**To configure Azure AD single sign-on with Ariba, perform the following steps:**</span></span>

1. <span data-ttu-id="246d4-151">In de Azure-portal op de **Ariba** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="246d4-151">In the Azure portal, on the **Ariba** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="246d4-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="246d4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_samlbase.png)

3. <span data-ttu-id="246d4-155">Op de **Ariba domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="246d4-155">On the **Ariba Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_url.png)

    <span data-ttu-id="246d4-157">a.</span><span class="sxs-lookup"><span data-stu-id="246d4-157">a.</span></span> <span data-ttu-id="246d4-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen: `https://<subdomain>.sourcing.ariba.com` of`https://<subdomain>.supplier.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="246d4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sourcing.ariba.com` or `https://<subdomain>.supplier.ariba.com`</span></span>

    <span data-ttu-id="246d4-159">b.</span><span class="sxs-lookup"><span data-stu-id="246d4-159">b.</span></span> <span data-ttu-id="246d4-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`http://<subdomain>.procurement-2.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="246d4-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<subdomain>.procurement-2.ariba.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="246d4-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="246d4-161">These values are not real.</span></span> <span data-ttu-id="246d4-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="246d4-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="246d4-163">Hier raden we u voor het gebruik van de unieke waarde van een tekenreeks in de id.</span><span class="sxs-lookup"><span data-stu-id="246d4-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="246d4-164">Neem contact op met het ondersteuningsteam Ariba Client op **1-866-218-2155** ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="246d4-164">Contact Ariba Client support team at **1-866-218-2155** to get these values.</span></span> 
 

4. <span data-ttu-id="246d4-165">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="246d4-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate  file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_certificate.png) 

5. <span data-ttu-id="246d4-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="246d4-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ariba-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="246d4-169">Als u eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, Ariba ondersteuningsteam niet aanroepen voor **1-866-218-2155** en ze helpt u verder gaat over het om ze te bieden de gedownloade **certificaat (Base64)** bestand.</span><span class="sxs-lookup"><span data-stu-id="246d4-169">To get SSO configured for your application, call Ariba support team on **1-866-218-2155** and they'll assist you further on how to provide them the downloaded **Certificate (Base64)** file.</span></span>  
 
> [!TIP]
> <span data-ttu-id="246d4-170">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="246d4-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="246d4-171">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="246d4-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="246d4-172">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="246d4-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="246d4-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="246d4-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="246d4-174">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="246d4-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="246d4-176">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="246d4-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="246d4-177">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="246d4-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ariba-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="246d4-179">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="246d4-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ariba-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="246d4-181">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="246d4-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ariba-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="246d4-183">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="246d4-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-ariba-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="246d4-185">a.</span><span class="sxs-lookup"><span data-stu-id="246d4-185">a.</span></span> <span data-ttu-id="246d4-186">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="246d4-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="246d4-187">b.</span><span class="sxs-lookup"><span data-stu-id="246d4-187">b.</span></span> <span data-ttu-id="246d4-188">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="246d4-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="246d4-189">c.</span><span class="sxs-lookup"><span data-stu-id="246d4-189">c.</span></span> <span data-ttu-id="246d4-190">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="246d4-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="246d4-191">d.</span><span class="sxs-lookup"><span data-stu-id="246d4-191">d.</span></span> <span data-ttu-id="246d4-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="246d4-192">Click **Create**.</span></span>
 
### <a name="creating-an-ariba-test-user"></a><span data-ttu-id="246d4-193">Een testgebruiker Ariba maken</span><span class="sxs-lookup"><span data-stu-id="246d4-193">Creating an Ariba test user</span></span>

<span data-ttu-id="246d4-194">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Ariba genoemd.</span><span class="sxs-lookup"><span data-stu-id="246d4-194">The objective of this section is to create a user called Britta Simon in Ariba.</span></span> <span data-ttu-id="246d4-195">Werken met het ondersteuningsteam Ariba op **1-866-218-2155** de gebruikers in het systeem Ariba toevoegen.</span><span class="sxs-lookup"><span data-stu-id="246d4-195">Work with Ariba support team at **1-866-218-2155** to add the users in the Ariba system.</span></span> 

 >[!NOTE]
 ><span data-ttu-id="246d4-196">Als u een gebruiker handmatig maken wilt, moet u contact op met het ondersteuningsteam Ariba op **1-866-218-2155**.</span><span class="sxs-lookup"><span data-stu-id="246d4-196">If you need to create a user manually, you need to contact the Ariba support team at **1-866-218-2155**.</span></span>
 >  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="246d4-197">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="246d4-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="246d4-198">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Ariba.</span><span class="sxs-lookup"><span data-stu-id="246d4-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ariba.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="246d4-200">**Britta Simon om aan te wijzen Ariba, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="246d4-200">**To assign Britta Simon to Ariba, perform the following steps:**</span></span>

1. <span data-ttu-id="246d4-201">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="246d4-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="246d4-203">Selecteer in de lijst met toepassingen **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="246d4-203">In the applications list, select **Ariba**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_app.png) 

3. <span data-ttu-id="246d4-205">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="246d4-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="246d4-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="246d4-207">Click **Add** button.</span></span> <span data-ttu-id="246d4-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="246d4-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="246d4-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="246d4-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="246d4-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="246d4-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="246d4-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="246d4-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="246d4-213">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="246d4-213">Testing single sign-on</span></span>
<span data-ttu-id="246d4-214">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="246d4-214">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="246d4-215">Als u op de tegel Ariba in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Ariba.</span><span class="sxs-lookup"><span data-stu-id="246d4-215">When you click the Ariba tile in the Access Panel, you should get automatically signed-on to your Ariba application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="246d4-216">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="246d4-216">Additional resources</span></span>

* [<span data-ttu-id="246d4-217">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="246d4-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="246d4-218">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="246d4-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_203.png

