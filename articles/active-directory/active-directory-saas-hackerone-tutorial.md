---
title: 'Zelfstudie: Azure Active Directory-integratie met Hackerone | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Hackerone.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 657d8d4c98b7b133698a5cda0aa675da7f68c464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="980ef-103">Zelfstudie: Azure Active Directory-integratie met HackerOne</span><span class="sxs-lookup"><span data-stu-id="980ef-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>

<span data-ttu-id="980ef-104">In deze zelfstudie leert u hoe HackerOne integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="980ef-104">In this tutorial, you learn how to integrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="980ef-105">HackerOne integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="980ef-105">Integrating HackerOne with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="980ef-106">U kunt beheren in Azure AD die toegang tot HackerOne heeft</span><span class="sxs-lookup"><span data-stu-id="980ef-106">You can control in Azure AD who has access to HackerOne</span></span>
- <span data-ttu-id="980ef-107">U kunt uw gebruikers automatisch ophalen aangemeld bij HackerOne (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="980ef-107">You can enable your users to automatically get signed-on to HackerOne (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="980ef-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="980ef-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="980ef-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="980ef-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="980ef-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="980ef-110">Prerequisites</span></span>

<span data-ttu-id="980ef-111">Voor het configureren van Azure AD-integratie met HackerOne, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="980ef-111">To configure Azure AD integration with HackerOne, you need the following items:</span></span>

- <span data-ttu-id="980ef-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="980ef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="980ef-113">Een HackerOne eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="980ef-113">A HackerOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="980ef-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="980ef-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="980ef-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="980ef-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="980ef-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="980ef-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="980ef-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="980ef-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="980ef-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="980ef-118">Scenario description</span></span>
<span data-ttu-id="980ef-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="980ef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="980ef-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="980ef-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="980ef-121">HackerOne uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="980ef-121">Adding HackerOne from the gallery</span></span>
2. <span data-ttu-id="980ef-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="980ef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hackerone-from-the-gallery"></a><span data-ttu-id="980ef-123">HackerOne uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="980ef-123">Adding HackerOne from the gallery</span></span>
<span data-ttu-id="980ef-124">Voor het configureren van de integratie van HackerOne in Azure AD, moet u HackerOne uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="980ef-124">To configure the integration of HackerOne into Azure AD, you need to add HackerOne from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="980ef-125">**Als u wilt toevoegen HackerOne uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="980ef-125">**To add HackerOne from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="980ef-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="980ef-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="980ef-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="980ef-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="980ef-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="980ef-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="980ef-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="980ef-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="980ef-133">Typ in het zoekvak **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="980ef-133">In the search box, type **HackerOne**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. <span data-ttu-id="980ef-135">Selecteer in het deelvenster resultaten **HackerOne**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="980ef-135">In the results panel, select **HackerOne**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="980ef-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="980ef-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="980ef-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met HackerOne op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="980ef-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="980ef-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in HackerOne is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="980ef-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HackerOne is to a user in Azure AD.</span></span> <span data-ttu-id="980ef-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in HackerOne tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="980ef-140">In other words, a link relationship between an Azure AD user and the related user in HackerOne needs to be established.</span></span>

<span data-ttu-id="980ef-141">Wijs in HackerOne, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="980ef-141">In HackerOne, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="980ef-142">Om te configureren en testen van Azure AD eenmalige aanmelding met HackerOne, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="980ef-142">To configure and test Azure AD single sign-on with HackerOne, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="980ef-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="980ef-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="980ef-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="980ef-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="980ef-145">**[Maken van een testgebruiker HackerOne](#creating-a-hackerone-test-user)**  - HackerOne die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="980ef-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - to have a counterpart of Britta Simon in HackerOne that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="980ef-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="980ef-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="980ef-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="980ef-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="980ef-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="980ef-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="980ef-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing HackerOne configureren.</span><span class="sxs-lookup"><span data-stu-id="980ef-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="980ef-150">**Voor het configureren van Azure AD eenmalige aanmelding met HackerOne, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="980ef-150">**To configure Azure AD single sign-on with HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="980ef-151">In de Azure-portal op de **HackerOne** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="980ef-151">In the Azure portal, on the **HackerOne** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="980ef-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="980ef-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. <span data-ttu-id="980ef-155">Op de **HackerOne één aanmeldings-URL en id** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="980ef-155">On the **HackerOne Single sign-on URL and Identifier** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    <span data-ttu-id="980ef-157">a.</span><span class="sxs-lookup"><span data-stu-id="980ef-157">a.</span></span> <span data-ttu-id="980ef-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://hackerone.com/<company name>/authentication`</span><span class="sxs-lookup"><span data-stu-id="980ef-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hackerone.com/<company name>/authentication`</span></span>

    <span data-ttu-id="980ef-159">b.</span><span class="sxs-lookup"><span data-stu-id="980ef-159">b.</span></span> <span data-ttu-id="980ef-160">In de **id** textbox, typ een URL als:`https://hackerone.com/users/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="980ef-160">In the **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="980ef-161">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="980ef-161">This value is not real.</span></span> <span data-ttu-id="980ef-162">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="980ef-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="980ef-163">Neem contact op met [HackerOne ondersteuningsteam](mailto:support@hackerone.com) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="980ef-163">Contact [HackerOne support team](mailto:support@hackerone.com) to get this value.</span></span> 
 
4. <span data-ttu-id="980ef-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="980ef-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. <span data-ttu-id="980ef-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="980ef-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="980ef-168">Op de **HackerOne configuratie** sectie, klikt u op **configureren HackerOne** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="980ef-168">On the **HackerOne Configuration** section, click **Configure HackerOne** to open **Configure sign-on** window.</span></span> <span data-ttu-id="980ef-169">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="980ef-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. <span data-ttu-id="980ef-171">Aanmelding voor uw tenant HackerOne als beheerder.</span><span class="sxs-lookup"><span data-stu-id="980ef-171">Sign On to your HackerOne tenant as an administrator.</span></span>

8. <span data-ttu-id="980ef-172">Klik in het menu bovenaan op de '**instellingen**. "</span><span class="sxs-lookup"><span data-stu-id="980ef-172">In the menu on the top, click the "**Settings**."</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. <span data-ttu-id="980ef-174">Navigeer naar '**verificatie**'en klik op'**SAML-instellingen toevoegen**. "</span><span class="sxs-lookup"><span data-stu-id="980ef-174">Navigate to "**Authentication**" and click "**Add SAML settings**."</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. <span data-ttu-id="980ef-176">Op de **SAML instellingen** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="980ef-176">On the **SAML Settings** dialog, perform the following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    <span data-ttu-id="980ef-178">a.</span><span class="sxs-lookup"><span data-stu-id="980ef-178">a.</span></span> <span data-ttu-id="980ef-179">In de **e-maildomein** textbox, typt u een geregistreerde domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="980ef-179">In the **Email Domain** textbox, type a registered domain.</span></span>

    <span data-ttu-id="980ef-180">b.</span><span class="sxs-lookup"><span data-stu-id="980ef-180">b.</span></span> <span data-ttu-id="980ef-181">In **eenmalige aanmelding op URL** tekstvakken, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="980ef-181">In  **Single Sign On URL** textboxes, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="980ef-182">c.</span><span class="sxs-lookup"><span data-stu-id="980ef-182">c.</span></span> <span data-ttu-id="980ef-183">Open uw **certificaatbestand** in Kladblok van Azure portal hebt gedownload, kopieert u de inhoud ervan naar het Klembord en plakt u deze naar de **X509-certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="980ef-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X509 Certificate**  textbox.</span></span>
    
    <span data-ttu-id="980ef-184">d.</span><span class="sxs-lookup"><span data-stu-id="980ef-184">d.</span></span> <span data-ttu-id="980ef-185">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="980ef-185">Click **Save**.</span></span>

11. <span data-ttu-id="980ef-186">In het dialoogvenster Instellingen voor verificatie, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="980ef-186">On the Authentication Settings dialog, perform the following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    <span data-ttu-id="980ef-188">a.</span><span class="sxs-lookup"><span data-stu-id="980ef-188">a.</span></span> <span data-ttu-id="980ef-189">Klik op **test uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="980ef-189">Click **Run test**.</span></span>

    <span data-ttu-id="980ef-190">b.</span><span class="sxs-lookup"><span data-stu-id="980ef-190">b.</span></span> <span data-ttu-id="980ef-191">Als de waarde van de **Status** veld gelijk is aan **status van de laatste test: gemaakt**Neem contact op met uw [HackerOne ondersteuningsteam](mailto:support@hackerone.com) om aan te vragen een overzicht van uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="980ef-191">If the value of the **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) to request a review of your configuration.</span></span>

> [!TIP]
> <span data-ttu-id="980ef-192">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="980ef-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="980ef-193">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="980ef-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="980ef-194">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="980ef-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="980ef-195">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="980ef-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="980ef-196">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="980ef-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="980ef-198">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="980ef-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="980ef-199">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="980ef-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="980ef-201">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="980ef-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="980ef-203">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="980ef-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="980ef-205">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="980ef-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="980ef-207">a.</span><span class="sxs-lookup"><span data-stu-id="980ef-207">a.</span></span> <span data-ttu-id="980ef-208">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="980ef-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="980ef-209">b.</span><span class="sxs-lookup"><span data-stu-id="980ef-209">b.</span></span> <span data-ttu-id="980ef-210">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="980ef-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="980ef-211">c.</span><span class="sxs-lookup"><span data-stu-id="980ef-211">c.</span></span> <span data-ttu-id="980ef-212">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="980ef-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="980ef-213">d.</span><span class="sxs-lookup"><span data-stu-id="980ef-213">d.</span></span> <span data-ttu-id="980ef-214">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="980ef-214">Click **Create**.</span></span>
 
### <a name="creating-a-hackerone-test-user"></a><span data-ttu-id="980ef-215">Een testgebruiker HackerOne maken</span><span class="sxs-lookup"><span data-stu-id="980ef-215">Creating a HackerOne test user</span></span>

<span data-ttu-id="980ef-216">Maak vervolgens een gebruiker Britta Simon in HackerOne genoemd.</span><span class="sxs-lookup"><span data-stu-id="980ef-216">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="980ef-217">HackerOne ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="980ef-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="980ef-218">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="980ef-218">There is no action item for you in this section.</span></span> <span data-ttu-id="980ef-219">Wanneer u HackerOne opent, wordt een nieuwe gebruiker gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="980ef-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="980ef-220">Als u een gebruiker handmatig maken moet, moet u contact op met het ondersteuningsteam certificeren.</span><span class="sxs-lookup"><span data-stu-id="980ef-220">If you need to create a user manually, you need to contact the Certify support team.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="980ef-221">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="980ef-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="980ef-222">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan HackerOne.</span><span class="sxs-lookup"><span data-stu-id="980ef-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HackerOne.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="980ef-224">**Britta Simon om aan te wijzen HackerOne, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="980ef-224">**To assign Britta Simon to HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="980ef-225">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="980ef-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="980ef-227">Selecteer in de lijst met toepassingen **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="980ef-227">In the applications list, select **HackerOne**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. <span data-ttu-id="980ef-229">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="980ef-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="980ef-231">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="980ef-231">Click **Add** button.</span></span> <span data-ttu-id="980ef-232">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="980ef-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="980ef-234">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="980ef-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="980ef-235">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="980ef-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="980ef-236">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="980ef-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="980ef-237">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="980ef-237">Testing single sign-on</span></span>

<span data-ttu-id="980ef-238">Ten slotte kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="980ef-238">Finally, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="980ef-239">Als u op de tegel HackerOne in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing HackerOne.</span><span class="sxs-lookup"><span data-stu-id="980ef-239">When you click the HackerOne tile in the Access Panel, you should get automatically signed-on to your HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="980ef-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="980ef-240">Additional resources</span></span>

* [<span data-ttu-id="980ef-241">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="980ef-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="980ef-242">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="980ef-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png

