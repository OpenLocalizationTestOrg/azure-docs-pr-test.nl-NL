---
title: 'Zelfstudie: Azure Active Directory-integratie met werkplek door Facebook | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en werkplek met Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 1590a66f215f0c093d24ff602c0ad951ba1e1eea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="1c56b-103">Zelfstudie: Azure Active Directory-integratie met werkplek door Facebook</span><span class="sxs-lookup"><span data-stu-id="1c56b-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="1c56b-104">In deze zelfstudie leert u hoe werkplek door Facebook integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1c56b-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1c56b-105">Werkplek door Facebook integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1c56b-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1c56b-106">U kunt beheren in Azure AD die toegang tot de werkplek door Facebook heeft</span><span class="sxs-lookup"><span data-stu-id="1c56b-106">You can control in Azure AD who has access to Workplace by Facebook</span></span>
- <span data-ttu-id="1c56b-107">U kunt uw gebruikers automatisch ophalen aangemeld bij werkplek door Facebook (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="1c56b-107">You can enable your users to automatically get signed-on to Workplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1c56b-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="1c56b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1c56b-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1c56b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c56b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1c56b-110">Prerequisites</span></span>

<span data-ttu-id="1c56b-111">Voor het configureren van Azure AD-integratie met werkplek door Facebook, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="1c56b-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="1c56b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1c56b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1c56b-113">Een werkplek met eenmalige aanmelding Facebook abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="1c56b-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1c56b-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1c56b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1c56b-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1c56b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1c56b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1c56b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1c56b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c56b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1c56b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1c56b-118">Scenario description</span></span>
<span data-ttu-id="1c56b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1c56b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1c56b-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1c56b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1c56b-121">Werkplek door Facebook uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1c56b-121">Adding Workplace by Facebook from the gallery</span></span>
2. <span data-ttu-id="1c56b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1c56b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="1c56b-123">Werkplek door Facebook uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1c56b-123">Adding Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="1c56b-124">Voor het configureren van de integratie van werkplek door Facebook in Azure AD, moet u werkplek door Facebook uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1c56b-124">To configure the integration of Workplace by Facebook into Azure AD, you need to add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1c56b-125">**Als u wilt toevoegen werkplek door Facebook uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1c56b-125">**To add Workplace by Facebook from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1c56b-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1c56b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1c56b-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1c56b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1c56b-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1c56b-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="1c56b-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1c56b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="1c56b-133">Typ in het zoekvak **werkplek door Facebook**.</span><span class="sxs-lookup"><span data-stu-id="1c56b-133">In the search box, type **Workplace by Facebook**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="1c56b-135">Selecteer in het deelvenster resultaten **werkplek door Facebook**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1c56b-135">In the results panel, select **Workplace by Facebook**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1c56b-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1c56b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1c56b-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met werkplek door Facebook op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="1c56b-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1c56b-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in werkplek door Facebook is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c56b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="1c56b-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de gebruiker op de werkplek door Facebook tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="1c56b-140">In other words, a link relationship between an Azure AD user and the related user in Workplace by Facebook needs to be established.</span></span>

<span data-ttu-id="1c56b-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in werkplek met Facebook.</span><span class="sxs-lookup"><span data-stu-id="1c56b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="1c56b-142">Om te configureren en testen van Azure AD eenmalige aanmelding met werkplek door Facebook, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="1c56b-142">To configure and test Azure AD single sign-on with Workplace by Facebook, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1c56b-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1c56b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1c56b-144">**[Configureren van Herauthenticatie frequentie](#configuring-reauthentication-frequency)**  - werkplek vraagt om een SAML-controle configureren.</span><span class="sxs-lookup"><span data-stu-id="1c56b-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - to configure Workplace to prompt for a SAML check.</span></span>
3. <span data-ttu-id="1c56b-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1c56b-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="1c56b-146">**[Maken van een werkplek door Facebook testgebruiker](#creating-a-workplace-by-facebook-test-user)**  - werkplek door Facebook die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="1c56b-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - to have a counterpart of Britta Simon in Workplace by Facebook that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="1c56b-147">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1c56b-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="1c56b-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1c56b-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1c56b-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1c56b-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1c56b-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren op uw werkplek met Facebook-toepassing.</span><span class="sxs-lookup"><span data-stu-id="1c56b-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="1c56b-151">**Voor het configureren van Azure AD eenmalige aanmelding met werkplek door Facebook, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1c56b-151">**To configure Azure AD single sign-on with Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="1c56b-152">In de Azure-portal op de **werkplek door Facebook** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1c56b-152">In the Azure portal, on the **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1c56b-154">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1c56b-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="1c56b-156">Op de **werkplek Facebook-domein en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1c56b-156">On the **Workplace by Facebook Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="1c56b-158">a.</span><span class="sxs-lookup"><span data-stu-id="1c56b-158">a.</span></span> <span data-ttu-id="1c56b-159">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<instancename>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="1c56b-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="1c56b-160">b.</span><span class="sxs-lookup"><span data-stu-id="1c56b-160">b.</span></span> <span data-ttu-id="1c56b-161">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://www.facebook.com/company/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1c56b-161">In the **Identifier** textbox, type a URL using the following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1c56b-162">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="1c56b-162">These values are not the real.</span></span> <span data-ttu-id="1c56b-163">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="1c56b-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1c56b-164">Neem contact op met [werkplek door Facebook Client-ondersteuningsteam](https://workplace.fb.com/faq/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="1c56b-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="1c56b-165">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1c56b-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="1c56b-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1c56b-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1c56b-169">Op de **werkplek door Facebook configuratie** sectie, klikt u op **werkplek configureren door Facebook** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="1c56b-169">On the **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1c56b-170">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="1c56b-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="1c56b-172">In een ander browservenster, meld u aan bij uw werkplek door Facebook bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="1c56b-172">In a different web browser window, login to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="1c56b-173">Als onderdeel van het SAML-verificatieproces mag werkplek queryreeksen van de grootte van maximaal 2,5 kB gebruiken om de parameters doorgeven aan Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c56b-173">As part of the SAML authentication process, Workplace may utilize query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="1c56b-174">In de **bedrijf Dashboard**, gaat u naar de **verificatie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="1c56b-174">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="1c56b-175">Onder **SAML-verificatie**, selecteer **eenmalige aanmelding alleen** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="1c56b-175">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="1c56b-176">Voer de waarden die zijn gekopieerd uit **werkplek door Facebook-configuratie** sectie van de Azure portal naar de bijbehorende velden:</span><span class="sxs-lookup"><span data-stu-id="1c56b-176">Input the values copied from **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="1c56b-177">In **SAML URL** textbox, plak de waarde van **Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1c56b-177">In **SAML URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="1c56b-178">In **URL-verlener SAML textbox**, plak de waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1c56b-178">In **SAML Issuer URL textbox**, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="1c56b-179">In **SAML afmelding omleiden** (optioneel), plak de waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1c56b-179">In **SAML Logout Redirect** (Optional), paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="1c56b-180">Open uw **base-64 gecodeerde certificaat** in Kladblok van Azure portal hebt gedownload, kopieert u de inhoud ervan naar het Klembord en plakt u deze naar de **SAML certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="1c56b-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="1c56b-181">Mogelijk moet u de doelgroep URL invoeren, de URL van de geadresseerde, en de URL van de ACS (Assertion Consumer-Service) die worden vermeld onder de **SAML-configuratie** sectie.</span><span class="sxs-lookup"><span data-stu-id="1c56b-181">You may need to enter the Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="1c56b-182">Ga naar de onderkant van de sectie en klik op de **Test SSO** knop.</span><span class="sxs-lookup"><span data-stu-id="1c56b-182">Scroll to the bottom of the section and click the **Test SSO** button.</span></span> <span data-ttu-id="1c56b-183">Dit resulteert in een pop-upvenster wordt weergegeven met Azure AD-aanmeldingspagina weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1c56b-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="1c56b-184">Geef uw referenties in als normaal om te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="1c56b-184">Enter your credentials in as normal to authenticate.</span></span> 

    <span data-ttu-id="1c56b-185">**Voor probleemoplossing:** Zorg ervoor dat het e-mailadres dat wordt geretourneerd back vanuit Azure AD is hetzelfde als het werkplekaccount dat u bent aangemeld.</span><span class="sxs-lookup"><span data-stu-id="1c56b-185">**Troubleshooting:** Ensure the email address being returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="1c56b-186">Zodra de test is voltooid, Ga naar de onderkant van de pagina en klik op de **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1c56b-186">Once the test has been completed successfully, scroll to the bottom of the page and click the **Save** button.</span></span>

14. <span data-ttu-id="1c56b-187">Alle gebruikers met behulp van werkplek wordt nu weergegeven met Azure AD-aanmeldingspagina voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="1c56b-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="1c56b-188">**SAML afmelding omleiden (optioneel)** -</span><span class="sxs-lookup"><span data-stu-id="1c56b-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="1c56b-189">U kunt desgewenst een SAML afmelding-Url, die kan worden gebruikt om te verwijzen op de pagina voor Azure AD-Meld u af te configureren.</span><span class="sxs-lookup"><span data-stu-id="1c56b-189">You can choose to optionally configure a SAML Logout Url, which can be used to point at Azure AD's logout page.</span></span> <span data-ttu-id="1c56b-190">Als deze instelling is ingeschakeld en geconfigureerd, wordt de gebruiker niet langer worden omgeleid naar de pagina Werkplek afmelden.</span><span class="sxs-lookup"><span data-stu-id="1c56b-190">When this setting is enabled and configured, the user will no longer be directed to the Workplace logout page.</span></span> <span data-ttu-id="1c56b-191">In plaats daarvan wordt de gebruiker wordt omgeleid naar de url die is toegevoegd in de instelling voor het omleiden van SAML-afmelden.</span><span class="sxs-lookup"><span data-stu-id="1c56b-191">Instead, the user will be redirected to the url that was added in the SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="1c56b-192">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="1c56b-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1c56b-193">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="1c56b-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1c56b-194">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1c56b-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="1c56b-195">Herauthenticatie frequentie configureren</span><span class="sxs-lookup"><span data-stu-id="1c56b-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="1c56b-196">U kunt configureren werkplek om aan te vragen om een SAML-controle elke dag, drie dagen, week, twee weken, maanden of nooit.</span><span class="sxs-lookup"><span data-stu-id="1c56b-196">You can configure Workplace to prompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="1c56b-197">De minimumwaarde voor de SAML-controle voor mobiele toepassingen is ingesteld op één week.</span><span class="sxs-lookup"><span data-stu-id="1c56b-197">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="1c56b-198">U kunt ook een SAML opnieuw instellen voor alle gebruikers met behulp van de knop afdwingen: vereisen SAML-verificatie voor alle gebruikers nu.</span><span class="sxs-lookup"><span data-stu-id="1c56b-198">You can also force a SAML reset for all users using the button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1c56b-199">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1c56b-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="1c56b-200">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1c56b-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="1c56b-202">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1c56b-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1c56b-203">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1c56b-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1c56b-205">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1c56b-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1c56b-207">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1c56b-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1c56b-209">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1c56b-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1c56b-211">a.</span><span class="sxs-lookup"><span data-stu-id="1c56b-211">a.</span></span> <span data-ttu-id="1c56b-212">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1c56b-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1c56b-213">b.</span><span class="sxs-lookup"><span data-stu-id="1c56b-213">b.</span></span> <span data-ttu-id="1c56b-214">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1c56b-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1c56b-215">c.</span><span class="sxs-lookup"><span data-stu-id="1c56b-215">c.</span></span> <span data-ttu-id="1c56b-216">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1c56b-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1c56b-217">d.</span><span class="sxs-lookup"><span data-stu-id="1c56b-217">d.</span></span> <span data-ttu-id="1c56b-218">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1c56b-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="1c56b-219">Maken van een werkplek door Facebook testgebruiker</span><span class="sxs-lookup"><span data-stu-id="1c56b-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="1c56b-220">In deze sectie wordt een gebruiker met de naam Britta Simon in werkplek gemaakt door Facebook.</span><span class="sxs-lookup"><span data-stu-id="1c56b-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="1c56b-221">Werkplek door Facebook ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="1c56b-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="1c56b-222">Er is geen actie voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="1c56b-222">There is no action for you in this section.</span></span> <span data-ttu-id="1c56b-223">Als een gebruiker niet op de werkplek door Facebook bestaat, wordt een nieuw gemaakt wanneer u probeert te openen, werkplek met Facebook.</span><span class="sxs-lookup"><span data-stu-id="1c56b-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="1c56b-224">Als u wilt een gebruiker handmatig maken, neem contact op met [werkplek door ondersteuningsteam Facebook-Client](https://workplace.fb.com/faq/)</span><span class="sxs-lookup"><span data-stu-id="1c56b-224">If you need to create a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1c56b-225">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c56b-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1c56b-226">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang te verlenen aan een werkplek met Facebook.</span><span class="sxs-lookup"><span data-stu-id="1c56b-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workplace by Facebook.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="1c56b-228">**Als u wilt toewijzen Britta Simon werkplek door Facebook, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1c56b-228">**To assign Britta Simon to Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="1c56b-229">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1c56b-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1c56b-231">Selecteer in de lijst met toepassingen **werkplek door Facebook**.</span><span class="sxs-lookup"><span data-stu-id="1c56b-231">In the applications list, select **Workplace by Facebook**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="1c56b-233">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1c56b-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="1c56b-235">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1c56b-235">Click **Add** button.</span></span> <span data-ttu-id="1c56b-236">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1c56b-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="1c56b-238">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1c56b-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1c56b-239">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1c56b-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1c56b-240">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1c56b-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1c56b-241">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1c56b-241">Testing single sign-on</span></span>

<span data-ttu-id="1c56b-242">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="1c56b-242">If you want to test your single sign-on settings, open the Access Panel.</span></span>
<span data-ttu-id="1c56b-243">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1c56b-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1c56b-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1c56b-244">Additional resources</span></span>

* [<span data-ttu-id="1c56b-245">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c56b-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1c56b-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1c56b-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="1c56b-247">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="1c56b-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

