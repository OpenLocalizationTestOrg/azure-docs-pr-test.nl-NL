---
title: 'Zelfstudie: Azure Active Directory-integratie met Velpic SAML | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Velpic SAML.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5325f3cca00167e6b7b687509ce43435447ad2f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="33228-103">Zelfstudie: Azure Active Directory-integratie met Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="33228-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="33228-104">In deze zelfstudie leert u hoe Velpic SAML integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="33228-104">In this tutorial, you learn how to integrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="33228-105">Velpic SAML integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="33228-105">Integrating Velpic SAML with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="33228-106">U kunt beheren in Azure AD die toegang tot Velpic SAML heeft</span><span class="sxs-lookup"><span data-stu-id="33228-106">You can control in Azure AD who has access to Velpic SAML</span></span>
- <span data-ttu-id="33228-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Velpic SAML (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="33228-107">You can enable your users to automatically get signed-on to Velpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="33228-108">U kunt uw accounts op één centrale locatie - en de Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="33228-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="33228-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="33228-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33228-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="33228-110">Prerequisites</span></span>

<span data-ttu-id="33228-111">Voor het configureren van Azure AD-integratie met Velpic SAML, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="33228-111">To configure Azure AD integration with Velpic SAML, you need the following items:</span></span>

- <span data-ttu-id="33228-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="33228-112">An Azure AD subscription</span></span>
- <span data-ttu-id="33228-113">Een Velpic SAML-eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="33228-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="33228-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="33228-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="33228-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="33228-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="33228-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="33228-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="33228-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="33228-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="33228-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="33228-118">Scenario description</span></span>
<span data-ttu-id="33228-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="33228-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="33228-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="33228-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="33228-121">Velpic SAML uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="33228-121">Adding Velpic SAML from the gallery</span></span>
2. <span data-ttu-id="33228-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="33228-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-the-gallery"></a><span data-ttu-id="33228-123">Velpic SAML uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="33228-123">Adding Velpic SAML from the gallery</span></span>
<span data-ttu-id="33228-124">Voor het configureren van de integratie van Velpic SAML in Azure AD, moet u Velpic SAML uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="33228-124">To configure the integration of Velpic SAML into Azure AD, you need to add Velpic SAML from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="33228-125">**Als u wilt toevoegen Velpic SAML uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="33228-125">**To add Velpic SAML from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="33228-126">In de  **[Azure Management Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="33228-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="33228-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="33228-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="33228-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="33228-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="33228-131">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="33228-131">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="33228-133">Typ in het zoekvak **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="33228-133">In the search box, type **Velpic SAML**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="33228-135">Selecteer in het deelvenster resultaten **Velpic SAML**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="33228-135">In the results panel, select **Velpic SAML**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="33228-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="33228-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="33228-138">In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Velpic SAML op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="33228-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="33228-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Velpic SAML is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33228-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Velpic SAML is to a user in Azure AD.</span></span> <span data-ttu-id="33228-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante Velpic SAML-gebruiker worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="33228-140">In other words, a link relationship between an Azure AD user and the related user in Velpic SAML needs to be established.</span></span>

<span data-ttu-id="33228-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="33228-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Velpic SAML.</span></span>

<span data-ttu-id="33228-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Velpic SAML, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="33228-142">To configure and test Azure AD single sign-on with Velpic SAML, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="33228-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="33228-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="33228-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="33228-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="33228-145">**[Maken van een testgebruiker Velpic SAML](#creating-a-velpic-saml-test-user)**  - Velpic SAML die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="33228-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - to have a counterpart of Britta Simon in Velpic SAML that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="33228-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="33228-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="33228-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="33228-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="33228-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="33228-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="33228-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="33228-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="33228-150">**Voor het configureren van Azure AD eenmalige aanmelding met Velpic SAML, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="33228-150">**To configure Azure AD single sign-on with Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="33228-151">In de Azure-beheerportal op de **Velpic SAML** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="33228-151">In the Azure Management portal, on the **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="33228-153">Op de **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** eenmalige aanmelding inschakelen op.</span><span class="sxs-lookup"><span data-stu-id="33228-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="33228-155">Voer de gegevens in de **Velpic SAML-domein en de URL's** sectie -</span><span class="sxs-lookup"><span data-stu-id="33228-155">Enter the details in the **Velpic SAML Domain and URLs** section-</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="33228-157">a.</span><span class="sxs-lookup"><span data-stu-id="33228-157">a.</span></span> <span data-ttu-id="33228-158">In de **aanmeldings-URL** textbox, typ de waarde als:`https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="33228-158">In the **Sign-on URL** textbox, type the value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="33228-159">b.</span><span class="sxs-lookup"><span data-stu-id="33228-159">b.</span></span> <span data-ttu-id="33228-160">In de **id** textbox, plak de **'Eenmalige op URL'** waarde`https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="33228-160">In the **Identifier** textbox, paste the **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="33228-161">Houd er rekening mee dat de aanmelding URL worden geleverd door het team Velpic SAML en id-waarde beschikbaar zijn bij het configureren van de SSO-invoegtoepassing Velpic SAML-zijde.</span><span class="sxs-lookup"><span data-stu-id="33228-161">Please note that the Sign on URL will be provided by the Velpic SAML team and Identifier value will be available when you configure the SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="33228-162">U wilt dat de waarde van de Velpic SAML toepassingspagina kopiëren en plak dit hier.</span><span class="sxs-lookup"><span data-stu-id="33228-162">You need to copy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="33228-163">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="33228-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="33228-165">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="33228-165">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="33228-167">Klik in de configuratiesectie Velpic SAML Velpic SAML configureren om configureren aanmelding venster te openen.</span><span class="sxs-lookup"><span data-stu-id="33228-167">On the Velpic SAML Configuration section, click Configure Velpic SAML to open Configure sign-on window.</span></span> <span data-ttu-id="33228-168">Kopieer de SAML-entiteit-ID uit de sectie eenvoudig kunt raadplegen.</span><span class="sxs-lookup"><span data-stu-id="33228-168">Copy the SAML Entity ID from the Quick Reference section.</span></span>

7. <span data-ttu-id="33228-169">In een ander browservenster, meld u bij uw bedrijf Velpic SAML site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="33228-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="33228-170">Klik op **beheren** tabblad en Ga naar **integratie** sectie waarin u klikt u wilt op **Plugins** knop nieuwe invoegtoepassing maken voor aanmelden.</span><span class="sxs-lookup"><span data-stu-id="33228-170">Click on **Manage** tab and go to **Integration** section where you need to click on **Plugins** button to create new plugin for Sign-In.</span></span>

    ![Invoegtoepassing](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="33228-172">Klik op de **'Add invoegtoepassing'** knop.</span><span class="sxs-lookup"><span data-stu-id="33228-172">Click on the **‘Add plugin’** button.</span></span>
    
    ![Invoegtoepassing](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="33228-174">Klik op de **SAML** -tegel in de pagina invoegtoepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="33228-174">Click on the **SAML** tile in the Add Plugin page.</span></span>
    
    ![Invoegtoepassing](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="33228-176">Voer de naam van de nieuwe SAML-invoegtoepassing en klik op de **'Add-** knop.</span><span class="sxs-lookup"><span data-stu-id="33228-176">Enter the name of the new SAML plugin and click the **‘Add’** button.</span></span>

    ![Invoegtoepassing](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="33228-178">Voer de gegevens als volgt:</span><span class="sxs-lookup"><span data-stu-id="33228-178">Enter the details as follows:</span></span>

    ![Invoegtoepassing](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="33228-180">a.</span><span class="sxs-lookup"><span data-stu-id="33228-180">a.</span></span> <span data-ttu-id="33228-181">In de **naam** textbox, typ de naam van SAML-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="33228-181">In the **Name** textbox, type the name of SAML plugin.</span></span>

    <span data-ttu-id="33228-182">b.</span><span class="sxs-lookup"><span data-stu-id="33228-182">b.</span></span> <span data-ttu-id="33228-183">In de **URL-verlener** textbox plakken de **SAML entiteit-ID** u gekopieerd uit de **eenmalige aanmelding configureren** venster van de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="33228-183">In the **Issuer URL** textbox, paste the **SAML Entity ID** you copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="33228-184">c.</span><span class="sxs-lookup"><span data-stu-id="33228-184">c.</span></span> <span data-ttu-id="33228-185">In de **Provider metagegevens Config** het Metadata XML-bestand dat u hebt gedownload van Azure-portal uploaden.</span><span class="sxs-lookup"><span data-stu-id="33228-185">In the **Provider Metadata Config** upload the Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="33228-186">d.</span><span class="sxs-lookup"><span data-stu-id="33228-186">d.</span></span> <span data-ttu-id="33228-187">U kunt er ook voor kiezen om in te schakelen SAML in tijd inrichten doordat de **'Automatische Maak nieuwe gebruikers'** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="33228-187">You can also choose to enable SAML just in time provisioning by enabling the **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="33228-188">Als een gebruiker niet in Velpic bestaat en deze markering niet is ingeschakeld, mislukt de aanmelding van Azure.</span><span class="sxs-lookup"><span data-stu-id="33228-188">If a user doesn’t exist in Velpic and this flag is not enabled, the login from Azure will fail.</span></span> <span data-ttu-id="33228-189">Als de vlag is ingeschakeld. de gebruiker automatisch worden ingericht in Velpic op het moment van de aanmelding.</span><span class="sxs-lookup"><span data-stu-id="33228-189">If the flag is enabled the user will automatically be provisioned into Velpic at the time of login.</span></span> 

    <span data-ttu-id="33228-190">e.</span><span class="sxs-lookup"><span data-stu-id="33228-190">e.</span></span> <span data-ttu-id="33228-191">Kopieer de **eenmalige op URL** uit de tekst vak en plak deze in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="33228-191">Copy the **Single sign on URL** from the text box and paste it in the Azure portal.</span></span>
    
    <span data-ttu-id="33228-192">f.</span><span class="sxs-lookup"><span data-stu-id="33228-192">f.</span></span> <span data-ttu-id="33228-193">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="33228-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="33228-194">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="33228-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="33228-195">Het doel van deze sectie is het een testgebruiker maken in Azure Management portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="33228-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="33228-197">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="33228-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="33228-198">In de **Azure Management portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="33228-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="33228-200">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="33228-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="33228-202">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="33228-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="33228-204">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="33228-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="33228-206">a.</span><span class="sxs-lookup"><span data-stu-id="33228-206">a.</span></span> <span data-ttu-id="33228-207">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="33228-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="33228-208">b.</span><span class="sxs-lookup"><span data-stu-id="33228-208">b.</span></span> <span data-ttu-id="33228-209">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="33228-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="33228-210">c.</span><span class="sxs-lookup"><span data-stu-id="33228-210">c.</span></span> <span data-ttu-id="33228-211">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="33228-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="33228-212">d.</span><span class="sxs-lookup"><span data-stu-id="33228-212">d.</span></span> <span data-ttu-id="33228-213">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="33228-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="33228-214">Een testgebruiker Velpic SAML maken</span><span class="sxs-lookup"><span data-stu-id="33228-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="33228-215">Deze stap is meestal niet vereist als de toepassing alleen bij tijd gebruikersaanvragen ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="33228-215">This step is usually not required as the application supports just in time user provisioning.</span></span> <span data-ttu-id="33228-216">Als de automatische gebruikersinrichting niet is ingeschakeld kan vervolgens maken van een handmatige gebruikersaccount worden uitgevoerd zoals hieronder wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="33228-216">If the automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="33228-217">Meld u aan bij uw site van het bedrijf Velpic SAML als beheerder en voert u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="33228-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="33228-218">Klik op het tabblad beheren en gaat u naar de sectie gebruikers en klik vervolgens op de knop Nieuw gebruikers toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="33228-218">Click on Manage tab and go to Users section, then click on New button to add users.</span></span>

    ![gebruiker toevoegen](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="33228-220">Op de **'Nieuwe gebruiker maken'** dialoogvenster pagina, de volgende stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="33228-220">On the **“Create New User”** dialog page, perform the following steps.</span></span>

    ![Gebruiker](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="33228-222">a.</span><span class="sxs-lookup"><span data-stu-id="33228-222">a.</span></span> <span data-ttu-id="33228-223">In de **voornaam** textbox typenaam de eerste van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="33228-223">In the **First Name** textbox, type the first name of Britta Simon.</span></span>

    <span data-ttu-id="33228-224">b.</span><span class="sxs-lookup"><span data-stu-id="33228-224">b.</span></span> <span data-ttu-id="33228-225">In de **achternaam** textbox, typt u de achternaam van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="33228-225">In the **Last Name** textbox, type the last name of Britta Simon.</span></span>

    <span data-ttu-id="33228-226">c.</span><span class="sxs-lookup"><span data-stu-id="33228-226">c.</span></span> <span data-ttu-id="33228-227">In de **gebruikersnaam** textbox, typ de gebruikersnaam van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="33228-227">In the **User Name** textbox, type the user name of Britta Simon.</span></span>

    <span data-ttu-id="33228-228">d.</span><span class="sxs-lookup"><span data-stu-id="33228-228">d.</span></span> <span data-ttu-id="33228-229">In de **e** textbox, typ de e-mailadres van Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="33228-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="33228-230">e.</span><span class="sxs-lookup"><span data-stu-id="33228-230">e.</span></span> <span data-ttu-id="33228-231">De rest van de informatie is optioneel en kan ingevuld als die nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="33228-231">Rest of the information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="33228-232">f.</span><span class="sxs-lookup"><span data-stu-id="33228-232">f.</span></span> <span data-ttu-id="33228-233">Klik op **OPSLAAN**.</span><span class="sxs-lookup"><span data-stu-id="33228-233">Click **SAVE**.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="33228-234">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="33228-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="33228-235">In deze sectie maakt inschakelen u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="33228-235">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Velpic SAML.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="33228-237">**Britta Simon om aan te wijzen Velpic SAML, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="33228-237">**To assign Britta Simon to Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="33228-238">In de Azure-beheerportal, opent u de weergave toepassingen en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="33228-238">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="33228-240">Selecteer in de lijst met toepassingen **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="33228-240">In the applications list, select **Velpic SAML**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="33228-242">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="33228-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="33228-244">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="33228-244">Click **Add** button.</span></span> <span data-ttu-id="33228-245">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="33228-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="33228-247">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="33228-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="33228-248">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="33228-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="33228-249">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="33228-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="33228-250">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="33228-250">Testing single sign-on</span></span>

<span data-ttu-id="33228-251">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="33228-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="33228-252">Als u op de tegel Velpic SAML in het deelvenster toegang, krijgt u de aanmeldingspagina van Velpic SAML-toepassing.</span><span class="sxs-lookup"><span data-stu-id="33228-252">When you click the Velpic SAML tile in the Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="33228-253">U ziet de **'Aanmelden met Azure AD'** knop op de aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="33228-253">You should see the **‘Log In With Azure AD’** button on the sign in page.</span></span>

    ![Invoegtoepassing](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="33228-255">Klik op de **'Aanmelden met Azure AD'** knop aanmelden bij Velpic met behulp van uw Azure AD-account.</span><span class="sxs-lookup"><span data-stu-id="33228-255">Click on the **‘Log In With Azure AD’** button to log in to Velpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="33228-256">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="33228-256">Additional resources</span></span>

* [<span data-ttu-id="33228-257">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="33228-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="33228-258">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="33228-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

