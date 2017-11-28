---
title: 'Zelfstudie: Azure Active Directory-integratie met Sansan | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Sansan.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f653a0f2-c44a-4670-b936-68c136b578ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: e1a9653d5feea910308cefabdbdfe3a6af44bbe4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sansan"></a><span data-ttu-id="6e711-103">Zelfstudie: Azure Active Directory-integratie met Sansan</span><span class="sxs-lookup"><span data-stu-id="6e711-103">Tutorial: Azure Active Directory integration with Sansan</span></span>

<span data-ttu-id="6e711-104">In deze zelfstudie leert u hoe Sansan integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6e711-104">In this tutorial, you learn how to integrate Sansan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6e711-105">Sansan integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6e711-105">Integrating Sansan with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6e711-106">U kunt beheren in Azure AD die toegang tot Sansan heeft</span><span class="sxs-lookup"><span data-stu-id="6e711-106">You can control in Azure AD who has access to Sansan</span></span>
- <span data-ttu-id="6e711-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Sansan (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="6e711-107">You can enable your users to automatically get signed-on to Sansan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6e711-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6e711-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6e711-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6e711-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e711-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6e711-110">Prerequisites</span></span>

<span data-ttu-id="6e711-111">Voor het configureren van Azure AD-integratie met Sansan, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="6e711-111">To configure Azure AD integration with Sansan, you need the following items:</span></span>

- <span data-ttu-id="6e711-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6e711-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6e711-113">Een Sansan eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6e711-113">A Sansan single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6e711-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6e711-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6e711-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6e711-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6e711-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6e711-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6e711-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6e711-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6e711-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6e711-118">Scenario description</span></span>
<span data-ttu-id="6e711-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6e711-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6e711-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6e711-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6e711-121">Sansan uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6e711-121">Adding Sansan from the gallery</span></span>
2. <span data-ttu-id="6e711-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6e711-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sansan-from-the-gallery"></a><span data-ttu-id="6e711-123">Sansan uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6e711-123">Adding Sansan from the gallery</span></span>
<span data-ttu-id="6e711-124">Voor het configureren van de integratie van Sansan in Azure AD, moet u Sansan uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6e711-124">To configure the integration of Sansan into Azure AD, you need to add Sansan from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6e711-125">**Als u wilt toevoegen Sansan uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6e711-125">**To add Sansan from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6e711-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6e711-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6e711-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6e711-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6e711-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6e711-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6e711-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e711-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6e711-133">Typ in het zoekvak **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="6e711-133">In the search box, type **Sansan**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_search.png)

5. <span data-ttu-id="6e711-135">Selecteer in het deelvenster resultaten **Sansan**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="6e711-135">In the results panel, select **Sansan**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6e711-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6e711-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6e711-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met Sansan op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="6e711-138">In this section, you configure and test Azure AD single sign-on with Sansan based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6e711-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Sansan is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e711-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sansan is to a user in Azure AD.</span></span> <span data-ttu-id="6e711-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Sansan tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="6e711-140">In other words, a link relationship between an Azure AD user and the related user in Sansan needs to be established.</span></span>

<span data-ttu-id="6e711-141">Wijs in Sansan, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="6e711-141">In Sansan, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6e711-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Sansan, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="6e711-142">To configure and test Azure AD single sign-on with Sansan, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6e711-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6e711-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6e711-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e711-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6e711-145">**[Maken van een testgebruiker Sansan](#creating-a-sansan-test-user)**  - Sansan die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="6e711-145">**[Creating a Sansan test user](#creating-a-sansan-test-user)** - to have a counterpart of Britta Simon in Sansan that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6e711-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6e711-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6e711-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6e711-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6e711-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6e711-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6e711-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Sansan configureren.</span><span class="sxs-lookup"><span data-stu-id="6e711-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sansan application.</span></span>

<span data-ttu-id="6e711-150">**Voor het configureren van Azure AD eenmalige aanmelding met Sansan, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6e711-150">**To configure Azure AD single sign-on with Sansan, perform the following steps:**</span></span>

1. <span data-ttu-id="6e711-151">In de Azure-portal op de **Sansan** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6e711-151">In the Azure portal, on the **Sansan** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6e711-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6e711-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_samlbase.png)

3. <span data-ttu-id="6e711-155">Op de **Sansan domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6e711-155">On the **Sansan Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_url.png)

    <span data-ttu-id="6e711-157">a.</span><span class="sxs-lookup"><span data-stu-id="6e711-157">a.</span></span> <span data-ttu-id="6e711-158">In de **aanmeldings-URL** textbox, typ een URL met de volgende patronen:</span><span class="sxs-lookup"><span data-stu-id="6e711-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    
    | <span data-ttu-id="6e711-159">Omgeving</span><span class="sxs-lookup"><span data-stu-id="6e711-159">Environment</span></span> | <span data-ttu-id="6e711-160">URL</span><span class="sxs-lookup"><span data-stu-id="6e711-160">URL</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="6e711-161">PC web</span><span class="sxs-lookup"><span data-stu-id="6e711-161">PC web</span></span> |`https://ap.sansan.com/v/saml2/<company name>/acs` |
    | <span data-ttu-id="6e711-162">Systeemeigen mobiele app</span><span class="sxs-lookup"><span data-stu-id="6e711-162">Native Mobile app</span></span> |`https://internal.api.sansan.com/saml2/<company name>/acs` |
    | <span data-ttu-id="6e711-163">Mobiele-browserinstellingen</span><span class="sxs-lookup"><span data-stu-id="6e711-163">Mobile browser settings</span></span> |`https://ap.sansan.com/s/saml2/<company name>/acs` |  

    <span data-ttu-id="6e711-164">b.</span><span class="sxs-lookup"><span data-stu-id="6e711-164">b.</span></span> <span data-ttu-id="6e711-165">In de **id** textbox, typ een URL met de volgende patronen:</span><span class="sxs-lookup"><span data-stu-id="6e711-165">In the **Identifier** textbox, type a URL using the following patterns:</span></span>
    | <span data-ttu-id="6e711-166">Omgeving</span><span class="sxs-lookup"><span data-stu-id="6e711-166">Environment</span></span>             | <span data-ttu-id="6e711-167">URL</span><span class="sxs-lookup"><span data-stu-id="6e711-167">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="6e711-168">PC web</span><span class="sxs-lookup"><span data-stu-id="6e711-168">PC web</span></span>                  | `https://ap.sansan.com/v/saml2/<company name>`|
    | <span data-ttu-id="6e711-169">Systeemeigen mobiele app</span><span class="sxs-lookup"><span data-stu-id="6e711-169">Native Mobile app</span></span>       | `https://internal.api.sansan.com/saml2/<company name>` |
    | <span data-ttu-id="6e711-170">Mobiele-browserinstellingen</span><span class="sxs-lookup"><span data-stu-id="6e711-170">Mobile browser settings</span></span> | `https://ap.sansan.com/s/saml2/<company name>` |

    > [!NOTE] 
    > <span data-ttu-id="6e711-171">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="6e711-171">These values are not real.</span></span> <span data-ttu-id="6e711-172">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="6e711-172">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6e711-173">Neem contact op met [Sansan Client ondersteuningsteam](https://www.sansan.com/form/contact) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="6e711-173">Contact [Sansan Client support team](https://www.sansan.com/form/contact) to get these values.</span></span> 

4. <span data-ttu-id="6e711-174">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6e711-174">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_certificate.png) 

5. <span data-ttu-id="6e711-176">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6e711-176">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sansan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6e711-178">Op de **Sansan configuratie** sectie, klikt u op **configureren Sansan** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="6e711-178">On the **Sansan Configuration** section, click **Configure Sansan** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6e711-179">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="6e711-179">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_configure.png) 

7. <span data-ttu-id="6e711-181">Eenmalige aanmelding configureren op **Sansan** zijde, moet u de gedownloade verzenden **certificaat**, **Sign-Out URL**, **SAML entiteit-ID**, en **SAML Single Sign-On Service-URL** naar [Sansan ondersteuningsteam](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="6e711-181">To configure single sign-on on **Sansan** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** to [Sansan support team](https://www.sansan.com/form/contact).</span></span> <span data-ttu-id="6e711-182">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6e711-182">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="6e711-183">PC browserinstelling werken ook voor mobiele Apps en mobiele browser samen met PC web.</span><span class="sxs-lookup"><span data-stu-id="6e711-183">PC browser setting also work for Mobile app and Mobile browser along with PC web.</span></span>  

> [!TIP]
> <span data-ttu-id="6e711-184">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="6e711-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6e711-185">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="6e711-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6e711-186">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6e711-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6e711-187">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6e711-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="6e711-188">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6e711-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6e711-190">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6e711-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6e711-191">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6e711-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sansan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6e711-193">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6e711-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sansan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6e711-195">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e711-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sansan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6e711-197">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6e711-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sansan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6e711-199">a.</span><span class="sxs-lookup"><span data-stu-id="6e711-199">a.</span></span> <span data-ttu-id="6e711-200">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6e711-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6e711-201">b.</span><span class="sxs-lookup"><span data-stu-id="6e711-201">b.</span></span> <span data-ttu-id="6e711-202">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6e711-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6e711-203">c.</span><span class="sxs-lookup"><span data-stu-id="6e711-203">c.</span></span> <span data-ttu-id="6e711-204">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6e711-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6e711-205">d.</span><span class="sxs-lookup"><span data-stu-id="6e711-205">d.</span></span> <span data-ttu-id="6e711-206">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6e711-206">Click **Create**.</span></span>
 
### <a name="creating-a-sansan-test-user"></a><span data-ttu-id="6e711-207">Een testgebruiker Sansan maken</span><span class="sxs-lookup"><span data-stu-id="6e711-207">Creating a Sansan test user</span></span>

<span data-ttu-id="6e711-208">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in SanSan maken.</span><span class="sxs-lookup"><span data-stu-id="6e711-208">In this section, you create a user called Britta Simon in SanSan.</span></span> <span data-ttu-id="6e711-209">SanSan toepassing moet de gebruiker moeten worden ingericht in de toepassing voordat u eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6e711-209">SanSan application needs the user to be provisioned in the application before doing SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="6e711-210">Als u wilt maken van een gebruiker handmatig of batch-gebruikers, moet u contact opnemen met de [Sansan ondersteuningsteam](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="6e711-210">If you need to create a user manually or batch of users, you need to contact the [Sansan support team](https://www.sansan.com/form/contact).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6e711-211">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e711-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6e711-212">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Sansan.</span><span class="sxs-lookup"><span data-stu-id="6e711-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sansan.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6e711-214">**Britta Simon om aan te wijzen Sansan, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6e711-214">**To assign Britta Simon to Sansan, perform the following steps:**</span></span>

1. <span data-ttu-id="6e711-215">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6e711-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6e711-217">Selecteer in de lijst met toepassingen **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="6e711-217">In the applications list, select **Sansan**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_app.png) 

3. <span data-ttu-id="6e711-219">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6e711-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6e711-221">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6e711-221">Click **Add** button.</span></span> <span data-ttu-id="6e711-222">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e711-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6e711-224">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6e711-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6e711-225">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e711-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6e711-226">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e711-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6e711-227">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6e711-227">Testing single sign-on</span></span>

<span data-ttu-id="6e711-228">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="6e711-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6e711-229">Als u op de tegel Sansan in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Sansan.</span><span class="sxs-lookup"><span data-stu-id="6e711-229">When you click the Sansan tile in the Access Panel, you should get automatically signed-on to your Sansan application.</span></span>
<span data-ttu-id="6e711-230">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6e711-230">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6e711-231">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6e711-231">Additional resources</span></span>

* [<span data-ttu-id="6e711-232">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e711-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6e711-233">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6e711-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_203.png

