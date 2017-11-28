---
title: 'Zelfstudie: Azure Active Directory-integratie met CompetencyIQ | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en CompetencyIQ.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e262bf7e-cc7d-4d0e-aea7-861f00d8837d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: ad3cec3de9034ddab2161952620d31540ae51978
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-competencyiq"></a><span data-ttu-id="78f9f-103">Zelfstudie: Azure Active Directory-integratie met CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="78f9f-103">Tutorial: Azure Active Directory integration with CompetencyIQ</span></span>

<span data-ttu-id="78f9f-104">In deze zelfstudie leert u hoe CompetencyIQ integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="78f9f-104">In this tutorial, you learn how to integrate CompetencyIQ with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="78f9f-105">CompetencyIQ integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="78f9f-105">Integrating CompetencyIQ with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="78f9f-106">U kunt beheren in Azure AD die toegang tot CompetencyIQ heeft</span><span class="sxs-lookup"><span data-stu-id="78f9f-106">You can control in Azure AD who has access to CompetencyIQ</span></span>
- <span data-ttu-id="78f9f-107">U kunt uw gebruikers automatisch ophalen aangemeld bij CompetencyIQ (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="78f9f-107">You can enable your users to automatically get signed-on to CompetencyIQ (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="78f9f-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="78f9f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="78f9f-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="78f9f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78f9f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="78f9f-110">Prerequisites</span></span>

<span data-ttu-id="78f9f-111">Voor het configureren van Azure AD-integratie met CompetencyIQ, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="78f9f-111">To configure Azure AD integration with CompetencyIQ, you need the following items:</span></span>

- <span data-ttu-id="78f9f-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="78f9f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="78f9f-113">Een CompetencyIQ eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="78f9f-113">A CompetencyIQ single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="78f9f-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="78f9f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="78f9f-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="78f9f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="78f9f-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="78f9f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="78f9f-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78f9f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="78f9f-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="78f9f-118">Scenario description</span></span>
<span data-ttu-id="78f9f-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="78f9f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="78f9f-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="78f9f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="78f9f-121">CompetencyIQ uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="78f9f-121">Adding CompetencyIQ from the gallery</span></span>
2. <span data-ttu-id="78f9f-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="78f9f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-competencyiq-from-the-gallery"></a><span data-ttu-id="78f9f-123">CompetencyIQ uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="78f9f-123">Adding CompetencyIQ from the gallery</span></span>
<span data-ttu-id="78f9f-124">Voor het configureren van de integratie van CompetencyIQ in Azure AD, moet u CompetencyIQ uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="78f9f-124">To configure the integration of CompetencyIQ into Azure AD, you need to add CompetencyIQ from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="78f9f-125">**Als u wilt toevoegen CompetencyIQ uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="78f9f-125">**To add CompetencyIQ from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="78f9f-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="78f9f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="78f9f-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="78f9f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="78f9f-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="78f9f-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="78f9f-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="78f9f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="78f9f-133">Typ in het zoekvak **CompetencyIQ**.</span><span class="sxs-lookup"><span data-stu-id="78f9f-133">In the search box, type **CompetencyIQ**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_search.png)

5. <span data-ttu-id="78f9f-135">Selecteer in het deelvenster resultaten **CompetencyIQ**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="78f9f-135">In the results panel, select **CompetencyIQ**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="78f9f-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="78f9f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="78f9f-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met CompetencyIQ op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="78f9f-138">In this section, you configure and test Azure AD single sign-on with CompetencyIQ based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="78f9f-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in CompetencyIQ is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78f9f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CompetencyIQ is to a user in Azure AD.</span></span> <span data-ttu-id="78f9f-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in CompetencyIQ tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="78f9f-140">In other words, a link relationship between an Azure AD user and the related user in CompetencyIQ needs to be established.</span></span>

<span data-ttu-id="78f9f-141">Wijs in CompetencyIQ, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="78f9f-141">In CompetencyIQ, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="78f9f-142">Om te configureren en testen van Azure AD eenmalige aanmelding met CompetencyIQ, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="78f9f-142">To configure and test Azure AD single sign-on with CompetencyIQ, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="78f9f-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="78f9f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="78f9f-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="78f9f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="78f9f-145">**[Maken van een testgebruiker CompetencyIQ](#creating-a-competencyiq-test-user)**  - CompetencyIQ die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="78f9f-145">**[Creating a CompetencyIQ test user](#creating-a-competencyiq-test-user)** - to have a counterpart of Britta Simon in CompetencyIQ that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="78f9f-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="78f9f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="78f9f-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="78f9f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="78f9f-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="78f9f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="78f9f-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing CompetencyIQ configureren.</span><span class="sxs-lookup"><span data-stu-id="78f9f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CompetencyIQ application.</span></span>

<span data-ttu-id="78f9f-150">**Voor het configureren van Azure AD eenmalige aanmelding met CompetencyIQ, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="78f9f-150">**To configure Azure AD single sign-on with CompetencyIQ, perform the following steps:**</span></span>

1. <span data-ttu-id="78f9f-151">In de Azure-portal op de **CompetencyIQ** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="78f9f-151">In the Azure portal, on the **CompetencyIQ** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="78f9f-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="78f9f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_samlbase.png)

3. <span data-ttu-id="78f9f-155">Op de **CompetencyIQ domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="78f9f-155">On the **CompetencyIQ Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_url1.png)

    <span data-ttu-id="78f9f-157">a.</span><span class="sxs-lookup"><span data-stu-id="78f9f-157">a.</span></span> <span data-ttu-id="78f9f-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<customer>.competencyiq.com/`</span><span class="sxs-lookup"><span data-stu-id="78f9f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<customer>.competencyiq.com/`</span></span>
    
    <span data-ttu-id="78f9f-159">b.</span><span class="sxs-lookup"><span data-stu-id="78f9f-159">b.</span></span> <span data-ttu-id="78f9f-160">In de **id** textbox, typ de URL:`https://www.competencyiq.com/`</span><span class="sxs-lookup"><span data-stu-id="78f9f-160">In the **Identifier** textbox, type the URL: `https://www.competencyiq.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="78f9f-161">De waarde van de aanmeldings-URL is niet echt dus bijwerken dit met de werkelijke aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="78f9f-161">The Sign-on URL value is not real so update this with actual Sign-On URL.</span></span> <span data-ttu-id="78f9f-162">Neem contact op met [CompetencyIQ Client ondersteuningsteam](https://www.competencyiq.com/) om dit.</span><span class="sxs-lookup"><span data-stu-id="78f9f-162">Contact [CompetencyIQ Client support team](https://www.competencyiq.com/) to get this.</span></span> 
 
4. <span data-ttu-id="78f9f-163">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="78f9f-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_certificate.png) 

5. <span data-ttu-id="78f9f-165">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="78f9f-165">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-competencyiq-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="78f9f-167">Op de **CompetencyIQ configuratie** sectie, klikt u op **configureren CompetencyIQ** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="78f9f-167">On the **CompetencyIQ Configuration** section, click **Configure CompetencyIQ** to open **Configure sign-on** window.</span></span> <span data-ttu-id="78f9f-168">Kopieer de **SAML entiteit-ID**, en **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="78f9f-168">Copy the **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_configure.png) 

7. <span data-ttu-id="78f9f-170">Eenmalige aanmelding configureren op **CompetencyIQ** zijde, moet u de gedownloade verzenden **Metadata XML**, **SAML entiteit-ID** en **SAML Single Sign-On-Service URL** naar [CompetencyIQ ondersteuningsteam](https://www.competencyiq.com/).</span><span class="sxs-lookup"><span data-stu-id="78f9f-170">To configure single sign-on on **CompetencyIQ** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [CompetencyIQ support team](https://www.competencyiq.com/).</span></span> <span data-ttu-id="78f9f-171">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="78f9f-171">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="78f9f-172">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="78f9f-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="78f9f-173">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="78f9f-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="78f9f-174">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="78f9f-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="78f9f-175">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="78f9f-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="78f9f-176">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="78f9f-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="78f9f-178">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="78f9f-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="78f9f-179">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="78f9f-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="78f9f-181">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="78f9f-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="78f9f-183">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="78f9f-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="78f9f-185">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="78f9f-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="78f9f-187">a.</span><span class="sxs-lookup"><span data-stu-id="78f9f-187">a.</span></span> <span data-ttu-id="78f9f-188">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="78f9f-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="78f9f-189">b.</span><span class="sxs-lookup"><span data-stu-id="78f9f-189">b.</span></span> <span data-ttu-id="78f9f-190">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="78f9f-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="78f9f-191">c.</span><span class="sxs-lookup"><span data-stu-id="78f9f-191">c.</span></span> <span data-ttu-id="78f9f-192">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="78f9f-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="78f9f-193">d.</span><span class="sxs-lookup"><span data-stu-id="78f9f-193">d.</span></span> <span data-ttu-id="78f9f-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="78f9f-194">Click **Create**.</span></span>
 
### <a name="creating-a-competencyiq-test-user"></a><span data-ttu-id="78f9f-195">Een testgebruiker CompetencyIQ maken</span><span class="sxs-lookup"><span data-stu-id="78f9f-195">Creating a CompetencyIQ test user</span></span>

<span data-ttu-id="78f9f-196">Om Azure AD-gebruikers zich aanmelden bij CompetencyIQ, moeten ze worden ingericht in CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="78f9f-196">To enable Azure AD users to log in to CompetencyIQ, they must be provisioned into CompetencyIQ.</span></span> <span data-ttu-id="78f9f-197">Neem contact op met [CompetencyIQ ondersteuningsteam](https://www.competencyiq.com/) om gebruikers te maken in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="78f9f-197">Contact [CompetencyIQ support team](https://www.competencyiq.com/) to create users in the application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="78f9f-198">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="78f9f-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="78f9f-199">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="78f9f-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CompetencyIQ.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="78f9f-201">**Britta Simon om aan te wijzen CompetencyIQ, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="78f9f-201">**To assign Britta Simon to CompetencyIQ, perform the following steps:**</span></span>

1. <span data-ttu-id="78f9f-202">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="78f9f-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="78f9f-204">Selecteer in de lijst met toepassingen **CompetencyIQ**.</span><span class="sxs-lookup"><span data-stu-id="78f9f-204">In the applications list, select **CompetencyIQ**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_app.png) 

3. <span data-ttu-id="78f9f-206">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="78f9f-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="78f9f-208">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="78f9f-208">Click **Add** button.</span></span> <span data-ttu-id="78f9f-209">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="78f9f-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="78f9f-211">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="78f9f-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="78f9f-212">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="78f9f-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="78f9f-213">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="78f9f-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="78f9f-214">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="78f9f-214">Testing single sign-on</span></span>

<span data-ttu-id="78f9f-215">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="78f9f-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="78f9f-216">Als u op de tegel CompetencyIQ in het deelvenster toegang, moet u automatisch worden geregistreerd in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="78f9f-216">When you click the CompetencyIQ tile in the Access Panel, you should get automatically logged into the application.</span></span>
<span data-ttu-id="78f9f-217">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="78f9f-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="78f9f-218">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="78f9f-218">Additional resources</span></span>

* [<span data-ttu-id="78f9f-219">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78f9f-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="78f9f-220">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="78f9f-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_203.png

