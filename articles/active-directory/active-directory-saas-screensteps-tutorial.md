---
title: 'Zelfstudie: Azure Active Directory-integratie met ScreenSteps | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en ScreenSteps.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: b6ded8ba1adf03fdccbdb7573c09fae1857c8b16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="b9cff-103">Zelfstudie: Azure Active Directory-integratie met ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="b9cff-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="b9cff-104">In deze zelfstudie leert u hoe ScreenSteps integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9cff-104">In this tutorial, you learn how to integrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9cff-105">ScreenSteps integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b9cff-105">Integrating ScreenSteps with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b9cff-106">U kunt beheren in Azure AD die toegang tot ScreenSteps heeft.</span><span class="sxs-lookup"><span data-stu-id="b9cff-106">You can control in Azure AD who has access to ScreenSteps.</span></span>
- <span data-ttu-id="b9cff-107">U kunt uw gebruikers automatisch ophalen aangemeld bij ScreenSteps (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b9cff-107">You can enable your users to automatically get signed-on to ScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b9cff-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="b9cff-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b9cff-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b9cff-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9cff-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b9cff-110">Prerequisites</span></span>

<span data-ttu-id="b9cff-111">Voor het configureren van Azure AD-integratie met ScreenSteps, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b9cff-111">To configure Azure AD integration with ScreenSteps, you need the following items:</span></span>

- <span data-ttu-id="b9cff-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b9cff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9cff-113">Een ScreenSteps eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b9cff-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9cff-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b9cff-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9cff-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b9cff-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9cff-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b9cff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9cff-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9cff-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9cff-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b9cff-118">Scenario description</span></span>
<span data-ttu-id="b9cff-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b9cff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9cff-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b9cff-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9cff-121">ScreenSteps uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b9cff-121">Adding ScreenSteps from the gallery</span></span>
2. <span data-ttu-id="b9cff-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b9cff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-the-gallery"></a><span data-ttu-id="b9cff-123">ScreenSteps uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b9cff-123">Adding ScreenSteps from the gallery</span></span>
<span data-ttu-id="b9cff-124">Voor het configureren van de integratie van ScreenSteps in Azure AD, moet u ScreenSteps uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b9cff-124">To configure the integration of ScreenSteps into Azure AD, you need to add ScreenSteps from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b9cff-125">**Als u wilt toevoegen ScreenSteps uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b9cff-125">**To add ScreenSteps from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b9cff-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b9cff-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="b9cff-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b9cff-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b9cff-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b9cff-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="b9cff-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b9cff-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="b9cff-133">Typ in het zoekvak **ScreenSteps**, selecteer **ScreenSteps** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b9cff-133">In the search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button to add the application.</span></span>

    ![ScreenSteps in de lijst met resultaten](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b9cff-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9cff-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b9cff-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met ScreenSteps op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b9cff-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b9cff-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in ScreenSteps is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9cff-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ScreenSteps is to a user in Azure AD.</span></span> <span data-ttu-id="b9cff-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in ScreenSteps tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="b9cff-138">In other words, a link relationship between an Azure AD user and the related user in ScreenSteps needs to be established.</span></span>

<span data-ttu-id="b9cff-139">Wijs in ScreenSteps, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="b9cff-139">In ScreenSteps, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b9cff-140">Om te configureren en testen van Azure AD eenmalige aanmelding met ScreenSteps, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="b9cff-140">To configure and test Azure AD single sign-on with ScreenSteps, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b9cff-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b9cff-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b9cff-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9cff-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9cff-143">**[Maak een testgebruiker ScreenSteps](#create-a-screensteps-test-user)**  - ScreenSteps die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="b9cff-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - to have a counterpart of Britta Simon in ScreenSteps that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9cff-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b9cff-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9cff-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b9cff-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b9cff-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b9cff-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b9cff-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing ScreenSteps configureren.</span><span class="sxs-lookup"><span data-stu-id="b9cff-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="b9cff-148">**Voor het configureren van Azure AD eenmalige aanmelding met ScreenSteps, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b9cff-148">**To configure Azure AD single sign-on with ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="b9cff-149">In de Azure-portal op de **ScreenSteps** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b9cff-149">In the Azure portal, on the **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b9cff-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b9cff-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="b9cff-153">Op de **ScreenSteps domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b9cff-153">On the **ScreenSteps Domain and URLs** section, perform the following steps:</span></span>

    ![URL's en ScreenSteps domein eenmalige aanmelding informatie](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="b9cff-155">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="b9cff-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b9cff-156">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="b9cff-156">This value is not real.</span></span> <span data-ttu-id="b9cff-157">Deze waarde bijwerken met de werkelijke aanmeldings-URL, die verderop in deze zelfstudie wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="b9cff-157">Update this value with the actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="b9cff-158">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b9cff-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="b9cff-160">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b9cff-160">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b9cff-162">Op de **ScreenSteps configuratie** sectie, klikt u op **configureren ScreenSteps** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="b9cff-162">On the **ScreenSteps Configuration** section, click **Configure ScreenSteps** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b9cff-163">Kopieer de **Sign-Out URL's en SAML Single Sign-On Service** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="b9cff-163">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![ScreenSteps configuratie](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="b9cff-165">In een ander browservenster, meld u bij uw bedrijf ScreenSteps site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b9cff-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="b9cff-166">Klik op **Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="b9cff-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="b9cff-167">![Accountbeheer](./media/active-directory-saas-screensteps-tutorial/ic778523.png "accountbeheer")</span><span class="sxs-lookup"><span data-stu-id="b9cff-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="b9cff-168">Klik op **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b9cff-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="b9cff-169">![Externe verificatie](./media/active-directory-saas-screensteps-tutorial/ic778524.png "externe verificatie")</span><span class="sxs-lookup"><span data-stu-id="b9cff-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="b9cff-170">Klik op **Single Sign-on-eindpunt maken**.</span><span class="sxs-lookup"><span data-stu-id="b9cff-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="b9cff-171">![Externe verificatie](./media/active-directory-saas-screensteps-tutorial/ic778525.png "externe verificatie")</span><span class="sxs-lookup"><span data-stu-id="b9cff-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="b9cff-172">In de **maken één aanmelding eindpunt** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b9cff-172">In the **Create Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="b9cff-173">![Maak een verificatie-eindpunt](./media/active-directory-saas-screensteps-tutorial/ic778526.png "een verificatie-eindpunt maken")</span><span class="sxs-lookup"><span data-stu-id="b9cff-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="b9cff-174">a.</span><span class="sxs-lookup"><span data-stu-id="b9cff-174">a.</span></span> <span data-ttu-id="b9cff-175">In de **titel** textbox, typ een titel.</span><span class="sxs-lookup"><span data-stu-id="b9cff-175">In the **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="b9cff-176">b.</span><span class="sxs-lookup"><span data-stu-id="b9cff-176">b.</span></span> <span data-ttu-id="b9cff-177">Van de **modus** selecteert **SAML**.</span><span class="sxs-lookup"><span data-stu-id="b9cff-177">From the **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="b9cff-178">c.</span><span class="sxs-lookup"><span data-stu-id="b9cff-178">c.</span></span> <span data-ttu-id="b9cff-179">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b9cff-179">Click **Create**.</span></span>

12. <span data-ttu-id="b9cff-180">**Bewerken** het nieuwe eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b9cff-180">**Edit** the new endpoint.</span></span>

    <span data-ttu-id="b9cff-181">![Eindpunt bewerken](./media/active-directory-saas-screensteps-tutorial/ic778528.png "eindpunt bewerken")</span><span class="sxs-lookup"><span data-stu-id="b9cff-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="b9cff-182">In de **bewerken één aanmelding eindpunt** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b9cff-182">In the **Edit Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="b9cff-183">![Externe verificatie-eindpunt](./media/active-directory-saas-screensteps-tutorial/ic778527.png "externe verificatie-eindpunt")</span><span class="sxs-lookup"><span data-stu-id="b9cff-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="b9cff-184">a.</span><span class="sxs-lookup"><span data-stu-id="b9cff-184">a.</span></span> <span data-ttu-id="b9cff-185">Klik op **nieuwe SAML certificaat uploadbestand**, en vervolgens het certificaat dat u hebt gedownload vanuit Azure-portal uploaden.</span><span class="sxs-lookup"><span data-stu-id="b9cff-185">Click **Upload new SAML Certificate file**, and then upload the certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="b9cff-186">b.</span><span class="sxs-lookup"><span data-stu-id="b9cff-186">b.</span></span> <span data-ttu-id="b9cff-187">Plakken **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd vanuit de Azure-portal in de **externe aanmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="b9cff-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="b9cff-188">c.</span><span class="sxs-lookup"><span data-stu-id="b9cff-188">c.</span></span> <span data-ttu-id="b9cff-189">Plakken **Sign-Out URL** waarde, die u hebt gekopieerd vanuit de Azure-portal in de **afmeldings-URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="b9cff-189">Paste **Sign-Out URL** value, which you have copied from the Azure portal into the **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="b9cff-190">d.</span><span class="sxs-lookup"><span data-stu-id="b9cff-190">d.</span></span> <span data-ttu-id="b9cff-191">Selecteer een **groep** gebruikers toewijzen aan wanneer deze zijn ingericht.</span><span class="sxs-lookup"><span data-stu-id="b9cff-191">Select a **Group** to assign users to when they are provisioned.</span></span>
    
    <span data-ttu-id="b9cff-192">e.</span><span class="sxs-lookup"><span data-stu-id="b9cff-192">e.</span></span> <span data-ttu-id="b9cff-193">Klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="b9cff-193">Click **Update**.</span></span>

    <span data-ttu-id="b9cff-194">f.</span><span class="sxs-lookup"><span data-stu-id="b9cff-194">f.</span></span> <span data-ttu-id="b9cff-195">Kopiëren de **SAML Consumer URL** naar het Klembord en plakken in de **aanmeldings-URL** textbox in **ScreenSteps domein en de URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="b9cff-195">Copy the **SAML Consumer URL** to the clipboard and paste in to the **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="b9cff-196">g.</span><span class="sxs-lookup"><span data-stu-id="b9cff-196">g.</span></span> <span data-ttu-id="b9cff-197">Ga terug naar de **bewerken één aanmelding eindpunt**.</span><span class="sxs-lookup"><span data-stu-id="b9cff-197">Return to the **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="b9cff-198">h.</span><span class="sxs-lookup"><span data-stu-id="b9cff-198">h.</span></span> <span data-ttu-id="b9cff-199">Klik op de **voor account instellen als standaardbrowser** knop met dit eindpunt voor alle gebruikers die zich bij ScreenSteps aanmelden.</span><span class="sxs-lookup"><span data-stu-id="b9cff-199">Click the **Make default for account** button to use this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="b9cff-200">U kunt ook klikken op de **toevoegen aan de Site** knop met dit eindpunt voor specifieke sites in **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="b9cff-200">Alternatively you can click the **Add to Site** button to use this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="b9cff-201">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="b9cff-201">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b9cff-202">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="b9cff-202">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b9cff-203">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b9cff-203">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b9cff-204">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b9cff-204">Create an Azure AD test user</span></span>

<span data-ttu-id="b9cff-205">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b9cff-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="b9cff-207">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b9cff-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b9cff-208">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="b9cff-208">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b9cff-210">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b9cff-210">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b9cff-212">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b9cff-212">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b9cff-214">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b9cff-214">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b9cff-216">a.</span><span class="sxs-lookup"><span data-stu-id="b9cff-216">a.</span></span> <span data-ttu-id="b9cff-217">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9cff-217">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9cff-218">b.</span><span class="sxs-lookup"><span data-stu-id="b9cff-218">b.</span></span> <span data-ttu-id="b9cff-219">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9cff-219">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b9cff-220">c.</span><span class="sxs-lookup"><span data-stu-id="b9cff-220">c.</span></span> <span data-ttu-id="b9cff-221">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="b9cff-221">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b9cff-222">d.</span><span class="sxs-lookup"><span data-stu-id="b9cff-222">d.</span></span> <span data-ttu-id="b9cff-223">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b9cff-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="b9cff-224">Een testgebruiker ScreenSteps maken</span><span class="sxs-lookup"><span data-stu-id="b9cff-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="b9cff-225">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in ScreenSteps maken.</span><span class="sxs-lookup"><span data-stu-id="b9cff-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="b9cff-226">Werken met [ScreenSteps Client ondersteuningsteam](https://www.screensteps.com/contact) de gebruikers van het platform ScreenSteps toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b9cff-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add the users in the ScreenSteps platform.</span></span> <span data-ttu-id="b9cff-227">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b9cff-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b9cff-228">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="b9cff-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="b9cff-229">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="b9cff-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ScreenSteps.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="b9cff-231">**Britta Simon om aan te wijzen ScreenSteps, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b9cff-231">**To assign Britta Simon to ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="b9cff-232">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b9cff-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b9cff-234">Selecteer in de lijst met toepassingen **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="b9cff-234">In the applications list, select **ScreenSteps**.</span></span>

    ![De koppeling ScreenSteps in de lijst met toepassingen](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="b9cff-236">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b9cff-236">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="b9cff-238">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b9cff-238">Click **Add** button.</span></span> <span data-ttu-id="b9cff-239">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b9cff-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="b9cff-241">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b9cff-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b9cff-242">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b9cff-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9cff-243">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b9cff-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b9cff-244">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b9cff-244">Test single sign-on</span></span>

<span data-ttu-id="b9cff-245">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b9cff-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b9cff-246">Als u op de tegel ScreenSteps in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="b9cff-246">When you click the ScreenSteps tile in the Access Panel, you should get automatically signed-on to your ScreenSteps application.</span></span>
<span data-ttu-id="b9cff-247">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b9cff-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b9cff-248">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b9cff-248">Additional resources</span></span>

* [<span data-ttu-id="b9cff-249">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9cff-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9cff-250">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b9cff-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

