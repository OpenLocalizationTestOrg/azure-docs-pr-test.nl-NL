---
title: 'Zelfstudie: Azure Active Directory-integratie met Freshservice | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Freshservice.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d32775fa91d3a49da1ef55e57d1d38990fa09346
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="63072-103">Zelfstudie: Azure Active Directory-integratie met Freshservice</span><span class="sxs-lookup"><span data-stu-id="63072-103">Tutorial: Azure Active Directory integration with Freshservice</span></span>

<span data-ttu-id="63072-104">In deze zelfstudie leert u hoe Freshservice integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="63072-104">In this tutorial, you learn how to integrate Freshservice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="63072-105">Freshservice integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="63072-105">Integrating Freshservice with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="63072-106">U kunt beheren in Azure AD die toegang tot Freshservice heeft</span><span class="sxs-lookup"><span data-stu-id="63072-106">You can control in Azure AD who has access to Freshservice</span></span>
- <span data-ttu-id="63072-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Freshservice (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="63072-107">You can enable your users to automatically get signed-on to Freshservice (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="63072-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="63072-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="63072-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="63072-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63072-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="63072-110">Prerequisites</span></span>

<span data-ttu-id="63072-111">Voor het configureren van Azure AD-integratie met Freshservice, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="63072-111">To configure Azure AD integration with Freshservice, you need the following items:</span></span>

- <span data-ttu-id="63072-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="63072-112">An Azure AD subscription</span></span>
- <span data-ttu-id="63072-113">Een Freshservice eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="63072-113">A Freshservice single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="63072-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="63072-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="63072-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="63072-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="63072-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="63072-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="63072-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="63072-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="63072-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="63072-118">Scenario description</span></span>
<span data-ttu-id="63072-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="63072-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="63072-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="63072-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="63072-121">Freshservice uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="63072-121">Adding Freshservice from the gallery</span></span>
2. <span data-ttu-id="63072-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="63072-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshservice-from-the-gallery"></a><span data-ttu-id="63072-123">Freshservice uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="63072-123">Adding Freshservice from the gallery</span></span>
<span data-ttu-id="63072-124">Voor het configureren van de integratie van Freshservice in Azure AD, moet u Freshservice uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="63072-124">To configure the integration of Freshservice into Azure AD, you need to add Freshservice from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="63072-125">**Als u wilt toevoegen Freshservice uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="63072-125">**To add Freshservice from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="63072-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="63072-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="63072-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="63072-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="63072-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="63072-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="63072-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="63072-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="63072-133">Typ in het zoekvak **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="63072-133">In the search box, type **Freshservice**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. <span data-ttu-id="63072-135">Selecteer in het deelvenster resultaten **Freshservice**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="63072-135">In the results panel, select **Freshservice**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="63072-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="63072-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="63072-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Freshservice op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="63072-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="63072-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Freshservice is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63072-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Freshservice is to a user in Azure AD.</span></span> <span data-ttu-id="63072-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Freshservice tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="63072-140">In other words, a link relationship between an Azure AD user and the related user in Freshservice needs to be established.</span></span>

<span data-ttu-id="63072-141">Wijs in Freshservice, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="63072-141">In Freshservice, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="63072-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Freshservice, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="63072-142">To configure and test Azure AD single sign-on with Freshservice, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="63072-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="63072-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="63072-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="63072-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="63072-145">**[Maken van een testgebruiker Freshservice](#creating-a-freshservice-test-user)**  - Freshservice die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="63072-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - to have a counterpart of Britta Simon in Freshservice that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="63072-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="63072-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="63072-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="63072-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="63072-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="63072-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="63072-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Freshservice configureren.</span><span class="sxs-lookup"><span data-stu-id="63072-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Freshservice application.</span></span>

<span data-ttu-id="63072-150">**Voor het configureren van Azure AD eenmalige aanmelding met Freshservice, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="63072-150">**To configure Azure AD single sign-on with Freshservice, perform the following steps:**</span></span>

1. <span data-ttu-id="63072-151">In de Azure-portal op de **Freshservice** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="63072-151">In the Azure portal, on the **Freshservice** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="63072-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="63072-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. <span data-ttu-id="63072-155">Op de **Freshservice domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="63072-155">On the **Freshservice Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    <span data-ttu-id="63072-157">a.</span><span class="sxs-lookup"><span data-stu-id="63072-157">a.</span></span> <span data-ttu-id="63072-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="63072-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<democompany>.freshservice.com`</span></span>

    <span data-ttu-id="63072-159">b.</span><span class="sxs-lookup"><span data-stu-id="63072-159">b.</span></span> <span data-ttu-id="63072-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="63072-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<democompany>.freshservice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="63072-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="63072-161">These values are not real.</span></span> <span data-ttu-id="63072-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="63072-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="63072-163">Neem contact op met [Freshservice Client ondersteuningsteam](https://support.freshservice.com/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="63072-163">Contact [Freshservice Client support team](https://support.freshservice.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="63072-164">Op de **SAML-certificaat voor ondertekening van** sectie, Kopieer **VINGERAFDRUK** waarde van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="63072-164">On the **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. <span data-ttu-id="63072-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="63072-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="63072-168">Op de **Freshservice configuratie** sectie, klikt u op **configureren Freshservice** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="63072-168">On the **Freshservice Configuration** section, click **Configure Freshservice** to open **Configure sign-on** window.</span></span> <span data-ttu-id="63072-169">Kopieer de **Sign-Out URL's, en SAML Single Sign-On Service** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="63072-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. <span data-ttu-id="63072-171">In een ander browservenster, meld u aan bij uw bedrijf Freshservice site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="63072-171">In a different web browser window, log in to your Freshservice company site as an administrator.</span></span>

8. <span data-ttu-id="63072-172">Klik in het menu bovenaan op **Admin**.</span><span class="sxs-lookup"><span data-stu-id="63072-172">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="63072-173">![Beheerder](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="63072-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

9. <span data-ttu-id="63072-174">In de **Customer Portal**, klikt u op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="63072-174">In the **Customer Portal**, click **Security**.</span></span>
   
    <span data-ttu-id="63072-175">![Beveiliging](./media/active-directory-saas-freshservice-tutorial/ic790815.png "beveiliging")</span><span class="sxs-lookup"><span data-stu-id="63072-175">![Security](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Security")</span></span>

10. <span data-ttu-id="63072-176">In de **beveiliging** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="63072-176">In the **Security** section, perform the following steps:</span></span>
   
    <span data-ttu-id="63072-177">![Eenmalige aanmelding](./media/active-directory-saas-freshservice-tutorial/ic790816.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="63072-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span></span>
   
    <span data-ttu-id="63072-178">a.</span><span class="sxs-lookup"><span data-stu-id="63072-178">a.</span></span> <span data-ttu-id="63072-179">Switch **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="63072-179">Switch **Single Sign On**.</span></span>

    <span data-ttu-id="63072-180">b.</span><span class="sxs-lookup"><span data-stu-id="63072-180">b.</span></span> <span data-ttu-id="63072-181">Selecteer **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="63072-181">Select **SAML SSO**.</span></span>

    <span data-ttu-id="63072-182">c.</span><span class="sxs-lookup"><span data-stu-id="63072-182">c.</span></span> <span data-ttu-id="63072-183">In de **aanmeldings-URL van SAML** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="63072-183">In the **SAML Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="63072-184">d.</span><span class="sxs-lookup"><span data-stu-id="63072-184">d.</span></span> <span data-ttu-id="63072-185">In de **afmelding URL** textbox, plak de waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="63072-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="63072-186">e.</span><span class="sxs-lookup"><span data-stu-id="63072-186">e.</span></span> <span data-ttu-id="63072-187">In **beveiliging certificaat vingerafdruk** textbox, plak de **VINGERAFDRUK** waarde van het certificaat dat u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="63072-187">In **Security Certificate Fingerprint** textbox, paste the **THUMBPRINT** value of certificate which you have copied from Azure portal.</span></span>

    <span data-ttu-id="63072-188">f.</span><span class="sxs-lookup"><span data-stu-id="63072-188">f.</span></span> <span data-ttu-id="63072-189">Klik op **opslaan**</span><span class="sxs-lookup"><span data-stu-id="63072-189">Click **Save**</span></span>
   
> [!TIP]
> <span data-ttu-id="63072-190">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="63072-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="63072-191">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="63072-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="63072-192">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="63072-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="63072-193">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="63072-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="63072-194">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="63072-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="63072-196">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="63072-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="63072-197">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="63072-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="63072-199">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="63072-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="63072-201">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="63072-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="63072-203">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="63072-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="63072-205">a.</span><span class="sxs-lookup"><span data-stu-id="63072-205">a.</span></span> <span data-ttu-id="63072-206">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="63072-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="63072-207">b.</span><span class="sxs-lookup"><span data-stu-id="63072-207">b.</span></span> <span data-ttu-id="63072-208">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="63072-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="63072-209">c.</span><span class="sxs-lookup"><span data-stu-id="63072-209">c.</span></span> <span data-ttu-id="63072-210">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="63072-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="63072-211">d.</span><span class="sxs-lookup"><span data-stu-id="63072-211">d.</span></span> <span data-ttu-id="63072-212">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="63072-212">Click **Create**.</span></span>
 
### <a name="creating-a-freshservice-test-user"></a><span data-ttu-id="63072-213">Een testgebruiker Freshservice maken</span><span class="sxs-lookup"><span data-stu-id="63072-213">Creating a Freshservice test user</span></span>

<span data-ttu-id="63072-214">Om Azure AD-gebruikers zich aanmelden bij FreshService, moeten ze worden ingericht in FreshService.</span><span class="sxs-lookup"><span data-stu-id="63072-214">To enable Azure AD users to log in to FreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="63072-215">In het geval van FreshService is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="63072-215">In the case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="63072-216">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="63072-216">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="63072-217">Meld u aan bij uw **FreshService** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="63072-217">Log in to your **FreshService** company site as an administrator.</span></span>

2. <span data-ttu-id="63072-218">Klik in het menu bovenaan op **Admin**.</span><span class="sxs-lookup"><span data-stu-id="63072-218">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="63072-219">![Beheerder](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="63072-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

3. <span data-ttu-id="63072-220">In de **Gebruikersbeheer** sectie, klikt u op **aanvragers**.</span><span class="sxs-lookup"><span data-stu-id="63072-220">In the **User Management** section, click **Requesters**.</span></span>
   
    <span data-ttu-id="63072-221">![Aanvragers](./media/active-directory-saas-freshservice-tutorial/ic790818.png "aanvragers")</span><span class="sxs-lookup"><span data-stu-id="63072-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span></span>

4. <span data-ttu-id="63072-222">Klik op **nieuwe aanvrager**.</span><span class="sxs-lookup"><span data-stu-id="63072-222">Click **New Requester**.</span></span>
   
    <span data-ttu-id="63072-223">![Nieuwe aanvragers](./media/active-directory-saas-freshservice-tutorial/ic790819.png "nieuwe aanvragers")</span><span class="sxs-lookup"><span data-stu-id="63072-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span></span>

5. <span data-ttu-id="63072-224">In de **nieuwe aanvrager** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="63072-224">In the **New Requester** section, perform the following steps:</span></span>
   
    <span data-ttu-id="63072-225">![Nieuwe aanvrager](./media/active-directory-saas-freshservice-tutorial/ic790820.png "nieuwe aanvrager")</span><span class="sxs-lookup"><span data-stu-id="63072-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span></span>   

    <span data-ttu-id="63072-226">a.</span><span class="sxs-lookup"><span data-stu-id="63072-226">a.</span></span> <span data-ttu-id="63072-227">Voer de **voornaam** en **e** kenmerken van een geldig Azure Active Directory-account dat u inrichten in de bijbehorende tekstvakken wilt.</span><span class="sxs-lookup"><span data-stu-id="63072-227">Enter the **First Name** and **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="63072-228">b.</span><span class="sxs-lookup"><span data-stu-id="63072-228">b.</span></span> <span data-ttu-id="63072-229">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="63072-229">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="63072-230">De accounthouder Azure Active Directory wordt een e-mailbericht met inbegrip van een koppeling om te bevestigen van het account voordat deze geactiveerd wordt</span><span class="sxs-lookup"><span data-stu-id="63072-230">The Azure Active Directory account holder gets an email including a link to confirm the account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="63072-231">U kunt andere FreshService gebruiker account hulpmiddelen voor het maken of API's die is geleverd door FreshService aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="63072-231">You can use any other FreshService user account creation tools or APIs provided by FreshService to provision AAD user accounts.</span></span>
>  

![Gebruiker toewijzen][200] 

<span data-ttu-id="63072-233">**Britta Simon om aan te wijzen Freshservice, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="63072-233">**To assign Britta Simon to Freshservice, perform the following steps:**</span></span>

1. <span data-ttu-id="63072-234">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="63072-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="63072-236">Selecteer in de lijst met toepassingen **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="63072-236">In the applications list, select **Freshservice**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. <span data-ttu-id="63072-238">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="63072-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="63072-240">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="63072-240">Click **Add** button.</span></span> <span data-ttu-id="63072-241">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="63072-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="63072-243">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="63072-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="63072-244">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="63072-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="63072-245">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="63072-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="63072-246">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="63072-246">Testing single sign-on</span></span>

<span data-ttu-id="63072-247">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="63072-247">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="63072-248">Als u op de tegel Freshservice in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Freshservice.</span><span class="sxs-lookup"><span data-stu-id="63072-248">When you click the Freshservice tile in the Access Panel, you should get automatically signed-on to your Freshservice application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="63072-249">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="63072-249">Additional resources</span></span>

* [<span data-ttu-id="63072-250">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="63072-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="63072-251">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="63072-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

