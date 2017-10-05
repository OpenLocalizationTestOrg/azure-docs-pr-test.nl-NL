---
title: 'Zelfstudie: Azure Active Directory-integratie met ITRP | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en ITRP.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: fae1c7b6b0e04c1e23123d3aee7913cb3131e645
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a><span data-ttu-id="49282-103">Zelfstudie: Azure Active Directory-integratie met ITRP</span><span class="sxs-lookup"><span data-stu-id="49282-103">Tutorial: Azure Active Directory integration with ITRP</span></span>

<span data-ttu-id="49282-104">In deze zelfstudie leert u hoe ITRP integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="49282-104">In this tutorial, you learn how to integrate ITRP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="49282-105">ITRP integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="49282-105">Integrating ITRP with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="49282-106">U kunt beheren in Azure AD die toegang tot ITRP heeft</span><span class="sxs-lookup"><span data-stu-id="49282-106">You can control in Azure AD who has access to ITRP</span></span>
- <span data-ttu-id="49282-107">U kunt uw gebruikers automatisch ophalen aangemeld bij ITRP (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="49282-107">You can enable your users to automatically get signed-on to ITRP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="49282-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="49282-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="49282-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="49282-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49282-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="49282-110">Prerequisites</span></span>

<span data-ttu-id="49282-111">Voor het configureren van Azure AD-integratie met ITRP, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="49282-111">To configure Azure AD integration with ITRP, you need the following items:</span></span>

- <span data-ttu-id="49282-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="49282-112">An Azure AD subscription</span></span>
- <span data-ttu-id="49282-113">Een ITRP eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="49282-113">An ITRP single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="49282-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="49282-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="49282-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="49282-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="49282-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="49282-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="49282-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49282-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="49282-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="49282-118">Scenario description</span></span>
<span data-ttu-id="49282-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="49282-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="49282-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="49282-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="49282-121">ITRP uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="49282-121">Adding ITRP from the gallery</span></span>
2. <span data-ttu-id="49282-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="49282-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itrp-from-the-gallery"></a><span data-ttu-id="49282-123">ITRP uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="49282-123">Adding ITRP from the gallery</span></span>
<span data-ttu-id="49282-124">Voor het configureren van de integratie van ITRP in naar Azure AD, moet u ITRP uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="49282-124">To configure the integration of ITRP in to Azure AD, you need to add ITRP from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="49282-125">**Als u wilt toevoegen ITRP uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="49282-125">**To add ITRP from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="49282-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="49282-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="49282-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="49282-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="49282-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="49282-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="49282-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="49282-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="49282-133">Typ in het zoekvak **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="49282-133">In the search box, type **ITRP**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_search.png)

5. <span data-ttu-id="49282-135">Selecteer in het deelvenster resultaten **ITRP**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="49282-135">In the results panel, select **ITRP**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="49282-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="49282-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="49282-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met ITRP op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="49282-138">In this section, you configure and test Azure AD single sign-on with ITRP based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="49282-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in ITRP is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49282-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ITRP is to a user in Azure AD.</span></span> <span data-ttu-id="49282-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in ITRP tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="49282-140">In other words, a link relationship between an Azure AD user and the related user in ITRP needs to be established.</span></span>

<span data-ttu-id="49282-141">Wijs in ITRP, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="49282-141">In ITRP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="49282-142">Om te configureren en testen van Azure AD eenmalige aanmelding met ITRP, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="49282-142">To configure and test Azure AD single sign-on with ITRP, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="49282-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="49282-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="49282-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="49282-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="49282-145">**[Maken van een ITRP testgebruiker](#creating-an-itrp-test-user)**  - ITRP die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="49282-145">**[Creating an ITRP test user](#creating-an-itrp-test-user)** - to have a counterpart of Britta Simon in ITRP that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="49282-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="49282-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="49282-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="49282-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="49282-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="49282-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="49282-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing ITRP configureren.</span><span class="sxs-lookup"><span data-stu-id="49282-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ITRP application.</span></span>

<span data-ttu-id="49282-150">**Voor het configureren van Azure AD eenmalige aanmelding met ITRP, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="49282-150">**To configure Azure AD single sign-on with ITRP, perform the following steps:**</span></span>

1. <span data-ttu-id="49282-151">In de Azure-portal op de **ITRP** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="49282-151">In the Azure portal, on the **ITRP** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="49282-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="49282-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_samlbase.png)

3. <span data-ttu-id="49282-155">Op de **ITRP domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="49282-155">On the **ITRP Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_url.png)

    <span data-ttu-id="49282-157">a.</span><span class="sxs-lookup"><span data-stu-id="49282-157">a.</span></span> <span data-ttu-id="49282-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="49282-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.itrp.com`</span></span>

    <span data-ttu-id="49282-159">b.</span><span class="sxs-lookup"><span data-stu-id="49282-159">b.</span></span> <span data-ttu-id="49282-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="49282-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.itrp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="49282-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="49282-161">These values are not real.</span></span> <span data-ttu-id="49282-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="49282-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="49282-163">Neem contact op met [ITRP Client ondersteuningsteam](https://www.itrp.com/support) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="49282-163">Contact [ITRP Client support team](https://www.itrp.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="49282-164">Op de **SAML-certificaat voor ondertekening van** sectie, Kopieer de **VINGERAFDRUK** waarde van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="49282-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_certificate.png) 

5. <span data-ttu-id="49282-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="49282-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-itrp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="49282-168">Op de **ITRP configuratie** sectie, klikt u op **configureren ITRP** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="49282-168">On the **ITRP Configuration** section, click **Configure ITRP** to open **Configure sign-on** window.</span></span> <span data-ttu-id="49282-169">Kopieer de **SAML Single Sign-On Service URL's en Sign-Out** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="49282-169">Copy the **SAML Single Sign-On Service URL and Sign-Out URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_configure.png) 

7. <span data-ttu-id="49282-171">In een ander browservenster, meld u aan bij uw bedrijf ITRP site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="49282-171">In a different web browser window, log in to your ITRP company site as an administrator.</span></span>

8. <span data-ttu-id="49282-172">Klik in de werkbalk bovenaan op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="49282-172">In the toolbar on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="49282-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="49282-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span></span>

8. <span data-ttu-id="49282-174">Selecteer in het navigatiedeelvenster links **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="49282-174">In the left navigation pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="49282-175">![Eenmalige aanmelding](./media/active-directory-saas-itrp-tutorial/ic775571.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="49282-175">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span></span>

9. <span data-ttu-id="49282-176">Voer de volgende stappen uit in de configuratiesectie eenmalige aanmelding:</span><span class="sxs-lookup"><span data-stu-id="49282-176">In the Single Sign-On configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="49282-177">![Eenmalige aanmelding](./media/active-directory-saas-itrp-tutorial/ic775572.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="49282-177">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="49282-178">![Eenmalige aanmelding](./media/active-directory-saas-itrp-tutorial/ic775573.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="49282-178">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span></span>   

    <span data-ttu-id="49282-179">a.</span><span class="sxs-lookup"><span data-stu-id="49282-179">a.</span></span> <span data-ttu-id="49282-180">Klik op **inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="49282-180">Click **Enable**.</span></span>

    <span data-ttu-id="49282-181">b.</span><span class="sxs-lookup"><span data-stu-id="49282-181">b.</span></span> <span data-ttu-id="49282-182">In **externe afmeldings-URL** textbox, plak de waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="49282-182">In **Remote Log Out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="49282-183">c.</span><span class="sxs-lookup"><span data-stu-id="49282-183">c.</span></span> <span data-ttu-id="49282-184">In **SAML SSO URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="49282-184">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="49282-185">d.In **vingerafdruk van certificaat** textbox, plak de **vingerafdruk** waarde van het certificaat dat u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="49282-185">d.In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span> 
      
10. <span data-ttu-id="49282-186">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="49282-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="49282-187">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="49282-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="49282-188">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="49282-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="49282-189">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="49282-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="49282-190">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="49282-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="49282-191">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="49282-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="49282-193">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="49282-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="49282-194">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="49282-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-itrp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="49282-196">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="49282-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-itrp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="49282-198">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="49282-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-itrp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="49282-200">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="49282-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-itrp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="49282-202">a.</span><span class="sxs-lookup"><span data-stu-id="49282-202">a.</span></span> <span data-ttu-id="49282-203">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="49282-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="49282-204">b.</span><span class="sxs-lookup"><span data-stu-id="49282-204">b.</span></span> <span data-ttu-id="49282-205">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="49282-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="49282-206">c.</span><span class="sxs-lookup"><span data-stu-id="49282-206">c.</span></span> <span data-ttu-id="49282-207">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="49282-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="49282-208">d.</span><span class="sxs-lookup"><span data-stu-id="49282-208">d.</span></span> <span data-ttu-id="49282-209">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="49282-209">Click **Create**.</span></span>
 
### <a name="creating-an-itrp-test-user"></a><span data-ttu-id="49282-210">Een testgebruiker ITRP maken</span><span class="sxs-lookup"><span data-stu-id="49282-210">Creating an ITRP test user</span></span>

<span data-ttu-id="49282-211">Om Azure AD-gebruikers zich aanmelden bij ITRP, moeten ze worden ingericht op ITRP.</span><span class="sxs-lookup"><span data-stu-id="49282-211">To enable Azure AD users to log in to ITRP, they must be provisioned in to ITRP.</span></span>  

<span data-ttu-id="49282-212">In het geval van ITRP is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="49282-212">In the case of ITRP, provisioning is a manual task.</span></span>

<span data-ttu-id="49282-213">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="49282-213">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="49282-214">Meld u aan bij uw **ITRP** tenant.</span><span class="sxs-lookup"><span data-stu-id="49282-214">Log in to your **ITRP** tenant.</span></span>

2. <span data-ttu-id="49282-215">Klik in de werkbalk bovenaan op **Records**.</span><span class="sxs-lookup"><span data-stu-id="49282-215">In the toolbar on the top, click **Records**.</span></span>
   
    <span data-ttu-id="49282-216">![Beheerder](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="49282-216">![Admin](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span></span>

3. <span data-ttu-id="49282-217">Selecteer in het pop-upmenu **mensen**.</span><span class="sxs-lookup"><span data-stu-id="49282-217">From the popup menu, select **People**.</span></span>
   
    <span data-ttu-id="49282-218">![Mensen](./media/active-directory-saas-itrp-tutorial/ic775587.png "personen")</span><span class="sxs-lookup"><span data-stu-id="49282-218">![People](./media/active-directory-saas-itrp-tutorial/ic775587.png "People")</span></span>

4. <span data-ttu-id="49282-219">Klik op **toevoegen van nieuwe persoon** ('+').</span><span class="sxs-lookup"><span data-stu-id="49282-219">Click **Add New Person** (“+”).</span></span>
   
    <span data-ttu-id="49282-220">![Beheerder](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="49282-220">![Admin](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span></span>

5. <span data-ttu-id="49282-221">Voer de volgende stappen uit in het dialoogvenster nieuwe persoon toevoegen:</span><span class="sxs-lookup"><span data-stu-id="49282-221">On the Add New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="49282-222">![Gebruiker](./media/active-directory-saas-itrp-tutorial/ic775577.png "gebruiker")</span><span class="sxs-lookup"><span data-stu-id="49282-222">![User](./media/active-directory-saas-itrp-tutorial/ic775577.png "User")</span></span> 
      
    <span data-ttu-id="49282-223">a.</span><span class="sxs-lookup"><span data-stu-id="49282-223">a.</span></span> <span data-ttu-id="49282-224">Typ de **naam**, **e** van een geldige AAD-account dat u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="49282-224">Type the **Name**, **Email** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="49282-225">b.</span><span class="sxs-lookup"><span data-stu-id="49282-225">b.</span></span> <span data-ttu-id="49282-226">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="49282-226">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="49282-227">U kunt andere ITRP gebruiker account hulpmiddelen voor het maken of API's die is geleverd door ITRP aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="49282-227">You can use any other ITRP user account creation tools or APIs provided by ITRP to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="49282-228">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="49282-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="49282-229">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan ITRP.</span><span class="sxs-lookup"><span data-stu-id="49282-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ITRP.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="49282-231">**Britta Simon om aan te wijzen ITRP, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="49282-231">**To assign Britta Simon to ITRP, perform the following steps:**</span></span>

1. <span data-ttu-id="49282-232">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="49282-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="49282-234">Selecteer in de lijst met toepassingen **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="49282-234">In the applications list, select **ITRP**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_app.png) 

3. <span data-ttu-id="49282-236">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="49282-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="49282-238">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="49282-238">Click **Add** button.</span></span> <span data-ttu-id="49282-239">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="49282-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="49282-241">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="49282-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="49282-242">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="49282-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="49282-243">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="49282-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="49282-244">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="49282-244">Testing single sign-on</span></span>

<span data-ttu-id="49282-245">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="49282-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="49282-246">Als u op de tegel ITRP in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing ITRP.</span><span class="sxs-lookup"><span data-stu-id="49282-246">When you click the ITRP tile in the Access Panel, you should get automatically signed-on to your ITRP application.</span></span>
<span data-ttu-id="49282-247">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="49282-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="49282-248">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="49282-248">Additional resources</span></span>

* [<span data-ttu-id="49282-249">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49282-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="49282-250">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="49282-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_203.png

