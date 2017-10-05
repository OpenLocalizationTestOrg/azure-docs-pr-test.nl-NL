---
title: 'Zelfstudie: Azure Active Directory-integratie met ScaleX Enterprise | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en ScaleX Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: 0ebed0c2605862426384c0e219e52c9d626b6246
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="2b63b-103">Zelfstudie: Azure Active Directory-integratie met ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="2b63b-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="2b63b-104">In deze zelfstudie leert u hoe ScaleX-onderneming integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2b63b-104">In this tutorial, you learn how to integrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2b63b-105">ScaleX-onderneming integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2b63b-105">Integrating ScaleX Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2b63b-106">U kunt beheren in Azure AD die toegang tot ScaleX Enterprise heeft</span><span class="sxs-lookup"><span data-stu-id="2b63b-106">You can control in Azure AD who has access to ScaleX Enterprise</span></span>
- <span data-ttu-id="2b63b-107">U kunt uw gebruikers automatisch ophalen aangemeld bij ScaleX Enterprise (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="2b63b-107">You can enable your users to automatically get signed-on to ScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2b63b-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="2b63b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2b63b-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, zien.</span><span class="sxs-lookup"><span data-stu-id="2b63b-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="2b63b-110">Wat is er toegang tot toepassingen en eenmalige aanmelding met [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2b63b-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b63b-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2b63b-111">Prerequisites</span></span>

<span data-ttu-id="2b63b-112">Voor het configureren van Azure AD-integratie met ScaleX voor ondernemingen, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="2b63b-112">To configure Azure AD integration with ScaleX Enterprise, you need the following items:</span></span>

- <span data-ttu-id="2b63b-113">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2b63b-113">An Azure AD subscription</span></span>
- <span data-ttu-id="2b63b-114">Een ScaleX Enterprise eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2b63b-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2b63b-115">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2b63b-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2b63b-116">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2b63b-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2b63b-117">Gebruik niet uw productieomgeving, tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2b63b-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2b63b-118">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2b63b-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2b63b-119">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2b63b-119">Scenario description</span></span>
<span data-ttu-id="2b63b-120">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2b63b-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2b63b-121">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2b63b-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2b63b-122">ScaleX Enterprise uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="2b63b-122">Adding ScaleX Enterprise from the gallery</span></span>
2. <span data-ttu-id="2b63b-123">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2b63b-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-the-gallery"></a><span data-ttu-id="2b63b-124">ScaleX Enterprise uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="2b63b-124">Adding ScaleX Enterprise from the gallery</span></span>
<span data-ttu-id="2b63b-125">Voor het configureren van de integratie van ScaleX Enterprise in Azure AD, moet u ScaleX Enterprise uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2b63b-125">To configure the integration of ScaleX Enterprise in to Azure AD, you need to add ScaleX Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2b63b-126">**Als u wilt toevoegen ScaleX Enterprise uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2b63b-126">**To add ScaleX Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2b63b-127">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2b63b-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2b63b-129">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2b63b-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2b63b-130">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2b63b-130">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="2b63b-132">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b63b-132">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="2b63b-134">Typ in het zoekvak **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="2b63b-134">In the search box, type **ScaleX Enterprise**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="2b63b-136">Selecteer in het deelvenster resultaten **ScaleX Enterprise**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="2b63b-136">In the results panel, select **ScaleX Enterprise**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2b63b-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2b63b-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2b63b-139">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met ScaleX Enterprise op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="2b63b-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2b63b-140">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in de onderneming ScaleX is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b63b-140">For single sign-on to work, Azure AD needs to know what the counterpart user in ScaleX Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="2b63b-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de onderneming ScaleX tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="2b63b-141">In other words, a link relationship between an Azure AD user and the related user in ScaleX Enterprise needs to be established.</span></span>

<span data-ttu-id="2b63b-142">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in ScaleX onderneming.</span><span class="sxs-lookup"><span data-stu-id="2b63b-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="2b63b-143">Om te configureren en testen van Azure AD eenmalige aanmelding met ScaleX voor ondernemingen, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="2b63b-143">To configure and test Azure AD single sign-on with ScaleX Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2b63b-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2b63b-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2b63b-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2b63b-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2b63b-146">**[Maken van een testgebruiker ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)**  - ScaleX Enterprise die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="2b63b-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - to have a counterpart of Britta Simon in ScaleX Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2b63b-147">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2b63b-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2b63b-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2b63b-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2b63b-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2b63b-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2b63b-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="2b63b-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="2b63b-151">**Voor het configureren van Azure AD eenmalige aanmelding met ScaleX voor ondernemingen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2b63b-151">**To configure Azure AD single sign-on with ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="2b63b-152">In de Azure-portal op de **ScaleX Enterprise** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2b63b-152">In the Azure portal, on the **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2b63b-154">Op de **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2b63b-154">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="2b63b-156">Op de **ScaleX Enterprise domein en de URL's** sectie, voert u de volgende stappen uit als u wilt configureren, de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="2b63b-156">On the **ScaleX Enterprise Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="2b63b-158">a.</span><span class="sxs-lookup"><span data-stu-id="2b63b-158">a.</span></span> <span data-ttu-id="2b63b-159">In de **id** textbox, typ de waarde met het volgende patroon volgen:`https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="2b63b-159">In the **Identifier** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="2b63b-160">b.</span><span class="sxs-lookup"><span data-stu-id="2b63b-160">b.</span></span> <span data-ttu-id="2b63b-161">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="2b63b-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="2b63b-162">Controleer **weergeven geavanceerde instellingen voor URL**, als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="2b63b-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="2b63b-164">In de **aanmeldings-URL** textbox, typ de waarde met het volgende patroon volgen:`https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="2b63b-164">In the **Sign-on URL** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="2b63b-165">Deze zijn niet de werkelijke waarden.</span><span class="sxs-lookup"><span data-stu-id="2b63b-165">These are not the real values.</span></span> <span data-ttu-id="2b63b-166">Deze waarden bijwerken met de werkelijke-id, antwoord-URL of aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="2b63b-166">Update these values with the actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="2b63b-167">Neem contact op met [ScaleX Enterprise Client ondersteuningsteam](http://info.rescale.com/contact_sales) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="2b63b-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) to get these values.</span></span> 

5. <span data-ttu-id="2b63b-168">Uw toepassing ScaleX verwacht de SAML-asserties in een specifieke indeling waarvoor u het aangepaste kenmerktoewijzingen aan uw configuratie van SAML-token kenmerken wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2b63b-168">Your ScaleX application expects the SAML assertions in a specific format, which requires you to modify custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="2b63b-169">Klik op **weergeven en bewerken van alle andere gebruikerskenmerken** selectievakje openen van de aangepaste kenmerken instellingen.</span><span class="sxs-lookup"><span data-stu-id="2b63b-169">Click **View and edit all other user attributes** checkbox to open the custom attributes settings.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="2b63b-171">a.</span><span class="sxs-lookup"><span data-stu-id="2b63b-171">a.</span></span> <span data-ttu-id="2b63b-172">Klik met de rechtermuisknop op het kenmerk **naam** en klik op verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2b63b-172">Right click the attribute **name** and click delete.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="2b63b-174">b.</span><span class="sxs-lookup"><span data-stu-id="2b63b-174">b.</span></span> <span data-ttu-id="2b63b-175">Klik op **emailaddress** kenmerk om het kenmerk bewerken-venster te openen.</span><span class="sxs-lookup"><span data-stu-id="2b63b-175">Click **emailaddress** attribute to open the Edit Attribute window.</span></span> <span data-ttu-id="2b63b-176">Wijzig de waarde van **user.mail** naar **user.userprincipalname** en klik op Ok.</span><span class="sxs-lookup"><span data-stu-id="2b63b-176">Change its value from **user.mail** to **user.userprincipalname** and click Ok.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="2b63b-178">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2b63b-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="2b63b-180">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2b63b-180">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="2b63b-182">Op de **ScaleX Ondernemingsconfiguratie** sectie, klikt u op **configureren ScaleX Enterprise** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="2b63b-182">On the **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2b63b-183">Kopieer de **SAML entiteit-ID** en **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="2b63b-183">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="2b63b-185">Eenmalige aanmelding configureren op **ScaleX Enterprise** side, meld u aan bij de bedrijfswebsite ScaleX Enterprise als beheerder.</span><span class="sxs-lookup"><span data-stu-id="2b63b-185">To configure single sign-on on **ScaleX Enterprise** side, login to the ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="2b63b-186">Klik op het menu in het bovenste rechts en selecteer **Contoso beheer**.</span><span class="sxs-lookup"><span data-stu-id="2b63b-186">Click the menu in the upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2b63b-187">Contoso is slechts een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="2b63b-187">Contoso is just an example.</span></span> <span data-ttu-id="2b63b-188">Dit moet de werkelijke naam van uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="2b63b-188">This should be your actual Company Name.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="2b63b-190">Selecteer **integraties** van het bovenste menu en selecteer **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2b63b-190">Select **Integrations** from the top menu and select **Single Sign-On**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="2b63b-192">Vul het formulier als volgt:</span><span class="sxs-lookup"><span data-stu-id="2b63b-192">Complete the form as follows:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="2b63b-194">a.</span><span class="sxs-lookup"><span data-stu-id="2b63b-194">a.</span></span> <span data-ttu-id="2b63b-195">Selecteer **'Alle gebruikers die kan worden geverifieerd met eenmalige aanmelding maken'.**</span><span class="sxs-lookup"><span data-stu-id="2b63b-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="2b63b-196">b.</span><span class="sxs-lookup"><span data-stu-id="2b63b-196">b.</span></span> <span data-ttu-id="2b63b-197">**Service Provider saml**: waarde van het plakken ***urn: oasis: namen: tc: SAML:2.0:nameid-indeling: permanente***</span><span class="sxs-lookup"><span data-stu-id="2b63b-197">**Service Provider saml**: Paste the value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="2b63b-198">c.</span><span class="sxs-lookup"><span data-stu-id="2b63b-198">c.</span></span> <span data-ttu-id="2b63b-199">**Naam van identiteitsprovider e veld in de ACS-antwoord**: waarde van het plakken`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="2b63b-199">**Name of Identity Provider email field in ACS response**: Paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="2b63b-200">d.</span><span class="sxs-lookup"><span data-stu-id="2b63b-200">d.</span></span> <span data-ttu-id="2b63b-201">**Identiteit EntityDescriptor entiteit-ID van Provider:** plakken de **SAML entiteit-ID** waarde opgehaald uit de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2b63b-201">**Identity Provider EntityDescriptor Entity ID:** Paste the **SAML Entity ID** value copied from the Azure portal.</span></span>

    <span data-ttu-id="2b63b-202">e.</span><span class="sxs-lookup"><span data-stu-id="2b63b-202">e.</span></span> <span data-ttu-id="2b63b-203">**ID-Provider SingleSignOnService URL:** plakken de **SAML Single Sign-On Service-URL** vanuit de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2b63b-203">**Identity Provider SingleSignOnService URL:** Paste the **SAML Single Sign-On Service URL** from the Azure portal.</span></span>

    <span data-ttu-id="2b63b-204">f.</span><span class="sxs-lookup"><span data-stu-id="2b63b-204">f.</span></span> <span data-ttu-id="2b63b-205">**Provider openbare X509 identiteitscertificaat:** Open de X509 certificaat gedownload van de Azure in Kladblok en plak de inhoud in dit vak.</span><span class="sxs-lookup"><span data-stu-id="2b63b-205">**Identity Provider public X509 certificate:** Open the X509 certificate downloaded from the Azure in notepad and paste the contents in this box.</span></span> <span data-ttu-id="2b63b-206">Zorg ervoor dat er dat geen regeleinden in het midden van de inhoud van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="2b63b-206">Ensure there are no line breaks in the middle of the certificate contents.</span></span>
    
    <span data-ttu-id="2b63b-207">g.</span><span class="sxs-lookup"><span data-stu-id="2b63b-207">g.</span></span> <span data-ttu-id="2b63b-208">Controleer de volgende selectievakjes: **ingeschakeld, NameID versleutelen en aanmelding AuthnRequests.**</span><span class="sxs-lookup"><span data-stu-id="2b63b-208">Check the following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="2b63b-209">h.</span><span class="sxs-lookup"><span data-stu-id="2b63b-209">h.</span></span> <span data-ttu-id="2b63b-210">Klik op **SSO-Update-instellingen** de instellingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="2b63b-210">Click **Update SSO Settings** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="2b63b-211">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="2b63b-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2b63b-212">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="2b63b-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2b63b-213">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2b63b-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2b63b-214">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2b63b-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="2b63b-215">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2b63b-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="2b63b-217">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2b63b-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2b63b-218">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2b63b-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2b63b-220">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="2b63b-220">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2b63b-222">Aan de bovenkant van het dialoogvenster, klikt u op **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b63b-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2b63b-224">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2b63b-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2b63b-226">a.</span><span class="sxs-lookup"><span data-stu-id="2b63b-226">a.</span></span> <span data-ttu-id="2b63b-227">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2b63b-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2b63b-228">b.</span><span class="sxs-lookup"><span data-stu-id="2b63b-228">b.</span></span> <span data-ttu-id="2b63b-229">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2b63b-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2b63b-230">c.</span><span class="sxs-lookup"><span data-stu-id="2b63b-230">c.</span></span> <span data-ttu-id="2b63b-231">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2b63b-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2b63b-232">d.</span><span class="sxs-lookup"><span data-stu-id="2b63b-232">d.</span></span> <span data-ttu-id="2b63b-233">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2b63b-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="2b63b-234">Maken van een testgebruiker ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="2b63b-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="2b63b-235">Om Azure AD-gebruikers zich aanmelden bij ScaleX Enterprise, moeten ze worden ingericht voor ScaleX onderneming.</span><span class="sxs-lookup"><span data-stu-id="2b63b-235">To enable Azure AD users to log in to ScaleX Enterprise, they must be provisioned in to ScaleX Enterprise.</span></span> <span data-ttu-id="2b63b-236">Inrichting is een automatische taak in het geval van ScaleX Enterprise, en er zijn geen handmatige stappen vereist.</span><span class="sxs-lookup"><span data-stu-id="2b63b-236">In the case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="2b63b-237">Elke gebruiker die kan worden geverifieerd met eenmalige aanmelding referenties worden automatisch aan de kant ScaleX ingericht.</span><span class="sxs-lookup"><span data-stu-id="2b63b-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on the ScaleX side.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2b63b-238">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b63b-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2b63b-239">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door de gebruikerstoegang verlenen aan ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="2b63b-239">In this section, you enable Britta Simon to use Azure single sign-on by granting user access to ScaleX Enterprise.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="2b63b-241">**Britta Simon om aan te wijzen ScaleX Enterprise, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2b63b-241">**To assign Britta Simon to ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="2b63b-242">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2b63b-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2b63b-244">Selecteer in de lijst met toepassingen **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="2b63b-244">In the applications list, select **ScaleX Enterprise**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="2b63b-246">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2b63b-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="2b63b-248">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2b63b-248">Click **Add** button.</span></span> <span data-ttu-id="2b63b-249">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b63b-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="2b63b-251">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="2b63b-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2b63b-252">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b63b-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2b63b-253">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b63b-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="2b63b-254">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2b63b-254">Testing single sign-on</span></span>

<span data-ttu-id="2b63b-255">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="2b63b-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2b63b-256">Klik op de tegel ScaleX Enterprise in het deelvenster toegang, u wordt u automatisch aangemeld bij uw toepassing ScaleX Enterprise.</span><span class="sxs-lookup"><span data-stu-id="2b63b-256">Click the ScaleX Enterprise tile in the Access Panel, you will get automatically signed-on to your ScaleX Enterprise application.</span></span> <span data-ttu-id="2b63b-257">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="2b63b-257">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2b63b-258">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2b63b-258">Additional resources</span></span>

* [<span data-ttu-id="2b63b-259">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b63b-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2b63b-260">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2b63b-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

