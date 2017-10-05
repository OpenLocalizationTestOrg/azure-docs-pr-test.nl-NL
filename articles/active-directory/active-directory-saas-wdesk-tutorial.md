---
title: 'Zelfstudie: Azure Active Directory-integratie met Wdesk | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Wdesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 37660b80cfb01d6a3105aea5ce248f1e03c46695
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a><span data-ttu-id="1e7f4-103">Zelfstudie: Azure Active Directory-integratie met Wdesk</span><span class="sxs-lookup"><span data-stu-id="1e7f4-103">Tutorial: Azure Active Directory integration with Wdesk</span></span>

<span data-ttu-id="1e7f4-104">In deze zelfstudie leert u hoe Wdesk integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1e7f4-104">In this tutorial, you learn how to integrate Wdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e7f4-105">Wdesk integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1e7f4-105">Integrating Wdesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1e7f4-106">U kunt beheren in Azure AD die toegang tot Wdesk heeft</span><span class="sxs-lookup"><span data-stu-id="1e7f4-106">You can control in Azure AD who has access to Wdesk</span></span>
- <span data-ttu-id="1e7f4-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Wdesk (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="1e7f4-107">You can enable your users to automatically get signed-on to Wdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1e7f4-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="1e7f4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1e7f4-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, zien.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="1e7f4-110">[Wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1e7f4-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e7f4-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1e7f4-111">Prerequisites</span></span>

<span data-ttu-id="1e7f4-112">Voor het configureren van Azure AD-integratie met Wdesk, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="1e7f4-112">To configure Azure AD integration with Wdesk, you need the following items:</span></span>

- <span data-ttu-id="1e7f4-113">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1e7f4-113">An Azure AD subscription</span></span>
- <span data-ttu-id="1e7f4-114">Een Wdesk eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="1e7f4-114">A Wdesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1e7f4-115">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1e7f4-116">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1e7f4-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e7f4-117">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1e7f4-118">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e7f4-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1e7f4-119">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1e7f4-119">Scenario description</span></span>
<span data-ttu-id="1e7f4-120">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1e7f4-121">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1e7f4-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e7f4-122">Wdesk uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1e7f4-122">Adding Wdesk from the gallery</span></span>
2. <span data-ttu-id="1e7f4-123">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1e7f4-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wdesk-from-the-gallery"></a><span data-ttu-id="1e7f4-124">Wdesk uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1e7f4-124">Adding Wdesk from the gallery</span></span>
<span data-ttu-id="1e7f4-125">Voor het configureren van de integratie van Wdesk in Azure AD, moet u Wdesk uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-125">To configure the integration of Wdesk into Azure AD, you need to add Wdesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1e7f4-126">**Als u wilt toevoegen Wdesk uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1e7f4-126">**To add Wdesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1e7f4-127">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1e7f4-129">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1e7f4-130">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-130">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="1e7f4-132">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="1e7f4-134">Typ in het zoekvak **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-134">In the search box, type **Wdesk**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. <span data-ttu-id="1e7f4-136">Selecteer in het deelvenster resultaten **Wdesk**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-136">In the results panel, select **Wdesk**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1e7f4-138">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1e7f4-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1e7f4-139">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Wdesk op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="1e7f4-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1e7f4-140">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Wdesk is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Wdesk is to a user in Azure AD.</span></span> <span data-ttu-id="1e7f4-141">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Wdesk tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-141">In other words, a link relationship between an Azure AD user and the related user in Wdesk needs to be established.</span></span>

<span data-ttu-id="1e7f4-142">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Wdesk.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wdesk.</span></span>

<span data-ttu-id="1e7f4-143">Om te configureren en testen van Azure AD eenmalige aanmelding met Wdesk, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="1e7f4-143">To configure and test Azure AD single sign-on with Wdesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1e7f4-144">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1e7f4-145">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1e7f4-146">**[Maken van een testgebruiker Wdesk](#creating-a-wdesk-test-user)**  - Wdesk die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - to have a counterpart of Britta Simon in Wdesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1e7f4-147">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1e7f4-148">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1e7f4-149">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1e7f4-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1e7f4-150">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Wdesk configureren.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wdesk application.</span></span>

<span data-ttu-id="1e7f4-151">**Voor het configureren van Azure AD eenmalige aanmelding met Wdesk, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1e7f4-151">**To configure Azure AD single sign-on with Wdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="1e7f4-152">In de Azure-portal op de **Wdesk** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-152">In the Azure portal, on the **Wdesk** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1e7f4-154">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. <span data-ttu-id="1e7f4-156">Op de **Wdesk domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP** geïnitieerd modus de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1e7f4-156">On the **Wdesk Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    <span data-ttu-id="1e7f4-158">a.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-158">a.</span></span> <span data-ttu-id="1e7f4-159">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1e7f4-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span></span>

    <span data-ttu-id="1e7f4-160">b.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-160">b.</span></span> <span data-ttu-id="1e7f4-161">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1e7f4-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span></span>

4. <span data-ttu-id="1e7f4-162">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="1e7f4-163">Als u wilt configureren van de toepassing in **SP** geïnitieerd modus, voer de volgende stap:</span><span class="sxs-lookup"><span data-stu-id="1e7f4-163">If you wish to configure the application in **SP** initiated mode, perform the following step:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    <span data-ttu-id="1e7f4-165">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1e7f4-165">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="1e7f4-166">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-166">These values are not real.</span></span> <span data-ttu-id="1e7f4-167">Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1e7f4-168">U krijgt deze waarden van de portal WDesk bij het configureren van de SSO.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-168">You get these values from WDesk portal when you configure the SSO.</span></span> 
  
5. <span data-ttu-id="1e7f4-169">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. <span data-ttu-id="1e7f4-171">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-171">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="1e7f4-173">In een ander browservenster, meld u aan bij Wdesk als een beveiligingsbeheerder.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-173">In a different web browser window, login to Wdesk as a Security Administrator.</span></span>

8. <span data-ttu-id="1e7f4-174">In de onderste links, klikt u op **Admin** en kies **accountbeheerder**:</span><span class="sxs-lookup"><span data-stu-id="1e7f4-174">In the bottom left, click **Admin** and choose **Account Admin**:</span></span>
 
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. <span data-ttu-id="1e7f4-176">Navigeer in Wdesk Admin, naar **beveiliging**, klikt u vervolgens **SAML** > **SAML instellingen**:</span><span class="sxs-lookup"><span data-stu-id="1e7f4-176">In Wdesk Admin, navigate to **Security**, then **SAML** > **SAML Settings**:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. <span data-ttu-id="1e7f4-178">Onder **algemene instellingen**, Controleer de **SAML eenmalige aanmelding inschakelen**:</span><span class="sxs-lookup"><span data-stu-id="1e7f4-178">Under **General Settings**, check the **Enable SAML Single Sign On**:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. <span data-ttu-id="1e7f4-180">Onder **Details van Service Provider**, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1e7f4-180">Under **Service Provider Details**, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      <span data-ttu-id="1e7f4-182">a.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-182">a.</span></span> <span data-ttu-id="1e7f4-183">Kopieer de **aanmeldings-URL** en plak deze in **aanmeldings-Url** textbox in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-183">Copy the **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="1e7f4-184">b.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-184">b.</span></span> <span data-ttu-id="1e7f4-185">Kopieer de **metagegevens-Url** en plak deze in **id** textbox in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-185">Copy the **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span></span>
       
      <span data-ttu-id="1e7f4-186">c.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-186">c.</span></span> <span data-ttu-id="1e7f4-187">Kopieer de **Consumer url** en plak deze in **antwoord-Url** textbox in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-187">Copy the **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="1e7f4-188">d.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-188">d.</span></span> <span data-ttu-id="1e7f4-189">Klik op **opslaan** in Azure portal de wijzigingen wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-189">Click **Save** on Azure portal to save the changes.</span></span>      

12. <span data-ttu-id="1e7f4-190">Klik op **IdP-instellingen configureren** openen **IdP-instellingen bewerken** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-190">Click **Configure IdP Settings** to open **Edit IdP Settings** dialog.</span></span> <span data-ttu-id="1e7f4-191">Klik op **bestand kiezen** vinden de **Metadata.xml** opgeslagen vanuit Azure-portal-bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-191">Click **Choose File** to locate the **Metadata.xml** file you saved from Azure portal, then upload it.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. <span data-ttu-id="1e7f4-193">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-193">Click **Save changes**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> <span data-ttu-id="1e7f4-195">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="1e7f4-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1e7f4-196">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1e7f4-197">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1e7f4-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1e7f4-198">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1e7f4-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="1e7f4-199">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="1e7f4-201">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1e7f4-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1e7f4-202">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1e7f4-204">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1e7f4-206">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1e7f4-208">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1e7f4-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1e7f4-210">a.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-210">a.</span></span> <span data-ttu-id="1e7f4-211">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1e7f4-212">b.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-212">b.</span></span> <span data-ttu-id="1e7f4-213">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1e7f4-214">c.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-214">c.</span></span> <span data-ttu-id="1e7f4-215">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1e7f4-216">d.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-216">d.</span></span> <span data-ttu-id="1e7f4-217">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-217">Click **Create**.</span></span>
 
### <a name="creating-a-wdesk-test-user"></a><span data-ttu-id="1e7f4-218">Een testgebruiker Wdesk maken</span><span class="sxs-lookup"><span data-stu-id="1e7f4-218">Creating a Wdesk test user</span></span>

<span data-ttu-id="1e7f4-219">Om Azure AD-gebruikers zich aanmelden bij Wdesk, moeten ze worden ingericht in Wdesk.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-219">To enable Azure AD users to log in to Wdesk, they must be provisioned into Wdesk.</span></span> <span data-ttu-id="1e7f4-220">In Wdesk is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-220">In Wdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="1e7f4-221">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1e7f4-221">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="1e7f4-222">Meld u aan als een beveiligingsbeheerder Wdesk bij.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-222">Log in to Wdesk as a Security Administrator.</span></span>
2. <span data-ttu-id="1e7f4-223">Navigeer naar **Admin** > **Admin-Account**.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-223">Navigate to **Admin** > **Account Admin**.</span></span>

     ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. <span data-ttu-id="1e7f4-225">Klik op **leden** onder **mensen**.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-225">Click **Members** under **People**.</span></span>

4. <span data-ttu-id="1e7f4-226">Klik nu op **lid toevoegen** openen **lid toevoegen** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-226">Now click **Add Member** to open **Add Member** dialog box.</span></span> 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. <span data-ttu-id="1e7f4-228">In **gebruiker** tekst en voer de gebruikersnaam van de gebruiker zoals  **brittasimon@contoso.com**  en klik op **doorgaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-228">In **User** text box, enter the username of user like **brittasimon@contoso.com** and click **Continue** button.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  <span data-ttu-id="1e7f4-230">Voer de gegevens, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="1e7f4-230">Enter the details as shown below:</span></span>
  
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    <span data-ttu-id="1e7f4-232">a.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-232">a.</span></span> <span data-ttu-id="1e7f4-233">In **e** tekst en voer het e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="1e7f4-233">In **E-mail** text box, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="1e7f4-234">b.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-234">b.</span></span> <span data-ttu-id="1e7f4-235">In **voornaam** tekst en voer de voornaam van de gebruiker zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-235">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="1e7f4-236">c.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-236">c.</span></span> <span data-ttu-id="1e7f4-237">In **achternaam** tekst en voer de achternaam van de gebruiker zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-237">In **Last Name** text box, enter the last name of user like **Simon**.</span></span>

7. <span data-ttu-id="1e7f4-238">Klik op **lid opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-238">Click **Save Member** button.</span></span>  

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1e7f4-240">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e7f4-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1e7f4-241">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Wdesk.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wdesk.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="1e7f4-243">**Britta Simon om aan te wijzen Wdesk, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1e7f4-243">**To assign Britta Simon to Wdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="1e7f4-244">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1e7f4-246">Selecteer in de lijst met toepassingen **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-246">In the applications list, select **Wdesk**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. <span data-ttu-id="1e7f4-248">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="1e7f4-250">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-250">Click **Add** button.</span></span> <span data-ttu-id="1e7f4-251">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="1e7f4-253">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1e7f4-254">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1e7f4-255">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1e7f4-256">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1e7f4-256">Testing single sign-on</span></span>

<span data-ttu-id="1e7f4-257">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-257">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1e7f4-258">Als u op de tegel Wdesk in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Wdesk.</span><span class="sxs-lookup"><span data-stu-id="1e7f4-258">When you click the Wdesk tile in the Access Panel, you should get automatically signed-on to your Wdesk application.</span></span>
<span data-ttu-id="1e7f4-259">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1e7f4-259">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1e7f4-260">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1e7f4-260">Additional resources</span></span>

* [<span data-ttu-id="1e7f4-261">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e7f4-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e7f4-262">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1e7f4-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

