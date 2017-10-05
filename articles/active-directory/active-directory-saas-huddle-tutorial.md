---
title: 'Zelfstudie: Azure Active Directory-integratie met kruipen dicht | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en kruipen dicht.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 59d4019545d39ec76bf401696338140f430630c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="0b71c-103">Zelfstudie: Azure Active Directory-integratie met kruipen dicht</span><span class="sxs-lookup"><span data-stu-id="0b71c-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="0b71c-104">In deze zelfstudie leert u hoe kruipen dicht integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0b71c-104">In this tutorial, you learn how to integrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0b71c-105">Kruipen dicht integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="0b71c-105">Integrating Huddle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0b71c-106">U kunt beheren in Azure AD die toegang tot kruipen dicht heeft</span><span class="sxs-lookup"><span data-stu-id="0b71c-106">You can control in Azure AD who has access to Huddle</span></span>
- <span data-ttu-id="0b71c-107">U kunt uw gebruikers automatisch ophalen aangemeld bij kruipen dicht (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="0b71c-107">You can enable your users to automatically get signed-on to Huddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0b71c-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="0b71c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0b71c-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0b71c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b71c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0b71c-110">Prerequisites</span></span>

<span data-ttu-id="0b71c-111">Voor het configureren van Azure AD-integratie met kruipen dicht, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="0b71c-111">To configure Azure AD integration with Huddle, you need the following items:</span></span>

- <span data-ttu-id="0b71c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="0b71c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0b71c-113">Een kruipen dicht eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="0b71c-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0b71c-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="0b71c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0b71c-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="0b71c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0b71c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="0b71c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0b71c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b71c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0b71c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="0b71c-118">Scenario description</span></span>

<span data-ttu-id="0b71c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="0b71c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0b71c-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="0b71c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0b71c-121">Toe te voegen kruipen dicht in de galerie</span><span class="sxs-lookup"><span data-stu-id="0b71c-121">Adding Huddle from the gallery</span></span>
2. <span data-ttu-id="0b71c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0b71c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-the-gallery"></a><span data-ttu-id="0b71c-123">Toe te voegen kruipen dicht in de galerie</span><span class="sxs-lookup"><span data-stu-id="0b71c-123">Adding Huddle from the gallery</span></span>
<span data-ttu-id="0b71c-124">Voor het configureren van de integratie van kruipen dicht in Azure AD, moet u kruipen dicht in de galerie aan de lijst met beheerde SaaS-apps toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0b71c-124">To configure the integration of Huddle into Azure AD, you need to add Huddle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0b71c-125">**Als u wilt toevoegen kruipen dicht in de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0b71c-125">**To add Huddle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0b71c-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0b71c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0b71c-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0b71c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0b71c-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0b71c-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="0b71c-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0b71c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="0b71c-133">Typ in het zoekvak **kruipen dicht**.</span><span class="sxs-lookup"><span data-stu-id="0b71c-133">In the search box, type **Huddle**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="0b71c-135">Selecteer in het deelvenster resultaten **kruipen dicht**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="0b71c-135">In the results panel, select **Huddle**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0b71c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0b71c-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="0b71c-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met kruipen dicht op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="0b71c-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0b71c-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in kruipen dicht in Azure AD voor een gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="0b71c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Huddle is to a user in Azure AD.</span></span> <span data-ttu-id="0b71c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in kruipen dicht tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="0b71c-140">In other words, a link relationship between an Azure AD user and the related user in Huddle needs to be established.</span></span>

<span data-ttu-id="0b71c-141">Wijs in het kruipen dicht, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="0b71c-141">In Huddle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0b71c-142">Om te configureren en testen van Azure AD eenmalige aanmelding met kruipen dicht, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="0b71c-142">To configure and test Azure AD single sign-on with Huddle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0b71c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0b71c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>

2. <span data-ttu-id="0b71c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b71c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="0b71c-145">**[Maken van een testgebruiker kruipen dicht](#creating-a-huddle-test-user)**  - kruipen dicht die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="0b71c-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - to have a counterpart of Britta Simon in Huddle that is linked to the Azure AD representation of user.</span></span>

4. <span data-ttu-id="0b71c-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0b71c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>

5. <span data-ttu-id="0b71c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="0b71c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0b71c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="0b71c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0b71c-149">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing kruipen dicht.</span><span class="sxs-lookup"><span data-stu-id="0b71c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="0b71c-150">**Voor het configureren van Azure AD eenmalige aanmelding met kruipen dicht, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0b71c-150">**To configure Azure AD single sign-on with Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="0b71c-151">In de Azure-portal op de **kruipen dicht** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="0b71c-151">In the Azure portal, on the **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="0b71c-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0b71c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="0b71c-155">Op de **kruipen dicht domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="0b71c-155">On the **Huddle Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="0b71c-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`http://<company name>.huddle.com`</span><span class="sxs-lookup"><span data-stu-id="0b71c-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0b71c-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="0b71c-158">This value is not real.</span></span> <span data-ttu-id="0b71c-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0b71c-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="0b71c-160">Neem contact op met [Client kruipen dicht ondersteuningsteam](https://huddle.zendesk.com) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="0b71c-160">Contact [Huddle Client support team](https://huddle.zendesk.com) to get this value.</span></span> 

4. <span data-ttu-id="0b71c-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="0b71c-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="0b71c-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="0b71c-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0b71c-165">Op de **kruipen dicht configuratie** sectie, klikt u op **configureren kruipen dicht** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="0b71c-165">On the **Huddle Configuration** section, click **Configure Huddle** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0b71c-166">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="0b71c-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="0b71c-168">Voor het configureren van eenmalige aanmelding kruipen dicht zijde, moet u de gedownloade verzenden **certificaat**, **SAML Single Sign-On Service-URL**, en **SAML entiteit-ID** naar [ Client-ondersteuningsteam kruipen dicht](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="0b71c-168">To configure single sign-on on Huddle side, you need to send the downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** to [Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="0b71c-169">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="0b71c-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="0b71c-170">Eenmalige aanmelding moet worden ingeschakeld door het ondersteuningsteam kruipen dicht.</span><span class="sxs-lookup"><span data-stu-id="0b71c-170">Single sign-on needs to be enabled by the Huddle support team.</span></span> <span data-ttu-id="0b71c-171">U krijgt een melding wanneer de configuratie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="0b71c-171">You get a notification when the configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="0b71c-172">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="0b71c-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0b71c-173">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="0b71c-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0b71c-174">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0b71c-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0b71c-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="0b71c-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="0b71c-176">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0b71c-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="0b71c-178">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0b71c-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0b71c-179">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0b71c-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0b71c-181">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="0b71c-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0b71c-183">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0b71c-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0b71c-185">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="0b71c-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0b71c-187">a.</span><span class="sxs-lookup"><span data-stu-id="0b71c-187">a.</span></span> <span data-ttu-id="0b71c-188">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0b71c-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0b71c-189">b.</span><span class="sxs-lookup"><span data-stu-id="0b71c-189">b.</span></span> <span data-ttu-id="0b71c-190">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0b71c-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0b71c-191">c.</span><span class="sxs-lookup"><span data-stu-id="0b71c-191">c.</span></span> <span data-ttu-id="0b71c-192">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="0b71c-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0b71c-193">d.</span><span class="sxs-lookup"><span data-stu-id="0b71c-193">d.</span></span> <span data-ttu-id="0b71c-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0b71c-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="0b71c-195">Een testgebruiker kruipen dicht maken</span><span class="sxs-lookup"><span data-stu-id="0b71c-195">Creating a Huddle test user</span></span>

<span data-ttu-id="0b71c-196">Om Azure AD-gebruikers zich aanmelden bij kruipen dicht, moeten ze worden ingericht in kruipen dicht.</span><span class="sxs-lookup"><span data-stu-id="0b71c-196">To enable Azure AD users to log in to Huddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="0b71c-197">In het geval van kruipen dicht is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="0b71c-197">In the case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="0b71c-198">**Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0b71c-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="0b71c-199">Meld u aan bij uw **kruipen dicht** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="0b71c-199">Log in to your **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="0b71c-200">Klik op **werkruimte**.</span><span class="sxs-lookup"><span data-stu-id="0b71c-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="0b71c-201">Klik op **mensen \> personen uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="0b71c-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="0b71c-202">![Mensen](./media/active-directory-saas-huddle-tutorial/IC787838.png "personen")</span><span class="sxs-lookup"><span data-stu-id="0b71c-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="0b71c-203">In de **maken van een nieuwe uitnodiging** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="0b71c-203">In the **Create a new invitation** section, perform the following steps:</span></span>
   
   <span data-ttu-id="0b71c-204">![Nieuwe uitnodiging](./media/active-directory-saas-huddle-tutorial/IC787839.png "nieuwe uitnodiging")</span><span class="sxs-lookup"><span data-stu-id="0b71c-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="0b71c-205">a.</span><span class="sxs-lookup"><span data-stu-id="0b71c-205">a.</span></span> <span data-ttu-id="0b71c-206">In de **personen uitnodigen voor lid worden van een team kiezen** selecteert **team**.</span><span class="sxs-lookup"><span data-stu-id="0b71c-206">In the **Choose a team to invite people to join** list, select **team**.</span></span>

   <span data-ttu-id="0b71c-207">b.</span><span class="sxs-lookup"><span data-stu-id="0b71c-207">b.</span></span> <span data-ttu-id="0b71c-208">Typ de **e-mailadres** van een geldig Azure AD-account die u inrichten wilt **Enter e-mailadres voor mensen die u wilt uitnodigen** textbox.</span><span class="sxs-lookup"><span data-stu-id="0b71c-208">Type the **Email Address** of a valid Azure AD account you want to provision in to **Enter email address for people you'd like to invite** textbox.</span></span>

   <span data-ttu-id="0b71c-209">c.</span><span class="sxs-lookup"><span data-stu-id="0b71c-209">c.</span></span> <span data-ttu-id="0b71c-210">Klik op **uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="0b71c-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="0b71c-211">De accounthouder Azure AD ontvangt een e-mailbericht met inbegrip van een koppeling om te bevestigen van het account voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="0b71c-211">The Azure AD account holder will receive an email including a link to confirm the account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="0b71c-212">U kunt geen andere kruipen dicht gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door kruipen dicht gebruiken voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="0b71c-212">You can use any other Huddle user account creation tools or APIs provided by Huddle to provision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0b71c-213">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b71c-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0b71c-214">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen kruipen dicht.</span><span class="sxs-lookup"><span data-stu-id="0b71c-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Huddle.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="0b71c-216">**Britta Simon om aan te wijzen kruipen dicht, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0b71c-216">**To assign Britta Simon to Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="0b71c-217">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0b71c-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="0b71c-219">Selecteer in de lijst met toepassingen **kruipen dicht**.</span><span class="sxs-lookup"><span data-stu-id="0b71c-219">In the applications list, select **Huddle**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="0b71c-221">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="0b71c-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="0b71c-223">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="0b71c-223">Click **Add** button.</span></span> <span data-ttu-id="0b71c-224">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0b71c-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="0b71c-226">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="0b71c-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0b71c-227">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0b71c-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0b71c-228">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0b71c-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0b71c-229">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0b71c-229">Testing single sign-on</span></span>

<span data-ttu-id="0b71c-230">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="0b71c-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0b71c-231">Als u op de tegel kruipen dicht in het deelvenster toegang, moet u de aanmeldingspagina van kruipen dicht toepassing automatisch ophalen.</span><span class="sxs-lookup"><span data-stu-id="0b71c-231">When you click the Huddle tile in the Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="0b71c-232">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0b71c-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0b71c-233">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="0b71c-233">Additional resources</span></span>

* [<span data-ttu-id="0b71c-234">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0b71c-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0b71c-235">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0b71c-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
