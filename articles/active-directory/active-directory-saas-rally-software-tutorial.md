---
title: 'Zelfstudie: Azure Active Directory-integratie met Rally Software | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Rally Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: 6481c9ef0ca71419ccfa6f7956f4702985743df3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="4b1a8-103">Zelfstudie: Azure Active Directory-integratie met Rally Software</span><span class="sxs-lookup"><span data-stu-id="4b1a8-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="4b1a8-104">In deze zelfstudie leert u hoe Software Rally integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4b1a8-104">In this tutorial, you learn how to integrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b1a8-105">Software Rally integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="4b1a8-105">Integrating Rally Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4b1a8-106">U kunt beheren in Azure AD die toegang tot Rally Software heeft.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-106">You can control in Azure AD who has access to Rally Software.</span></span>
- <span data-ttu-id="4b1a8-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Rally Software (Single Sign-On) inschakelen met hun Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-107">You can enable your users to automatically get signed-on to Rally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4b1a8-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="4b1a8-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4b1a8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b1a8-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4b1a8-110">Prerequisites</span></span>

<span data-ttu-id="4b1a8-111">Voor het configureren van Azure AD-integratie met Rally Software, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="4b1a8-111">To configure Azure AD integration with Rally Software, you need the following items:</span></span>

- <span data-ttu-id="4b1a8-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="4b1a8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b1a8-113">Een Software Rally eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="4b1a8-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b1a8-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b1a8-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="4b1a8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b1a8-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b1a8-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b1a8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b1a8-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="4b1a8-118">Scenario description</span></span>
<span data-ttu-id="4b1a8-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b1a8-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="4b1a8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b1a8-121">Rally Software uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="4b1a8-121">Adding Rally Software from the gallery</span></span>
2. <span data-ttu-id="4b1a8-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4b1a8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-the-gallery"></a><span data-ttu-id="4b1a8-123">Rally Software uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="4b1a8-123">Adding Rally Software from the gallery</span></span>
<span data-ttu-id="4b1a8-124">Voor het configureren van de integratie van Software Rally in Azure AD, moet u Rally Software uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-124">To configure the integration of Rally Software into Azure AD, you need to add Rally Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4b1a8-125">**Als u wilt toevoegen Rally Software uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="4b1a8-125">**To add Rally Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4b1a8-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="4b1a8-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4b1a8-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-129">Then go to **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="4b1a8-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="4b1a8-133">Typ in het zoekvak **Rally Software**, selecteer **Rally Software** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-133">In the search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button to add the application.</span></span>

    ![Rally Software in de lijst met resultaten](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4b1a8-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b1a8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4b1a8-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Rally Software op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4b1a8-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Software Rally is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Rally Software is to a user in Azure AD.</span></span> <span data-ttu-id="4b1a8-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Software Rally tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-138">In other words, a link relationship between an Azure AD user and the related user in Rally Software needs to be established.</span></span>

<span data-ttu-id="4b1a8-139">Wijs in Rally Software, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-139">In Rally Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4b1a8-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Rally Software, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="4b1a8-140">To configure and test Azure AD single sign-on with Rally Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4b1a8-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4b1a8-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b1a8-143">**[Maak een testgebruiker Rally Software](#create-a-rally-software-test-user)**  - Rally Software die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - to have a counterpart of Britta Simon in Rally Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4b1a8-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b1a8-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4b1a8-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="4b1a8-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4b1a8-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Rally configureren.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="4b1a8-148">**Voor het configureren van Azure AD eenmalige aanmelding met Rally Software, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="4b1a8-148">**To configure Azure AD single sign-on with Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="4b1a8-149">In de Azure-portal op de **Rally Software** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-149">In the Azure portal, on the **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. <span data-ttu-id="4b1a8-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. <span data-ttu-id="4b1a8-153">Op de **Rally Software domein en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="4b1a8-153">On the **Rally Software Domain and URLs** section, perform the following steps:</span></span>

    ![Software-domein en de URL's eenmalige aanmelding informatie Rally](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="4b1a8-155">a.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-155">a.</span></span> <span data-ttu-id="4b1a8-156">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="4b1a8-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="4b1a8-157">b.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-157">b.</span></span> <span data-ttu-id="4b1a8-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="4b1a8-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4b1a8-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-159">These values are not real.</span></span> <span data-ttu-id="4b1a8-160">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4b1a8-161">Neem contact op met [Rally Software Client ondersteuningsteam](https://help.rallydev.com/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-161">Contact [Rally Software Client support team](https://help.rallydev.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="4b1a8-162">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![De downloadkoppeling certificaat](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. <span data-ttu-id="4b1a8-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-164">Click **Save** button.</span></span>

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4b1a8-166">Op de **softwareconfiguratie Rally** sectie, klikt u op **Rally Software configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-166">On the **Rally Software Configuration** section, click **Configure Rally Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4b1a8-167">Kopieer de **Sign-Out-URL en SAML entiteit-ID** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="4b1a8-167">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![De softwareconfiguratie Rally](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. <span data-ttu-id="4b1a8-169">Meld u aan bij uw **Rally Software** tenant.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-169">Log in to your **Rally Software** tenant.</span></span>

8. <span data-ttu-id="4b1a8-170">Klik in de werkbalk bovenaan op **Setup**, en selecteer vervolgens **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-170">In the toolbar on the top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="4b1a8-171">![Abonnement](./media/active-directory-saas-rally-software-tutorial/ic769531.png "abonnement")</span><span class="sxs-lookup"><span data-stu-id="4b1a8-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span></span>

9. <span data-ttu-id="4b1a8-172">Klik op de **actie** knop.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-172">Click the **Action** button.</span></span> <span data-ttu-id="4b1a8-173">Selecteer **abonnement bewerken** op de rechtsboven in de werkbalk.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-173">Select **Edit Subscription** at the top right side of the toolbar.</span></span>

10. <span data-ttu-id="4b1a8-174">Op de **abonnement** dialoogvenster pagina de volgende stappen uit en klik vervolgens op **opslaan en sluiten**:</span><span class="sxs-lookup"><span data-stu-id="4b1a8-174">On the **Subscription** dialog page, perform the following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="4b1a8-175">![Verificatie](./media/active-directory-saas-rally-software-tutorial/ic769542.png "verificatie")</span><span class="sxs-lookup"><span data-stu-id="4b1a8-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="4b1a8-176">a.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-176">a.</span></span> <span data-ttu-id="4b1a8-177">Selecteer **Rally of eenmalige aanmelding verificatie** uit de vervolgkeuzelijst verificatie.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="4b1a8-178">b.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-178">b.</span></span> <span data-ttu-id="4b1a8-179">In de **identiteit provider URL** textbox, plak de waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-179">In the **Identity provider URL** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="4b1a8-180">c.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-180">c.</span></span> <span data-ttu-id="4b1a8-181">In de **eenmalige aanmelding, afmelding** textbox, plak de waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-181">In the **SSO Logout** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="4b1a8-182">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="4b1a8-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4b1a8-183">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4b1a8-184">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4b1a8-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4b1a8-185">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="4b1a8-185">Create an Azure AD test user</span></span>

<span data-ttu-id="4b1a8-186">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Een Azure AD-testgebruiker maken][100]

<span data-ttu-id="4b1a8-188">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="4b1a8-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4b1a8-189">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4b1a8-191">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4b1a8-193">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![De knop toevoegen](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4b1a8-195">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="4b1a8-195">In the **User** dialog box, perform the following steps:</span></span>

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4b1a8-197">a.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-197">a.</span></span> <span data-ttu-id="4b1a8-198">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b1a8-199">b.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-199">b.</span></span> <span data-ttu-id="4b1a8-200">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="4b1a8-201">c.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-201">c.</span></span> <span data-ttu-id="4b1a8-202">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="4b1a8-203">d.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-203">d.</span></span> <span data-ttu-id="4b1a8-204">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="4b1a8-205">Een testgebruiker Rally Software maken</span><span class="sxs-lookup"><span data-stu-id="4b1a8-205">Create a Rally Software test user</span></span>

<span data-ttu-id="4b1a8-206">Azure AD-gebruikers moeten kunnen aanmelden, als ze worden ingericht voor de Software Rally-toepassing met behulp van de namen van de Azure Active Directory-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-206">For Azure AD users to be able to sign in, they must be provisioned to the Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="4b1a8-207">**Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="4b1a8-207">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="4b1a8-208">Aanmelden bij uw tenant Rally Software.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-208">Log in to your Rally Software tenant.</span></span>

2. <span data-ttu-id="4b1a8-209">Ga naar **Setup \> gebruikers**, en klik vervolgens op **+ nieuw toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-209">Go to **Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="4b1a8-210">![Gebruikers](./media/active-directory-saas-rally-software-tutorial/ic781039.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="4b1a8-210">![Users](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Users")</span></span>

3. <span data-ttu-id="4b1a8-211">Typ de naam in het tekstvak voor de nieuwe gebruiker en klik vervolgens op **toevoegen met Details**.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-211">Type the name in the New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="4b1a8-212">In de **gebruiker maken** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="4b1a8-212">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="4b1a8-213">![Gebruiker maken](./media/active-directory-saas-rally-software-tutorial/ic781040.png "gebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="4b1a8-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="4b1a8-214">a.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-214">a.</span></span> <span data-ttu-id="4b1a8-215">In de **gebruikersnaam** textbox, typ de naam van gebruiker, zoals **Brittsimon**.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-215">In the **User Name** textbox, type the name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="4b1a8-216">b.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-216">b.</span></span> <span data-ttu-id="4b1a8-217">In **e-mailadres** textbox, voer het e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="4b1a8-217">In **E-mail Address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="4b1a8-218">c.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-218">c.</span></span> <span data-ttu-id="4b1a8-219">In **voornaam** tekst en voer de voornaam van de gebruiker zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-219">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="4b1a8-220">d.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-220">d.</span></span> <span data-ttu-id="4b1a8-221">In **achternaam** tekst en voer de achternaam van de gebruiker zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-221">In **Last Name** text box, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="4b1a8-222">e.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-222">e.</span></span> <span data-ttu-id="4b1a8-223">Klik op **opslaan en sluiten**.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="4b1a8-224">U kunt geen andere hulpprogramma's voor Software Rally gebruiker-account maken of API's die worden geleverd door Software Rally gebruiken voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4b1a8-225">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="4b1a8-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="4b1a8-226">In deze sectie maakt inschakelen u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot Software Rally.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rally Software.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="4b1a8-228">**Britta Simon om aan te wijzen Rally Software, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="4b1a8-228">**To assign Britta Simon to Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="4b1a8-229">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="4b1a8-231">Selecteer in de lijst met toepassingen **Rally Software**.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-231">In the applications list, select **Rally Software**.</span></span>

    ![De koppeling Rally Software in de lijst met toepassingen](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. <span data-ttu-id="4b1a8-233">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-233">In the menu on the left, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202]

4. <span data-ttu-id="4b1a8-235">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-235">Click **Add** button.</span></span> <span data-ttu-id="4b1a8-236">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="4b1a8-238">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4b1a8-239">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b1a8-240">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4b1a8-241">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="4b1a8-241">Test single sign-on</span></span>

<span data-ttu-id="4b1a8-242">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4b1a8-243">Als u op de tegel Rally Software in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Rally Software.</span><span class="sxs-lookup"><span data-stu-id="4b1a8-243">When you click the Rally Software tile in the Access Panel, you should get automatically signed-on to your Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4b1a8-244">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="4b1a8-244">Additional resources</span></span>

* [<span data-ttu-id="4b1a8-245">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b1a8-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b1a8-246">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4b1a8-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

