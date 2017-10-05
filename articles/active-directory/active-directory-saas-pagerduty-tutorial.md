---
title: 'Zelfstudie: Azure Active Directory-integratie met PagerDuty | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en PagerDuty.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: bf5263ce4d8fbc231029c101f167f4b55a921e60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="b1c48-103">Zelfstudie: Azure Active Directory-integratie met PagerDuty</span><span class="sxs-lookup"><span data-stu-id="b1c48-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="b1c48-104">In deze zelfstudie leert u hoe PagerDuty integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b1c48-104">In this tutorial, you learn how to integrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b1c48-105">PagerDuty integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b1c48-105">Integrating PagerDuty with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b1c48-106">U kunt beheren in Azure AD die toegang tot PagerDuty heeft</span><span class="sxs-lookup"><span data-stu-id="b1c48-106">You can control in Azure AD who has access to PagerDuty</span></span>
- <span data-ttu-id="b1c48-107">U kunt uw gebruikers automatisch ophalen aangemeld bij PagerDuty (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="b1c48-107">You can enable your users to automatically get signed-on to PagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b1c48-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b1c48-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b1c48-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b1c48-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1c48-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b1c48-110">Prerequisites</span></span>

<span data-ttu-id="b1c48-111">Voor het configureren van Azure AD-integratie met PagerDuty, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b1c48-111">To configure Azure AD integration with PagerDuty, you need the following items:</span></span>

- <span data-ttu-id="b1c48-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b1c48-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b1c48-113">Een PagerDuty eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b1c48-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b1c48-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b1c48-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b1c48-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b1c48-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b1c48-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b1c48-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b1c48-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b1c48-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b1c48-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b1c48-118">Scenario description</span></span>
<span data-ttu-id="b1c48-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b1c48-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b1c48-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b1c48-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b1c48-121">PagerDuty uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b1c48-121">Adding PagerDuty from the gallery</span></span>
2. <span data-ttu-id="b1c48-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b1c48-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-the-gallery"></a><span data-ttu-id="b1c48-123">PagerDuty uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b1c48-123">Adding PagerDuty from the gallery</span></span>
<span data-ttu-id="b1c48-124">Voor het configureren van de integratie van PagerDuty in Azure AD, moet u PagerDuty uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b1c48-124">To configure the integration of PagerDuty into Azure AD, you need to add PagerDuty from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b1c48-125">**Als u wilt toevoegen PagerDuty uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b1c48-125">**To add PagerDuty from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b1c48-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b1c48-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="b1c48-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b1c48-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b1c48-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b1c48-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="b1c48-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b1c48-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="b1c48-133">Typ in het zoekvak **PagerDuty**, selecteer **PagerDuty** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b1c48-133">In the search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b1c48-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1c48-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b1c48-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met PagerDuty op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b1c48-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b1c48-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in PagerDuty is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1c48-137">For single sign-on to work, Azure AD needs to know what the counterpart user in PagerDuty is to a user in Azure AD.</span></span> <span data-ttu-id="b1c48-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in PagerDuty tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="b1c48-138">In other words, a link relationship between an Azure AD user and the related user in PagerDuty needs to be established.</span></span>

<span data-ttu-id="b1c48-139">Wijs in PagerDuty, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="b1c48-139">In PagerDuty, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b1c48-140">Om te configureren en testen van Azure AD eenmalige aanmelding met PagerDuty, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="b1c48-140">To configure and test Azure AD single sign-on with PagerDuty, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b1c48-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b1c48-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b1c48-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b1c48-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b1c48-143">**[Maak een testgebruiker PagerDuty](#create-a-pagerduty-test-user)**  - PagerDuty die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="b1c48-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - to have a counterpart of Britta Simon in PagerDuty that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b1c48-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b1c48-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b1c48-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b1c48-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b1c48-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b1c48-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b1c48-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing PagerDuty configureren.</span><span class="sxs-lookup"><span data-stu-id="b1c48-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="b1c48-148">**Voor het configureren van Azure AD eenmalige aanmelding met PagerDuty, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b1c48-148">**To configure Azure AD single sign-on with PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="b1c48-149">In de Azure-portal op de **PagerDuty** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b1c48-149">In the Azure portal, on the **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b1c48-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b1c48-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. <span data-ttu-id="b1c48-153">Op de **PagerDuty domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b1c48-153">On the **PagerDuty Domain and URLs** section, perform the following steps:</span></span>

    ![URL's en PagerDuty domein eenmalige aanmelding informatie](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="b1c48-155">a.</span><span class="sxs-lookup"><span data-stu-id="b1c48-155">a.</span></span> <span data-ttu-id="b1c48-156">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="b1c48-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="b1c48-157">b.</span><span class="sxs-lookup"><span data-stu-id="b1c48-157">b.</span></span> <span data-ttu-id="b1c48-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="b1c48-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b1c48-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="b1c48-159">These values are not real.</span></span> <span data-ttu-id="b1c48-160">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="b1c48-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b1c48-161">Neem contact op met [PagerDuty Client ondersteuningsteam](https://www.pagerduty.com/support/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="b1c48-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) to get these values.</span></span> 

4. <span data-ttu-id="b1c48-162">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b1c48-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. <span data-ttu-id="b1c48-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b1c48-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b1c48-166">Op de **PagerDuty configuratie** sectie, klikt u op **configureren PagerDuty** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="b1c48-166">On the **PagerDuty Configuration** section, click **Configure PagerDuty** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b1c48-167">Kopieer de **Sign-Out URL's en SAML Single Sign-On Service** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="b1c48-167">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![PagerDuty configuratie](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. <span data-ttu-id="b1c48-169">In een ander browservenster, meld u bij uw bedrijf Pagerduty site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b1c48-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

8. <span data-ttu-id="b1c48-170">Klik in het menu bovenaan op **Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="b1c48-170">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="b1c48-171">![Instellingen account](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Accountinstellingen")</span><span class="sxs-lookup"><span data-stu-id="b1c48-171">![Account Settings](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

9. <span data-ttu-id="b1c48-172">Klik op **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b1c48-172">Click **Single Sign-on**.</span></span>
   
    <span data-ttu-id="b1c48-173">![Eenmalige aanmelding](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="b1c48-173">![Single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

10. <span data-ttu-id="b1c48-174">Op de **Schakel eenmalige aanmelding (SSO)** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b1c48-174">On the **Enable Single Sign-on (SSO)** page, perform the following steps:</span></span>
   
    <span data-ttu-id="b1c48-175">![Eenmalige aanmelding inschakelen](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "eenmalige aanmelding inschakelen")</span><span class="sxs-lookup"><span data-stu-id="b1c48-175">![Enable single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>
   
    <span data-ttu-id="b1c48-176">a.</span><span class="sxs-lookup"><span data-stu-id="b1c48-176">a.</span></span> <span data-ttu-id="b1c48-177">Open uw base-64 gecodeerde certificaat gedownload vanuit Azure-portal in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **X.509-certificaat** tekstvak</span><span class="sxs-lookup"><span data-stu-id="b1c48-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="b1c48-178">b.</span><span class="sxs-lookup"><span data-stu-id="b1c48-178">b.</span></span> <span data-ttu-id="b1c48-179">In de **aanmeldings-URL** textbox plakken **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b1c48-179">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="b1c48-180">c.</span><span class="sxs-lookup"><span data-stu-id="b1c48-180">c.</span></span> <span data-ttu-id="b1c48-181">In de **afmelding URL** textbox plakken **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b1c48-181">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="b1c48-182">d.</span><span class="sxs-lookup"><span data-stu-id="b1c48-182">d.</span></span> <span data-ttu-id="b1c48-183">Selecteer **Single Sign-on inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="b1c48-183">Select **Turn on Single Sign-on**.</span></span>
 
    <span data-ttu-id="b1c48-184">e.</span><span class="sxs-lookup"><span data-stu-id="b1c48-184">e.</span></span> <span data-ttu-id="b1c48-185">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b1c48-185">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="b1c48-186">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="b1c48-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b1c48-187">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="b1c48-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b1c48-188">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b1c48-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b1c48-189">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b1c48-189">Create an Azure AD test user</span></span>

<span data-ttu-id="b1c48-190">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b1c48-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="b1c48-192">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b1c48-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b1c48-193">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b1c48-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b1c48-195">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b1c48-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b1c48-197">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b1c48-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![De knop toevoegen](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b1c48-199">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b1c48-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Het dialoogvenster gebruiker](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b1c48-201">a.</span><span class="sxs-lookup"><span data-stu-id="b1c48-201">a.</span></span> <span data-ttu-id="b1c48-202">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b1c48-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b1c48-203">b.</span><span class="sxs-lookup"><span data-stu-id="b1c48-203">b.</span></span> <span data-ttu-id="b1c48-204">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b1c48-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b1c48-205">c.</span><span class="sxs-lookup"><span data-stu-id="b1c48-205">c.</span></span> <span data-ttu-id="b1c48-206">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b1c48-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b1c48-207">d.</span><span class="sxs-lookup"><span data-stu-id="b1c48-207">d.</span></span> <span data-ttu-id="b1c48-208">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b1c48-208">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="b1c48-209">Een testgebruiker PagerDuty maken</span><span class="sxs-lookup"><span data-stu-id="b1c48-209">Create a PagerDuty test user</span></span>

<span data-ttu-id="b1c48-210">Om Azure AD-gebruikers zich aanmelden bij PagerDuty, moeten ze worden ingericht in PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="b1c48-210">To enable Azure AD users to log in to PagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="b1c48-211">In het geval van PagerDuty is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="b1c48-211">In the case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="b1c48-212">U kunt andere Pagerduty gebruiker account hulpmiddelen voor het maken of API's geleverd door Pagerduty om in te richten Azure Active Directory-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="b1c48-212">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty to provision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="b1c48-213">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b1c48-213">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="b1c48-214">Meld u aan bij uw **Pagerduty** tenant.</span><span class="sxs-lookup"><span data-stu-id="b1c48-214">Log in to your **Pagerduty** tenant.</span></span>

2. <span data-ttu-id="b1c48-215">Klik in het menu bovenaan op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b1c48-215">In the menu on the top, click **Users**.</span></span>

3. <span data-ttu-id="b1c48-216">Klik op **gebruikers toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b1c48-216">Click **Add Users**.</span></span>
   
    <span data-ttu-id="b1c48-217">![Gebruikers toevoegen](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "gebruikers toevoegen")</span><span class="sxs-lookup"><span data-stu-id="b1c48-217">![Add Users](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Add Users")</span></span>

4.  <span data-ttu-id="b1c48-218">Op de **uitnodigen van uw team** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b1c48-218">On the **Invite your team** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="b1c48-219">![Uw team uitnodigen](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "uitnodigen van uw team")</span><span class="sxs-lookup"><span data-stu-id="b1c48-219">![Invite your team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="b1c48-220">a.</span><span class="sxs-lookup"><span data-stu-id="b1c48-220">a.</span></span> <span data-ttu-id="b1c48-221">Typ de **eerste en laatste naam** van gebruiker zoals **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b1c48-221">Type the **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="b1c48-222">b.</span><span class="sxs-lookup"><span data-stu-id="b1c48-222">b.</span></span> <span data-ttu-id="b1c48-223">Voer **e** adres van de gebruiker, zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="b1c48-223">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="b1c48-224">c.</span><span class="sxs-lookup"><span data-stu-id="b1c48-224">c.</span></span> <span data-ttu-id="b1c48-225">Klik op **toevoegen**, en klik vervolgens op **verzenden nodigt**.</span><span class="sxs-lookup"><span data-stu-id="b1c48-225">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="b1c48-226">Alle toegevoegde gebruikers ontvangen een uitnodiging voor een account PagerDuty maken.</span><span class="sxs-lookup"><span data-stu-id="b1c48-226">All added users will receive an invite to create a PagerDuty account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b1c48-227">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="b1c48-227">Assign the Azure AD test user</span></span>

<span data-ttu-id="b1c48-228">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="b1c48-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PagerDuty.</span></span>

![Toewijzen van de gebruikersrol][200]

<span data-ttu-id="b1c48-230">**Britta Simon om aan te wijzen PagerDuty, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b1c48-230">**To assign Britta Simon to PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="b1c48-231">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b1c48-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b1c48-233">Selecteer in de lijst met toepassingen **PagerDuty**.</span><span class="sxs-lookup"><span data-stu-id="b1c48-233">In the applications list, select **PagerDuty**.</span></span>

    ![De koppeling PagerDuty in de lijst met toepassingen](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. <span data-ttu-id="b1c48-235">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b1c48-235">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="b1c48-237">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b1c48-237">Click **Add** button.</span></span> <span data-ttu-id="b1c48-238">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b1c48-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="b1c48-240">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b1c48-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b1c48-241">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b1c48-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b1c48-242">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b1c48-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b1c48-243">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b1c48-243">Test single sign-on</span></span>

<span data-ttu-id="b1c48-244">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b1c48-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b1c48-245">Wanneer u klikt op de tegel PagerDuty in de Panelyou toegang moet krijgen automatisch aangemeld bij uw toepassing PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="b1c48-245">When you click the PagerDuty tile in the Access Panelyou should get automatically signed-on to your PagerDuty application.</span></span>

<span data-ttu-id="b1c48-246">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b1c48-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b1c48-247">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b1c48-247">Additional resources</span></span>

* [<span data-ttu-id="b1c48-248">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1c48-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b1c48-249">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b1c48-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

