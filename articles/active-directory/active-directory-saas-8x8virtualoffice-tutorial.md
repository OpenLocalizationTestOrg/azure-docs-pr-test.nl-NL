---
title: 'Zelfstudie: Azure Active Directory-integratie met 8 x 8 virtuele Office | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en 8 x 8 virtuele Office.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d8dcf0171b93fec15347e810a1b525bd815dbf04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="dd999-103">Zelfstudie: Azure Active Directory-integratie met 8 x 8 virtuele Office</span><span class="sxs-lookup"><span data-stu-id="dd999-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="dd999-104">In deze zelfstudie leert u hoe 8 x 8 virtuele Office integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dd999-104">In this tutorial, you learn how to integrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dd999-105">Integratie van 8 x 8 virtuele Office met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="dd999-105">Integrating 8x8 Virtual Office with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dd999-106">U kunt beheren in Azure AD die toegang tot 8 x 8 virtuele Office heeft</span><span class="sxs-lookup"><span data-stu-id="dd999-106">You can control in Azure AD who has access to 8x8 Virtual Office</span></span>
- <span data-ttu-id="dd999-107">U kunt uw gebruikers automatisch ophalen aangemeld bij 8 x 8 virtuele Office (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="dd999-107">You can enable your users to automatically get signed-on to 8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dd999-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="dd999-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dd999-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dd999-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd999-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="dd999-110">Prerequisites</span></span>

<span data-ttu-id="dd999-111">Voor het configureren van Azure AD-integratie met 8 x 8 virtuele Office, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="dd999-111">To configure Azure AD integration with 8x8 Virtual Office, you need the following items:</span></span>

- <span data-ttu-id="dd999-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="dd999-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dd999-113">Een 8 x 8 virtuele Office eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="dd999-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dd999-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="dd999-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dd999-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="dd999-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dd999-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="dd999-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dd999-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dd999-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dd999-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="dd999-118">Scenario description</span></span>
<span data-ttu-id="dd999-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="dd999-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dd999-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="dd999-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dd999-121">8 x 8 virtuele Office toevoegen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="dd999-121">Adding 8x8 Virtual Office from the gallery</span></span>
2. <span data-ttu-id="dd999-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="dd999-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-the-gallery"></a><span data-ttu-id="dd999-123">8 x 8 virtuele Office toevoegen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="dd999-123">Adding 8x8 Virtual Office from the gallery</span></span>
<span data-ttu-id="dd999-124">Voor het configureren van de integratie van 8 x 8 virtuele Office in Azure AD, moet u 8 x 8 virtuele Office uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="dd999-124">To configure the integration of 8x8 Virtual Office into Azure AD, you need to add 8x8 Virtual Office from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dd999-125">**Als u wilt toevoegen 8 x 8 virtuele Office uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="dd999-125">**To add 8x8 Virtual Office from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dd999-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="dd999-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dd999-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="dd999-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dd999-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="dd999-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="dd999-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dd999-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="dd999-133">Typ in het zoekvak **8 x 8 virtuele Office**.</span><span class="sxs-lookup"><span data-stu-id="dd999-133">In the search box, type **8x8 Virtual Office**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="dd999-135">Selecteer in het deelvenster resultaten **8 x 8 virtuele Office**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="dd999-135">In the results panel, select **8x8 Virtual Office**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dd999-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="dd999-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dd999-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met 8 x 8 die virtuele Office op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="dd999-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dd999-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de equivalente gebruiker in 8 x 8 virtuele Office aan een gebruiker in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="dd999-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 8x8 Virtual Office is to a user in Azure AD.</span></span> <span data-ttu-id="dd999-140">Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in 8 x 8 virtuele Office moet tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="dd999-140">In other words, a link relationship between an Azure AD user and the related user in 8x8 Virtual Office needs to be established.</span></span>

<span data-ttu-id="dd999-141">Wijs in 8 x 8 virtuele kantoor, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="dd999-141">In 8x8 Virtual Office, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dd999-142">Om te configureren en testen van Azure AD eenmalige aanmelding met 8 x 8 virtuele Office, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="dd999-142">To configure and test Azure AD single sign-on with 8x8 Virtual Office, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dd999-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dd999-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dd999-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd999-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dd999-145">**[Maken van een testgebruiker van 8 x 8 virtuele Office](#creating-a-8x8-virtual-office-test-user)**  - 8 x 8 virtuele Office die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="dd999-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - to have a counterpart of Britta Simon in 8x8 Virtual Office that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dd999-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="dd999-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dd999-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="dd999-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dd999-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="dd999-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dd999-149">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw 8 x 8 virtuele Office-toepassing.</span><span class="sxs-lookup"><span data-stu-id="dd999-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="dd999-150">**Voor het configureren van Azure AD eenmalige aanmelding met 8 x 8 virtuele Office, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="dd999-150">**To configure Azure AD single sign-on with 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="dd999-151">In de Azure-portal op de **8 x 8 virtuele Office** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="dd999-151">In the Azure portal, on the **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="dd999-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="dd999-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="dd999-155">Op de **8 x 8 virtuele Office domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="dd999-155">On the **8x8 Virtual Office Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="dd999-157">a.</span><span class="sxs-lookup"><span data-stu-id="dd999-157">a.</span></span> <span data-ttu-id="dd999-158">In de **id** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="dd999-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="dd999-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="dd999-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="dd999-160">b.</span><span class="sxs-lookup"><span data-stu-id="dd999-160">b.</span></span> <span data-ttu-id="dd999-161">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="dd999-161">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="dd999-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="dd999-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dd999-163">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="dd999-163">These values are not real.</span></span> <span data-ttu-id="dd999-164">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="dd999-164">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="dd999-165">Neem contact op met [8 x 8 virtuele Office ondersteuningsteam](https://www.8x8.com/about-us/contact-us) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="dd999-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) to get these values.</span></span>
 


4. <span data-ttu-id="dd999-166">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Raw)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="dd999-166">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="dd999-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="dd999-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dd999-170">Op de **8 x 8 virtuele Office-configuratie** sectie, klikt u op **configureren 8 x 8 virtuele Office** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="dd999-170">On the **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dd999-171">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="dd999-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="dd999-173">Eenmalige aanmelding in uw tenant, 8 x 8 virtuele Office als beheerder.</span><span class="sxs-lookup"><span data-stu-id="dd999-173">Sign-on to your 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="dd999-174">Selecteer **virtuele Office Account Mgr** in deelvenster van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="dd999-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![Zijde van de App configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="dd999-176">Selecteer **Business** account te beheren en klikt u op **aanmelden** knop.</span><span class="sxs-lookup"><span data-stu-id="dd999-176">Select **Business** account to manage and click **Sign In** button.</span></span>
   
    ![Zijde van de App configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="dd999-178">Klik op **Accounts** tabblad in de menulijst.</span><span class="sxs-lookup"><span data-stu-id="dd999-178">Click **Accounts** tab in the menu list.</span></span>
   
    ![Zijde van de App configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="dd999-180">Klik op **eenmalige aanmelding** in de lijst van Accounts.</span><span class="sxs-lookup"><span data-stu-id="dd999-180">Click **Single Sign On** in the list of Accounts.</span></span>
   
    ![Zijde van de App configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="dd999-182">Selecteer **eenmalige aanmelding** onder verificatiemethode en op **SAML**.</span><span class="sxs-lookup"><span data-stu-id="dd999-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![Zijde van de App configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="dd999-184">Kopiëren **SAML SSO URL**, **Kana uit de URL van één** en **URL-verlener** van Azure AD **URL aanmelden**, **URL afmelden**  en **URL-verlener** in 8 x 8 virtuele Office.</span><span class="sxs-lookup"><span data-stu-id="dd999-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD to **Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![Zijde van de App configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="dd999-186">Klik op **Browser** om het certificaat dat u hebt gedownload van Azure AD te uploaden en klik op de **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="dd999-186">Click **Browser** button to upload the certificate which you downloaded from Azure AD, and click the **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="dd999-187">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="dd999-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dd999-188">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="dd999-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dd999-189">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dd999-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dd999-190">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="dd999-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="dd999-191">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="dd999-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="dd999-193">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="dd999-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dd999-194">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="dd999-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dd999-196">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="dd999-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dd999-198">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dd999-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dd999-200">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="dd999-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dd999-202">a.</span><span class="sxs-lookup"><span data-stu-id="dd999-202">a.</span></span> <span data-ttu-id="dd999-203">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dd999-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dd999-204">b.</span><span class="sxs-lookup"><span data-stu-id="dd999-204">b.</span></span> <span data-ttu-id="dd999-205">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dd999-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dd999-206">c.</span><span class="sxs-lookup"><span data-stu-id="dd999-206">c.</span></span> <span data-ttu-id="dd999-207">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="dd999-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dd999-208">d.</span><span class="sxs-lookup"><span data-stu-id="dd999-208">d.</span></span> <span data-ttu-id="dd999-209">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="dd999-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="dd999-210">Maken van een 8 x 8 virtuele Office-testgebruiker</span><span class="sxs-lookup"><span data-stu-id="dd999-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="dd999-211">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in 8 x 8 virtuele Office.</span><span class="sxs-lookup"><span data-stu-id="dd999-211">The objective of this section is to create a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="dd999-212">8 x 8 virtuele Office ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="dd999-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="dd999-213">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="dd999-213">There is no action item for you in this section.</span></span> <span data-ttu-id="dd999-214">Een nieuwe gebruiker is gemaakt tijdens een poging tot toegang tot 8 x 8 virtuele Office als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="dd999-214">A new user is created during an attempt to access 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="dd999-215">Als u een gebruiker handmatig maken wilt, moet u contact op met de [8 x 8 virtuele Office ondersteuningsteam](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="dd999-215">If you need to create a user manually, you need to contact the [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dd999-216">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd999-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dd999-217">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan 8 x 8 virtuele Office.</span><span class="sxs-lookup"><span data-stu-id="dd999-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 8x8 Virtual Office.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="dd999-219">**Britta Simon om aan te wijzen 8 x 8 virtuele Office, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="dd999-219">**To assign Britta Simon to 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="dd999-220">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="dd999-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="dd999-222">Selecteer in de lijst met toepassingen **8 x 8 virtuele Office**.</span><span class="sxs-lookup"><span data-stu-id="dd999-222">In the applications list, select **8x8 Virtual Office**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="dd999-224">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="dd999-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="dd999-226">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="dd999-226">Click **Add** button.</span></span> <span data-ttu-id="dd999-227">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dd999-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="dd999-229">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="dd999-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dd999-230">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dd999-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dd999-231">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dd999-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dd999-232">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="dd999-232">Testing single sign-on</span></span>

<span data-ttu-id="dd999-233">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="dd999-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dd999-234">Als u op de tegel 8 x 8 virtuele Office in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw 8 x 8 virtuele Office-toepassing.</span><span class="sxs-lookup"><span data-stu-id="dd999-234">When you click the 8x8 Virtual Office tile in the Access Panel, you should get automatically signed-on to your 8x8 Virtual Office application.</span></span>
<span data-ttu-id="dd999-235">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="dd999-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dd999-236">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="dd999-236">Additional resources</span></span>

* [<span data-ttu-id="dd999-237">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd999-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dd999-238">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dd999-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png

