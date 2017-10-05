---
title: 'Zelfstudie: Azure Active Directory-integratie met Zscaler ZSCloud | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Zscaler ZSCloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 2b6eb113e5725260bc04f50e9218939bf28b1ff0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a><span data-ttu-id="13657-103">Zelfstudie: Azure Active Directory-integratie met Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="13657-103">Tutorial: Azure Active Directory integration with Zscaler ZSCloud</span></span>

<span data-ttu-id="13657-104">In deze zelfstudie leert u hoe Zscaler ZSCloud integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="13657-104">In this tutorial, you learn how to integrate Zscaler ZSCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="13657-105">Zscaler ZSCloud integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="13657-105">Integrating Zscaler ZSCloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="13657-106">U kunt beheren in Azure AD die toegang tot Zscaler ZSCloud heeft</span><span class="sxs-lookup"><span data-stu-id="13657-106">You can control in Azure AD who has access to Zscaler ZSCloud</span></span>
- <span data-ttu-id="13657-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Zscaler ZSCloud (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="13657-107">You can enable your users to automatically get signed-on to Zscaler ZSCloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="13657-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="13657-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="13657-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="13657-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13657-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="13657-110">Prerequisites</span></span>

<span data-ttu-id="13657-111">Voor het configureren van Azure AD-integratie met Zscaler ZSCloud, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="13657-111">To configure Azure AD integration with Zscaler ZSCloud, you need the following items:</span></span>

- <span data-ttu-id="13657-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="13657-112">An Azure AD subscription</span></span>
- <span data-ttu-id="13657-113">Een Zscaler ZSCloud eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="13657-113">A Zscaler ZSCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="13657-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="13657-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="13657-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="13657-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="13657-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="13657-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="13657-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="13657-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="13657-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="13657-118">Scenario description</span></span>
<span data-ttu-id="13657-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="13657-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="13657-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="13657-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="13657-121">Zscaler ZSCloud uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="13657-121">Adding Zscaler ZSCloud from the gallery</span></span>
2. <span data-ttu-id="13657-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="13657-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-zscloud-from-the-gallery"></a><span data-ttu-id="13657-123">Zscaler ZSCloud uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="13657-123">Adding Zscaler ZSCloud from the gallery</span></span>
<span data-ttu-id="13657-124">Voor het configureren van de integratie van Zscaler ZSCloud in Azure AD, moet u Zscaler ZSCloud uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="13657-124">To configure the integration of Zscaler ZSCloud into Azure AD, you need to add Zscaler ZSCloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="13657-125">**Als u wilt toevoegen Zscaler ZSCloud uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="13657-125">**To add Zscaler ZSCloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="13657-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="13657-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="13657-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="13657-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="13657-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="13657-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="13657-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="13657-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="13657-133">Typ in het zoekvak **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="13657-133">In the search box, type **Zscaler ZSCloud**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. <span data-ttu-id="13657-135">Selecteer in het deelvenster resultaten **Zscaler ZSCloud**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="13657-135">In the results panel, select **Zscaler ZSCloud**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="13657-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="13657-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="13657-138">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met Zscaler ZSCloud op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="13657-138">In this section, you configure and test Azure AD single sign-on with Zscaler ZSCloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="13657-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Zscaler ZSCloud is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13657-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler ZSCloud is to a user in Azure AD.</span></span> <span data-ttu-id="13657-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Zscaler ZSCloud tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="13657-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler ZSCloud needs to be established.</span></span>

<span data-ttu-id="13657-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="13657-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zscaler ZSCloud.</span></span>

<span data-ttu-id="13657-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Zscaler ZSCloud, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="13657-142">To configure and test Azure AD single sign-on with Zscaler ZSCloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="13657-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="13657-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="13657-144">**[Proxy-instellingen configureren](#configuring-proxy-settings)**  : als u wilt de proxy-instellingen in Internet Explorer configureren</span><span class="sxs-lookup"><span data-stu-id="13657-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
2. <span data-ttu-id="13657-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="13657-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)**  - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="13657-146">**[Maken van een testgebruiker Zscaler ZSCloud](#creating-a-zscaler-zscloud-test-user)**  - Zscaler ZSCloud die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="13657-146">**[Creating a Zscaler ZSCloud test user](#creating-a-zscaler-zscloud-test-user)** - to have a counterpart of Britta Simon in Zscaler ZSCloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="13657-147">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="13657-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="13657-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="13657-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="13657-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="13657-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="13657-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Zscaler ZSCloud configureren.</span><span class="sxs-lookup"><span data-stu-id="13657-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="13657-151">**Voor het configureren van Azure AD eenmalige aanmelding met Zscaler ZSCloud, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="13657-151">**To configure Azure AD single sign-on with Zscaler ZSCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="13657-152">In de Azure-portal op de **Zscaler ZSCloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="13657-152">In the Azure portal, on the **Zscaler ZSCloud** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="13657-154">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="13657-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. <span data-ttu-id="13657-156">Op de **Zscaler ZSCloud domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="13657-156">On the **Zscaler ZSCloud Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     <span data-ttu-id="13657-158">In de **aanmeldings-URL** textbox, typ de URL moet worden gebruikt door uw gebruikers aan te melden bij uw toepassing ZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="13657-158">In the **Sign-on URL** textbox, type the URL used by your users to sign-on to your ZScaler ZSCloud application.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="13657-159">U moet deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="13657-159">You have to update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="13657-160">Neem contact op met [Zscaler ZSCloud Client ondersteuningsteam](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="13657-160">Contact [Zscaler ZSCloud Client support team](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) to get this value.</span></span> 
 
4. <span data-ttu-id="13657-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="13657-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. <span data-ttu-id="13657-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="13657-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="13657-165">Op de **Zscaler ZSCloud configuratie** sectie, klikt u op **configureren Zscaler ZSCloud** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="13657-165">On the **Zscaler ZSCloud Configuration** section, click **Configure Zscaler ZSCloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="13657-166">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="13657-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. <span data-ttu-id="13657-168">In een ander browservenster, meld u aan bij uw bedrijf ZScaler ZSCloud site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="13657-168">In a different web browser window, log in to your ZScaler ZSCloud company site as an administrator.</span></span>

8. <span data-ttu-id="13657-169">Klik in het menu bovenaan op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="13657-169">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="13657-170">![Beheer](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="13657-170">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="13657-171">Onder **beheerders beheren en rollen**, klikt u op **gebruikers beheren & verificatie**.</span><span class="sxs-lookup"><span data-stu-id="13657-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="13657-172">![Gebruikers & verificatie beheren](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "gebruikers & verificatie beheren")</span><span class="sxs-lookup"><span data-stu-id="13657-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="13657-173">In de **verificatie-opties kiezen voor uw organisatie** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="13657-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="13657-174">![Verificatie](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "verificatie")</span><span class="sxs-lookup"><span data-stu-id="13657-174">![Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="13657-175">a.</span><span class="sxs-lookup"><span data-stu-id="13657-175">a.</span></span> <span data-ttu-id="13657-176">Selecteer **verificatie met eenmalige aanmelding SAML**.</span><span class="sxs-lookup"><span data-stu-id="13657-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="13657-177">b.</span><span class="sxs-lookup"><span data-stu-id="13657-177">b.</span></span> <span data-ttu-id="13657-178">Klik op **één SAML aanmelding Parameters configureren**.</span><span class="sxs-lookup"><span data-stu-id="13657-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="13657-179">Op de **configureren SAML Single Sign-On Parameters** dialoogvenster pagina de volgende stappen uit en klik vervolgens op **gedaan**</span><span class="sxs-lookup"><span data-stu-id="13657-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="13657-180">![Eenmalige aanmelding](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "eenmalige aanmelding")</span><span class="sxs-lookup"><span data-stu-id="13657-180">![Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="13657-181">a.</span><span class="sxs-lookup"><span data-stu-id="13657-181">a.</span></span> <span data-ttu-id="13657-182">Plak de **SAML Single Sign-On Service-URL** waarde in de **URL van de SAML-Portal waarmee gebruikers worden verzonden voor verificatie** textbox.</span><span class="sxs-lookup"><span data-stu-id="13657-182">Paste the **SAML Single Sign-On Service URL** value into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="13657-183">b.</span><span class="sxs-lookup"><span data-stu-id="13657-183">b.</span></span> <span data-ttu-id="13657-184">In de **kenmerk met naam van de aanmelding** textbox type **NameID**.</span><span class="sxs-lookup"><span data-stu-id="13657-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="13657-185">c.</span><span class="sxs-lookup"><span data-stu-id="13657-185">c.</span></span> <span data-ttu-id="13657-186">Als u wilt uw gedownloade certificaat uploaden, klikt u op **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="13657-186">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="13657-187">d.</span><span class="sxs-lookup"><span data-stu-id="13657-187">d.</span></span> <span data-ttu-id="13657-188">Selecteer **SAML automatische inrichting inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="13657-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="13657-189">Op de **gebruikersverificatie configureren** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="13657-189">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="13657-190">![Beheer](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="13657-190">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="13657-191">a.</span><span class="sxs-lookup"><span data-stu-id="13657-191">a.</span></span> <span data-ttu-id="13657-192">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="13657-192">Click **Save**.</span></span>

    <span data-ttu-id="13657-193">b.</span><span class="sxs-lookup"><span data-stu-id="13657-193">b.</span></span> <span data-ttu-id="13657-194">Klik op **nu activeren**.</span><span class="sxs-lookup"><span data-stu-id="13657-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="13657-195">Proxy-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="13657-195">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="13657-196">De proxy-instellingen in Internet Explorer configureren</span><span class="sxs-lookup"><span data-stu-id="13657-196">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="13657-197">Start **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="13657-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="13657-198">Selecteer **Internetopties** van de **extra** menu voor open de **Internetopties** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="13657-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="13657-199">![Internetopties](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internetopties")</span><span class="sxs-lookup"><span data-stu-id="13657-199">![Internet Options](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="13657-200">Klik op de **verbindingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="13657-200">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="13657-201">![Verbindingen](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "verbindingen")</span><span class="sxs-lookup"><span data-stu-id="13657-201">![Connections](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="13657-202">Klik op **LAN-instellingen** openen de **LAN-instellingen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="13657-202">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="13657-203">Voer de volgende stappen uit in de sectie Proxy-server:</span><span class="sxs-lookup"><span data-stu-id="13657-203">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="13657-204">![Proxyserver](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "proxyserver")</span><span class="sxs-lookup"><span data-stu-id="13657-204">![Proxy server](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="13657-205">a.</span><span class="sxs-lookup"><span data-stu-id="13657-205">a.</span></span> <span data-ttu-id="13657-206">Selecteer **een proxyserver gebruiken voor uw LAN**.</span><span class="sxs-lookup"><span data-stu-id="13657-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="13657-207">b.</span><span class="sxs-lookup"><span data-stu-id="13657-207">b.</span></span> <span data-ttu-id="13657-208">Typ in het tekstvak adres **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="13657-208">In the Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="13657-209">c.</span><span class="sxs-lookup"><span data-stu-id="13657-209">c.</span></span> <span data-ttu-id="13657-210">Typ in het tekstvak poort **80**.</span><span class="sxs-lookup"><span data-stu-id="13657-210">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="13657-211">d.</span><span class="sxs-lookup"><span data-stu-id="13657-211">d.</span></span> <span data-ttu-id="13657-212">Selecteer **proxyserver niet gebruiken voor lokale adressen**.</span><span class="sxs-lookup"><span data-stu-id="13657-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="13657-213">e.</span><span class="sxs-lookup"><span data-stu-id="13657-213">e.</span></span> <span data-ttu-id="13657-214">Klik op **OK** sluiten de **Local Area Network (LAN)-instellingen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="13657-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="13657-215">Klik op **OK** sluiten de **Internetopties** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="13657-215">Click **OK** to close the **Internet Options** dialog.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="13657-216">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="13657-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="13657-217">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="13657-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="13657-219">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="13657-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="13657-220">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="13657-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="13657-222">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="13657-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="13657-224">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="13657-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="13657-226">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="13657-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="13657-228">a.</span><span class="sxs-lookup"><span data-stu-id="13657-228">a.</span></span> <span data-ttu-id="13657-229">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="13657-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="13657-230">b.</span><span class="sxs-lookup"><span data-stu-id="13657-230">b.</span></span> <span data-ttu-id="13657-231">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="13657-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="13657-232">c.</span><span class="sxs-lookup"><span data-stu-id="13657-232">c.</span></span> <span data-ttu-id="13657-233">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="13657-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="13657-234">d.</span><span class="sxs-lookup"><span data-stu-id="13657-234">d.</span></span> <span data-ttu-id="13657-235">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="13657-235">Click **Create**.</span></span>

### <a name="creating-a-zscaler-zscloud-test-user"></a><span data-ttu-id="13657-236">Een testgebruiker Zscaler ZSCloud maken</span><span class="sxs-lookup"><span data-stu-id="13657-236">Creating a Zscaler ZSCloud test user</span></span>

<span data-ttu-id="13657-237">Om Azure AD-gebruikers zich aanmelden bij ZScaler ZSCloud, moeten ze worden ingericht op ZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="13657-237">To enable Azure AD users to log in to ZScaler ZSCloud, they must be provisioned to ZScaler ZSCloud.</span></span>  
<span data-ttu-id="13657-238">In het geval van ZScaler ZSCloud is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="13657-238">In the case of ZScaler ZSCloud, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="13657-239">Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="13657-239">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="13657-240">Meld u aan bij uw **Zscaler** tenant.</span><span class="sxs-lookup"><span data-stu-id="13657-240">Log in to your **Zscaler** tenant.</span></span>

2. <span data-ttu-id="13657-241">Klik op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="13657-241">Click **Administration**.</span></span>   
   
    <span data-ttu-id="13657-242">![Beheer](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="13657-242">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="13657-243">Klik op **Gebruikersbeheer**.</span><span class="sxs-lookup"><span data-stu-id="13657-243">Click **User Management**.</span></span>   
        
     <span data-ttu-id="13657-244">![Voeg](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "toevoegen")</span><span class="sxs-lookup"><span data-stu-id="13657-244">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

4. <span data-ttu-id="13657-245">In de **gebruikers** tabblad **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="13657-245">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="13657-246">![Voeg](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "toevoegen")</span><span class="sxs-lookup"><span data-stu-id="13657-246">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="13657-247">Voer de volgende stappen uit in de sectie gebruiker toevoegen:</span><span class="sxs-lookup"><span data-stu-id="13657-247">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="13657-248">![Gebruiker toevoegen](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "gebruiker toevoegen")</span><span class="sxs-lookup"><span data-stu-id="13657-248">![Add User](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="13657-249">a.</span><span class="sxs-lookup"><span data-stu-id="13657-249">a.</span></span> <span data-ttu-id="13657-250">Typ de **UserID**, **weergavenaam gebruiker**, **wachtwoord**, **wachtwoord bevestigen**, en selecteer vervolgens **groepen**en de **afdeling** van een geldige AAD-account dat u inrichten wilt.</span><span class="sxs-lookup"><span data-stu-id="13657-250">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="13657-251">b.</span><span class="sxs-lookup"><span data-stu-id="13657-251">b.</span></span> <span data-ttu-id="13657-252">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="13657-252">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="13657-253">U kunt andere ZScaler ZSCloud gebruiker account hulpmiddelen voor het maken of API's die is geleverd door ZScaler ZSCloud aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="13657-253">You can use any other ZScaler ZSCloud user account creation tools or APIs provided by ZScaler ZSCloud to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="13657-254">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="13657-254">Assigning the Azure AD test user</span></span>

<span data-ttu-id="13657-255">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="13657-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler ZSCloud.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="13657-257">**Britta Simon om aan te wijzen Zscaler ZSCloud, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="13657-257">**To assign Britta Simon to Zscaler ZSCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="13657-258">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="13657-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="13657-260">Selecteer in de lijst met toepassingen **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="13657-260">In the applications list, select **Zscaler ZSCloud**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. <span data-ttu-id="13657-262">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="13657-262">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="13657-264">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="13657-264">Click **Add** button.</span></span> <span data-ttu-id="13657-265">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="13657-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="13657-267">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="13657-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="13657-268">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="13657-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="13657-269">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="13657-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="13657-270">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="13657-270">Testing single sign-on</span></span>

<span data-ttu-id="13657-271">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="13657-271">If you want to test your single sign-on settings, open the Access Panel.</span></span>

<span data-ttu-id="13657-272">Als u op de tegel Zscaler ZSCloud in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="13657-272">When you click the Zscaler ZSCloud tile in the Access Panel, you should get automatically signed-on to your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="13657-273">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="13657-273">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="13657-274">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="13657-274">Additional resources</span></span>

* [<span data-ttu-id="13657-275">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="13657-275">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="13657-276">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="13657-276">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

