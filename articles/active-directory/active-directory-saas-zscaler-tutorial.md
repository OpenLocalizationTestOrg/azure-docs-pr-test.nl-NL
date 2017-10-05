---
title: 'Zelfstudie: Azure Active Directory-integratie met Zscaler | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Zscaler.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68c453f7-aff1-4614-92d3-9b86f3ad99dc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 73c81691b68ee820e1d905a17b4f2ab6b6ceb5fd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler"></a><span data-ttu-id="564c1-103">Zelfstudie: Azure Active Directory-integratie met Zscaler</span><span class="sxs-lookup"><span data-stu-id="564c1-103">Tutorial: Azure Active Directory integration with Zscaler</span></span>

<span data-ttu-id="564c1-104">In deze zelfstudie leert u hoe Zscaler integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="564c1-104">In this tutorial, you learn how to integrate Zscaler with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="564c1-105">Zscaler integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="564c1-105">Integrating Zscaler with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="564c1-106">U kunt beheren in Azure AD die toegang tot Zscaler heeft</span><span class="sxs-lookup"><span data-stu-id="564c1-106">You can control in Azure AD who has access to Zscaler</span></span>
- <span data-ttu-id="564c1-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Zscaler (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="564c1-107">You can enable your users to automatically get signed-on to Zscaler (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="564c1-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="564c1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="564c1-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="564c1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="564c1-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="564c1-110">Prerequisites</span></span>

<span data-ttu-id="564c1-111">Voor het configureren van Azure AD-integratie met Zscaler, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="564c1-111">To configure Azure AD integration with Zscaler, you need the following items:</span></span>

- <span data-ttu-id="564c1-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="564c1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="564c1-113">Een Zscaler eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="564c1-113">A Zscaler single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="564c1-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="564c1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="564c1-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="564c1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="564c1-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="564c1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="564c1-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="564c1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="564c1-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="564c1-118">Scenario description</span></span>
<span data-ttu-id="564c1-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="564c1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="564c1-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="564c1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="564c1-121">Zscaler uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="564c1-121">Adding Zscaler from the gallery</span></span>
2. <span data-ttu-id="564c1-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="564c1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-from-the-gallery"></a><span data-ttu-id="564c1-123">Zscaler uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="564c1-123">Adding Zscaler from the gallery</span></span>
<span data-ttu-id="564c1-124">Voor het configureren van de integratie van Zscaler in Azure AD, moet u Zscaler uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="564c1-124">To configure the integration of Zscaler into Azure AD, you need to add Zscaler from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="564c1-125">**Als u wilt toevoegen Zscaler uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="564c1-125">**To add Zscaler from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="564c1-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="564c1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="564c1-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="564c1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="564c1-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="564c1-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="564c1-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="564c1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="564c1-133">Typ in het zoekvak **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="564c1-133">In the search box, type **Zscaler**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_search.png)

5. <span data-ttu-id="564c1-135">Selecteer in het deelvenster resultaten **Zscaler**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="564c1-135">In the results panel, select **Zscaler**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="564c1-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="564c1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="564c1-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Zscaler op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="564c1-138">In this section, you configure and test Azure AD single sign-on with Zscaler based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="564c1-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Zscaler is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="564c1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler is to a user in Azure AD.</span></span> <span data-ttu-id="564c1-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Zscaler tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="564c1-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler needs to be established.</span></span>

<span data-ttu-id="564c1-141">Wijs in Zscaler, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="564c1-141">In Zscaler, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="564c1-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Zscaler, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="564c1-142">To configure and test Azure AD single sign-on with Zscaler, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="564c1-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="564c1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="564c1-144">**[Proxy-instellingen configureren](#configuring-proxy-settings)**  : als u wilt de proxy-instellingen in Internet Explorer configureren</span><span class="sxs-lookup"><span data-stu-id="564c1-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="564c1-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="564c1-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="564c1-146">**[Maken van een testgebruiker Zscaler](#creating-a-zscaler-test-user)**  - Zscaler die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="564c1-146">**[Creating a Zscaler test user](#creating-a-zscaler-test-user)** - to have a counterpart of Britta Simon in Zscaler that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="564c1-147">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="564c1-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="564c1-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="564c1-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="564c1-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="564c1-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="564c1-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Zscaler configureren.</span><span class="sxs-lookup"><span data-stu-id="564c1-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler application.</span></span>

<span data-ttu-id="564c1-151">**Voor het configureren van Azure AD eenmalige aanmelding met Zscaler, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="564c1-151">**To configure Azure AD single sign-on with Zscaler, perform the following steps:**</span></span>

1. <span data-ttu-id="564c1-152">In de Azure-portal op de **Zscaler** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="564c1-152">In the Azure portal, on the **Zscaler** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="564c1-154">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="564c1-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_samlbase.png)

3. <span data-ttu-id="564c1-156">Op de **Zscaler domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="564c1-156">On the **Zscaler Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_url.png)

    <span data-ttu-id="564c1-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.zsclaer.net`</span><span class="sxs-lookup"><span data-stu-id="564c1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.zsclaer.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="564c1-159">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="564c1-159">This value is not real.</span></span> <span data-ttu-id="564c1-160">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="564c1-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="564c1-161">Neem contact op met [Zscaler Client ondersteuningsteam](https://www.zscaler.com/company/contact) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="564c1-161">Contact [Zscaler Client support team](https://www.zscaler.com/company/contact) to get this value.</span></span> 

4. <span data-ttu-id="564c1-162">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="564c1-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_certificate.png) 

5. <span data-ttu-id="564c1-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="564c1-164">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="564c1-166">Op de **Zscaler configuratie** sectie, klikt u op **configureren Zscaler** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="564c1-166">On the **Zscaler Configuration** section, click **Configure Zscaler** to open **Configure sign-on** window.</span></span> <span data-ttu-id="564c1-167">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="564c1-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_configure.png) 

7. <span data-ttu-id="564c1-169">In een ander browservenster, meld u aan bij uw bedrijf ZScaler site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="564c1-169">In a different web browser window, log in to your ZScaler company site as an administrator.</span></span>

8. <span data-ttu-id="564c1-170">Klik in het menu bovenaan op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="564c1-170">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="564c1-171">![Beheer](./media/active-directory-saas-zscaler-tutorial/ic800206.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="564c1-171">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="564c1-172">Onder **beheerders beheren en rollen**, klikt u op **gebruikers beheren & verificatie**.</span><span class="sxs-lookup"><span data-stu-id="564c1-172">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="564c1-173">![Gebruikers & verificatie beheren](./media/active-directory-saas-zscaler-tutorial/ic800207.png "gebruikers & verificatie beheren")</span><span class="sxs-lookup"><span data-stu-id="564c1-173">![Manage Users & Authentication](./media/active-directory-saas-zscaler-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="564c1-174">In de **verificatie-opties kiezen voor uw organisatie** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="564c1-174">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="564c1-175">![Verificatie](./media/active-directory-saas-zscaler-tutorial/ic800208.png "verificatie")</span><span class="sxs-lookup"><span data-stu-id="564c1-175">![Authentication](./media/active-directory-saas-zscaler-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="564c1-176">a.</span><span class="sxs-lookup"><span data-stu-id="564c1-176">a.</span></span> <span data-ttu-id="564c1-177">Selecteer **verificatie met eenmalige aanmelding SAML**.</span><span class="sxs-lookup"><span data-stu-id="564c1-177">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="564c1-178">b.</span><span class="sxs-lookup"><span data-stu-id="564c1-178">b.</span></span> <span data-ttu-id="564c1-179">Klik op **één SAML aanmelding Parameters configureren**.</span><span class="sxs-lookup"><span data-stu-id="564c1-179">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="564c1-180">Op de **configureren SAML Single Sign-On Parameters** dialoogvenster pagina de volgende stappen uit en klik vervolgens op **gedaan**</span><span class="sxs-lookup"><span data-stu-id="564c1-180">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="564c1-181">![Eenmalige aanmelding](./media/active-directory-saas-zscaler-tutorial/ic800209.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="564c1-181">![Single Sign-On](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="564c1-182">a.</span><span class="sxs-lookup"><span data-stu-id="564c1-182">a.</span></span> <span data-ttu-id="564c1-183">Plak de **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd vanuit de Azure-portal in de **URL van de SAML-Portal waarmee gebruikers worden verzonden voor verificatie** textbox.</span><span class="sxs-lookup"><span data-stu-id="564c1-183">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="564c1-184">b.</span><span class="sxs-lookup"><span data-stu-id="564c1-184">b.</span></span> <span data-ttu-id="564c1-185">In de **kenmerk met naam van de aanmelding** textbox type **NameID**.</span><span class="sxs-lookup"><span data-stu-id="564c1-185">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="564c1-186">c.</span><span class="sxs-lookup"><span data-stu-id="564c1-186">c.</span></span> <span data-ttu-id="564c1-187">Als u wilt uw gedownloade certificaat uploaden, klikt u op **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="564c1-187">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="564c1-188">d.</span><span class="sxs-lookup"><span data-stu-id="564c1-188">d.</span></span> <span data-ttu-id="564c1-189">Selecteer **SAML automatische inrichting inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="564c1-189">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="564c1-190">Op de **gebruikersverificatie configureren** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="564c1-190">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="564c1-191">![Beheer](./media/active-directory-saas-zscaler-tutorial/ic800210.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="564c1-191">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="564c1-192">a.</span><span class="sxs-lookup"><span data-stu-id="564c1-192">a.</span></span> <span data-ttu-id="564c1-193">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="564c1-193">Click **Save**.</span></span>

    <span data-ttu-id="564c1-194">b.</span><span class="sxs-lookup"><span data-stu-id="564c1-194">b.</span></span> <span data-ttu-id="564c1-195">Klik op **nu activeren**.</span><span class="sxs-lookup"><span data-stu-id="564c1-195">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="564c1-196">Proxy-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="564c1-196">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="564c1-197">De proxy-instellingen in Internet Explorer configureren</span><span class="sxs-lookup"><span data-stu-id="564c1-197">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="564c1-198">Start **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="564c1-198">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="564c1-199">Selecteer **Internetopties** van de **extra** menu voor open de **Internetopties** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="564c1-199">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="564c1-200">![Internetopties](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Internetopties")</span><span class="sxs-lookup"><span data-stu-id="564c1-200">![Internet Options](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="564c1-201">Klik op de **verbindingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="564c1-201">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="564c1-202">![Verbindingen](./media/active-directory-saas-zscaler-tutorial/ic769493.png "verbindingen")</span><span class="sxs-lookup"><span data-stu-id="564c1-202">![Connections](./media/active-directory-saas-zscaler-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="564c1-203">Klik op **LAN-instellingen** openen de **LAN-instellingen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="564c1-203">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="564c1-204">Voer de volgende stappen uit in de sectie Proxy-server:</span><span class="sxs-lookup"><span data-stu-id="564c1-204">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="564c1-205">![Proxyserver](./media/active-directory-saas-zscaler-tutorial/ic769494.png "proxyserver")</span><span class="sxs-lookup"><span data-stu-id="564c1-205">![Proxy server](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="564c1-206">a.</span><span class="sxs-lookup"><span data-stu-id="564c1-206">a.</span></span> <span data-ttu-id="564c1-207">Selecteer **een proxyserver gebruiken voor uw LAN**.</span><span class="sxs-lookup"><span data-stu-id="564c1-207">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="564c1-208">b.</span><span class="sxs-lookup"><span data-stu-id="564c1-208">b.</span></span> <span data-ttu-id="564c1-209">Typ in het tekstvak adres **gateway.zscaler.net**.</span><span class="sxs-lookup"><span data-stu-id="564c1-209">In the Address textbox, type **gateway.zscaler.net**.</span></span>

    <span data-ttu-id="564c1-210">c.</span><span class="sxs-lookup"><span data-stu-id="564c1-210">c.</span></span> <span data-ttu-id="564c1-211">Typ in het tekstvak poort **80**.</span><span class="sxs-lookup"><span data-stu-id="564c1-211">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="564c1-212">d.</span><span class="sxs-lookup"><span data-stu-id="564c1-212">d.</span></span> <span data-ttu-id="564c1-213">Selecteer **proxyserver niet gebruiken voor lokale adressen**.</span><span class="sxs-lookup"><span data-stu-id="564c1-213">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="564c1-214">e.</span><span class="sxs-lookup"><span data-stu-id="564c1-214">e.</span></span> <span data-ttu-id="564c1-215">Klik op **OK** sluiten de **Local Area Network (LAN)-instellingen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="564c1-215">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="564c1-216">Klik op **OK** sluiten de **Internetopties** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="564c1-216">Click **OK** to close the **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="564c1-217">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="564c1-217">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="564c1-218">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="564c1-218">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="564c1-219">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="564c1-219">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="564c1-220">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="564c1-220">Creating an Azure AD test user</span></span>
<span data-ttu-id="564c1-221">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="564c1-221">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="564c1-223">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="564c1-223">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="564c1-224">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="564c1-224">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="564c1-226">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="564c1-226">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="564c1-228">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="564c1-228">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="564c1-230">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="564c1-230">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="564c1-232">a.</span><span class="sxs-lookup"><span data-stu-id="564c1-232">a.</span></span> <span data-ttu-id="564c1-233">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="564c1-233">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="564c1-234">b.</span><span class="sxs-lookup"><span data-stu-id="564c1-234">b.</span></span> <span data-ttu-id="564c1-235">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="564c1-235">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="564c1-236">c.</span><span class="sxs-lookup"><span data-stu-id="564c1-236">c.</span></span> <span data-ttu-id="564c1-237">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="564c1-237">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="564c1-238">d.</span><span class="sxs-lookup"><span data-stu-id="564c1-238">d.</span></span> <span data-ttu-id="564c1-239">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="564c1-239">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-test-user"></a><span data-ttu-id="564c1-240">Een testgebruiker Zscaler maken</span><span class="sxs-lookup"><span data-stu-id="564c1-240">Creating a Zscaler test user</span></span>

<span data-ttu-id="564c1-241">Om Azure AD-gebruikers zich aanmelden bij ZScaler, moeten ze worden ingericht op ZScaler.</span><span class="sxs-lookup"><span data-stu-id="564c1-241">To enable Azure AD users to log in to ZScaler, they must be provisioned to ZScaler.</span></span>  
<span data-ttu-id="564c1-242">In het geval van ZScaler is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="564c1-242">In the case of ZScaler, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="564c1-243">Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="564c1-243">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="564c1-244">Meld u aan bij uw **Zscaler** tenant.</span><span class="sxs-lookup"><span data-stu-id="564c1-244">Log in to your **Zscaler** tenant.</span></span>

2. <span data-ttu-id="564c1-245">Klik op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="564c1-245">Click **Administration**.</span></span>   
   
    <span data-ttu-id="564c1-246">![Beheer](./media/active-directory-saas-zscaler-tutorial/ic781035.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="564c1-246">![Administration](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="564c1-247">Klik op **Gebruikersbeheer**.</span><span class="sxs-lookup"><span data-stu-id="564c1-247">Click **User Management**.</span></span>   
        
     <span data-ttu-id="564c1-248">![Voeg](./media/active-directory-saas-zscaler-tutorial/ic781036.png "toevoegen")</span><span class="sxs-lookup"><span data-stu-id="564c1-248">![Add](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="564c1-249">In de **gebruikers** tabblad **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="564c1-249">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="564c1-250">![Voeg](./media/active-directory-saas-zscaler-tutorial/ic781037.png "toevoegen")</span><span class="sxs-lookup"><span data-stu-id="564c1-250">![Add](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="564c1-251">Voer de volgende stappen uit in de sectie gebruiker toevoegen:</span><span class="sxs-lookup"><span data-stu-id="564c1-251">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="564c1-252">![Gebruiker toevoegen](./media/active-directory-saas-zscaler-tutorial/ic781038.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="564c1-252">![Add User](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="564c1-253">a.</span><span class="sxs-lookup"><span data-stu-id="564c1-253">a.</span></span> <span data-ttu-id="564c1-254">Typ de **UserID**, **weergavenaam gebruiker**, **wachtwoord**, **wachtwoord bevestigen**, en selecteer vervolgens **groepen**en de **afdeling** van een geldige AAD-account dat u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="564c1-254">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="564c1-255">b.</span><span class="sxs-lookup"><span data-stu-id="564c1-255">b.</span></span> <span data-ttu-id="564c1-256">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="564c1-256">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="564c1-257">U kunt andere ZScaler gebruiker account hulpmiddelen voor het maken of API's die is geleverd door ZScaler aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="564c1-257">You can use any other ZScaler user account creation tools or APIs provided by ZScaler to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="564c1-258">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="564c1-258">Assigning the Azure AD test user</span></span>

<span data-ttu-id="564c1-259">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Zscaler.</span><span class="sxs-lookup"><span data-stu-id="564c1-259">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="564c1-261">**Britta Simon om aan te wijzen Zscaler, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="564c1-261">**To assign Britta Simon to Zscaler, perform the following steps:**</span></span>

1. <span data-ttu-id="564c1-262">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="564c1-262">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="564c1-264">Selecteer in de lijst met toepassingen **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="564c1-264">In the applications list, select **Zscaler**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_app.png) 

3. <span data-ttu-id="564c1-266">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="564c1-266">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="564c1-268">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="564c1-268">Click **Add** button.</span></span> <span data-ttu-id="564c1-269">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="564c1-269">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="564c1-271">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="564c1-271">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="564c1-272">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="564c1-272">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="564c1-273">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="564c1-273">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="564c1-274">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="564c1-274">Testing single sign-on</span></span>

<span data-ttu-id="564c1-275">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="564c1-275">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="564c1-276">Als u op de tegel Zscaler in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Zscaler.</span><span class="sxs-lookup"><span data-stu-id="564c1-276">When you click the Zscaler tile in the Access Panel, you should get automatically signed-on to your Zscaler application.</span></span>
<span data-ttu-id="564c1-277">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="564c1-277">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="564c1-278">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="564c1-278">Additional resources</span></span>

* [<span data-ttu-id="564c1-279">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="564c1-279">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="564c1-280">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="564c1-280">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_203.png

