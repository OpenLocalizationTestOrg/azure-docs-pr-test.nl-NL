---
title: 'Zelfstudie: Azure Active Directory-integratie met werkplek door Facebook | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en werkplek met Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: 27e62a00832484667117d8718db9f2fc05e2f4e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="f42a3-103">Zelfstudie: Azure Active Directory-integratie met werkplek door Facebook</span><span class="sxs-lookup"><span data-stu-id="f42a3-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="f42a3-104">In deze zelfstudie leert u hoe werkplek door Facebook integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f42a3-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f42a3-105">Werkplek door Facebook integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="f42a3-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f42a3-106">U kunt beheren in Azure AD die toegang tot de werkplek met Facebook heeft.</span><span class="sxs-lookup"><span data-stu-id="f42a3-106">You can control in Azure AD who has access to Workplace by Facebook.</span></span>
- <span data-ttu-id="f42a3-107">U kunt uw gebruikers automatisch ophalen aangemeld werkplek door Facebook (eenmalige aanmelding) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f42a3-107">You can enable your users to automatically get signed on to Workplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f42a3-108">U kunt uw accounts op één locatie beheren: de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f42a3-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="f42a3-109">Zie voor meer informatie over de software als een dienst (SaaS)-app-integratie met Azure AD [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f42a3-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f42a3-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f42a3-110">Prerequisites</span></span>

<span data-ttu-id="f42a3-111">Voor het configureren van Azure AD-integratie met werkplek door Facebook, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="f42a3-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="f42a3-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="f42a3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f42a3-113">Een werkplek door Facebook eenmalige aanmelding (SSO) abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="f42a3-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="f42a3-114">Test de stappen in deze zelfstudie, volgt u deze aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="f42a3-114">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="f42a3-115">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="f42a3-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f42a3-116">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f42a3-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f42a3-117">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="f42a3-117">Scenario description</span></span>
<span data-ttu-id="f42a3-118">In deze zelfstudie kunt u Azure AD SSO testen in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="f42a3-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="f42a3-119">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="f42a3-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f42a3-120">Werkplek door Facebook uit de galerie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f42a3-120">Add Workplace by Facebook from the gallery.</span></span>
2. <span data-ttu-id="f42a3-121">Configureren en testen eenmalige aanmelding Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f42a3-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="f42a3-122">Werkplek door Facebook uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="f42a3-122">Add Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="f42a3-123">Voor het configureren van de integratie van werkplek door Facebook in Azure AD werkplek door Facebook uit de galerie te toevoegt aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="f42a3-123">To configure the integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="f42a3-124">In de [Azure-portal](https://portal.azure.com), selecteer in het linkerdeelvenster **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f42a3-124">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="f42a3-126">Blader naar **bedrijfstoepassingen** > **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f42a3-126">Browse to **Enterprise applications** > **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="f42a3-128">Selecteer om de nieuwe toepassing toe **nieuwe toepassing** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f42a3-128">To add the new application, select **New application** on the top of the dialog box.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="f42a3-130">Typ in het zoekvak **werkplek door Facebook**, en selecteer **werkplek door Facebook** van resultaten.</span><span class="sxs-lookup"><span data-stu-id="f42a3-130">In the search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="f42a3-131">Selecteer vervolgens **toevoegen**, de toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f42a3-131">Then select **Add**, to add the application.</span></span>

    ![Werkplek door Facebook in de lijst met resultaten](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f42a3-133">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="f42a3-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="f42a3-134">In deze sectie kunt u configureren en testen van Azure AD-SSO met werkplek door Facebook, op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="f42a3-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f42a3-135">Azure AD moet weten wat de gebruiker equivalent in werkplek door Facebook is aan een gebruiker in Azure AD voor eenmalige aanmelding werkt.</span><span class="sxs-lookup"><span data-stu-id="f42a3-135">For SSO to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="f42a3-136">Met andere woorden, moet een gekoppelde relatie tussen een Azure AD-gebruiker en de verwante werkplek door Facebook-gebruiker worden vastgesteld.</span><span class="sxs-lookup"><span data-stu-id="f42a3-136">In other words, a linked relationship between an Azure AD user and the related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="f42a3-137">Deze relatie tot stand brengen door toe te wijzen de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in werkplek met Facebook.</span><span class="sxs-lookup"><span data-stu-id="f42a3-137">Establish this relationship by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f42a3-138">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="f42a3-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f42a3-139">In deze sectie kunt u Azure AD-eenmalige aanmelding inschakelen in de Azure-portal en u eenmalige aanmelding configureren op uw werkplek met Facebook-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f42a3-139">In this section, you enable Azure AD SSO in the Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="f42a3-140">In de Azure-portal op de **werkplek door Facebook** toepassing Integratiepagina **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="f42a3-140">In the Azure portal, on the **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="f42a3-142">In de **eenmalige aanmelding** dialoogvenster, **modus** als **op basis van SAML aanmelding** eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f42a3-142">In the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="f42a3-144">In de **werkplek Facebook-domein en URL's** sectie, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="f42a3-144">In the **Workplace by Facebook Domain and URLs** section, do the following:</span></span>

    <span data-ttu-id="f42a3-145">a.</span><span class="sxs-lookup"><span data-stu-id="f42a3-145">a.</span></span> <span data-ttu-id="f42a3-146">In de **aanmeldings-URL** tekstvak, typt u een URL die gebruikmaakt van het volgende patroon volgen:`https://<company subdomain>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="f42a3-146">In the **Sign-on URL** text box, type a URL that uses the following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="f42a3-147">b.</span><span class="sxs-lookup"><span data-stu-id="f42a3-147">b.</span></span> <span data-ttu-id="f42a3-148">In de **id** tekstvak, typt u een URL die gebruikmaakt van het volgende patroon volgen:`https://www.facebook.com/company/<scim company id>`</span><span class="sxs-lookup"><span data-stu-id="f42a3-148">In the **Identifier** text box, type a URL that uses the following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="f42a3-149">Deze waarden zijn alleen een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f42a3-149">These values are an example only.</span></span> <span data-ttu-id="f42a3-150">Deze waarden bijwerken met de werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="f42a3-150">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="f42a3-151">Neem contact op met de [werkplek door Facebook Client-ondersteuningsteam](https://workplace.fb.com/faq/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="f42a3-151">Contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="f42a3-152">In de **SAML-certificaat voor ondertekening van** sectie **certificaat (Base64)**, en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f42a3-152">In the **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save the certificate file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="f42a3-154">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f42a3-154">Select **Save**.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f42a3-156">In de **werkplek door Facebook configuratie** sectie **werkplek configureren door Facebook** openen de **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="f42a3-156">In the **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="f42a3-157">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids** sectie.</span><span class="sxs-lookup"><span data-stu-id="f42a3-157">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Werkplek door Facebook-configuratie](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="f42a3-159">In een ander browservenster aanmelden bij uw werkplek door Facebook bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="f42a3-159">In a different web browser window, sign in to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="f42a3-160">Als onderdeel van het SAML-verificatieproces kunt werkplek queryreeksen van maximaal 2,5 kilobytes in grootte gebruiken om de parameters doorgeven aan Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f42a3-160">As part of the SAML authentication process, Workplace can use query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="f42a3-161">In de **bedrijf Dashboard**, gaat u naar de **verificatie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="f42a3-161">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="f42a3-162">Onder **SAML-verificatie**, selecteer **eenmalige aanmelding alleen** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="f42a3-162">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="f42a3-163">Voer de waarden die zijn gekopieerd uit de **werkplek door Facebook configuratie** sectie van de Azure portal naar de bijbehorende velden:</span><span class="sxs-lookup"><span data-stu-id="f42a3-163">Enter the values copied from the **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="f42a3-164">In de **SAML URL** tekst vak, plak de waarde van **Single Sign-On Service-URL**, die u hebt gekopieerd uit de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f42a3-164">In the **SAML URL** text box, paste the value of **Single Sign-On Service URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="f42a3-165">In de **URL-verlener SAML** tekst vak, plak de waarde van **SAML entiteit-ID**, die u hebt gekopieerd uit de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f42a3-165">In the **SAML Issuer URL** text box, paste the value of **SAML Entity ID**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="f42a3-166">In **SAML afmelding omleiden (optioneel)**, plak de waarde van **Sign-Out URL**, die u hebt gekopieerd uit de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f42a3-166">In **SAML Logout Redirect (optional)**, paste the value of **Sign-Out URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="f42a3-167">Open uw **base-64 gecodeerde certificaat** in Kladblok gedownload van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f42a3-167">Open your **base-64 encoded certificate** in Notepad, downloaded from the Azure portal.</span></span> <span data-ttu-id="f42a3-168">Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **SAML certificaat** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="f42a3-168">Copy the content of it into your clipboard, and then paste it to the **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="f42a3-169">Mogelijk moet u de doelgroep URL invoeren, ontvanger URL en de URL van de ACS (Assertion Consumer-Service), worden vermeld in de **SAML-configuratie** sectie.</span><span class="sxs-lookup"><span data-stu-id="f42a3-169">You might need to enter the audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="f42a3-170">Ga naar de onderkant van de sectie en selecteer **Test SSO**.</span><span class="sxs-lookup"><span data-stu-id="f42a3-170">Scroll to the bottom of the section, and select **Test SSO**.</span></span> <span data-ttu-id="f42a3-171">Een pop-upvenster wordt weergegeven, met de aanmeldingspagina van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f42a3-171">A pop-up window appears, with the Azure AD sign-in page.</span></span> <span data-ttu-id="f42a3-172">Om te verifiëren, Geef uw referenties als normaal.</span><span class="sxs-lookup"><span data-stu-id="f42a3-172">To authenticate, enter your credentials as normal.</span></span> <span data-ttu-id="f42a3-173">Zorg ervoor dat het e-mailadres dat is geretourneerd door Azure AD is hetzelfde als het werkplekaccount dat u bent aangemeld.</span><span class="sxs-lookup"><span data-stu-id="f42a3-173">Ensure the email address returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="f42a3-174">Als de test is voltooid, Ga naar de onderkant van de pagina en selecteer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f42a3-174">If the test has finished successfully, scroll to the bottom of the page and select **Save**.</span></span>

14. <span data-ttu-id="f42a3-175">Iedereen met behulp van werkplek wordt nu weergegeven met Azure AD-aanmeldingspagina voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="f42a3-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="f42a3-176">U kunt een SAML afmeldings-URL die kan worden gebruikt om te verwijzen op de pagina voor het afmelden van Azure AD configureren.</span><span class="sxs-lookup"><span data-stu-id="f42a3-176">You can choose to configure a SAML sign out URL, which can be used to point at the Azure AD sign-out page.</span></span> <span data-ttu-id="f42a3-177">Wanneer deze instelling is ingeschakeld en geconfigureerd, wordt de gebruiker niet langer doorgestuurd naar de afmelden pagina Werkplek.</span><span class="sxs-lookup"><span data-stu-id="f42a3-177">When this setting is enabled and configured, the user is no longer directed to the Workplace sign-out page.</span></span> <span data-ttu-id="f42a3-178">In plaats daarvan wordt de gebruiker omgeleid naar de URL die is toegevoegd in de SAML-afmelden omleidings-instelling.</span><span class="sxs-lookup"><span data-stu-id="f42a3-178">Instead, the user is redirected to the URL that was added in the SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="f42a3-179">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt.</span><span class="sxs-lookup"><span data-stu-id="f42a3-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app.</span></span> <span data-ttu-id="f42a3-180">Na het toevoegen van deze app uit de **Active Directory** > **bedrijfstoepassingen** sectie gewoon de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="f42a3-180">After adding this app from the **Active Directory** > **Enterprise Applications** section, simply select the **Single Sign-On** tab, and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f42a3-181">U kunt meer lezen over de functie embedded-documentatie in de [documentatie van Azure AD ingesloten]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="f42a3-181">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="f42a3-182">De frequentie van herauthenticatie configureren</span><span class="sxs-lookup"><span data-stu-id="f42a3-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="f42a3-183">U kunt configureren werkplek vraagt om een SAML-controle elke dag drie dagen één week, twee weken, één maand of nooit.</span><span class="sxs-lookup"><span data-stu-id="f42a3-183">You can configure Workplace to prompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="f42a3-184">De minimumwaarde voor de SAML-controle voor mobiele toepassingen is ingesteld op één week.</span><span class="sxs-lookup"><span data-stu-id="f42a3-184">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="f42a3-185">U kunt ook een SAML opnieuw instellen voor alle gebruikers afdwingen.</span><span class="sxs-lookup"><span data-stu-id="f42a3-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="f42a3-186">Gebruik hiervoor de **vereisen SAML-verificatie voor alle gebruikers nu** knop.</span><span class="sxs-lookup"><span data-stu-id="f42a3-186">To do this, use the **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f42a3-187">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="f42a3-187">Create an Azure AD test user</span></span>
<span data-ttu-id="f42a3-188">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f42a3-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

1. <span data-ttu-id="f42a3-190">In de **Azure-portal**, selecteer in het linkerdeelvenster **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f42a3-190">In the **Azure portal**, in the left pane, select **Azure Active Directory**.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f42a3-192">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en selecteer **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f42a3-192">To display the list of users, go to **Users and groups**, and select **All users**.</span></span>
    
    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f42a3-194">Openen van de **gebruiker** dialoogvenster, **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f42a3-194">To open the **User** dialog box, select **Add**.</span></span>
 
    ![De knop toevoegen](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f42a3-196">In de **gebruiker** dialoogvenster de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="f42a3-196">In the **User** dialog box, do the following:</span></span>
 
    ![Het dialoogvenster gebruiker](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f42a3-198">a.</span><span class="sxs-lookup"><span data-stu-id="f42a3-198">a.</span></span> <span data-ttu-id="f42a3-199">In de **naam** in het tekstvak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f42a3-199">In the **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f42a3-200">b.</span><span class="sxs-lookup"><span data-stu-id="f42a3-200">b.</span></span> <span data-ttu-id="f42a3-201">In de **gebruikersnaam** in het tekstvak de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f42a3-201">In the **User name** text box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f42a3-202">c.</span><span class="sxs-lookup"><span data-stu-id="f42a3-202">c.</span></span> <span data-ttu-id="f42a3-203">Selecteer **wachtwoord weergeven**, en schrijf deze op.</span><span class="sxs-lookup"><span data-stu-id="f42a3-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="f42a3-204">d.</span><span class="sxs-lookup"><span data-stu-id="f42a3-204">d.</span></span> <span data-ttu-id="f42a3-205">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="f42a3-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="f42a3-206">Maken van een werkplek door Facebook testgebruiker</span><span class="sxs-lookup"><span data-stu-id="f42a3-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="f42a3-207">In deze sectie wordt een gebruiker met de naam Britta Simon in werkplek gemaakt door Facebook.</span><span class="sxs-lookup"><span data-stu-id="f42a3-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="f42a3-208">Werkplek door Facebook ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f42a3-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="f42a3-209">Er is geen actie voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="f42a3-209">There is no action for you in this section.</span></span> <span data-ttu-id="f42a3-210">Als een gebruiker niet op de werkplek door Facebook bestaat, wordt een nieuw gemaakt wanneer u probeert te openen, werkplek met Facebook.</span><span class="sxs-lookup"><span data-stu-id="f42a3-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="f42a3-211">Als u maken van een gebruiker handmatig wilt, neem dan contact op met de [werkplek door Facebook Client-ondersteuningsteam](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="f42a3-211">If you need to create a user manually, contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f42a3-212">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="f42a3-212">Assign the Azure AD test user</span></span>

<span data-ttu-id="f42a3-213">In deze sectie maakt inschakelen u Britta Simon toegang te verlenen aan een werkplek door Facebook gebruikt Azure eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f42a3-213">In this section, you enable Britta Simon to use Azure SSO by granting access to Workplace by Facebook.</span></span>

![Gebruiker toewijzen][200] 

1. <span data-ttu-id="f42a3-215">Open de toepassingen in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f42a3-215">In the Azure portal, open the applications view.</span></span> <span data-ttu-id="f42a3-216">Ga naar de directoryweergave, gaat u naar **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f42a3-216">Go to the directory view, go to **Enterprise applications**, and then select **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="f42a3-218">Selecteer in de lijst met toepassingen **werkplek door Facebook**.</span><span class="sxs-lookup"><span data-stu-id="f42a3-218">In the applications list, select **Workplace by Facebook**.</span></span>

    ![De werkplek door Facebook-koppeling in de lijst met toepassingen](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="f42a3-220">Selecteer in het menu aan de linkerkant **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f42a3-220">In the menu on the left, select **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202] 

4. <span data-ttu-id="f42a3-222">Selecteer **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f42a3-222">Select **Add**.</span></span> <span data-ttu-id="f42a3-223">Klik in de **toevoegen toewijzing** deelvenster **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="f42a3-223">Then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="f42a3-225">In de **gebruikers en groepen** dialoogvenster, **Britta Simon** in de gebruikerslijst.</span><span class="sxs-lookup"><span data-stu-id="f42a3-225">In the **Users and groups** dialog box, select **Britta Simon** in the users list.</span></span>

6. <span data-ttu-id="f42a3-226">In de **gebruikers en groepen** dialoogvenster, **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="f42a3-226">In the **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="f42a3-227">In de **toevoegen toewijzing** dialoogvenster, **toewijzen**.</span><span class="sxs-lookup"><span data-stu-id="f42a3-227">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f42a3-228">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="f42a3-228">Test single sign-on</span></span>

<span data-ttu-id="f42a3-229">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="f42a3-229">If you want to test your SSO settings, open the Access Panel.</span></span>
<span data-ttu-id="f42a3-230">Zie [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md) (Inleiding tot het toegangsvenster) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f42a3-230">For more information, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="f42a3-231">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f42a3-231">Next steps</span></span>

* <span data-ttu-id="f42a3-232">Zie de [lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="f42a3-232">See the [list of tutorials on how to integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="f42a3-233">Lees [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f42a3-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="f42a3-234">Meer informatie over het [configureren gebruikersaanvragen](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="f42a3-234">Learn more about how to [configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

