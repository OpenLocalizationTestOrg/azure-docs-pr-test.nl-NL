---
title: 'Zelfstudie: Azure Active Directory-integratie met HappyFox | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en HappyFox.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8204ee77-f64b-4fac-b64a-25ea534feac0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jeedes
ms.openlocfilehash: 8b5ad750d7849e4037ed7ee93c48b5645c68e799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-happyfox"></a><span data-ttu-id="a514b-103">Zelfstudie: Azure Active Directory-integratie met HappyFox</span><span class="sxs-lookup"><span data-stu-id="a514b-103">Tutorial: Azure Active Directory integration with HappyFox</span></span>

<span data-ttu-id="a514b-104">In deze zelfstudie leert u hoe HappyFox integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a514b-104">In this tutorial, you learn how to integrate HappyFox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a514b-105">HappyFox integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="a514b-105">Integrating HappyFox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a514b-106">U kunt beheren in Azure AD die toegang tot HappyFox heeft</span><span class="sxs-lookup"><span data-stu-id="a514b-106">You can control in Azure AD who has access to HappyFox</span></span>
- <span data-ttu-id="a514b-107">U kunt uw gebruikers automatisch ophalen aangemeld bij HappyFox (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="a514b-107">You can enable your users to automatically get signed-on to HappyFox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a514b-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="a514b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a514b-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a514b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a514b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a514b-110">Prerequisites</span></span>

<span data-ttu-id="a514b-111">Voor het configureren van Azure AD-integratie met HappyFox, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="a514b-111">To configure Azure AD integration with HappyFox, you need the following items:</span></span>

- <span data-ttu-id="a514b-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="a514b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a514b-113">Een HappyFox eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="a514b-113">A HappyFox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a514b-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a514b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a514b-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="a514b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a514b-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="a514b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a514b-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a514b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a514b-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="a514b-118">Scenario description</span></span>
<span data-ttu-id="a514b-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="a514b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a514b-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="a514b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a514b-121">HappyFox uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="a514b-121">Adding HappyFox from the gallery</span></span>
2. <span data-ttu-id="a514b-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a514b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-happyfox-from-the-gallery"></a><span data-ttu-id="a514b-123">HappyFox uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="a514b-123">Adding HappyFox from the gallery</span></span>
<span data-ttu-id="a514b-124">Voor het configureren van de integratie van HappyFox in Azure AD, moet u HappyFox uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="a514b-124">To configure the integration of HappyFox into Azure AD, you need to add HappyFox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a514b-125">**Als u wilt toevoegen HappyFox uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a514b-125">**To add HappyFox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a514b-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a514b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a514b-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a514b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a514b-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a514b-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="a514b-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a514b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="a514b-133">Typ in het zoekvak **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="a514b-133">In the search box, type **HappyFox**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_search.png)

5. <span data-ttu-id="a514b-135">Selecteer in het deelvenster resultaten **HappyFox**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a514b-135">In the results panel, select **HappyFox**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a514b-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a514b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a514b-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met HappyFox op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a514b-138">In this section, you configure and test Azure AD single sign-on with HappyFox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a514b-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in HappyFox is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a514b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HappyFox is to a user in Azure AD.</span></span> <span data-ttu-id="a514b-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in HappyFox tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="a514b-140">In other words, a link relationship between an Azure AD user and the related user in HappyFox needs to be established.</span></span>

<span data-ttu-id="a514b-141">Wijs in HappyFox, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="a514b-141">In HappyFox, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a514b-142">Om te configureren en testen van Azure AD eenmalige aanmelding met HappyFox, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="a514b-142">To configure and test Azure AD single sign-on with HappyFox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a514b-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a514b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a514b-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a514b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a514b-145">**[Maken van een testgebruiker HappyFox](#creating-a-happyfox-test-user)**  - HappyFox die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="a514b-145">**[Creating a HappyFox test user](#creating-a-happyfox-test-user)** - to have a counterpart of Britta Simon in HappyFox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a514b-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a514b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a514b-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="a514b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a514b-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="a514b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a514b-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing HappyFox configureren.</span><span class="sxs-lookup"><span data-stu-id="a514b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HappyFox application.</span></span>

<span data-ttu-id="a514b-150">**Voor het configureren van Azure AD eenmalige aanmelding met HappyFox, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a514b-150">**To configure Azure AD single sign-on with HappyFox, perform the following steps:**</span></span>

1. <span data-ttu-id="a514b-151">In de Azure-portal op de **HappyFox** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a514b-151">In the Azure portal, on the **HappyFox** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="a514b-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a514b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_samlbase.png)

3. <span data-ttu-id="a514b-155">Op de **HappyFox domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a514b-155">On the **HappyFox Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_url.png)

    <span data-ttu-id="a514b-157">a.</span><span class="sxs-lookup"><span data-stu-id="a514b-157">a.</span></span> <span data-ttu-id="a514b-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.happyfox.com/`</span><span class="sxs-lookup"><span data-stu-id="a514b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.happyfox.com/`</span></span>

    <span data-ttu-id="a514b-159">b.</span><span class="sxs-lookup"><span data-stu-id="a514b-159">b.</span></span> <span data-ttu-id="a514b-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.happyfox.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="a514b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.happyfox.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a514b-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="a514b-161">These values are not real.</span></span> <span data-ttu-id="a514b-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="a514b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a514b-163">Neem contact op met [HappyFox Client ondersteuningsteam](https://support.happyfox.com/home) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="a514b-163">Contact [HappyFox Client support team](https://support.happyfox.com/home) to get these values.</span></span> 
 
4. <span data-ttu-id="a514b-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a514b-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_certificate.png) 

5. <span data-ttu-id="a514b-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a514b-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a514b-168">Op de **HappyFox configuratie** sectie, klikt u op **configureren HappyFox** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="a514b-168">On the **HappyFox Configuration** section, click **Configure HappyFox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a514b-169">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt**.</span><span class="sxs-lookup"><span data-stu-id="a514b-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_configure.png) 

7. <span data-ttu-id="a514b-171">Meld u bij uw medewerkers HappyFox portal en navigeer naar **beheren**, klikt u op **integraties** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a514b-171">Sign on to your HappyFox staff portal and navigate to **Manage**, Click on **Integrations** tab.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/header.png) 

8. <span data-ttu-id="a514b-173">Klik op het tabblad integraties **configureren** onder **SAML-integratie** om de eenmalige aanmelding op instellingen te openen.</span><span class="sxs-lookup"><span data-stu-id="a514b-173">In the Integrations tab, Click **Configure** under **SAML Integration** to open the Single Sign On Settings.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/configure.png) 

9. <span data-ttu-id="a514b-175">Binnen de SAML-configuratiesectie, plak de **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal in **doel-URL voor eenmalige aanmelding** textbox.</span><span class="sxs-lookup"><span data-stu-id="a514b-175">Inside SAML configuration section, paste the **SAML Single Sign-On Service URL** that you have copied from Azure portal into **SSO Target URL** textbox.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/targeturl.png)

10. <span data-ttu-id="a514b-177">Open het certificaat dat is gedownload van Azure-portal in Kladblok en plak de inhoud ervan in **IdP handtekening** sectie.</span><span class="sxs-lookup"><span data-stu-id="a514b-177">Open the certificate downloaded from Azure portal in notepad and paste its content in **IdP Signature** section.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/cert.png)

11. <span data-ttu-id="a514b-179">Klik op **instellingen opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="a514b-179">Click **Save Settings** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/savesettings.png)

> [!TIP]
> <span data-ttu-id="a514b-181">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="a514b-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a514b-182">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="a514b-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a514b-183">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a514b-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a514b-184">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="a514b-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="a514b-185">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a514b-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="a514b-187">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a514b-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a514b-188">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="a514b-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-happyfox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a514b-190">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="a514b-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-happyfox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a514b-192">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a514b-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-happyfox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a514b-194">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a514b-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-happyfox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a514b-196">a.</span><span class="sxs-lookup"><span data-stu-id="a514b-196">a.</span></span> <span data-ttu-id="a514b-197">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a514b-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a514b-198">b.</span><span class="sxs-lookup"><span data-stu-id="a514b-198">b.</span></span> <span data-ttu-id="a514b-199">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a514b-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a514b-200">c.</span><span class="sxs-lookup"><span data-stu-id="a514b-200">c.</span></span> <span data-ttu-id="a514b-201">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="a514b-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a514b-202">d.</span><span class="sxs-lookup"><span data-stu-id="a514b-202">d.</span></span> <span data-ttu-id="a514b-203">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a514b-203">Click **Create**.</span></span>
 
### <a name="creating-a-happyfox-test-user"></a><span data-ttu-id="a514b-204">Een testgebruiker HappyFox maken</span><span class="sxs-lookup"><span data-stu-id="a514b-204">Creating a HappyFox test user</span></span>

<span data-ttu-id="a514b-205">Toepassing ondersteunt Just in time gebruikers inrichten en na verificatie gebruikers automatisch in de toepassing gemaakt worden.</span><span class="sxs-lookup"><span data-stu-id="a514b-205">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a514b-206">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="a514b-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a514b-207">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan HappyFox.</span><span class="sxs-lookup"><span data-stu-id="a514b-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HappyFox.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="a514b-209">**Britta Simon om aan te wijzen HappyFox, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="a514b-209">**To assign Britta Simon to HappyFox, perform the following steps:**</span></span>

1. <span data-ttu-id="a514b-210">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a514b-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="a514b-212">Selecteer in de lijst met toepassingen **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="a514b-212">In the applications list, select **HappyFox**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_app.png) 

3. <span data-ttu-id="a514b-214">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="a514b-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="a514b-216">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="a514b-216">Click **Add** button.</span></span> <span data-ttu-id="a514b-217">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a514b-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="a514b-219">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a514b-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a514b-220">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a514b-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a514b-221">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a514b-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a514b-222">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a514b-222">Testing single sign-on</span></span>

<span data-ttu-id="a514b-223">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="a514b-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="a514b-224">Als u op de tegel HappyFox in het deelvenster toegang, krijgt u de aanmeldingspagina van HappyFox toepassing.</span><span class="sxs-lookup"><span data-stu-id="a514b-224">When you click the HappyFox tile in the Access Panel, you should get login page of HappyFox application.</span></span> <span data-ttu-id="a514b-225">U ziet de **'SAML'** knop op de aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="a514b-225">You should see the **‘SAML’** button on the sign-in page.</span></span>

    ![Invoegtoepassing](./media/active-directory-saas-happyfox-tutorial/saml.png) 

2. <span data-ttu-id="a514b-227">Klik op de **'SAML'** knop aanmelden bij HappyFox met behulp van uw Azure AD-account.</span><span class="sxs-lookup"><span data-stu-id="a514b-227">Click the **‘SAML’** button to log in to HappyFox using your Azure AD account.</span></span>

<span data-ttu-id="a514b-228">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a514b-228">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a514b-229">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a514b-229">Additional resources</span></span>

* [<span data-ttu-id="a514b-230">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a514b-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a514b-231">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a514b-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_203.png

