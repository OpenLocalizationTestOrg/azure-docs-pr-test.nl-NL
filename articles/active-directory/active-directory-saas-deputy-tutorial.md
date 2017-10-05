---
title: 'Zelfstudie: Azure Active Directory-integratie met vice | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en vice.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 51aed908208b7a40ea2ab710dffe84370b573991
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="eb394-103">Zelfstudie: Azure Active Directory-integratie met vice</span><span class="sxs-lookup"><span data-stu-id="eb394-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="eb394-104">In deze zelfstudie leert u hoe vice integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eb394-104">In this tutorial, you learn how to integrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eb394-105">Vice integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="eb394-105">Integrating Deputy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="eb394-106">U kunt beheren in Azure AD die toegang tot vice heeft</span><span class="sxs-lookup"><span data-stu-id="eb394-106">You can control in Azure AD who has access to Deputy</span></span>
- <span data-ttu-id="eb394-107">U kunt uw gebruikers automatisch ophalen aangemeld bij vice (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="eb394-107">You can enable your users to automatically get signed-on to Deputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eb394-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="eb394-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="eb394-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eb394-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb394-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="eb394-110">Prerequisites</span></span>

<span data-ttu-id="eb394-111">Voor het configureren van Azure AD-integratie met vice, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="eb394-111">To configure Azure AD integration with Deputy, you need the following items:</span></span>

- <span data-ttu-id="eb394-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="eb394-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eb394-113">Een vice eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="eb394-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eb394-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="eb394-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eb394-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="eb394-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eb394-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="eb394-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eb394-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eb394-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eb394-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="eb394-118">Scenario description</span></span>
<span data-ttu-id="eb394-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="eb394-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eb394-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="eb394-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eb394-121">Vice uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="eb394-121">Adding Deputy from the gallery</span></span>
2. <span data-ttu-id="eb394-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="eb394-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-the-gallery"></a><span data-ttu-id="eb394-123">Vice uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="eb394-123">Adding Deputy from the gallery</span></span>
<span data-ttu-id="eb394-124">Voor het configureren van de integratie van vice in Azure AD, moet u vice uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="eb394-124">To configure the integration of Deputy into Azure AD, you need to add Deputy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="eb394-125">**Als u wilt toevoegen vice uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="eb394-125">**To add Deputy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="eb394-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="eb394-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eb394-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="eb394-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="eb394-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="eb394-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="eb394-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eb394-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="eb394-133">Typ in het zoekvak **vice**.</span><span class="sxs-lookup"><span data-stu-id="eb394-133">In the search box, type **Deputy**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="eb394-135">Selecteer in het deelvenster resultaten **vice**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="eb394-135">In the results panel, select **Deputy**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eb394-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="eb394-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eb394-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met vice op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="eb394-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eb394-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in vice is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb394-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Deputy is to a user in Azure AD.</span></span> <span data-ttu-id="eb394-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in vice tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="eb394-140">In other words, a link relationship between an Azure AD user and the related user in Deputy needs to be established.</span></span>

<span data-ttu-id="eb394-141">Wijs in vice, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="eb394-141">In Deputy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="eb394-142">Om te configureren en testen van Azure AD eenmalige aanmelding met vice, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="eb394-142">To configure and test Azure AD single sign-on with Deputy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="eb394-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="eb394-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="eb394-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eb394-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eb394-145">**[Maken van een testgebruiker vice](#creating-a-deputy-test-user)**  - vice die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="eb394-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - to have a counterpart of Britta Simon in Deputy that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="eb394-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="eb394-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eb394-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="eb394-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eb394-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="eb394-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eb394-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing vice configureren.</span><span class="sxs-lookup"><span data-stu-id="eb394-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="eb394-150">**Voor het configureren van Azure AD eenmalige aanmelding met vice, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="eb394-150">**To configure Azure AD single sign-on with Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="eb394-151">In de Azure-portal op de **vice** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="eb394-151">In the Azure portal, on the **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="eb394-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="eb394-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="eb394-155">Op de **vice domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="eb394-155">On the **Deputy Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="eb394-157">a.</span><span class="sxs-lookup"><span data-stu-id="eb394-157">a.</span></span> <span data-ttu-id="eb394-158">In de **id** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="eb394-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="eb394-159">b.</span><span class="sxs-lookup"><span data-stu-id="eb394-159">b.</span></span> <span data-ttu-id="eb394-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="eb394-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="eb394-161">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="eb394-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="eb394-162">Als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="eb394-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="eb394-164">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="eb394-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="eb394-165">Vice regio achtervoegsel is optioneel, of moet een van de volgende gebruiken: Australië | n.v.t. | EU | als | la | af | een | ent Australië | ent na | ent eu | ent-als | ent la | ent af | ent een</span><span class="sxs-lookup"><span data-stu-id="eb394-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eb394-166">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="eb394-166">These values are not real.</span></span> <span data-ttu-id="eb394-167">Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="eb394-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="eb394-168">Neem contact op met [vice ondersteuningsteam](https://www.deputy.com/call-centers-customer-support-scheduling-software) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="eb394-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) to get these values.</span></span> 

5. <span data-ttu-id="eb394-169">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="eb394-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="eb394-171">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="eb394-171">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="eb394-173">Op de **vice configuratie** sectie, klikt u op **vice configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="eb394-173">On the **Deputy Configuration** section, click **Configure Deputy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="eb394-174">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="eb394-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="eb394-176">Navigeer naar de volgende URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span><span class="sxs-lookup"><span data-stu-id="eb394-176">Navigate to the following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="eb394-177">Ga naar **beveiligingsinstellingen** en klik op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="eb394-177">Go to **Security Settings** and click **Edit**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="eb394-179">Op deze **beveiligingsinstellingen** pagina, voert u onderstaande stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="eb394-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="eb394-181">a.</span><span class="sxs-lookup"><span data-stu-id="eb394-181">a.</span></span> <span data-ttu-id="eb394-182">Schakel **aanmelden bij sociale Media**.</span><span class="sxs-lookup"><span data-stu-id="eb394-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="eb394-183">b.</span><span class="sxs-lookup"><span data-stu-id="eb394-183">b.</span></span> <span data-ttu-id="eb394-184">Open uw Base64-gecodeerde certificaat gedownload vanuit Azure-portal in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **OpenSSL certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="eb394-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="eb394-185">c.</span><span class="sxs-lookup"><span data-stu-id="eb394-185">c.</span></span> <span data-ttu-id="eb394-186">Typ in het tekstvak URL van SAML-SSO`https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="eb394-186">In the SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="eb394-187">d.</span><span class="sxs-lookup"><span data-stu-id="eb394-187">d.</span></span> <span data-ttu-id="eb394-188">Vervang in het tekstvak URL van SAML SSO `<your subdomain>` met een subdomein.</span><span class="sxs-lookup"><span data-stu-id="eb394-188">In the SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="eb394-189">e.</span><span class="sxs-lookup"><span data-stu-id="eb394-189">e.</span></span> <span data-ttu-id="eb394-190">Vervang in het tekstvak URL van SAML SSO `<saml sso url>` met de **SAML Single Sign-On Service-URL** u hebt gekopieerd uit de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="eb394-190">In the SAML SSO URL textbox, replace `<saml sso url>` with the **SAML Single Sign-On Service URL** you have copied from the Azure portal.</span></span>
   
    <span data-ttu-id="eb394-191">f.</span><span class="sxs-lookup"><span data-stu-id="eb394-191">f.</span></span> <span data-ttu-id="eb394-192">Klik op **instellingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="eb394-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="eb394-193">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="eb394-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="eb394-194">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="eb394-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="eb394-195">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eb394-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eb394-196">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="eb394-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="eb394-197">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="eb394-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="eb394-199">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="eb394-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="eb394-200">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="eb394-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eb394-202">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="eb394-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eb394-204">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eb394-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eb394-206">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="eb394-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eb394-208">a.</span><span class="sxs-lookup"><span data-stu-id="eb394-208">a.</span></span> <span data-ttu-id="eb394-209">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eb394-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eb394-210">b.</span><span class="sxs-lookup"><span data-stu-id="eb394-210">b.</span></span> <span data-ttu-id="eb394-211">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eb394-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eb394-212">c.</span><span class="sxs-lookup"><span data-stu-id="eb394-212">c.</span></span> <span data-ttu-id="eb394-213">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="eb394-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="eb394-214">d.</span><span class="sxs-lookup"><span data-stu-id="eb394-214">d.</span></span> <span data-ttu-id="eb394-215">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="eb394-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="eb394-216">Een testgebruiker vice maken</span><span class="sxs-lookup"><span data-stu-id="eb394-216">Creating a Deputy test user</span></span>

<span data-ttu-id="eb394-217">Om Azure AD-gebruikers zich aanmelden bij vice, moeten ze worden ingericht in vice.</span><span class="sxs-lookup"><span data-stu-id="eb394-217">To enable Azure AD users to log in to Deputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="eb394-218">In geval van een vice is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="eb394-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="eb394-219">Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="eb394-219">To provision a user account, perform the following steps:</span></span>
1. <span data-ttu-id="eb394-220">Meld u aan bij uw bedrijf vice site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="eb394-220">Log in to your Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="eb394-221">Klik op het bovenste navigatiedeelvenster op **mensen**.</span><span class="sxs-lookup"><span data-stu-id="eb394-221">On the top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="eb394-222">![Mensen](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "personen")</span><span class="sxs-lookup"><span data-stu-id="eb394-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="eb394-223">Klik op de **mensen toevoegen** en klik op **toevoegen één persoon**.</span><span class="sxs-lookup"><span data-stu-id="eb394-223">Click the **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="eb394-224">![Personen toevoegen](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "personen toevoegen")</span><span class="sxs-lookup"><span data-stu-id="eb394-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="eb394-225">Voer de volgende stappen uit en klik op **opslaan en uit te nodigen**.</span><span class="sxs-lookup"><span data-stu-id="eb394-225">Perform the following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="eb394-226">![Nieuwe gebruiker](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "nieuwe gebruiker")</span><span class="sxs-lookup"><span data-stu-id="eb394-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="eb394-227">a.</span><span class="sxs-lookup"><span data-stu-id="eb394-227">a.</span></span> <span data-ttu-id="eb394-228">In de **naam** textbox typenaam van de gebruiker zoals **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eb394-228">In the **Name** textbox, type name of the user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="eb394-229">b.</span><span class="sxs-lookup"><span data-stu-id="eb394-229">b.</span></span> <span data-ttu-id="eb394-230">In de **e** textbox, typ de e-mailadres van een Azure AD-account dat u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="eb394-230">In the **Email** textbox, type the email address of an Azure AD account you want to provision.</span></span>
   
   <span data-ttu-id="eb394-231">c.</span><span class="sxs-lookup"><span data-stu-id="eb394-231">c.</span></span> <span data-ttu-id="eb394-232">In de **op werkt** textbox, typ de bedrijfsnaam.</span><span class="sxs-lookup"><span data-stu-id="eb394-232">In the **Work at** textbox, type the business name.</span></span>
   
   <span data-ttu-id="eb394-233">d.</span><span class="sxs-lookup"><span data-stu-id="eb394-233">d.</span></span> <span data-ttu-id="eb394-234">Klik op **opslaan en uit te nodigen** knop.</span><span class="sxs-lookup"><span data-stu-id="eb394-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="eb394-235">De accounthouder AAD ontvangt een e-mailbericht en volgt een koppeling om hun account te bevestigen voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="eb394-235">The AAD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="eb394-236">U kunt andere vice gebruiker account hulpmiddelen voor het maken of API's die is geleverd door vice aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="eb394-236">You can use any other Deputy user account creation tools or APIs provided by Deputy to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="eb394-237">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb394-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="eb394-238">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan vice.</span><span class="sxs-lookup"><span data-stu-id="eb394-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Deputy.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="eb394-240">**Britta Simon om aan te wijzen vice, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="eb394-240">**To assign Britta Simon to Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="eb394-241">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="eb394-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="eb394-243">Selecteer in de lijst met toepassingen **vice**.</span><span class="sxs-lookup"><span data-stu-id="eb394-243">In the applications list, select **Deputy**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="eb394-245">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="eb394-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="eb394-247">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="eb394-247">Click **Add** button.</span></span> <span data-ttu-id="eb394-248">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eb394-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="eb394-250">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="eb394-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="eb394-251">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eb394-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eb394-252">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="eb394-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eb394-253">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="eb394-253">Testing single sign-on</span></span>

<span data-ttu-id="eb394-254">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="eb394-254">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="eb394-255">Als u op de tegel vice in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing vice.</span><span class="sxs-lookup"><span data-stu-id="eb394-255">When you click the Deputy tile in the Access Panel, you should get automatically signed-on to your Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eb394-256">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="eb394-256">Additional resources</span></span>

* [<span data-ttu-id="eb394-257">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb394-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eb394-258">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eb394-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

