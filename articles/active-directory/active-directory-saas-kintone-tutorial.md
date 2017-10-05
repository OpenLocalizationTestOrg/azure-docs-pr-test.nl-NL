---
title: 'Zelfstudie: Azure Active Directory-integratie met Kintone | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Kintone.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: e5e847c12cba3611ce7ea2c3e956dbd55b1e0cac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="9152d-103">Zelfstudie: Azure Active Directory-integratie met Kintone</span><span class="sxs-lookup"><span data-stu-id="9152d-103">Tutorial: Azure Active Directory integration with Kintone</span></span>

<span data-ttu-id="9152d-104">In deze zelfstudie leert u hoe Kintone integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9152d-104">In this tutorial, you learn how to integrate Kintone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9152d-105">Kintone integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="9152d-105">Integrating Kintone with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9152d-106">U kunt beheren in Azure AD die toegang tot Kintone heeft</span><span class="sxs-lookup"><span data-stu-id="9152d-106">You can control in Azure AD who has access to Kintone</span></span>
- <span data-ttu-id="9152d-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Kintone (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="9152d-107">You can enable your users to automatically get signed-on to Kintone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9152d-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="9152d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9152d-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9152d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9152d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9152d-110">Prerequisites</span></span>

<span data-ttu-id="9152d-111">Voor het configureren van Azure AD-integratie met Kintone, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="9152d-111">To configure Azure AD integration with Kintone, you need the following items:</span></span>

- <span data-ttu-id="9152d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="9152d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9152d-113">Een Kintone eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="9152d-113">A Kintone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9152d-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="9152d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9152d-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="9152d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9152d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="9152d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9152d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9152d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9152d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="9152d-118">Scenario description</span></span>
<span data-ttu-id="9152d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="9152d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9152d-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="9152d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9152d-121">Kintone uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9152d-121">Adding Kintone from the gallery</span></span>
2. <span data-ttu-id="9152d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9152d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kintone-from-the-gallery"></a><span data-ttu-id="9152d-123">Kintone uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9152d-123">Adding Kintone from the gallery</span></span>
<span data-ttu-id="9152d-124">Voor het configureren van de integratie van Kintone in Azure AD, moet u Kintone uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="9152d-124">To configure the integration of Kintone into Azure AD, you need to add Kintone from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9152d-125">**Als u wilt toevoegen Kintone uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9152d-125">**To add Kintone from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9152d-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9152d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9152d-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9152d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9152d-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9152d-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="9152d-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9152d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="9152d-133">Typ in het zoekvak **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="9152d-133">In the search box, type **Kintone**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. <span data-ttu-id="9152d-135">Selecteer in het deelvenster resultaten **Kintone**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9152d-135">In the results panel, select **Kintone**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9152d-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9152d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9152d-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Kintone op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="9152d-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9152d-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Kintone is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9152d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kintone is to a user in Azure AD.</span></span> <span data-ttu-id="9152d-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Kintone tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="9152d-140">In other words, a link relationship between an Azure AD user and the related user in Kintone needs to be established.</span></span>

<span data-ttu-id="9152d-141">Wijs in Kintone, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="9152d-141">In Kintone, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9152d-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Kintone, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="9152d-142">To configure and test Azure AD single sign-on with Kintone, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9152d-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9152d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9152d-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9152d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9152d-145">**[Maken van een testgebruiker Kintone](#creating-a-kintone-test-user)**  - Kintone die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="9152d-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - to have a counterpart of Britta Simon in Kintone that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9152d-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9152d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9152d-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="9152d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9152d-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="9152d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9152d-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Kintone configureren.</span><span class="sxs-lookup"><span data-stu-id="9152d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kintone application.</span></span>

<span data-ttu-id="9152d-150">**Voor het configureren van Azure AD eenmalige aanmelding met Kintone, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9152d-150">**To configure Azure AD single sign-on with Kintone, perform the following steps:**</span></span>

1. <span data-ttu-id="9152d-151">In de Azure-portal op de **Kintone** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="9152d-151">In the Azure portal, on the **Kintone** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="9152d-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9152d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. <span data-ttu-id="9152d-155">Op de **Kintone domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9152d-155">On the **Kintone Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    <span data-ttu-id="9152d-157">a.</span><span class="sxs-lookup"><span data-stu-id="9152d-157">a.</span></span> <span data-ttu-id="9152d-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.kintone.com`</span><span class="sxs-lookup"><span data-stu-id="9152d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.kintone.com`</span></span>

    <span data-ttu-id="9152d-159">b.</span><span class="sxs-lookup"><span data-stu-id="9152d-159">b.</span></span> <span data-ttu-id="9152d-160">In de **id** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="9152d-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > <span data-ttu-id="9152d-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="9152d-161">These values are not real.</span></span> <span data-ttu-id="9152d-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="9152d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9152d-163">Neem contact op met [Kintone Client ondersteuningsteam](https://www.kintone.com/contact/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="9152d-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="9152d-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9152d-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. <span data-ttu-id="9152d-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="9152d-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9152d-168">Op de **Kintone configuratie** sectie, klikt u op **configureren Kintone** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="9152d-168">On the **Kintone Configuration** section, click **Configure Kintone** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9152d-169">Kopieer de **Sign-Out URL's, en SAML Single Sign-On Service** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="9152d-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. <span data-ttu-id="9152d-171">In een ander browservenster, meld u aan bij uw **Kintone** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="9152d-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

8. <span data-ttu-id="9152d-172">Klik op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="9152d-172">Click **Settings**.</span></span>
   
    <span data-ttu-id="9152d-173">![Instellingen](./media/active-directory-saas-kintone-tutorial/ic785879.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="9152d-173">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

9. <span data-ttu-id="9152d-174">Klik op **gebruikers & Systeembeheer**.</span><span class="sxs-lookup"><span data-stu-id="9152d-174">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="9152d-175">![Gebruikers & Systeembeheer](./media/active-directory-saas-kintone-tutorial/ic785880.png "gebruikers & Systeembeheer")</span><span class="sxs-lookup"><span data-stu-id="9152d-175">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration")</span></span>

10. <span data-ttu-id="9152d-176">Onder **Systeembeheer \> beveiliging** klikt u op **aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="9152d-176">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="9152d-177">![Aanmelding](./media/active-directory-saas-kintone-tutorial/ic785881.png "aanmelding")</span><span class="sxs-lookup"><span data-stu-id="9152d-177">![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login")</span></span>

11. <span data-ttu-id="9152d-178">Klik op **inschakelen SAML-verificatie**.</span><span class="sxs-lookup"><span data-stu-id="9152d-178">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="9152d-179">![SAML-verificatie](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML-verificatie")</span><span class="sxs-lookup"><span data-stu-id="9152d-179">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML Authentication")</span></span>

12. <span data-ttu-id="9152d-180">Voer de volgende stappen uit in de sectie SAML-verificatie:</span><span class="sxs-lookup"><span data-stu-id="9152d-180">In the SAML Authentication section, perform the following steps:</span></span>
    
    <span data-ttu-id="9152d-181">![SAML-verificatie](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML-verificatie")</span><span class="sxs-lookup"><span data-stu-id="9152d-181">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML Authentication")</span></span>
    
    <span data-ttu-id="9152d-182">a.</span><span class="sxs-lookup"><span data-stu-id="9152d-182">a.</span></span> <span data-ttu-id="9152d-183">In de **aanmeldings-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9152d-183">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="9152d-184">b.</span><span class="sxs-lookup"><span data-stu-id="9152d-184">b.</span></span> <span data-ttu-id="9152d-185">In de **afmelding URL** textbox, plak de waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9152d-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="9152d-186">c.</span><span class="sxs-lookup"><span data-stu-id="9152d-186">c.</span></span> <span data-ttu-id="9152d-187">Klik op **Bladeren** om uw gedownloade certificaat te uploaden.</span><span class="sxs-lookup"><span data-stu-id="9152d-187">Click **Browse** to upload your downloaded certificate.</span></span>
    
    <span data-ttu-id="9152d-188">d.</span><span class="sxs-lookup"><span data-stu-id="9152d-188">d.</span></span> <span data-ttu-id="9152d-189">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9152d-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="9152d-190">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="9152d-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9152d-191">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="9152d-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9152d-192">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9152d-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9152d-193">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="9152d-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="9152d-194">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9152d-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="9152d-196">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9152d-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9152d-197">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="9152d-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9152d-199">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="9152d-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9152d-201">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9152d-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9152d-203">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9152d-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9152d-205">a.</span><span class="sxs-lookup"><span data-stu-id="9152d-205">a.</span></span> <span data-ttu-id="9152d-206">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9152d-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9152d-207">b.</span><span class="sxs-lookup"><span data-stu-id="9152d-207">b.</span></span> <span data-ttu-id="9152d-208">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9152d-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9152d-209">c.</span><span class="sxs-lookup"><span data-stu-id="9152d-209">c.</span></span> <span data-ttu-id="9152d-210">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="9152d-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9152d-211">d.</span><span class="sxs-lookup"><span data-stu-id="9152d-211">d.</span></span> <span data-ttu-id="9152d-212">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="9152d-212">Click **Create**.</span></span>
 
### <a name="creating-a-kintone-test-user"></a><span data-ttu-id="9152d-213">Een testgebruiker Kintone maken</span><span class="sxs-lookup"><span data-stu-id="9152d-213">Creating a Kintone test user</span></span>

<span data-ttu-id="9152d-214">Om Azure AD-gebruikers zich aanmelden bij Kintone, moeten ze worden ingericht in Kintone.</span><span class="sxs-lookup"><span data-stu-id="9152d-214">To enable Azure AD users to log in to Kintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="9152d-215">In het geval van Kintone is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="9152d-215">In the case of Kintone, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="9152d-216">Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9152d-216">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="9152d-217">Meld u aan bij uw **Kintone** bedrijf site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="9152d-217">Log in to your **Kintone** company site as an administrator.</span></span>

2. <span data-ttu-id="9152d-218">Klik op **instelling**.</span><span class="sxs-lookup"><span data-stu-id="9152d-218">Click **Setting**.</span></span>
   
    <span data-ttu-id="9152d-219">![Instellingen](./media/active-directory-saas-kintone-tutorial/ic785879.png "instellingen")</span><span class="sxs-lookup"><span data-stu-id="9152d-219">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

3. <span data-ttu-id="9152d-220">Klik op **gebruikers & Systeembeheer**.</span><span class="sxs-lookup"><span data-stu-id="9152d-220">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="9152d-221">![Gebruikers & Systeembeheer](./media/active-directory-saas-kintone-tutorial/ic785880.png "gebruiker & Systeembeheer")</span><span class="sxs-lookup"><span data-stu-id="9152d-221">![User & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "User & System Administration")</span></span>

4. <span data-ttu-id="9152d-222">Onder **Gebruikersbeheer**, klikt u op **afdelingen gebr & uikers**.</span><span class="sxs-lookup"><span data-stu-id="9152d-222">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="9152d-223">![Afdeling gebr & uikers](./media/active-directory-saas-kintone-tutorial/ic785888.png "afdeling gebr & uikers")</span><span class="sxs-lookup"><span data-stu-id="9152d-223">![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users")</span></span>

5. <span data-ttu-id="9152d-224">Klik op **nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="9152d-224">Click **New User**.</span></span>
   
    <span data-ttu-id="9152d-225">![Nieuwe gebruikers](./media/active-directory-saas-kintone-tutorial/ic785889.png "nieuwe gebruikers")</span><span class="sxs-lookup"><span data-stu-id="9152d-225">![New Users](./media/active-directory-saas-kintone-tutorial/ic785889.png "New Users")</span></span>

6. <span data-ttu-id="9152d-226">In de **nieuwe gebruiker** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9152d-226">In the **New User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="9152d-227">![Nieuwe gebruikers](./media/active-directory-saas-kintone-tutorial/ic785890.png "nieuwe gebruikers")</span><span class="sxs-lookup"><span data-stu-id="9152d-227">![New Users](./media/active-directory-saas-kintone-tutorial/ic785890.png "New Users")</span></span>
   
    <span data-ttu-id="9152d-228">a.</span><span class="sxs-lookup"><span data-stu-id="9152d-228">a.</span></span> <span data-ttu-id="9152d-229">Typ een **weergavenaam**, **aanmeldingsnaam**, **nieuw wachtwoord**, **wachtwoord bevestigen**, **e-mailadres**, en andere details van een geldige AAD-account dat u inrichten in de bijbehorende tekstvakken wilt.</span><span class="sxs-lookup"><span data-stu-id="9152d-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want to provision into the related textboxes.</span></span>
 
    <span data-ttu-id="9152d-230">b.</span><span class="sxs-lookup"><span data-stu-id="9152d-230">b.</span></span> <span data-ttu-id="9152d-231">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9152d-231">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="9152d-232">U kunt andere Kintone gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Kintone aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="9152d-232">You can use any other Kintone user account creation tools or APIs provided by Kintone to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9152d-233">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="9152d-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9152d-234">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Kintone.</span><span class="sxs-lookup"><span data-stu-id="9152d-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kintone.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="9152d-236">**Britta Simon om aan te wijzen Kintone, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="9152d-236">**To assign Britta Simon to Kintone, perform the following steps:**</span></span>

1. <span data-ttu-id="9152d-237">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9152d-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="9152d-239">Selecteer in de lijst met toepassingen **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="9152d-239">In the applications list, select **Kintone**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. <span data-ttu-id="9152d-241">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="9152d-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="9152d-243">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="9152d-243">Click **Add** button.</span></span> <span data-ttu-id="9152d-244">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9152d-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="9152d-246">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="9152d-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9152d-247">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9152d-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9152d-248">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9152d-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9152d-249">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="9152d-249">Testing single sign-on</span></span>

<span data-ttu-id="9152d-250">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="9152d-250">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9152d-251">Als u op de tegel Kintone in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Kintone.</span><span class="sxs-lookup"><span data-stu-id="9152d-251">When you click the Kintone tile in the Access Panel, you should get automatically signed-on to your Kintone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9152d-252">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="9152d-252">Additional resources</span></span>

* [<span data-ttu-id="9152d-253">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9152d-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9152d-254">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9152d-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

