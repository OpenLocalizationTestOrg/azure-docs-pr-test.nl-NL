---
title: 'Zelfstudie: Azure Active Directory-integratie met Procore SSO | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Procore eenmalige aanmelding.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 042a41eaa6bb21670b4c12068f1b017222f64b99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="1d2cd-103">Zelfstudie: Azure Active Directory-integratie met Procore SSO</span><span class="sxs-lookup"><span data-stu-id="1d2cd-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="1d2cd-104">In deze zelfstudie leert u hoe Procore SSO integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1d2cd-104">In this tutorial, you learn how to integrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1d2cd-105">Procore SSO integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1d2cd-105">Integrating Procore SSO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1d2cd-106">U kunt beheren in Azure AD die toegang tot Procore SSO heeft</span><span class="sxs-lookup"><span data-stu-id="1d2cd-106">You can control in Azure AD who has access to Procore SSO</span></span>
- <span data-ttu-id="1d2cd-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Procore SSO (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="1d2cd-107">You can enable your users to automatically get signed-on to Procore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1d2cd-108">U kunt uw accounts op één centrale locatie - en de Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="1d2cd-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="1d2cd-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1d2cd-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Procore SSO, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="1d2cd-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1d2cd-110">Prerequisites</span></span>

<span data-ttu-id="1d2cd-111">Voor het configureren van Azure AD-integratie met Procore SSO, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="1d2cd-111">To configure Azure AD integration with Procore SSO, you need the following items:</span></span>

- <span data-ttu-id="1d2cd-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1d2cd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1d2cd-113">Een Procore SSO eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="1d2cd-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1d2cd-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1d2cd-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1d2cd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1d2cd-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="1d2cd-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1d2cd-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1d2cd-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1d2cd-118">Scenario description</span></span>
<span data-ttu-id="1d2cd-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1d2cd-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1d2cd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1d2cd-121">Procore SSO uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1d2cd-121">Adding Procore SSO from the gallery</span></span>
2. <span data-ttu-id="1d2cd-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1d2cd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-the-gallery"></a><span data-ttu-id="1d2cd-123">Procore SSO uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1d2cd-123">Adding Procore SSO from the gallery</span></span>
<span data-ttu-id="1d2cd-124">Voor het configureren van de integratie van Procore SSO in Azure AD, moet u Procore SSO uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-124">To configure the integration of Procore SSO into Azure AD, you need to add Procore SSO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1d2cd-125">**Als u wilt toevoegen Procore SSO uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1d2cd-125">**To add Procore SSO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1d2cd-126">In de  **[Azure Management Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1d2cd-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1d2cd-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="1d2cd-131">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-131">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="1d2cd-133">Typ in het zoekvak **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-133">In the search box, type **Procore SSO**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="1d2cd-135">Selecteer in het deelvenster resultaten **Procore SSO**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-135">In the results panel, select **Procore SSO**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1d2cd-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1d2cd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1d2cd-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Procore eenmalige aanmelding op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1d2cd-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Procore eenmalige aanmelding is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Procore SSO is to a user in Azure AD.</span></span> <span data-ttu-id="1d2cd-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Procore eenmalige aanmelding tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-140">In other words, a link relationship between an Azure AD user and the related user in Procore SSO needs to be established.</span></span>

<span data-ttu-id="1d2cd-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Procore eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Procore SSO.</span></span>

<span data-ttu-id="1d2cd-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Procore SSO, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="1d2cd-142">To configure and test Azure AD single sign-on with Procore SSO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1d2cd-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1d2cd-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1d2cd-145">**[Maken van een testgebruiker Procore SSO](#creating-a-procore-sso-test-user)**  - Procore eenmalige aanmelding die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - to have a counterpart of Britta Simon in Procore SSO that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="1d2cd-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1d2cd-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1d2cd-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1d2cd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1d2cd-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing Procore eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="1d2cd-150">**Voor het configureren van Azure AD eenmalige aanmelding met Procore SSO, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1d2cd-150">**To configure Azure AD single sign-on with Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="1d2cd-151">In de Azure-beheerportal op de **Procore SSO** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-151">In the Azure Management portal, on the **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1d2cd-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** eenmalige aanmelding inschakelen op.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="1d2cd-155">Op de **Procore SSO-domein en de URL's** sectie, de gebruiker heeft geen alle stappen uitvoeren als de app al vooraf is geïntegreerd met Azure.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-155">On the **Procore SSO Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="1d2cd-157">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="1d2cd-159">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-159">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1d2cd-161">Op de **Procore SSO configuratie** sectie, klikt u op **Procore eenmalige aanmelding configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-161">On the **Procore SSO Configuration** section, click **Configure Procore SSO** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1d2cd-162">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="1d2cd-162">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="1d2cd-164">Eenmalige aanmelding configureren op **Procore SSO** side, meld u aan bij uw site procore bedrijf als beheerder.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-164">To configure single sign-on on **Procore SSO** side, login to your procore company site as an administrator.</span></span>

8. <span data-ttu-id="1d2cd-165">In de vervolgkeuzelijst werkset omlaag, klikt u op **Admin** naar de instellingenpagina SSO openen.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-165">From the toolbox drop down, click on **Admin** to open the SSO settings page.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="1d2cd-167">De waarden in de vakken plakken, zoals beschreven onderstaande-</span><span class="sxs-lookup"><span data-stu-id="1d2cd-167">Paste the values in the boxes as described below-</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="1d2cd-169">a.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-169">a.</span></span> <span data-ttu-id="1d2cd-170">In de **eenmalige aanmelding op URL-verlener** vak, plak de SAML-entiteit-ID opgehaald uit de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-170">In the **Single Sign On Issuer URL** box, paste the SAML Entity ID copied from the Azure portal.</span></span>

    <span data-ttu-id="1d2cd-171">b.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-171">b.</span></span> <span data-ttu-id="1d2cd-172">In de **SAML aanmelding op de doel-URL** vak, plak de SAML Single Sign-On Service-URL van de Azure-portal gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-172">In the **SAML Sign On Target URL** box, paste the SAML Single Sign-On Service URL copied from the Azure portal.</span></span>

    <span data-ttu-id="1d2cd-173">c.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-173">c.</span></span> <span data-ttu-id="1d2cd-174">Open nu het **Metadata XML** hierboven gedownload vanuit de Azure portal en kopieert u het certificaat in de tag met de naam **X509Certificate**.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-174">Now open the **Metadata XML** downloaded above from the Azure portal and copy the certficate in the tag named **X509Certificate**.</span></span> <span data-ttu-id="1d2cd-175">Plak de gekopieerde waarde in de **certificaat voor eenmalige aanmelding x509** vak.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-175">Paste the copied value into the **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="1d2cd-176">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="1d2cd-177">Na deze instellingen moet u verzenden de **domeinnaam** (bijvoorbeeld **contoso.com**) via die u aan te bij Procore naar melden de [Procore ondersteuningsteam](https://support.procore.com/) en deze zullen activeren van federatieve SSO voor dat domein.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-177">After these settings, you needs to send the **domain name** (e.g **contoso.com**) through which you are logging into Procore to the [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

To ensure users can sign-in to Procore SSO after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Procore SSO in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1d2cd-178">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1d2cd-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="1d2cd-179">Het doel van deze sectie is het een testgebruiker maken in Azure Management portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-179">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="1d2cd-181">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1d2cd-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1d2cd-182">In de **Azure Management portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-182">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1d2cd-184">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-184">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1d2cd-186">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-186">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1d2cd-188">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1d2cd-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1d2cd-190">a.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-190">a.</span></span> <span data-ttu-id="1d2cd-191">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-191">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1d2cd-192">b.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-192">b.</span></span> <span data-ttu-id="1d2cd-193">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1d2cd-194">c.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-194">c.</span></span> <span data-ttu-id="1d2cd-195">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1d2cd-196">d.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-196">d.</span></span> <span data-ttu-id="1d2cd-197">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="1d2cd-198">Maken van een testgebruiker Procore SSO</span><span class="sxs-lookup"><span data-stu-id="1d2cd-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="1d2cd-199">Volg de onderstaande stappen voor het maken van een Procore testgebruiker op hun kant.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-199">Please follow the below steps to create a Procore test user on their side.</span></span>

1. <span data-ttu-id="1d2cd-200">Meld u aan bij uw site procore bedrijf als beheerder.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-200">Login to your procore company site as an administrator.</span></span>  

2. <span data-ttu-id="1d2cd-201">In de vervolgkeuzelijst werkset omlaag, klikt u op **Directory** openen van de directory-pagina van het bedrijf.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-201">From the toolbox drop down, click on **Directory** to open the company directory page.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="1d2cd-203">Klik op **toevoegen van een persoon** optie voor het openen van het formulier en voer uitvoeren na de opties -</span><span class="sxs-lookup"><span data-stu-id="1d2cd-203">Click on **Add a Person** option to open the form and enter perform following options -</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="1d2cd-205">a.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-205">a.</span></span> <span data-ttu-id="1d2cd-206">In de **voornaam** tekstvak de voornaam van de gebruiker van het type zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-206">In the **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="1d2cd-207">b.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-207">b.</span></span> <span data-ttu-id="1d2cd-208">In de **achternaam** tekstvak de achternaam van de gebruiker van het type zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-208">In the **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="1d2cd-209">c.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-209">c.</span></span> <span data-ttu-id="1d2cd-210">In de **e-mailadres** textbox e-mailadres van de gebruiker van het type, zoals  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="1d2cd-210">In the **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="1d2cd-211">d.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-211">d.</span></span> <span data-ttu-id="1d2cd-212">Selecteer **machtigingssjabloon** als **machtigingssjabloon Later toepassen**.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="1d2cd-213">e.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-213">e.</span></span> <span data-ttu-id="1d2cd-214">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-214">Click **Create**.</span></span>

4. <span data-ttu-id="1d2cd-215">Controleer en de details voor de zojuist toegevoegde contactpersoon bijwerken.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-215">Check and update the details for the newly added contact.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="1d2cd-217">Klik op **opslaan en verzenden Invitiation** (als een uitnodiging via e-mail vereist is) of **opslaan** (opslaan rechtstreeks) om de inschrijving van de gebruiker te voltooien.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) to complete the user registration.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1d2cd-219">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d2cd-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1d2cd-220">In deze sectie maakt inschakelen u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan Procore eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Procore SSO.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="1d2cd-222">**Britta Simon om aan te wijzen Procore SSO, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1d2cd-222">**To assign Britta Simon to Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="1d2cd-223">In de Azure-beheerportal, opent u de weergave toepassingen en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1d2cd-225">Selecteer in de lijst met toepassingen **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-225">In the applications list, select **Procore SSO**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="1d2cd-227">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="1d2cd-229">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-229">Click **Add** button.</span></span> <span data-ttu-id="1d2cd-230">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="1d2cd-232">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1d2cd-233">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1d2cd-234">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1d2cd-235">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1d2cd-235">Testing single sign-on</span></span>

<span data-ttu-id="1d2cd-236">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1d2cd-237">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="1d2cd-238">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="1d2cd-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="1d2cd-239">Als u op de tegel Procore SSO in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw Procore SSO-toepassing.</span><span class="sxs-lookup"><span data-stu-id="1d2cd-239">When you click the Procore SSO tile in the Access Panel, you should get automatically signed-on to your Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1d2cd-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1d2cd-240">Additional resources</span></span>

* [<span data-ttu-id="1d2cd-241">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d2cd-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1d2cd-242">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1d2cd-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

