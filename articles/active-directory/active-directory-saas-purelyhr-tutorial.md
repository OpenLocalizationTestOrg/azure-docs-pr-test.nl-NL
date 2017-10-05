---
title: 'Zelfstudie: Azure Active Directory-integratie met PurelyHR | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en PurelyHR.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: a9075b1759ebd39f164bfe288fb0a365acdcc44c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a><span data-ttu-id="d6036-103">Zelfstudie: Azure Active Directory-integratie met PurelyHR</span><span class="sxs-lookup"><span data-stu-id="d6036-103">Tutorial: Azure Active Directory integration with PurelyHR</span></span>

<span data-ttu-id="d6036-104">In deze zelfstudie leert u hoe PurelyHR integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d6036-104">In this tutorial, you learn how to integrate PurelyHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d6036-105">PurelyHR integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d6036-105">Integrating PurelyHR with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d6036-106">U kunt beheren in Azure AD die toegang tot PurelyHR heeft</span><span class="sxs-lookup"><span data-stu-id="d6036-106">You can control in Azure AD who has access to PurelyHR</span></span>
- <span data-ttu-id="d6036-107">U kunt uw gebruikers automatisch ophalen aangemeld bij PurelyHR (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="d6036-107">You can enable your users to automatically get signed-on to PurelyHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d6036-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="d6036-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d6036-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d6036-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6036-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d6036-110">Prerequisites</span></span>

<span data-ttu-id="d6036-111">Voor het configureren van Azure AD-integratie met PurelyHR, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="d6036-111">To configure Azure AD integration with PurelyHR, you need the following items:</span></span>

- <span data-ttu-id="d6036-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="d6036-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d6036-113">Een PurelyHR eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="d6036-113">A PurelyHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d6036-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d6036-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d6036-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="d6036-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d6036-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d6036-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d6036-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6036-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d6036-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d6036-118">Scenario description</span></span>
<span data-ttu-id="d6036-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d6036-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d6036-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d6036-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d6036-121">PurelyHR uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d6036-121">Adding PurelyHR from the gallery</span></span>
2. <span data-ttu-id="d6036-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d6036-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-purelyhr-from-the-gallery"></a><span data-ttu-id="d6036-123">PurelyHR uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d6036-123">Adding PurelyHR from the gallery</span></span>
<span data-ttu-id="d6036-124">Voor het configureren van de integratie van PurelyHR in Azure AD, moet u PurelyHR uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d6036-124">To configure the integration of PurelyHR into Azure AD, you need to add PurelyHR from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d6036-125">**Als u wilt toevoegen PurelyHR uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d6036-125">**To add PurelyHR from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d6036-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d6036-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d6036-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d6036-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d6036-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d6036-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d6036-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d6036-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d6036-133">Typ in het zoekvak **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="d6036-133">In the search box, type **PurelyHR**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. <span data-ttu-id="d6036-135">Selecteer in het deelvenster resultaten **PurelyHR**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d6036-135">In the results panel, select **PurelyHR**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d6036-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d6036-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d6036-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met PurelyHR op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="d6036-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d6036-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in PurelyHR is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6036-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PurelyHR is to a user in Azure AD.</span></span> <span data-ttu-id="d6036-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in PurelyHR tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="d6036-140">In other words, a link relationship between an Azure AD user and the related user in PurelyHR needs to be established.</span></span>

<span data-ttu-id="d6036-141">Wijs in PurelyHR, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="d6036-141">In PurelyHR, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d6036-142">Om te configureren en testen van Azure AD eenmalige aanmelding met PurelyHR, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="d6036-142">To configure and test Azure AD single sign-on with PurelyHR, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d6036-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d6036-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d6036-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d6036-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d6036-145">**[Maken van een testgebruiker PurelyHR](#creating-a-purelyhr-test-user)**  - PurelyHR die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="d6036-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - to have a counterpart of Britta Simon in PurelyHR that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d6036-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d6036-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d6036-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d6036-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d6036-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d6036-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d6036-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing PurelyHR configureren.</span><span class="sxs-lookup"><span data-stu-id="d6036-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PurelyHR application.</span></span>

<span data-ttu-id="d6036-150">**Voor het configureren van Azure AD eenmalige aanmelding met PurelyHR, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d6036-150">**To configure Azure AD single sign-on with PurelyHR, perform the following steps:**</span></span>

1. <span data-ttu-id="d6036-151">In de Azure-portal op de **PurelyHR** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d6036-151">In the Azure portal, on the **PurelyHR** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d6036-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d6036-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. <span data-ttu-id="d6036-155">Op de **PurelyHR domein en de URL's** sectie, voert u de volgende stappen uit als u wilt configureren, de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="d6036-155">On the **PurelyHR Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    <span data-ttu-id="d6036-157">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyID>.purelyhr.com/sso-consume`</span><span class="sxs-lookup"><span data-stu-id="d6036-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span></span>

4. <span data-ttu-id="d6036-158">Controleer **weergeven geavanceerde instellingen voor URL**, als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="d6036-158">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    <span data-ttu-id="d6036-160">In de **aanmeldings-URL** textbox, typ de waarde met het volgende patroon volgen:`https://<companyID>.purelyhr.com/sso-initiate`</span><span class="sxs-lookup"><span data-stu-id="d6036-160">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="d6036-161">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="d6036-161">These values are not the real.</span></span> <span data-ttu-id="d6036-162">Deze waarden bijwerken met de werkelijke antwoord-URL en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="d6036-162">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="d6036-163">Neem contact op met [PurelyHR Client ondersteuningsteam](http://support.purelyhr.com/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="d6036-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) to get these values.</span></span> 

5. <span data-ttu-id="d6036-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d6036-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. <span data-ttu-id="d6036-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d6036-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="d6036-168">Op de **PurelyHR configuratie** sectie, klikt u op **configureren PurelyHR** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="d6036-168">On the **PurelyHR Configuration** section, click **Configure PurelyHR** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d6036-169">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="d6036-169">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. <span data-ttu-id="d6036-171">Eenmalige aanmelding configureren op **PurelyHR** side, meld u aan bij de website als beheerder.</span><span class="sxs-lookup"><span data-stu-id="d6036-171">To configure single sign-on on **PurelyHR** side, login to their website as an administrator.</span></span>

9. <span data-ttu-id="d6036-172">Open de **Dashboard** van de opties in de werkbalk en klikt u op **SSO instellingen**.</span><span class="sxs-lookup"><span data-stu-id="d6036-172">Open the **Dashboard** from the options in the toolbar and click **SSO Settings**.</span></span>

10. <span data-ttu-id="d6036-173">De waarden in de vakken plakken, zoals beschreven onderstaande-</span><span class="sxs-lookup"><span data-stu-id="d6036-173">Paste the values in the boxes as described below-</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    <span data-ttu-id="d6036-175">a.</span><span class="sxs-lookup"><span data-stu-id="d6036-175">a.</span></span> <span data-ttu-id="d6036-176">Open de **Certificate(Bas64)** gedownload vanuit de Azure-portal in Kladblok en kopieer de waarde van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="d6036-176">Open the **Certificate(Bas64)** downloaded from the Azure portal in notepad and copy the certificate value.</span></span> <span data-ttu-id="d6036-177">Plak de gekopieerde waarde in de **X.509-certificaat** vak.</span><span class="sxs-lookup"><span data-stu-id="d6036-177">Paste the copied value into the **X.509 Certificate** box.</span></span>

    <span data-ttu-id="d6036-178">b.</span><span class="sxs-lookup"><span data-stu-id="d6036-178">b.</span></span> <span data-ttu-id="d6036-179">In de **URL-verlener Idp** vak, plak de **SAML entiteit-ID** gekopieerd van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d6036-179">In the **Idp Issuer URL** box, paste the **SAML Entity ID** copied from the Azure portal.</span></span>

    <span data-ttu-id="d6036-180">c.</span><span class="sxs-lookup"><span data-stu-id="d6036-180">c.</span></span> <span data-ttu-id="d6036-181">In de **Idp eindpunt-URL** vak, plak de **SAML Single Sign-On Service-URL** gekopieerd van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d6036-181">In the **Idp Endpoint URL** box, paste the **SAML Single Sign-On Service URL** copied from the Azure portal.</span></span> 

    <span data-ttu-id="d6036-182">d.</span><span class="sxs-lookup"><span data-stu-id="d6036-182">d.</span></span> <span data-ttu-id="d6036-183">Controleer de **gebruikers automatisch maken** vakje voor automatisch gebruikers inrichten in PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="d6036-183">Check the **Auto-Create Users** checkbox to enable automatic user provisioning in PurelyHR.</span></span>

    <span data-ttu-id="d6036-184">e.</span><span class="sxs-lookup"><span data-stu-id="d6036-184">e.</span></span> <span data-ttu-id="d6036-185">Klik op **wijzigingen opslaan** de instellingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="d6036-185">Click **Save Changes** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="d6036-186">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="d6036-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d6036-187">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="d6036-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d6036-188">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d6036-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d6036-189">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d6036-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="d6036-190">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d6036-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d6036-192">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d6036-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d6036-193">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d6036-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d6036-195">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="d6036-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d6036-197">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d6036-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d6036-199">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d6036-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d6036-201">a.</span><span class="sxs-lookup"><span data-stu-id="d6036-201">a.</span></span> <span data-ttu-id="d6036-202">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d6036-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d6036-203">b.</span><span class="sxs-lookup"><span data-stu-id="d6036-203">b.</span></span> <span data-ttu-id="d6036-204">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d6036-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d6036-205">c.</span><span class="sxs-lookup"><span data-stu-id="d6036-205">c.</span></span> <span data-ttu-id="d6036-206">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d6036-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d6036-207">d.</span><span class="sxs-lookup"><span data-stu-id="d6036-207">d.</span></span> <span data-ttu-id="d6036-208">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d6036-208">Click **Create**.</span></span>
 
### <a name="creating-a-purelyhr-test-user"></a><span data-ttu-id="d6036-209">Een testgebruiker PurelyHR maken</span><span class="sxs-lookup"><span data-stu-id="d6036-209">Creating a PurelyHR test user</span></span>

<span data-ttu-id="d6036-210">Om Azure AD-gebruikers zich aanmelden bij PurelyHR, moeten ze worden ingericht in PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="d6036-210">To enable Azure AD users to log in to PurelyHR, they must be provisioned into PurelyHR.</span></span> <span data-ttu-id="d6036-211">Inrichting is een automatische taak in PurelyHR, en zijn geen handmatige stappen vereist wanneer de Automatische gebruikersaanvragen is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d6036-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d6036-212">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6036-212">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d6036-213">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="d6036-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PurelyHR.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d6036-215">**Britta Simon om aan te wijzen PurelyHR, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d6036-215">**To assign Britta Simon to PurelyHR, perform the following steps:**</span></span>

1. <span data-ttu-id="d6036-216">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d6036-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d6036-218">Selecteer in de lijst met toepassingen **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="d6036-218">In the applications list, select **PurelyHR**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. <span data-ttu-id="d6036-220">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d6036-220">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d6036-222">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d6036-222">Click **Add** button.</span></span> <span data-ttu-id="d6036-223">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d6036-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d6036-225">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d6036-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d6036-226">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d6036-226">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d6036-227">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d6036-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d6036-228">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d6036-228">Testing single sign-on</span></span>

<span data-ttu-id="d6036-229">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="d6036-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d6036-230">Klik op de tegel LMS opnemen in het deelvenster toegang, u ophalen automatisch aangemeld bij uw toepassing LMS opnemen.</span><span class="sxs-lookup"><span data-stu-id="d6036-230">Click the Absorb LMS tile in the Access Panel, you get automatically signed-on to your Absorb LMS application.</span></span>

<span data-ttu-id="d6036-231">Zie voor meer informatie over het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="d6036-231">For more information about the Access Panel, see.</span></span> <span data-ttu-id="d6036-232">[Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="d6036-232">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d6036-233">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d6036-233">Additional resources</span></span>

* [<span data-ttu-id="d6036-234">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6036-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d6036-235">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d6036-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png

