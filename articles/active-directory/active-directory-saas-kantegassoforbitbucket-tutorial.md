---
title: 'Zelfstudie: Azure Active Directory-integratie met Kantega SSO voor Bitbucket | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Kantega SSO voor Bitbucket.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c41cdaaf-0441-493c-94c7-569615b7b1ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 6656c9abf8483ee98c0cb1a16c06d078e32240f2
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bitbucket"></a><span data-ttu-id="e3a31-103">Zelfstudie: Azure Active Directory-integratie met Kantega SSO voor Bitbucket</span><span class="sxs-lookup"><span data-stu-id="e3a31-103">Tutorial: Azure Active Directory integration with Kantega SSO for Bitbucket</span></span>

<span data-ttu-id="e3a31-104">In deze zelfstudie leert u hoe Kantega SSO voor Bitbucket integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e3a31-104">In this tutorial, you learn how to integrate Kantega SSO for Bitbucket with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e3a31-105">Kantega SSO voor Bitbucket integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e3a31-105">Integrating Kantega SSO for Bitbucket with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e3a31-106">U kunt beheren in Azure AD die toegang tot Kantega SSO voor Bitbucket heeft</span><span class="sxs-lookup"><span data-stu-id="e3a31-106">You can control in Azure AD who has access to Kantega SSO for Bitbucket</span></span>
- <span data-ttu-id="e3a31-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Kantega SSO voor Bitbucket (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="e3a31-107">You can enable your users to automatically get signed-on to Kantega SSO for Bitbucket (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e3a31-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="e3a31-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e3a31-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e3a31-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3a31-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e3a31-110">Prerequisites</span></span>

<span data-ttu-id="e3a31-111">Voor het configureren van Azure AD-integratie met Kantega SSO voor Bitbucket, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="e3a31-111">To configure Azure AD integration with Kantega SSO for Bitbucket, you need the following items:</span></span>

- <span data-ttu-id="e3a31-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e3a31-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e3a31-113">Een Kantega SSO voor eenmalige aanmelding Bitbucket abonnement ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="e3a31-113">A Kantega SSO for Bitbucket single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e3a31-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e3a31-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e3a31-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e3a31-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e3a31-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e3a31-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e3a31-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e3a31-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e3a31-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e3a31-118">Scenario description</span></span>
<span data-ttu-id="e3a31-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e3a31-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e3a31-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e3a31-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e3a31-121">Kantega SSO voor Bitbucket uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e3a31-121">Adding Kantega SSO for Bitbucket from the gallery</span></span>
2. <span data-ttu-id="e3a31-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e3a31-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-bitbucket-from-the-gallery"></a><span data-ttu-id="e3a31-123">Kantega SSO voor Bitbucket uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e3a31-123">Adding Kantega SSO for Bitbucket from the gallery</span></span>
<span data-ttu-id="e3a31-124">Voor het configureren van de integratie van Kantega SSO voor Bitbucket in Azure AD, moet u Kantega SSO voor Bitbucket uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e3a31-124">To configure the integration of Kantega SSO for Bitbucket into Azure AD, you need to add Kantega SSO for Bitbucket from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e3a31-125">**Als u wilt toevoegen Kantega SSO voor Bitbucket uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e3a31-125">**To add Kantega SSO for Bitbucket from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e3a31-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e3a31-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e3a31-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e3a31-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="e3a31-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e3a31-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="e3a31-133">Typ in het zoekvak **Kantega SSO voor Bitbucket**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-133">In the search box, type **Kantega SSO for Bitbucket**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_search.png)

5. <span data-ttu-id="e3a31-135">Selecteer in het deelvenster resultaten **Kantega SSO voor Bitbucket**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e3a31-135">In the results panel, select **Kantega SSO for Bitbucket**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e3a31-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e3a31-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e3a31-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Kantega SSO voor Bitbucket op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="e3a31-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Bitbucket based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e3a31-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Kantega SSO voor Bitbucket is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3a31-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for Bitbucket is to a user in Azure AD.</span></span> <span data-ttu-id="e3a31-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Kantega SSO voor Bitbucket tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="e3a31-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for Bitbucket needs to be established.</span></span>

<span data-ttu-id="e3a31-141">Wijs in Kantega SSO voor Bitbucket, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="e3a31-141">In Kantega SSO for Bitbucket, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e3a31-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Kantega SSO voor Bitbucket, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="e3a31-142">To configure and test Azure AD single sign-on with Kantega SSO for Bitbucket, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e3a31-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e3a31-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e3a31-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e3a31-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e3a31-145">**[Maken van een SSO Kantega voor de testgebruiker Bitbucket](#creating-a-kantega-sso-for-bitbucket-test-user)**  - Kantega SSO voor Bitbucket die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="e3a31-145">**[Creating a Kantega SSO for Bitbucket test user](#creating-a-kantega-sso-for-bitbucket-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for Bitbucket that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e3a31-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e3a31-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e3a31-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e3a31-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e3a31-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e3a31-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e3a31-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw Kantega SSO voor Bitbucket-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e3a31-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for Bitbucket application.</span></span>

<span data-ttu-id="e3a31-150">**Voor het configureren van Azure AD eenmalige aanmelding met Kantega SSO voor Bitbucket, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e3a31-150">**To configure Azure AD single sign-on with Kantega SSO for Bitbucket, perform the following steps:**</span></span>

1. <span data-ttu-id="e3a31-151">In de Azure-portal op de **Kantega SSO voor Bitbucket** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-151">In the Azure portal, on the **Kantega SSO for Bitbucket** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e3a31-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e3a31-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_samlbase.png)

3. <span data-ttu-id="e3a31-155">In **IDP** modus gestart op de **Kantega SSO voor domein Bitbucket en URL's** sectie de volgende stap uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e3a31-155">In **IDP** initiated mode, on the **Kantega SSO for Bitbucket Domain and URLs** section perform the following step:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_url1.png)

    <span data-ttu-id="e3a31-157">a.</span><span class="sxs-lookup"><span data-stu-id="e3a31-157">a.</span></span> <span data-ttu-id="e3a31-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="e3a31-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="e3a31-159">b.</span><span class="sxs-lookup"><span data-stu-id="e3a31-159">b.</span></span> <span data-ttu-id="e3a31-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="e3a31-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="e3a31-161">In **SP** geïnitieerd modus selectievakje **weergeven geavanceerde instellingen voor URL** en voer de volgende stap:</span><span class="sxs-lookup"><span data-stu-id="e3a31-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform the following step:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_url2.png)
    
    <span data-ttu-id="e3a31-163">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="e3a31-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e3a31-164">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="e3a31-164">These values are not real.</span></span> <span data-ttu-id="e3a31-165">Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="e3a31-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="e3a31-166">Deze waarden worden ontvangen tijdens de configuratie van de Bitbucket-invoegtoepassing die verderop in de zelfstudie wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="e3a31-166">These values are recieved during the configuration of Bitbucket plugin which is explained later in the tutorial.</span></span>

5. <span data-ttu-id="e3a31-167">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e3a31-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_certificate.png) 

6. <span data-ttu-id="e3a31-169">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e3a31-169">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="e3a31-171">In een ander browservenster, meld u aan bij uw Bitbucket-beheerportal als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e3a31-171">In a different web browser window, log in to your Bitbucket admin portal as an administrator.</span></span>

8. <span data-ttu-id="e3a31-172">Klik op tandwiel en op de **vinden van nieuwe invoegtoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-172">Click cog and click the **Find new add-ons**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon1.png)

9. <span data-ttu-id="e3a31-174">Search **Kantega SSO voor Bitbucket SAML & Kerberos** en klik op **installeren** knop voor het installeren van de nieuwe SAML-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="e3a31-174">Search **Kantega SSO for Bitbucket SAML & Kerberos** and click **Install** button to install the new SAML plugin.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon2.png)

10. <span data-ttu-id="e3a31-176">De installatie van de invoegtoepassing wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="e3a31-176">The plugin installation starts.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon31.png)

11. <span data-ttu-id="e3a31-178">Zodra de installatie voltooid is.</span><span class="sxs-lookup"><span data-stu-id="e3a31-178">Once the installation is complete.</span></span> <span data-ttu-id="e3a31-179">Klik op **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-179">Click **Close**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon33.png)

12. <span data-ttu-id="e3a31-181">Klik op **Beheren**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-181">Click **Manage**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon34.png)
    
13. <span data-ttu-id="e3a31-183">Klik op **configureren** voor het configureren van de nieuwe invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="e3a31-183">Click **Configure** to configure the new plugin.</span></span>    

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon35.png)

14. <span data-ttu-id="e3a31-185">In de **SAML** sectie.</span><span class="sxs-lookup"><span data-stu-id="e3a31-185">In the **SAML** section.</span></span> <span data-ttu-id="e3a31-186">Selecteer **Azure Active Directory (Azure AD)** van de **toevoegen identiteitsprovider** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="e3a31-186">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon4.png)

15. <span data-ttu-id="e3a31-188">Abonnement als selecteren **Basic**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-188">Select subscription level as **Basic**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon5.png)

16. <span data-ttu-id="e3a31-190">Op de **App-eigenschappen** sectie, voert u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="e3a31-190">On the **App properties** section, perform following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon6.png)

    <span data-ttu-id="e3a31-192">a.</span><span class="sxs-lookup"><span data-stu-id="e3a31-192">a.</span></span> <span data-ttu-id="e3a31-193">Kopieer de **App ID URI** waarde en deze gebruiken als **id, de antwoord-URL en de aanmeldings-URL** op de **Kantega SSO voor domein Bitbucket en URL's** sectie in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e3a31-193">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for Bitbucket Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="e3a31-194">b.</span><span class="sxs-lookup"><span data-stu-id="e3a31-194">b.</span></span> <span data-ttu-id="e3a31-195">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-195">Click **Next**.</span></span>

17. <span data-ttu-id="e3a31-196">Op de **metagegevens importeren** sectie, voert u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="e3a31-196">On the **Metadata import** section, perform following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon7.png)

    <span data-ttu-id="e3a31-198">a.</span><span class="sxs-lookup"><span data-stu-id="e3a31-198">a.</span></span> <span data-ttu-id="e3a31-199">Selecteer **metagegevensbestand op mijn computer**, en de metagegevens-uploadbestand, die u hebt gedownload vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e3a31-199">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="e3a31-200">b.</span><span class="sxs-lookup"><span data-stu-id="e3a31-200">b.</span></span> <span data-ttu-id="e3a31-201">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-201">Click **Next**.</span></span>

18. <span data-ttu-id="e3a31-202">Op de **en SSO** sectie, voert u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="e3a31-202">On the **Name and SSO location** section, perform following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon8.png)

    <span data-ttu-id="e3a31-204">a.</span><span class="sxs-lookup"><span data-stu-id="e3a31-204">a.</span></span> <span data-ttu-id="e3a31-205">Naam van de identiteitsprovider in toevoegen **identiteit providernaam** textbox (bijvoorbeeld Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e3a31-205">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="e3a31-206">b.</span><span class="sxs-lookup"><span data-stu-id="e3a31-206">b.</span></span> <span data-ttu-id="e3a31-207">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-207">Click **Next**.</span></span>

19. <span data-ttu-id="e3a31-208">Controleer of het certificaat voor ondertekening en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-208">Verify the Signing certificate and click **Next**.</span></span>  

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon9.png)

20. <span data-ttu-id="e3a31-210">Op de **Bitbucket gebruikersaccounts** sectie, voert u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="e3a31-210">On the **Bitbucket user accounts** section, perform following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon10.png)

    <span data-ttu-id="e3a31-212">a.</span><span class="sxs-lookup"><span data-stu-id="e3a31-212">a.</span></span> <span data-ttu-id="e3a31-213">Selecteer **gebruikers in de Bitbucket interne Directory maken, indien nodig** en voer de juiste naam van de groep voor gebruikers (kan meerdere Nee.</span><span class="sxs-lookup"><span data-stu-id="e3a31-213">Select **Create users in Bitbucket's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="e3a31-214">van groepen van elkaar gescheiden door komma's).</span><span class="sxs-lookup"><span data-stu-id="e3a31-214">of groups separated by comma).</span></span>

    <span data-ttu-id="e3a31-215">b.</span><span class="sxs-lookup"><span data-stu-id="e3a31-215">b.</span></span> <span data-ttu-id="e3a31-216">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-216">Click **Next**.</span></span>

21. <span data-ttu-id="e3a31-217">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-217">Click **Finish**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon11.png)

22. <span data-ttu-id="e3a31-219">Op de **bekend domeinen voor Azure AD** sectie, voert u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="e3a31-219">On the **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon12.png)

    <span data-ttu-id="e3a31-221">a.</span><span class="sxs-lookup"><span data-stu-id="e3a31-221">a.</span></span> <span data-ttu-id="e3a31-222">Selecteer **domeinen bekend** in het linkerpaneel van de pagina.</span><span class="sxs-lookup"><span data-stu-id="e3a31-222">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="e3a31-223">b.</span><span class="sxs-lookup"><span data-stu-id="e3a31-223">b.</span></span> <span data-ttu-id="e3a31-224">Geef de domeinnaam in de **domeinen bekend** textbox.</span><span class="sxs-lookup"><span data-stu-id="e3a31-224">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="e3a31-225">c.</span><span class="sxs-lookup"><span data-stu-id="e3a31-225">c.</span></span> <span data-ttu-id="e3a31-226">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-226">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="e3a31-227">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="e3a31-227">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e3a31-228">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="e3a31-228">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e3a31-229">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e3a31-229">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e3a31-230">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e3a31-230">Creating an Azure AD test user</span></span>
<span data-ttu-id="e3a31-231">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e3a31-231">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="e3a31-233">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e3a31-233">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e3a31-234">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e3a31-234">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e3a31-236">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-236">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e3a31-238">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e3a31-238">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e3a31-240">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e3a31-240">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e3a31-242">a.</span><span class="sxs-lookup"><span data-stu-id="e3a31-242">a.</span></span> <span data-ttu-id="e3a31-243">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-243">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e3a31-244">b.</span><span class="sxs-lookup"><span data-stu-id="e3a31-244">b.</span></span> <span data-ttu-id="e3a31-245">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e3a31-245">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e3a31-246">c.</span><span class="sxs-lookup"><span data-stu-id="e3a31-246">c.</span></span> <span data-ttu-id="e3a31-247">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-247">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e3a31-248">d.</span><span class="sxs-lookup"><span data-stu-id="e3a31-248">d.</span></span> <span data-ttu-id="e3a31-249">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-249">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-bitbucket-test-user"></a><span data-ttu-id="e3a31-250">Maken van een SSO Kantega voor Bitbucket testgebruiker</span><span class="sxs-lookup"><span data-stu-id="e3a31-250">Creating a Kantega SSO for Bitbucket test user</span></span>

<span data-ttu-id="e3a31-251">Om Azure AD-gebruikers zich aanmelden bij Bitbucket, moeten ze worden ingericht in Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="e3a31-251">To enable Azure AD users to log in to Bitbucket, they must be provisioned into Bitbucket.</span></span> <span data-ttu-id="e3a31-252">In Kantega SSO voor Bitbucket is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="e3a31-252">In Kantega SSO for Bitbucket, provisioning is a manual task.</span></span>

<span data-ttu-id="e3a31-253">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e3a31-253">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="e3a31-254">Meld u aan bij uw bedrijf Bitbucket site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e3a31-254">Log in to your Bitbucket company site as an administrator.</span></span>

2. <span data-ttu-id="e3a31-255">Klik op het Instellingenpictogram.</span><span class="sxs-lookup"><span data-stu-id="e3a31-255">Click on settings icon.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user1.png) 

3. <span data-ttu-id="e3a31-257">Onder **beheer** tabblad gedeelte, klikt u op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-257">Under **Administration** tab section, click **Users**.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user2.png)

4. <span data-ttu-id="e3a31-259">Klik op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-259">Click **Create user**.</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user3.png)     

5. <span data-ttu-id="e3a31-261">Op de **gebruiker maken** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e3a31-261">On the **Create User** dialog page, perform the following steps:</span></span>

    ![Werknemer toevoegen](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user4.png) 

    <span data-ttu-id="e3a31-263">a.</span><span class="sxs-lookup"><span data-stu-id="e3a31-263">a.</span></span> <span data-ttu-id="e3a31-264">In de **gebruikersnaam** textbox, typ het e-mailadres van gebruiker, zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="e3a31-264">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="e3a31-265">b.</span><span class="sxs-lookup"><span data-stu-id="e3a31-265">b.</span></span> <span data-ttu-id="e3a31-266">In de **volledige naam** textbox, volledige naam van de gebruiker zoals Britta Simon type.</span><span class="sxs-lookup"><span data-stu-id="e3a31-266">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>
    
    <span data-ttu-id="e3a31-267">c.</span><span class="sxs-lookup"><span data-stu-id="e3a31-267">c.</span></span> <span data-ttu-id="e3a31-268">In de **e-mailadres** textbox, typ het e-mailadres van gebruiker, zoals Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="e3a31-268">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="e3a31-269">d.</span><span class="sxs-lookup"><span data-stu-id="e3a31-269">d.</span></span> <span data-ttu-id="e3a31-270">In de **wachtwoord** textbox, typt u het wachtwoord van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e3a31-270">In the **Password** textbox, type the password of user.</span></span>  

    <span data-ttu-id="e3a31-271">e.</span><span class="sxs-lookup"><span data-stu-id="e3a31-271">e.</span></span> <span data-ttu-id="e3a31-272">In de **wachtwoord bevestigen** textbox, voer het wachtwoord van gebruiker opnieuw in.</span><span class="sxs-lookup"><span data-stu-id="e3a31-272">In the **Confirm Password** textbox, reenter the password of user.</span></span>

    <span data-ttu-id="e3a31-273">f.</span><span class="sxs-lookup"><span data-stu-id="e3a31-273">f.</span></span> <span data-ttu-id="e3a31-274">Klik op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-274">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e3a31-275">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3a31-275">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e3a31-276">In deze sectie maakt inschakelen u Britta Simon toegang verlenen aan Kantega SSO voor Bitbucket gebruiken Azure eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e3a31-276">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for Bitbucket.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="e3a31-278">**Britta Simon om aan te wijzen Kantega SSO voor Bitbucket, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e3a31-278">**To assign Britta Simon to Kantega SSO for Bitbucket, perform the following steps:**</span></span>

1. <span data-ttu-id="e3a31-279">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-279">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e3a31-281">Selecteer in de lijst met toepassingen **Kantega SSO voor Bitbucket**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-281">In the applications list, select **Kantega SSO for Bitbucket**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_app.png) 

3. <span data-ttu-id="e3a31-283">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e3a31-283">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="e3a31-285">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e3a31-285">Click **Add** button.</span></span> <span data-ttu-id="e3a31-286">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e3a31-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="e3a31-288">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e3a31-288">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e3a31-289">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e3a31-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e3a31-290">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e3a31-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e3a31-291">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e3a31-291">Testing single sign-on</span></span>

<span data-ttu-id="e3a31-292">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="e3a31-292">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e3a31-293">Als u op de Kantega SSO Bitbucket-tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw Kantega SSO voor Bitbucket-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e3a31-293">When you click the Kantega SSO for Bitbucket tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for Bitbucket application.</span></span>
<span data-ttu-id="e3a31-294">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e3a31-294">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e3a31-295">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e3a31-295">Additional resources</span></span>

* [<span data-ttu-id="e3a31-296">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3a31-296">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e3a31-297">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e3a31-297">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_203.png

