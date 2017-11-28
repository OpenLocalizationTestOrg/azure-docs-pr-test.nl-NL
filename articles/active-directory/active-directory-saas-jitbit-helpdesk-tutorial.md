---
title: 'Zelfstudie: Azure Active Directory-integratie met de Jitbit Helpdesk | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Jitbit Helpdesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 6523ee3179dafd79528093b856b0ec10fafb4f7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="77c2b-103">Zelfstudie: Azure Active Directory-integratie met Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="77c2b-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="77c2b-104">In deze zelfstudie leert u hoe Jitbit Helpdesk integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="77c2b-104">In this tutorial, you learn how to integrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="77c2b-105">Jitbit Helpdesk integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="77c2b-105">Integrating Jitbit Helpdesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="77c2b-106">U kunt beheren in Azure AD die toegang tot Jitbit Helpdesk heeft</span><span class="sxs-lookup"><span data-stu-id="77c2b-106">You can control in Azure AD who has access to Jitbit Helpdesk</span></span>
- <span data-ttu-id="77c2b-107">U kunt uw gebruikers automatisch ophalen aangemeld bij de Jitbit Helpdesk (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="77c2b-107">You can enable your users to automatically get signed-on to Jitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="77c2b-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="77c2b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="77c2b-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="77c2b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77c2b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="77c2b-110">Prerequisites</span></span>

<span data-ttu-id="77c2b-111">Voor het configureren van Azure AD-integratie met Jitbit Helpdesk, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="77c2b-111">To configure Azure AD integration with Jitbit Helpdesk, you need the following items:</span></span>

- <span data-ttu-id="77c2b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="77c2b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="77c2b-113">Een Jitbit Helpdesk eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="77c2b-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="77c2b-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="77c2b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="77c2b-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="77c2b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="77c2b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="77c2b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="77c2b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77c2b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="77c2b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="77c2b-118">Scenario description</span></span>
<span data-ttu-id="77c2b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="77c2b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="77c2b-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="77c2b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="77c2b-121">Jitbit Helpdesk uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="77c2b-121">Adding Jitbit Helpdesk from the gallery</span></span>
2. <span data-ttu-id="77c2b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="77c2b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-the-gallery"></a><span data-ttu-id="77c2b-123">Jitbit Helpdesk uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="77c2b-123">Adding Jitbit Helpdesk from the gallery</span></span>
<span data-ttu-id="77c2b-124">Voor het configureren van de integratie van Jitbit Helpdesk in Azure AD, moet u Jitbit Helpdesk uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="77c2b-124">To configure the integration of Jitbit Helpdesk into Azure AD, you need to add Jitbit Helpdesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="77c2b-125">**Als u wilt toevoegen Jitbit Helpdesk uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="77c2b-125">**To add Jitbit Helpdesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="77c2b-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="77c2b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="77c2b-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="77c2b-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="77c2b-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="77c2b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="77c2b-133">Typ in het zoekvak **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-133">In the search box, type **Jitbit Helpdesk**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="77c2b-135">Selecteer in het deelvenster resultaten **Jitbit Helpdesk**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="77c2b-135">In the results panel, select **Jitbit Helpdesk**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="77c2b-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="77c2b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="77c2b-138">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Jitbit Helpdesk op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="77c2b-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="77c2b-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Jitbit Helpdesk is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77c2b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jitbit Helpdesk is to a user in Azure AD.</span></span> <span data-ttu-id="77c2b-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Jitbit Helpdesk tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="77c2b-140">In other words, a link relationship between an Azure AD user and the related user in Jitbit Helpdesk needs to be established.</span></span>

<span data-ttu-id="77c2b-141">Wijs in Jitbit Helpdesk, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="77c2b-141">In Jitbit Helpdesk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="77c2b-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Jitbit Helpdesk, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="77c2b-142">To configure and test Azure AD single sign-on with Jitbit Helpdesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="77c2b-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="77c2b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="77c2b-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="77c2b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="77c2b-145">**[Maken van een testgebruiker Jitbit Helpdesk](#creating-a-jitbit-helpdesk-test-user)**  - Jitbit Helpdesk die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="77c2b-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - to have a counterpart of Britta Simon in Jitbit Helpdesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="77c2b-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="77c2b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="77c2b-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="77c2b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="77c2b-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="77c2b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="77c2b-149">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="77c2b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="77c2b-150">**Voor het configureren van Azure AD eenmalige aanmelding met de Jitbit Helpdesk, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="77c2b-150">**To configure Azure AD single sign-on with Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="77c2b-151">In de Azure-portal op de **Jitbit Helpdesk** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-151">In the Azure portal, on the **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="77c2b-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="77c2b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="77c2b-155">Op de **Jitbit Helpdesk domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="77c2b-155">On the **Jitbit Helpdesk Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="77c2b-157">a.</span><span class="sxs-lookup"><span data-stu-id="77c2b-157">a.</span></span> <span data-ttu-id="77c2b-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="77c2b-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="77c2b-159">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="77c2b-159">This value is not real.</span></span> <span data-ttu-id="77c2b-160">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="77c2b-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="77c2b-161">Neem contact op met [Jitbit Helpdesk Client ondersteuningsteam](https://www.jitbit.com/support/) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="77c2b-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) to get this value.</span></span> 
    
    <span data-ttu-id="77c2b-162">b.</span><span class="sxs-lookup"><span data-stu-id="77c2b-162">b.</span></span>  <span data-ttu-id="77c2b-163">In de **id** textbox, typ een URL als volgt:`https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="77c2b-163">In the **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="77c2b-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="77c2b-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="77c2b-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="77c2b-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="77c2b-168">Op de **Jitbit Helpdesk configuratie** sectie, klikt u op **configureren Jitbit Helpdesk** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="77c2b-168">On the **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="77c2b-169">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="77c2b-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="77c2b-171">In een ander browservenster, meld u bij uw bedrijf Jitbit Helpdesk site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="77c2b-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="77c2b-172">Klik in de werkbalk bovenaan op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-172">In the toolbar on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="77c2b-173">![Beheer](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="77c2b-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="77c2b-174">Klik op **algemene instellingen**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="77c2b-175">![Gebruikers, bedrijven en machtigingen](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "gebruikers, bedrijven en machtigingen")</span><span class="sxs-lookup"><span data-stu-id="77c2b-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="77c2b-176">In de **verificatie-instellingen** configuratie sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="77c2b-176">In the **Authentication settings** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="77c2b-177">![Verificatie-instellingen](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "verificatie-instellingen")</span><span class="sxs-lookup"><span data-stu-id="77c2b-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="77c2b-178">a.</span><span class="sxs-lookup"><span data-stu-id="77c2b-178">a.</span></span> <span data-ttu-id="77c2b-179">Selecteer **inschakelen-SAML één 2.0 aanmelden**, aan te melden met behulp van eenmalige aanmelding (SSO), met **OneLogin**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-179">Select **Enable SAML 2.0 single sign on**, to sign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="77c2b-180">b.</span><span class="sxs-lookup"><span data-stu-id="77c2b-180">b.</span></span> <span data-ttu-id="77c2b-181">In de **eindpunt-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="77c2b-181">In the **EndPoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="77c2b-182">c.</span><span class="sxs-lookup"><span data-stu-id="77c2b-182">c.</span></span> <span data-ttu-id="77c2b-183">Open uw **base 64-** gecodeerde certificaat in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **X.509-certificaat** tekstvak</span><span class="sxs-lookup"><span data-stu-id="77c2b-183">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="77c2b-184">d.</span><span class="sxs-lookup"><span data-stu-id="77c2b-184">d.</span></span> <span data-ttu-id="77c2b-185">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="77c2b-186">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="77c2b-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="77c2b-187">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="77c2b-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="77c2b-188">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="77c2b-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="77c2b-189">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="77c2b-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="77c2b-190">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="77c2b-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="77c2b-192">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="77c2b-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="77c2b-193">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="77c2b-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="77c2b-195">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="77c2b-197">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="77c2b-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="77c2b-199">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="77c2b-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="77c2b-201">a.</span><span class="sxs-lookup"><span data-stu-id="77c2b-201">a.</span></span> <span data-ttu-id="77c2b-202">In de **naam** textbox typenaam als **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-202">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="77c2b-203">b.</span><span class="sxs-lookup"><span data-stu-id="77c2b-203">b.</span></span> <span data-ttu-id="77c2b-204">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="77c2b-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="77c2b-205">c.</span><span class="sxs-lookup"><span data-stu-id="77c2b-205">c.</span></span> <span data-ttu-id="77c2b-206">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="77c2b-207">d.</span><span class="sxs-lookup"><span data-stu-id="77c2b-207">d.</span></span> <span data-ttu-id="77c2b-208">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="77c2b-209">Maken van een testgebruiker Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="77c2b-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="77c2b-210">Om in te schakelen gebruikers van Azure AD aan te melden bij Jitbit Helpdesk, moeten ze worden ingericht in Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="77c2b-210">In order to enable Azure AD users to log into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="77c2b-211">In het geval van Jitbit Helpdesk is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="77c2b-211">In the case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="77c2b-212">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="77c2b-212">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="77c2b-213">Meld u aan bij uw **Jitbit Helpdesk** tenant.</span><span class="sxs-lookup"><span data-stu-id="77c2b-213">Log in to your **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="77c2b-214">Klik in het menu bovenaan op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-214">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="77c2b-215">![Beheer](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="77c2b-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="77c2b-216">Klik op **gebruikers, bedrijven en machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="77c2b-217">![Gebruikers, bedrijven en machtigingen](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "gebruikers, bedrijven en machtigingen")</span><span class="sxs-lookup"><span data-stu-id="77c2b-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="77c2b-218">Klik op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="77c2b-219">![Gebruiker toevoegen](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="77c2b-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="77c2b-220">Typ in de sectie maken de gegevens van de Azure AD-account dat u wilt inrichten als volgt:</span><span class="sxs-lookup"><span data-stu-id="77c2b-220">In the Create section, type the data of the Azure AD account you want to provision as follows:</span></span>

    <span data-ttu-id="77c2b-221">![Maak](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "maken")</span><span class="sxs-lookup"><span data-stu-id="77c2b-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="77c2b-222">a.</span><span class="sxs-lookup"><span data-stu-id="77c2b-222">a.</span></span> <span data-ttu-id="77c2b-223">In de **gebruikersnaam** textbox type **BrittaSimon**, de gebruikersnaam, zoals in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="77c2b-223">In the **Username** textbox, type **BrittaSimon**, the user name as in the Azure portal.</span></span>

   <span data-ttu-id="77c2b-224">b.</span><span class="sxs-lookup"><span data-stu-id="77c2b-224">b.</span></span> <span data-ttu-id="77c2b-225">In de **e** textbox type e-mailadres van de gebruiker, zoals  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="77c2b-225">In the **Email** textbox, type email of the user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="77c2b-226">c.</span><span class="sxs-lookup"><span data-stu-id="77c2b-226">c.</span></span> <span data-ttu-id="77c2b-227">In de **voornaam** textbox type voornaam van de gebruiker zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-227">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>

   <span data-ttu-id="77c2b-228">d.</span><span class="sxs-lookup"><span data-stu-id="77c2b-228">d.</span></span> <span data-ttu-id="77c2b-229">In de **achternaam** textbox type achternaam van de gebruiker zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-229">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span>
   
   <span data-ttu-id="77c2b-230">e.</span><span class="sxs-lookup"><span data-stu-id="77c2b-230">e.</span></span> <span data-ttu-id="77c2b-231">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="77c2b-232">U kunt geen andere hulpprogramma's voor Jitbit Helpdesk gebruiker-account maken of API's die worden geleverd door Jitbit Helpdesk gebruiken voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="77c2b-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk to provision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="77c2b-233">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="77c2b-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="77c2b-234">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang te verlenen aan de Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="77c2b-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jitbit Helpdesk.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="77c2b-236">**Britta Simon om aan te wijzen Jitbit Helpdesk, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="77c2b-236">**To assign Britta Simon to Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="77c2b-237">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="77c2b-239">Selecteer in de lijst met toepassingen **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-239">In the applications list, select **Jitbit Helpdesk**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="77c2b-241">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="77c2b-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="77c2b-243">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="77c2b-243">Click **Add** button.</span></span> <span data-ttu-id="77c2b-244">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="77c2b-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="77c2b-246">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="77c2b-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="77c2b-247">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="77c2b-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="77c2b-248">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="77c2b-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="77c2b-249">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="77c2b-249">Testing single sign-on</span></span>

<span data-ttu-id="77c2b-250">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="77c2b-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="77c2b-251">Als u op de tegel Jitbit Helpdesk in het deelvenster toegang, krijgt u de aanmeldingspagina van Jitbit Helpdesk-toepassing.</span><span class="sxs-lookup"><span data-stu-id="77c2b-251">When you click the Jitbit Helpdesk tile in the Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="77c2b-252">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="77c2b-252">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="77c2b-253">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="77c2b-253">Additional resources</span></span>

* [<span data-ttu-id="77c2b-254">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77c2b-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77c2b-255">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="77c2b-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

