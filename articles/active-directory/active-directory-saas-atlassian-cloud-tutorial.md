---
title: 'Zelfstudie: Azure Active Directory-integratie met Atlassian Cloud | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Atlassian Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 2891838b56dd15cb5f97dcae391770143a80c781
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="1f06f-103">Zelfstudie: Azure Active Directory-integratie met Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="1f06f-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="1f06f-104">In deze zelfstudie leert u hoe Atlassian Cloud integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1f06f-104">In this tutorial, you learn how to integrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1f06f-105">Atlassian Cloud integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1f06f-105">Integrating Atlassian Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1f06f-106">U kunt beheren in Azure AD die toegang tot Atlassian Cloud heeft</span><span class="sxs-lookup"><span data-stu-id="1f06f-106">You can control in Azure AD who has access to Atlassian Cloud</span></span>
- <span data-ttu-id="1f06f-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Atlassian Cloud (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="1f06f-107">You can enable your users to automatically get signed-on to Atlassian Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1f06f-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="1f06f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1f06f-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1f06f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f06f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1f06f-110">Prerequisites</span></span>

<span data-ttu-id="1f06f-111">Voor het configureren van Azure AD-integratie met Atlassian Cloud, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="1f06f-111">To configure Azure AD integration with Atlassian Cloud, you need the following items:</span></span>

- <span data-ttu-id="1f06f-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1f06f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1f06f-113">Een Atlassian Cloud eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="1f06f-113">An Atlassian Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1f06f-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1f06f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1f06f-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1f06f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1f06f-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1f06f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1f06f-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f06f-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1f06f-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1f06f-118">Scenario description</span></span>
<span data-ttu-id="1f06f-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1f06f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1f06f-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1f06f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1f06f-121">Atlassian Cloud uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1f06f-121">Adding Atlassian Cloud from the gallery</span></span>
2. <span data-ttu-id="1f06f-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1f06f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atlassian-cloud-from-the-gallery"></a><span data-ttu-id="1f06f-123">Atlassian Cloud uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1f06f-123">Adding Atlassian Cloud from the gallery</span></span>
<span data-ttu-id="1f06f-124">Voor het configureren van de integratie van Atlassian Cloud met Azure AD, moet u Atlassian Cloud uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1f06f-124">To configure the integration of Atlassian Cloud into Azure AD, you need to add Atlassian Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1f06f-125">**Als u wilt toevoegen Atlassian Cloud uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1f06f-125">**To add Atlassian Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1f06f-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1f06f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1f06f-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1f06f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1f06f-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1f06f-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="1f06f-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1f06f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="1f06f-133">Typ in het zoekvak **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="1f06f-133">In the search box, type **Atlassian Cloud**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. <span data-ttu-id="1f06f-135">Selecteer in het deelvenster resultaten **Atlassian Cloud**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1f06f-135">In the results panel, select **Atlassian Cloud**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1f06f-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1f06f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1f06f-138">In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met Atlassian Cloud op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="1f06f-138">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1f06f-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in de Atlassian Cloud is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f06f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Atlassian Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="1f06f-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de Atlassian Cloud tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="1f06f-140">In other words, a link relationship between an Azure AD user and the related user in Atlassian Cloud needs to be established.</span></span>

<span data-ttu-id="1f06f-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="1f06f-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Atlassian Cloud.</span></span>

<span data-ttu-id="1f06f-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Atlassian Cloud, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="1f06f-142">To configure and test Azure AD single sign-on with Atlassian Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1f06f-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1f06f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1f06f-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1f06f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1f06f-145">**[Maken van een testgebruiker Atlassian Cloud](#creating-an-atlassian-cloud-test-user)**  - Atlassian Cloud die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="1f06f-145">**[Creating an Atlassian Cloud test user](#creating-an-atlassian-cloud-test-user)** - to have a counterpart of Britta Simon in Atlassian Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1f06f-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1f06f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1f06f-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1f06f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1f06f-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1f06f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1f06f-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="1f06f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Atlassian Cloud application.</span></span>

<span data-ttu-id="1f06f-150">**Om eenmalige aanmelding Azure AD met Atlassian Cloud configureert, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1f06f-150">**To configure Azure AD single sign-on with Atlassian Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="1f06f-151">In de Azure-portal op de **Atlassian Cloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1f06f-151">In the Azure portal, on the **Atlassian Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1f06f-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1f06f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. <span data-ttu-id="1f06f-155">Op de **Atlassian Cloud-domein en de URL's** sectie, voert u de volgende stappen uit als u wilt configureren, de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="1f06f-155">On the **Atlassian Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    <span data-ttu-id="1f06f-157">a.</span><span class="sxs-lookup"><span data-stu-id="1f06f-157">a.</span></span> <span data-ttu-id="1f06f-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<instancename>.atlassian.net/admin/saml/edit`</span><span class="sxs-lookup"><span data-stu-id="1f06f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.atlassian.net/admin/saml/edit`</span></span>

    <span data-ttu-id="1f06f-159">b.</span><span class="sxs-lookup"><span data-stu-id="1f06f-159">b.</span></span> <span data-ttu-id="1f06f-160">In de **antwoord-URL** textbox, typ een URL als:`https://id.atlassian.com/login/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="1f06f-160">In the **Reply URL** textbox, type a URL as: `https://id.atlassian.com/login/saml/acs`</span></span>

4. <span data-ttu-id="1f06f-161">Controleer **weergeven geavanceerde instellingen voor URL** en voer de volgende stap als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="1f06f-161">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    <span data-ttu-id="1f06f-163">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<instancename>.atlassian.net`</span><span class="sxs-lookup"><span data-stu-id="1f06f-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.atlassian.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1f06f-164">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="1f06f-164">These values are not real.</span></span> <span data-ttu-id="1f06f-165">Deze waarden bijwerken met de werkelijke id en de aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="1f06f-165">Update these values with the actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="1f06f-166">De exacte waarden kunt u krijgen via Cloud SAML-configuratie van Atlassian scherm.</span><span class="sxs-lookup"><span data-stu-id="1f06f-166">You can get the exact values from Atlassian Cloud SAML Configuration screen.</span></span>
 
5. <span data-ttu-id="1f06f-167">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1f06f-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. <span data-ttu-id="1f06f-169">Op de **Atlassian Cloudconfiguratie** sectie, klikt u op **Atlassian Cloud configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="1f06f-169">On the **Atlassian Cloud Configuration** section, click **Configure Atlassian Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1f06f-170">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="1f06f-170">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. <span data-ttu-id="1f06f-172">Ophalen van eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, meld u aan bij de Atlassian-Portal met behulp van de administrator-rechten.</span><span class="sxs-lookup"><span data-stu-id="1f06f-172">To get SSO configured for your application, login to the Atlassian Portal using the administrator rights.</span></span>

8. <span data-ttu-id="1f06f-173">Klik in de sectie verificatie van de Linkernavigatie **domeinen**.</span><span class="sxs-lookup"><span data-stu-id="1f06f-173">In the Authentication section of the left navigation click **Domains**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    <span data-ttu-id="1f06f-175">a.</span><span class="sxs-lookup"><span data-stu-id="1f06f-175">a.</span></span> <span data-ttu-id="1f06f-176">Typ de naam van uw domein in het tekstvak en klik vervolgens op **domein toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1f06f-176">In the textbox, type your domain name, and then click **Add domain**.</span></span>
        
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    <span data-ttu-id="1f06f-178">b.</span><span class="sxs-lookup"><span data-stu-id="1f06f-178">b.</span></span> <span data-ttu-id="1f06f-179">Om te controleren of het domein, klikt u op **controleren**.</span><span class="sxs-lookup"><span data-stu-id="1f06f-179">To verify the domain, click **Verify**.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    <span data-ttu-id="1f06f-181">c.</span><span class="sxs-lookup"><span data-stu-id="1f06f-181">c.</span></span> <span data-ttu-id="1f06f-182">Het domein verificatie HTML-bestand downloaden, uploaden naar de hoofdmap van de website van uw domein en klik op **domein controleren**.</span><span class="sxs-lookup"><span data-stu-id="1f06f-182">Download the domain verification html file, upload it to the root folder of your domain's website, and then click **Verify domain**.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    <span data-ttu-id="1f06f-184">d.</span><span class="sxs-lookup"><span data-stu-id="1f06f-184">d.</span></span> <span data-ttu-id="1f06f-185">Zodra het domein is geverifieerd, de waarde van de **Status** veld is **geverifieerde**.</span><span class="sxs-lookup"><span data-stu-id="1f06f-185">Once the domain is verified, the value of the **Status** field is **Verified**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. <span data-ttu-id="1f06f-187">Klik in de linkernavigatiebalk op **SAML**.</span><span class="sxs-lookup"><span data-stu-id="1f06f-187">In the left navigation bar, click **SAML**.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. <span data-ttu-id="1f06f-189">Een SAML-configuratie maken en toevoegen van de configuratie van de id-provider.</span><span class="sxs-lookup"><span data-stu-id="1f06f-189">Create a SAML Configuration and add the Identity provider configuration.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    <span data-ttu-id="1f06f-191">a.</span><span class="sxs-lookup"><span data-stu-id="1f06f-191">a.</span></span> <span data-ttu-id="1f06f-192">In de **identiteitsprovider entiteit-ID** tekst vak, plak de waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1f06f-192">In the **Identity provider Entity ID** text box, paste the value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1f06f-193">b.</span><span class="sxs-lookup"><span data-stu-id="1f06f-193">b.</span></span> <span data-ttu-id="1f06f-194">In de **identiteitsprovider URL SSO** tekst vak, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1f06f-194">In the **Identity provider SSO URL** text box, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1f06f-195">c.</span><span class="sxs-lookup"><span data-stu-id="1f06f-195">c.</span></span> <span data-ttu-id="1f06f-196">Het gedownloade certificaat openen vanuit Azure-portal en kopieer de waarden zonder het Begin en einde regels en plak deze in de **openbare X509 certificaat** vak.</span><span class="sxs-lookup"><span data-stu-id="1f06f-196">Open the downloaded certificate from Azure portal and copy the values without the Begin and End lines and paste it in the **Public X509 certificate** box.</span></span>
    
    <span data-ttu-id="1f06f-197">d.</span><span class="sxs-lookup"><span data-stu-id="1f06f-197">d.</span></span> <span data-ttu-id="1f06f-198">Klik op **configuratie opslaan** de instellingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="1f06f-198">Click **Save Configuration**  to Save the settings.</span></span>
     
11. <span data-ttu-id="1f06f-199">Werk de instellingen van Azure AD om ervoor te zorgen dat u setup de juiste id-URL hebt.</span><span class="sxs-lookup"><span data-stu-id="1f06f-199">Update the Azure AD settings to make sure that you have setup the correct Identifier URL.</span></span>
  
    <span data-ttu-id="1f06f-200">a.</span><span class="sxs-lookup"><span data-stu-id="1f06f-200">a.</span></span> <span data-ttu-id="1f06f-201">Kopieer de **SP identiteit ID** van het SAML scherm en plak deze in Azure AD als de **id** waarde.</span><span class="sxs-lookup"><span data-stu-id="1f06f-201">Copy the **SP Identity ID** from the SAML screen and paste it in Azure AD as the **Identifier** value.</span></span>

    <span data-ttu-id="1f06f-202">b.</span><span class="sxs-lookup"><span data-stu-id="1f06f-202">b.</span></span> <span data-ttu-id="1f06f-203">Meld u op de URL is de tenant-URL van uw Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="1f06f-203">Sign On URL is the tenant URL of your Atlassian Cloud.</span></span>   

     ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. <span data-ttu-id="1f06f-205">Klik in de Azure-portal op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1f06f-205">In the Azure portal, Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="1f06f-207">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="1f06f-207">You can now read a concise version of these instructions inside the [Azure  portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1f06f-208">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="1f06f-208">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1f06f-209">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1f06f-209">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1f06f-210">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1f06f-210">Creating an Azure AD test user</span></span>
<span data-ttu-id="1f06f-211">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1f06f-211">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="1f06f-213">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1f06f-213">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1f06f-214">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1f06f-214">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1f06f-216">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1f06f-216">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1f06f-218">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1f06f-218">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1f06f-220">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1f06f-220">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1f06f-222">a.</span><span class="sxs-lookup"><span data-stu-id="1f06f-222">a.</span></span> <span data-ttu-id="1f06f-223">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1f06f-223">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1f06f-224">b.</span><span class="sxs-lookup"><span data-stu-id="1f06f-224">b.</span></span> <span data-ttu-id="1f06f-225">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1f06f-225">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1f06f-226">c.</span><span class="sxs-lookup"><span data-stu-id="1f06f-226">c.</span></span> <span data-ttu-id="1f06f-227">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1f06f-227">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1f06f-228">d.</span><span class="sxs-lookup"><span data-stu-id="1f06f-228">d.</span></span> <span data-ttu-id="1f06f-229">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1f06f-229">Click **Create**.</span></span>
 
### <a name="creating-an-atlassian-cloud-test-user"></a><span data-ttu-id="1f06f-230">Een testgebruiker Atlassian Cloud maken</span><span class="sxs-lookup"><span data-stu-id="1f06f-230">Creating an Atlassian Cloud test user</span></span>

<span data-ttu-id="1f06f-231">Om Azure AD-gebruikers zich aanmelden bij Atlassian Cloud, moeten ze worden ingericht in Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="1f06f-231">To enable Azure AD users to log in to Atlassian Cloud, they must be provisioned into Atlassian Cloud.</span></span>  
<span data-ttu-id="1f06f-232">In geval van een Atlassian Cloud is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="1f06f-232">In case of Atlassian Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="1f06f-233">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1f06f-233">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="1f06f-234">Klik in de beheersectie van de Site op het **gebruikers** knop</span><span class="sxs-lookup"><span data-stu-id="1f06f-234">In the Site administration section, click the **Users** button</span></span>

    ![Atlassian Cloud-gebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. <span data-ttu-id="1f06f-236">Klik op de **gebruiker maken** om te maken van een gebruiker in de Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="1f06f-236">Click the **Create User** button to create a user in the Atlassian Cloud</span></span>

    ![Atlassian Cloud-gebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. <span data-ttu-id="1f06f-238">Voer de gebruiker **e-mailadres**, **gebruikersnaam**, en **volledige naam** en de toegang tot de toepassing toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="1f06f-238">Enter the user's **Email address**, **Username**, and **Full Name** and assign the application access.</span></span> 

    ![Atlassian Cloud-gebruiker maken](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. <span data-ttu-id="1f06f-240">Klik op **gebruiker maken** klikt, wordt de uitnodiging e-mailbericht naar de gebruiker wordt verzonden en na de uitnodiging accepteren de gebruiker zich actief in het systeem.</span><span class="sxs-lookup"><span data-stu-id="1f06f-240">Click **Create user** button, it will send the email invitation to the user and after accepting the invitation the user will be active in the system.</span></span> 

>[!NOTE] 
><span data-ttu-id="1f06f-241">U kunt ook de gebruikers bulksgewijs maken door te klikken op de **bulksgewijs maken** knop in de sectie gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1f06f-241">You can also create the bulk users by clicking the **Bulk Create** button in the Users section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1f06f-242">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f06f-242">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1f06f-243">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="1f06f-243">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Atlassian Cloud.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="1f06f-245">**Britta Simon om aan te wijzen Atlassian Cloud, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1f06f-245">**To assign Britta Simon to Atlassian Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="1f06f-246">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1f06f-246">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1f06f-248">Selecteer in de lijst met toepassingen **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="1f06f-248">In the applications list, select **Atlassian Cloud**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. <span data-ttu-id="1f06f-250">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1f06f-250">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="1f06f-252">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1f06f-252">Click **Add** button.</span></span> <span data-ttu-id="1f06f-253">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1f06f-253">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="1f06f-255">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1f06f-255">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1f06f-256">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1f06f-256">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1f06f-257">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1f06f-257">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1f06f-258">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1f06f-258">Testing single sign-on</span></span>

<span data-ttu-id="1f06f-259">In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="1f06f-259">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="1f06f-260">Als u op de tegel Atlassian Cloud in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="1f06f-260">When you click the Atlassian Cloud tile in the Access Panel, you should get automatically signed-on to your Atlassian Cloud application.</span></span> <span data-ttu-id="1f06f-261">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1f06f-261">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1f06f-262">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1f06f-262">Additional resources</span></span>

* [<span data-ttu-id="1f06f-263">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f06f-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1f06f-264">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1f06f-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

