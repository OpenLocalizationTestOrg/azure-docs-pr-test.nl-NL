---
title: 'Zelfstudie: Azure Active Directory-integratie met Kiteworks | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Kiteworks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 2fd9b346cb6d838069ef94ee9c2a8d113f22779c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="a6c6d-103">Zelfstudie: Azure Active Directory-integratie met Kiteworks</span><span class="sxs-lookup"><span data-stu-id="a6c6d-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>

<span data-ttu-id="a6c6d-104">In deze zelfstudie leert u hoe Kiteworks integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a6c6d-104">In this tutorial, you learn how to integrate Kiteworks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a6c6d-105">Kiteworks integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a6c6d-105">Integrating Kiteworks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a6c6d-106">U kunt beheren in Azure AD die toegang tot Kiteworks heeft</span><span class="sxs-lookup"><span data-stu-id="a6c6d-106">You can control in Azure AD who has access to Kiteworks</span></span>
- <span data-ttu-id="a6c6d-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Kiteworks (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="a6c6d-107">You can enable your users to automatically get signed-on to Kiteworks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a6c6d-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="a6c6d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a6c6d-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a6c6d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6c6d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a6c6d-110">Prerequisites</span></span>

<span data-ttu-id="a6c6d-111">Voor het configureren van Azure AD-integratie met Kiteworks, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="a6c6d-111">To configure Azure AD integration with Kiteworks, you need the following items:</span></span>

- <span data-ttu-id="a6c6d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a6c6d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a6c6d-113">Een Kiteworks eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a6c6d-113">A Kiteworks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a6c6d-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a6c6d-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a6c6d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a6c6d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a6c6d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a6c6d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a6c6d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a6c6d-118">Scenario description</span></span>
<span data-ttu-id="a6c6d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a6c6d-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a6c6d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a6c6d-121">Kiteworks uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="a6c6d-121">Adding Kiteworks from the gallery</span></span>
2. <span data-ttu-id="a6c6d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a6c6d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kiteworks-from-the-gallery"></a><span data-ttu-id="a6c6d-123">Kiteworks uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="a6c6d-123">Adding Kiteworks from the gallery</span></span>
<span data-ttu-id="a6c6d-124">Voor het configureren van de integratie van Kiteworks in Azure AD, moet u Kiteworks uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-124">To configure the integration of Kiteworks into Azure AD, you need to add Kiteworks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a6c6d-125">**Als u wilt toevoegen Kiteworks uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a6c6d-125">**To add Kiteworks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a6c6d-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a6c6d-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a6c6d-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a6c6d-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a6c6d-133">Typ in het zoekvak **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-133">In the search box, type **Kiteworks**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_search.png)

5. <span data-ttu-id="a6c6d-135">Selecteer in het deelvenster resultaten **Kiteworks**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-135">In the results panel, select **Kiteworks**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a6c6d-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a6c6d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a6c6d-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Kiteworks op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a6c6d-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Kiteworks is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kiteworks is to a user in Azure AD.</span></span> <span data-ttu-id="a6c6d-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Kiteworks tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-140">In other words, a link relationship between an Azure AD user and the related user in Kiteworks needs to be established.</span></span>

<span data-ttu-id="a6c6d-141">Wijs in Kiteworks, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-141">In Kiteworks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a6c6d-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Kiteworks, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="a6c6d-142">To configure and test Azure AD single sign-on with Kiteworks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a6c6d-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a6c6d-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a6c6d-145">**[Maken van een testgebruiker Kiteworks](#creating-a-kiteworks-test-user)**  - Kiteworks die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - to have a counterpart of Britta Simon in Kiteworks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a6c6d-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a6c6d-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a6c6d-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a6c6d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a6c6d-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Kiteworks configureren.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kiteworks application.</span></span>

<span data-ttu-id="a6c6d-150">**Voor het configureren van Azure AD eenmalige aanmelding met Kiteworks, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a6c6d-150">**To configure Azure AD single sign-on with Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="a6c6d-151">In de Azure-portal op de **Kiteworks** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-151">In the Azure portal, on the **Kiteworks** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a6c6d-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

3. <span data-ttu-id="a6c6d-155">Op de **Kiteworks domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a6c6d-155">On the **Kiteworks Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_url.png)

    <span data-ttu-id="a6c6d-157">a.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-157">a.</span></span> <span data-ttu-id="a6c6d-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.kiteworks.com`</span><span class="sxs-lookup"><span data-stu-id="a6c6d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com`</span></span>

    <span data-ttu-id="a6c6d-159">b.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-159">b.</span></span> <span data-ttu-id="a6c6d-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span><span class="sxs-lookup"><span data-stu-id="a6c6d-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a6c6d-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-161">These values are not real.</span></span> <span data-ttu-id="a6c6d-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a6c6d-163">Neem contact op met [Kiteworks Client ondersteuningsteam](http://accellion.com/support) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-163">Contact [Kiteworks Client support team](http://accellion.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="a6c6d-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

5. <span data-ttu-id="a6c6d-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kiteworks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a6c6d-168">Op de **Kiteworks configuratie** sectie, klikt u op **configureren Kiteworks** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-168">On the **Kiteworks Configuration** section, click **Configure Kiteworks** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a6c6d-169">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="a6c6d-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_configure.png) 

7. <span data-ttu-id="a6c6d-171">Meld u op met uw bedrijf Kiteworks site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-171">Sign on to your Kiteworks company site as an administrator.</span></span>

8. <span data-ttu-id="a6c6d-172">Klik in de werkbalk bovenaan op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-172">In the toolbar on the top, click **Settings**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 

9. <span data-ttu-id="a6c6d-174">In de **verificatie en autorisatie** sectie, klikt u op **SSO Setup**.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-174">In the **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png)
 
10. <span data-ttu-id="a6c6d-176">Voer de volgende stappen uit op de installatiepagina van eenmalige aanmelding:</span><span class="sxs-lookup"><span data-stu-id="a6c6d-176">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   

    <span data-ttu-id="a6c6d-178">a.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-178">a.</span></span> <span data-ttu-id="a6c6d-179">Selecteer **verifiëren via eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-179">Select **Authenticate via SSO**.</span></span>

    <span data-ttu-id="a6c6d-180">b.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-180">b.</span></span> <span data-ttu-id="a6c6d-181">Selecteer **AuthnRequest initiëren**.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-181">Select **Initiate AuthnRequest**.</span></span>

    <span data-ttu-id="a6c6d-182">c.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-182">c.</span></span> <span data-ttu-id="a6c6d-183">In de **IDP entiteit-ID** textbox, plak de waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="a6c6d-184">d.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-184">d.</span></span> <span data-ttu-id="a6c6d-185">In de **Single Sign-On Service-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-185">In the **Single Sign-On Service URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a6c6d-186">e.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-186">e.</span></span> <span data-ttu-id="a6c6d-187">In de **Service-URL met eenmalige afmelding** textbox, plak de waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-187">In the **Single Logout Service URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a6c6d-188">f.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-188">f.</span></span> <span data-ttu-id="a6c6d-189">Open uw gedownloade certificaat in Kladblok, Kopieer de inhoud en plakt u deze in de **RSA-certificaat voor openbare sleutel** textbox.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-189">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **RSA Public Key Certificate** textbox.</span></span>
 
    <span data-ttu-id="a6c6d-190">g.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-190">g.</span></span> <span data-ttu-id="a6c6d-191">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a6c6d-192">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="a6c6d-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a6c6d-193">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a6c6d-194">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a6c6d-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a6c6d-195">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a6c6d-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="a6c6d-196">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a6c6d-198">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a6c6d-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a6c6d-199">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a6c6d-201">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a6c6d-203">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a6c6d-205">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a6c6d-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a6c6d-207">a.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-207">a.</span></span> <span data-ttu-id="a6c6d-208">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a6c6d-209">b.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-209">b.</span></span> <span data-ttu-id="a6c6d-210">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a6c6d-211">c.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-211">c.</span></span> <span data-ttu-id="a6c6d-212">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a6c6d-213">d.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-213">d.</span></span> <span data-ttu-id="a6c6d-214">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-214">Click **Create**.</span></span>
 
### <a name="creating-a-kiteworks-test-user"></a><span data-ttu-id="a6c6d-215">Een testgebruiker Kiteworks maken</span><span class="sxs-lookup"><span data-stu-id="a6c6d-215">Creating a Kiteworks test user</span></span>

<span data-ttu-id="a6c6d-216">Het doel van deze sectie is het maken van een gebruiker Britta Simon in Kiteworks genoemd.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-216">The objective of this section is to create a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="a6c6d-217">Kiteworks ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="a6c6d-218">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-218">There is no action item for you in this section.</span></span> <span data-ttu-id="a6c6d-219">Een nieuwe gebruiker is gemaakt tijdens een poging tot toegang tot Kitewors als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-219">A new user is created during an attempt to access Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="a6c6d-220">Als u een gebruiker handmatig maken wilt, moet u contact op met de [Kiteworks ondersteuningsteam](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="a6c6d-220">If you need to create a user manually, you need to contact the [Kiteworks support team](http://accellion.com/support).</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a6c6d-221">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6c6d-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a6c6d-222">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kiteworks.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a6c6d-224">**Britta Simon om aan te wijzen Kiteworks, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a6c6d-224">**To assign Britta Simon to Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="a6c6d-225">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a6c6d-227">Selecteer in de lijst met toepassingen **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-227">In the applications list, select **Kiteworks**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_app.png) 

3. <span data-ttu-id="a6c6d-229">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a6c6d-231">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-231">Click **Add** button.</span></span> <span data-ttu-id="a6c6d-232">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a6c6d-234">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a6c6d-235">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a6c6d-236">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a6c6d-237">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a6c6d-237">Testing single sign-on</span></span>

<span data-ttu-id="a6c6d-238">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-238">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="a6c6d-239">Als u op de tegel Kiteworks in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="a6c6d-239">When you click the Kiteworks tile in the Access Panel, you should get automatically signed-on to your Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a6c6d-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a6c6d-240">Additional resources</span></span>

* [<span data-ttu-id="a6c6d-241">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6c6d-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a6c6d-242">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a6c6d-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png

