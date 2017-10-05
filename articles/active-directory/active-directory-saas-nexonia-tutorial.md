---
title: 'Zelfstudie: Azure Active Directory-integratie met Nexonia | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Nexonia.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/1/2017
ms.author: jeedes
ms.openlocfilehash: 1370fa64c2ddc25d3121c567ceea4828b1e50921
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="ddd7b-103">Zelfstudie: Azure Active Directory-integratie met Nexonia</span><span class="sxs-lookup"><span data-stu-id="ddd7b-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="ddd7b-104">In deze zelfstudie leert u hoe Nexonia integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ddd7b-104">In this tutorial, you learn how to integrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ddd7b-105">Nexonia integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="ddd7b-105">Integrating Nexonia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ddd7b-106">U kunt beheren in Azure AD die toegang tot Nexonia heeft</span><span class="sxs-lookup"><span data-stu-id="ddd7b-106">You can control in Azure AD who has access to Nexonia</span></span>
- <span data-ttu-id="ddd7b-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Nexonia (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="ddd7b-107">You can enable your users to automatically get signed-on to Nexonia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ddd7b-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="ddd7b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ddd7b-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, zien.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="ddd7b-110">[Wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ddd7b-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddd7b-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ddd7b-111">Prerequisites</span></span>

<span data-ttu-id="ddd7b-112">Voor het configureren van Azure AD-integratie met Nexonia, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="ddd7b-112">To configure Azure AD integration with Nexonia, you need the following items:</span></span>

- <span data-ttu-id="ddd7b-113">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="ddd7b-113">An Azure AD subscription</span></span>
- <span data-ttu-id="ddd7b-114">Een Nexonia eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="ddd7b-114">A Nexonia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ddd7b-115">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ddd7b-116">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="ddd7b-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ddd7b-117">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ddd7b-118">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ddd7b-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ddd7b-119">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="ddd7b-119">Scenario description</span></span>
<span data-ttu-id="ddd7b-120">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ddd7b-121">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="ddd7b-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ddd7b-122">Nexonia uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ddd7b-122">Adding Nexonia from the gallery</span></span>
2. <span data-ttu-id="ddd7b-123">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ddd7b-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nexonia-from-the-gallery"></a><span data-ttu-id="ddd7b-124">Nexonia uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="ddd7b-124">Adding Nexonia from the gallery</span></span>
<span data-ttu-id="ddd7b-125">Voor het configureren van de integratie van Nexonia in Azure AD, moet u Nexonia uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-125">To configure the integration of Nexonia into Azure AD, you need to add Nexonia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ddd7b-126">**Als u wilt toevoegen Nexonia uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ddd7b-126">**To add Nexonia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ddd7b-127">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ddd7b-129">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ddd7b-130">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-130">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="ddd7b-132">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="ddd7b-134">Typ in het zoekvak **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-134">In the search box, type **Nexonia**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_search.png)

5. <span data-ttu-id="ddd7b-136">Selecteer in het deelvenster resultaten **Nexonia**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-136">In the results panel, select **Nexonia**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ddd7b-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ddd7b-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ddd7b-139">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Nexonia op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="ddd7b-139">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ddd7b-140">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Nexonia is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Nexonia is to a user in Azure AD.</span></span> <span data-ttu-id="ddd7b-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Nexonia tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-141">In other words, a link relationship between an Azure AD user and the related user in Nexonia needs to be established.</span></span>

<span data-ttu-id="ddd7b-142">Wijs in Nexonia, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-142">In Nexonia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ddd7b-143">Om te configureren en testen van Azure AD eenmalige aanmelding met Nexonia, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="ddd7b-143">To configure and test Azure AD single sign-on with Nexonia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ddd7b-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ddd7b-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ddd7b-146">**[Maken van een testgebruiker Nexonia](#creating-a-nexonia-test-user)**  - Nexonia die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-146">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - to have a counterpart of Britta Simon in Nexonia that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ddd7b-147">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ddd7b-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ddd7b-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="ddd7b-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ddd7b-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Nexonia configureren.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nexonia application.</span></span>

>[!Note]
><span data-ttu-id="ddd7b-151">Als u problemen bij de integratie hebt en Raadpleeg dit [koppeling](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) voor het oplossen.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-151">If you have issues in the integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) for troubleshooting guide.</span></span> <span data-ttu-id="ddd7b-152">Als u nog steeds niet de oplossing hebt gevonden, kunt u de ondersteuningsaanvraag vanuit Azure-portal te verhogen.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-152">If you still have not found the solution, then raise the support request from Azure portal.</span></span>

<span data-ttu-id="ddd7b-153">**Voor het configureren van Azure AD eenmalige aanmelding met Nexonia, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ddd7b-153">**To configure Azure AD single sign-on with Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="ddd7b-154">In de Azure-portal op de **Nexonia** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-154">In the Azure portal, on the **Nexonia** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="ddd7b-156">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-156">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_samlbase.png)

3. <span data-ttu-id="ddd7b-158">Op de **Nexonia domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ddd7b-158">On the **Nexonia Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_url.png)

    <span data-ttu-id="ddd7b-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span><span class="sxs-lookup"><span data-stu-id="ddd7b-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ddd7b-161">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-161">This value is not real.</span></span> <span data-ttu-id="ddd7b-162">Deze waarde bijwerken met de werkelijke antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-162">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="ddd7b-163">Neem contact op met [Nexonia ondersteuningsteam](https://nexonia.zendesk.com/hc/requests/new) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to get this value.</span></span> 


4. <span data-ttu-id="ddd7b-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_certificate.png) 

5. <span data-ttu-id="ddd7b-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-nexonia-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ddd7b-168">Op de **Nexonia configuratie** sectie, klikt u op **configureren Nexonia** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-168">On the **Nexonia Configuration** section, click **Configure Nexonia** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ddd7b-169">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="ddd7b-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_configure.png) 

7. <span data-ttu-id="ddd7b-171">Als u eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, neem contact op met [Nexonia ondersteuningsteam](https://nexonia.zendesk.com/hc/requests/new) en geeft u het volgende:</span><span class="sxs-lookup"><span data-stu-id="ddd7b-171">To get SSO configured for your application, contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) and provide them with the following:</span></span>

    <span data-ttu-id="ddd7b-172">• De gedownloade **certificaat**</span><span class="sxs-lookup"><span data-stu-id="ddd7b-172">• The downloaded **certificate**</span></span>

    <span data-ttu-id="ddd7b-173">• De **SAML entiteit-ID**</span><span class="sxs-lookup"><span data-stu-id="ddd7b-173">• The **SAML Entity ID**</span></span>

    <span data-ttu-id="ddd7b-174">• De **URL voor SAML-Service voor eenmalige aanmelding**</span><span class="sxs-lookup"><span data-stu-id="ddd7b-174">• The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="ddd7b-175">• De **afmelden URL**</span><span class="sxs-lookup"><span data-stu-id="ddd7b-175">• The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="ddd7b-176">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="ddd7b-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ddd7b-177">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ddd7b-178">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ddd7b-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ddd7b-179">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ddd7b-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="ddd7b-180">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="ddd7b-182">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ddd7b-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ddd7b-183">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-nexonia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ddd7b-185">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-nexonia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ddd7b-187">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-nexonia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ddd7b-189">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ddd7b-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-nexonia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ddd7b-191">a.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-191">a.</span></span> <span data-ttu-id="ddd7b-192">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ddd7b-193">b.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-193">b.</span></span> <span data-ttu-id="ddd7b-194">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ddd7b-195">c.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-195">c.</span></span> <span data-ttu-id="ddd7b-196">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ddd7b-197">d.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-197">d.</span></span> <span data-ttu-id="ddd7b-198">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-198">Click **Create**.</span></span>
 
### <a name="creating-a-nexonia-test-user"></a><span data-ttu-id="ddd7b-199">Een testgebruiker Nexonia maken</span><span class="sxs-lookup"><span data-stu-id="ddd7b-199">Creating a Nexonia test user</span></span>

<span data-ttu-id="ddd7b-200">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Nexonia maken.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-200">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="ddd7b-201">Werken met [Nexonia ondersteuningsteam](https://nexonia.zendesk.com/hc/requests/new) de gebruikers van het platform Nexonia toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-201">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to add the users in the Nexonia platform.</span></span> <span data-ttu-id="ddd7b-202">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-202">Users must be created and activated before you use single sign-on.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ddd7b-203">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddd7b-203">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ddd7b-204">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Nexonia.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nexonia.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="ddd7b-206">**Britta Simon om aan te wijzen Nexonia, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="ddd7b-206">**To assign Britta Simon to Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="ddd7b-207">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="ddd7b-209">Selecteer in de lijst met toepassingen **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-209">In the applications list, select **Nexonia**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_app.png) 

3. <span data-ttu-id="ddd7b-211">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-211">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="ddd7b-213">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-213">Click **Add** button.</span></span> <span data-ttu-id="ddd7b-214">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="ddd7b-216">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ddd7b-217">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ddd7b-218">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ddd7b-219">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="ddd7b-219">Testing single sign-on</span></span>

<span data-ttu-id="ddd7b-220">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ddd7b-221">Als u op de tegel Nexonia in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Nexonia.</span><span class="sxs-lookup"><span data-stu-id="ddd7b-221">When you click the Nexonia tile in the Access Panel, you should get automatically signed-on to your Nexonia application.</span></span>
<span data-ttu-id="ddd7b-222">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="ddd7b-222">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ddd7b-223">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ddd7b-223">Additional resources</span></span>

* [<span data-ttu-id="ddd7b-224">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ddd7b-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ddd7b-225">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ddd7b-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_203.png

