---
title: 'Zelfstudie: Azure Active Directory-integratie met TeamSeer | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en TeamSeer.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 2a5e8f6d1443681c43db95da5cef0b7f2ef92291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="f5e1c-103">Zelfstudie: Azure Active Directory-integratie met TeamSeer</span><span class="sxs-lookup"><span data-stu-id="f5e1c-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>

<span data-ttu-id="f5e1c-104">In deze zelfstudie leert u hoe TeamSeer integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f5e1c-104">In this tutorial, you learn how to integrate TeamSeer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f5e1c-105">TeamSeer integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f5e1c-105">Integrating TeamSeer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f5e1c-106">U kunt beheren in Azure AD die toegang tot TeamSeer heeft</span><span class="sxs-lookup"><span data-stu-id="f5e1c-106">You can control in Azure AD who has access to TeamSeer</span></span>
- <span data-ttu-id="f5e1c-107">U kunt uw gebruikers automatisch ophalen aangemeld bij TeamSeer (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="f5e1c-107">You can enable your users to automatically get signed-on to TeamSeer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f5e1c-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="f5e1c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f5e1c-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f5e1c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5e1c-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f5e1c-110">Prerequisites</span></span>

<span data-ttu-id="f5e1c-111">Voor het configureren van Azure AD-integratie met TeamSeer, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="f5e1c-111">To configure Azure AD integration with TeamSeer, you need the following items:</span></span>

- <span data-ttu-id="f5e1c-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f5e1c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f5e1c-113">Een TeamSeer eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="f5e1c-113">A TeamSeer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f5e1c-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f5e1c-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="f5e1c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f5e1c-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f5e1c-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f5e1c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f5e1c-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f5e1c-118">Scenario description</span></span>
<span data-ttu-id="f5e1c-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f5e1c-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f5e1c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f5e1c-121">TeamSeer uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f5e1c-121">Adding TeamSeer from the gallery</span></span>
2. <span data-ttu-id="f5e1c-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f5e1c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamseer-from-the-gallery"></a><span data-ttu-id="f5e1c-123">TeamSeer uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f5e1c-123">Adding TeamSeer from the gallery</span></span>
<span data-ttu-id="f5e1c-124">Voor het configureren van de integratie van TeamSeer in naar Azure AD, moet u TeamSeer uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-124">To configure the integration of TeamSeer in to Azure AD, you need to add TeamSeer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f5e1c-125">**Als u wilt toevoegen TeamSeer uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f5e1c-125">**To add TeamSeer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f5e1c-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f5e1c-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f5e1c-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="f5e1c-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="f5e1c-133">Typ in het zoekvak **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-133">In the search box, type **TeamSeer**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. <span data-ttu-id="f5e1c-135">Selecteer in het deelvenster resultaten **TeamSeer**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-135">In the results panel, select **TeamSeer**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f5e1c-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f5e1c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f5e1c-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met TeamSeer op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="f5e1c-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f5e1c-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in TeamSeer is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TeamSeer is to a user in Azure AD.</span></span> <span data-ttu-id="f5e1c-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in TeamSeer tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-140">In other words, a link relationship between an Azure AD user and the related user in TeamSeer needs to be established.</span></span>

<span data-ttu-id="f5e1c-141">Wijs in TeamSeer, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-141">In TeamSeer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f5e1c-142">Om te configureren en testen van Azure AD eenmalige aanmelding met TeamSeer, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="f5e1c-142">To configure and test Azure AD single sign-on with TeamSeer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f5e1c-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f5e1c-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f5e1c-145">**[Maken van een testgebruiker TeamSeer](#creating-a-teamseer-test-user)**  - TeamSeer die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - to have a counterpart of Britta Simon in TeamSeer that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f5e1c-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f5e1c-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f5e1c-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f5e1c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f5e1c-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing TeamSeer configureren.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TeamSeer application.</span></span>

<span data-ttu-id="f5e1c-150">**Voor het configureren van Azure AD eenmalige aanmelding met TeamSeer, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f5e1c-150">**To configure Azure AD single sign-on with TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="f5e1c-151">In de Azure-portal op de **TeamSeer** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-151">In the Azure portal, on the **TeamSeer** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f5e1c-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. <span data-ttu-id="f5e1c-155">Op de **TeamSeer domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f5e1c-155">On the **TeamSeer Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     <span data-ttu-id="f5e1c-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://www.teamseer.com/<companyid>`</span><span class="sxs-lookup"><span data-stu-id="f5e1c-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.teamseer.com/<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f5e1c-158">De waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-158">The value is not real.</span></span> <span data-ttu-id="f5e1c-159">Werk de waarde met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="f5e1c-160">Neem contact op met [TeamSeer Client ondersteuningsteam](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) de waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) to get the value.</span></span> 
 
4. <span data-ttu-id="f5e1c-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. <span data-ttu-id="f5e1c-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f5e1c-165">Op de **TeamSeer configuratie** sectie, klikt u op **configureren TeamSeer** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-165">On the **TeamSeer Configuration** section, click **Configure TeamSeer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f5e1c-166">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="f5e1c-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. <span data-ttu-id="f5e1c-168">In een ander browservenster, meld u aan bij uw bedrijf TeamSeer site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-168">In a different web browser window, log in to your TeamSeer company site as an administrator.</span></span>

8. <span data-ttu-id="f5e1c-169">Ga naar **HR Admin**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-169">Go to **HR Admin**.</span></span>
   
    <span data-ttu-id="f5e1c-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR-beheerder")</span><span class="sxs-lookup"><span data-stu-id="f5e1c-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR Admin")</span></span>

9. <span data-ttu-id="f5e1c-171">Klik op **Setup**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-171">Click **Setup**.</span></span>
   
    <span data-ttu-id="f5e1c-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="f5e1c-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span></span>

10. <span data-ttu-id="f5e1c-173">Klik op **SAML provider details instellen**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-173">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="f5e1c-174">![Instellingen voor SAML](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML-instellingen")</span><span class="sxs-lookup"><span data-stu-id="f5e1c-174">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML Settings")</span></span>

11. <span data-ttu-id="f5e1c-175">In het gedeelte details van SAML-provider de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f5e1c-175">In the SAML provider details section, perform the following steps:</span></span>
   
    <span data-ttu-id="f5e1c-176">![Instellingen voor SAML](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML-instellingen")</span><span class="sxs-lookup"><span data-stu-id="f5e1c-176">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML Settings")</span></span>   

    <span data-ttu-id="f5e1c-177">a.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-177">a.</span></span> <span data-ttu-id="f5e1c-178">Plak de **Single Sign-On Service-URL** waarde in voor de **URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-178">Paste the **Single Sign-On Service URL** value in to the **URL** textbox.</span></span>
          
    <span data-ttu-id="f5e1c-179">b.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-179">b.</span></span> <span data-ttu-id="f5e1c-180">De base-64 gecodeerde certificaat openen in Kladblok, Kopieer de inhoud van in naar het Klembord en plakt u deze naar de **IdP openbaar certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-180">Open your base-64 encoded certificate in notepad, copy the content of it in to your clipboard, and then paste it to the **IdP Public Certificate** textbox.</span></span>

12. <span data-ttu-id="f5e1c-181">Voor het voltooien van de configuratie van de SAML-provider, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f5e1c-181">To complete the SAML provider configuration, perform the following steps:</span></span>
    
    <span data-ttu-id="f5e1c-182">![Instellingen voor SAML](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML-instellingen")</span><span class="sxs-lookup"><span data-stu-id="f5e1c-182">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML Settings")</span></span> 

    <span data-ttu-id="f5e1c-183">a.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-183">a.</span></span> <span data-ttu-id="f5e1c-184">In de **e-mailadressen testen**, typ de e-mailadres van de testgebruiker.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-184">In the **Test Email Addresses**, type the test user’s email address.</span></span> 
  
    <span data-ttu-id="f5e1c-185">b.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-185">b.</span></span> <span data-ttu-id="f5e1c-186">In de **verlener** textbox, typ de URL van de verlener van de serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-186">In the **Issuer** textbox, type the Issuer URL of the service provider.</span></span> 
  
    <span data-ttu-id="f5e1c-187">c.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-187">c.</span></span> <span data-ttu-id="f5e1c-188">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f5e1c-189">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="f5e1c-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f5e1c-190">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f5e1c-191">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f5e1c-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f5e1c-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f5e1c-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="f5e1c-193">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="f5e1c-195">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f5e1c-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f5e1c-196">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f5e1c-198">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f5e1c-200">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f5e1c-202">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f5e1c-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f5e1c-204">a.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-204">a.</span></span> <span data-ttu-id="f5e1c-205">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f5e1c-206">b.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-206">b.</span></span> <span data-ttu-id="f5e1c-207">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f5e1c-208">c.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-208">c.</span></span> <span data-ttu-id="f5e1c-209">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f5e1c-210">d.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-210">d.</span></span> <span data-ttu-id="f5e1c-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-211">Click **Create**.</span></span>
 
### <a name="creating-a-teamseer-test-user"></a><span data-ttu-id="f5e1c-212">Een testgebruiker TeamSeer maken</span><span class="sxs-lookup"><span data-stu-id="f5e1c-212">Creating a TeamSeer test user</span></span>

<span data-ttu-id="f5e1c-213">Om Azure AD-gebruikers zich aanmelden bij TeamSeer, moeten ze worden ingericht op ShiftPlanning.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-213">To enable Azure AD users to log in to TeamSeer, they must be provisioned in to ShiftPlanning.</span></span> <span data-ttu-id="f5e1c-214">In het geval van TeamSeer is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-214">In the case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="f5e1c-215">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f5e1c-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="f5e1c-216">Meld u aan bij uw **TeamSeer** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-216">Log in to your **TeamSeer** company site as an administrator.</span></span>

2. <span data-ttu-id="f5e1c-217">De volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f5e1c-217">Perform the following steps:</span></span>
   
    <span data-ttu-id="f5e1c-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR-beheerder")</span><span class="sxs-lookup"><span data-stu-id="f5e1c-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR Admin")</span></span>  
 
    <span data-ttu-id="f5e1c-219">a.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-219">a.</span></span> <span data-ttu-id="f5e1c-220">Ga naar **HR Admin \> gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-220">Go to **HR Admin \> Users**.</span></span>
  
    <span data-ttu-id="f5e1c-221">b.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-221">b.</span></span> <span data-ttu-id="f5e1c-222">Klik op **voert u de wizard nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-222">Click **Run the New User wizard**.</span></span>

3. <span data-ttu-id="f5e1c-223">In de **Gebruikersdetails** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f5e1c-223">In the **User Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="f5e1c-224">![Details van gebruiker](./media/active-directory-saas-teamseer-tutorial/ic789641.png "Gebruikersdetails")</span><span class="sxs-lookup"><span data-stu-id="f5e1c-224">![User Details](./media/active-directory-saas-teamseer-tutorial/ic789641.png "User Details")</span></span>

    <span data-ttu-id="f5e1c-225">a.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-225">a.</span></span> <span data-ttu-id="f5e1c-226">Typ de **voornaam**, **achternaam**, **gebruikersnaam (e-mailadres)** van een geldige AAD-account dat u inrichten wilt de bijbehorende tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-226">Type the **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want to provision in to the related textboxes.</span></span>
  
    <span data-ttu-id="f5e1c-227">b.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-227">b.</span></span> <span data-ttu-id="f5e1c-228">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-228">Click **Next**.</span></span>

4. <span data-ttu-id="f5e1c-229">Volg de aanwijzingen op het scherm instructies voor het toevoegen van een nieuwe gebruiker en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-229">Follow the on-screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="f5e1c-230">U kunt andere TeamSeer gebruiker account hulpmiddelen voor het maken of API's die is geleverd door TeamSeer voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f5e1c-231">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5e1c-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f5e1c-232">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TeamSeer.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="f5e1c-234">**Britta Simon om aan te wijzen TeamSeer, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="f5e1c-234">**To assign Britta Simon to TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="f5e1c-235">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f5e1c-237">Selecteer in de lijst met toepassingen **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-237">In the applications list, select **TeamSeer**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. <span data-ttu-id="f5e1c-239">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="f5e1c-241">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-241">Click **Add** button.</span></span> <span data-ttu-id="f5e1c-242">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="f5e1c-244">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f5e1c-245">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f5e1c-246">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f5e1c-247">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f5e1c-247">Testing single sign-on</span></span>

<span data-ttu-id="f5e1c-248">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="f5e1c-248">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="f5e1c-249">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f5e1c-249">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f5e1c-250">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="f5e1c-250">Additional resources</span></span>

* [<span data-ttu-id="f5e1c-251">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5e1c-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f5e1c-252">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f5e1c-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

