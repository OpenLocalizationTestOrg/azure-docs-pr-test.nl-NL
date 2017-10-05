---
title: 'Zelfstudie: Azure Active Directory-integratie met voorzijde | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en de voorgrond.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: d936bc50a66ac2a3c17038ff08351edf9902c99f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="bc9b3-103">Zelfstudie: Azure Active Directory-integratie met voorzijde</span><span class="sxs-lookup"><span data-stu-id="bc9b3-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="bc9b3-104">In deze zelfstudie leert u hoe voorzijde integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bc9b3-104">In this tutorial, you learn how to integrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bc9b3-105">Begin integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="bc9b3-105">Integrating Front with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bc9b3-106">U kunt beheren in Azure AD die toegang tot de voorgrond heeft.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-106">You can control in Azure AD who has access to Front.</span></span>
- <span data-ttu-id="bc9b3-107">U kunt uw gebruikers automatisch ophalen aangemelde naar voorgrond (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-107">You can enable your users to automatically get signed-on to Front (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="bc9b3-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="bc9b3-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bc9b3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc9b3-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bc9b3-110">Prerequisites</span></span>

<span data-ttu-id="bc9b3-111">Voor het configureren van Azure AD-integratie met voorgrond, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="bc9b3-111">To configure Azure AD integration with Front, you need the following items:</span></span>

- <span data-ttu-id="bc9b3-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="bc9b3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bc9b3-113">Een begin eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="bc9b3-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bc9b3-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bc9b3-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="bc9b3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bc9b3-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bc9b3-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bc9b3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bc9b3-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="bc9b3-118">Scenario description</span></span>
<span data-ttu-id="bc9b3-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bc9b3-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="bc9b3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bc9b3-121">Vooraan in de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="bc9b3-121">Adding Front from the gallery</span></span>
2. <span data-ttu-id="bc9b3-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bc9b3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-the-gallery"></a><span data-ttu-id="bc9b3-123">Vooraan in de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="bc9b3-123">Adding Front from the gallery</span></span>
<span data-ttu-id="bc9b3-124">Voor het configureren van de integratie van vooraan in Azure AD, moet u voorgrond uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-124">To configure the integration of Front into Azure AD, you need to add Front from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bc9b3-125">**Als u wilt toevoegen voor uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bc9b3-125">**To add Front from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bc9b3-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="bc9b3-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bc9b3-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="bc9b3-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="bc9b3-133">Typ in het zoekvak **Front**, selecteer **Front** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-133">In the search box, type **Front**, select **Front** from result panel then click **Add** button to add the application.</span></span>

    ![Vooraan in de lijst met resultaten](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bc9b3-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc9b3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="bc9b3-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met voorzijde op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bc9b3-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat het equivalent van de gebruiker op de voorgrond is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Front is to a user in Azure AD.</span></span> <span data-ttu-id="bc9b3-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de gebruiker op de voorgrond tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-138">In other words, a link relationship between an Azure AD user and the related user in Front needs to be established.</span></span>

<span data-ttu-id="bc9b3-139">Op de voorgrond, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-139">In Front, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bc9b3-140">Als u wilt configureren en testen Azure AD eenmalige aanmelding met voorgrond, moet u voltooien van de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="bc9b3-140">To configure and test Azure AD single sign-on with Front, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bc9b3-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bc9b3-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bc9b3-143">**[Maak een testgebruiker voorzijde](#create-a-front-test-user)**  - hebben een equivalent van Britta Simon op de voorgrond die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-143">**[Create a Front test user](#create-a-front-test-user)** - to have a counterpart of Britta Simon in Front that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bc9b3-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bc9b3-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bc9b3-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="bc9b3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bc9b3-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing voorgrond.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="bc9b3-148">**Voor het configureren van Azure AD eenmalige aanmelding met voorgrond, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bc9b3-148">**To configure Azure AD single sign-on with Front, perform the following steps:**</span></span>

1. <span data-ttu-id="bc9b3-149">In de Azure-portal op de **Front** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-149">In the Azure portal, on the **Front** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="bc9b3-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="bc9b3-153">Op de **Front-domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="bc9b3-153">On the **Front Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="bc9b3-155">a.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-155">a.</span></span> <span data-ttu-id="bc9b3-156">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="bc9b3-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="bc9b3-157">b.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-157">b.</span></span> <span data-ttu-id="bc9b3-158">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="bc9b3-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="bc9b3-159">Controleer **weergeven geavanceerde instellingen voor URL**, als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="bc9b3-159">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="bc9b3-161">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="bc9b3-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="bc9b3-162">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-162">These values are not real.</span></span> <span data-ttu-id="bc9b3-163">Deze waarden bijwerken met de werkelijke id, het antwoord-URL en de aanmeldings-URL die worden beschreven verderop in de zelfstudie of neem contact op met [Front Client ondersteuningsteam](mailto:support@frontapp.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) to get these values.</span></span> 

5. <span data-ttu-id="bc9b3-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="bc9b3-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="bc9b3-168">Op de **Front configuratie** sectie, klikt u op **Front configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-168">On the **Front Configuration** section, click **Configure Front** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bc9b3-169">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="bc9b3-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="bc9b3-171">Eenmalige aanmelding voor uw tenant voorzijde als beheerder.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-171">Sign-on to your Front tenant as an administrator.</span></span>

9. <span data-ttu-id="bc9b3-172">Ga naar **instellingen (tandwiel pictogram onder aan de linkerkant zijbalk) > Voorkeuren**.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-172">Go to **Settings (cog icon at the bottom of the left sidebar) > Preferences**.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="bc9b3-174">Klik op **eenmalige aanmelding** koppeling.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-174">Click **Single Sign On** link.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="bc9b3-176">Selecteer **SAML** in de vervolgkeuzelijst van **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-176">Select **SAML** in the drop-down list of **Single Sign On**.</span></span>
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="bc9b3-178">In de **toegangspunt** textbox plaatsen de waarde van **één Service-URL aanmelding** van de configuratiewizard voor Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-178">In the **Entry Point** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="bc9b3-180">Open uw gedownloade **Certificate(Base64)** bestand in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **handtekeningcertificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-180">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Signing certificate** textbox.</span></span>
    
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="bc9b3-182">Op de **Service-Providerinstellingen** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bc9b3-182">On the **Service provider settings** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="bc9b3-184">a.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-184">a.</span></span> <span data-ttu-id="bc9b3-185">Kopieer de waarde van **entiteit-ID** en plak deze in de **id** textbox in **Front-domein en de URL's** sectie in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-185">Copy the value of **Entity ID** and paste it into the **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="bc9b3-186">b.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-186">b.</span></span> <span data-ttu-id="bc9b3-187">Kopieer de waarde van **ACS URL** en plak deze in de **aanmeldings-URL** textbox in **Front-domein en de URL's** sectie in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-187">Copy the value of **ACS URL** and paste it into the **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="bc9b3-188">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="bc9b3-189">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="bc9b3-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bc9b3-190">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bc9b3-191">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bc9b3-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bc9b3-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="bc9b3-192">Create an Azure AD test user</span></span>

<span data-ttu-id="bc9b3-193">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="bc9b3-195">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bc9b3-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bc9b3-196">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="bc9b3-198">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="bc9b3-200">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="bc9b3-202">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="bc9b3-202">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="bc9b3-204">a.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-204">a.</span></span> <span data-ttu-id="bc9b3-205">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bc9b3-206">b.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-206">b.</span></span> <span data-ttu-id="bc9b3-207">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="bc9b3-208">c.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-208">c.</span></span> <span data-ttu-id="bc9b3-209">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="bc9b3-210">d.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-210">d.</span></span> <span data-ttu-id="bc9b3-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="bc9b3-212">Een Front-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="bc9b3-212">Create a Front test user</span></span>

<span data-ttu-id="bc9b3-213">In deze sectie maakt u een gebruiker op de voorgrond Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="bc9b3-214">Werken met [Front Client ondersteuningsteam](mailto:support@frontapp.com) toevoegen van de gebruikers in het Front-platform.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-214">Work with [Front Client support team](mailto:support@frontapp.com) to add the users in the Front platform.</span></span> <span data-ttu-id="bc9b3-215">Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="bc9b3-216">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="bc9b3-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="bc9b3-217">In deze sectie maakt inschakelen u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang aan de voorzijde.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Front.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="bc9b3-219">**Als u wilt toewijzen Britta Simon naar voorgrond, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="bc9b3-219">**To assign Britta Simon to Front, perform the following steps:**</span></span>

1. <span data-ttu-id="bc9b3-220">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="bc9b3-222">Selecteer in de lijst met toepassingen **Front**.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-222">In the applications list, select **Front**.</span></span>

    ![De Front-koppeling in de lijst met toepassingen](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="bc9b3-224">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-224">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="bc9b3-226">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-226">Click **Add** button.</span></span> <span data-ttu-id="bc9b3-227">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="bc9b3-229">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bc9b3-230">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bc9b3-231">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bc9b3-232">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="bc9b3-232">Test single sign-on</span></span>

<span data-ttu-id="bc9b3-233">Het doel van deze sectie is het testen van uw Azure AD-SSOconfiguration met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-233">The objective of this section is to test your Azure AD SSOconfiguration using the Access Panel.</span></span>

<span data-ttu-id="bc9b3-234">Als u op de Front-tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw Front-toepassing.</span><span class="sxs-lookup"><span data-stu-id="bc9b3-234">When you click the Front tile in the Access Panel, you should get automatically signed-on to your Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bc9b3-235">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="bc9b3-235">Additional resources</span></span>

* [<span data-ttu-id="bc9b3-236">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bc9b3-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bc9b3-237">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bc9b3-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

