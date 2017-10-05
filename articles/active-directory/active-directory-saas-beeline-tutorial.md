---
title: 'Zelfstudie: Azure Active Directory-integratie met BeeLine | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en BeeLine.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 93acbd90bbe5f0a40bf3f56edb766a0fdd30f68f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a><span data-ttu-id="aa5f9-103">Zelfstudie: Azure Active Directory-integratie met BeeLine</span><span class="sxs-lookup"><span data-stu-id="aa5f9-103">Tutorial: Azure Active Directory integration with BeeLine</span></span>

<span data-ttu-id="aa5f9-104">In deze zelfstudie leert u hoe BeeLine integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aa5f9-104">In this tutorial, you learn how to integrate BeeLine with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aa5f9-105">BeeLine integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="aa5f9-105">Integrating BeeLine with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="aa5f9-106">U kunt beheren in Azure AD die toegang tot BeeLine heeft</span><span class="sxs-lookup"><span data-stu-id="aa5f9-106">You can control in Azure AD who has access to BeeLine</span></span>
- <span data-ttu-id="aa5f9-107">U kunt uw gebruikers automatisch ophalen aangemeld bij BeeLine (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="aa5f9-107">You can enable your users to automatically get signed-on to BeeLine (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aa5f9-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="aa5f9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="aa5f9-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aa5f9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa5f9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="aa5f9-110">Prerequisites</span></span>

<span data-ttu-id="aa5f9-111">Voor het configureren van Azure AD-integratie met BeeLine, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="aa5f9-111">To configure Azure AD integration with BeeLine, you need the following items:</span></span>

- <span data-ttu-id="aa5f9-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="aa5f9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aa5f9-113">Een BeeLine eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="aa5f9-113">A BeeLine single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aa5f9-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aa5f9-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="aa5f9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aa5f9-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aa5f9-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aa5f9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aa5f9-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="aa5f9-118">Scenario description</span></span>
<span data-ttu-id="aa5f9-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aa5f9-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="aa5f9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aa5f9-121">BeeLine uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="aa5f9-121">Adding BeeLine from the gallery</span></span>
2. <span data-ttu-id="aa5f9-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="aa5f9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-beeline-from-the-gallery"></a><span data-ttu-id="aa5f9-123">BeeLine uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="aa5f9-123">Adding BeeLine from the gallery</span></span>
<span data-ttu-id="aa5f9-124">Voor het configureren van de integratie van BeeLine in Azure AD, moet u BeeLine uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-124">To configure the integration of BeeLine into Azure AD, you need to add BeeLine from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="aa5f9-125">**Als u wilt toevoegen BeeLine uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="aa5f9-125">**To add BeeLine from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="aa5f9-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aa5f9-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="aa5f9-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="aa5f9-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="aa5f9-133">Typ in het zoekvak **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-133">In the search box, type **BeeLine**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_search.png)

5. <span data-ttu-id="aa5f9-135">Selecteer in het deelvenster resultaten **BeeLine**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-135">In the results panel, select **BeeLine**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aa5f9-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="aa5f9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aa5f9-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met BeeLine op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="aa5f9-138">In this section, you configure and test Azure AD single sign-on with BeeLine based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="aa5f9-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in BeeLine is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BeeLine is to a user in Azure AD.</span></span> <span data-ttu-id="aa5f9-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in BeeLine tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-140">In other words, a link relationship between an Azure AD user and the related user in BeeLine needs to be established.</span></span>

<span data-ttu-id="aa5f9-141">Wijs in BeeLine, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-141">In BeeLine, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="aa5f9-142">Om te configureren en testen van Azure AD eenmalige aanmelding met BeeLine, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="aa5f9-142">To configure and test Azure AD single sign-on with BeeLine, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="aa5f9-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="aa5f9-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aa5f9-145">**[Maken van een testgebruiker BeeLine](#creating-a-beeline-test-user)**  - BeeLine die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-145">**[Creating a BeeLine test user](#creating-a-beeline-test-user)** - to have a counterpart of Britta Simon in BeeLine that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="aa5f9-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aa5f9-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aa5f9-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="aa5f9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aa5f9-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing BeeLine configureren.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BeeLine application.</span></span>

<span data-ttu-id="aa5f9-150">**Voor het configureren van Azure AD eenmalige aanmelding met BeeLine, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="aa5f9-150">**To configure Azure AD single sign-on with BeeLine, perform the following steps:**</span></span>

1. <span data-ttu-id="aa5f9-151">In de Azure-portal op de **BeeLine** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-151">In the Azure portal, on the **BeeLine** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="aa5f9-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_samlbase.png)

3. <span data-ttu-id="aa5f9-155">Op de **BeeLine domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="aa5f9-155">On the **BeeLine Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_url.png)

    <span data-ttu-id="aa5f9-157">a.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-157">a.</span></span> <span data-ttu-id="aa5f9-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://projects.beeline.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="aa5f9-158">In the **Identifier** textbox, type a URL using the following pattern: `https://projects.beeline.net/<instancename>`</span></span>

    <span data-ttu-id="aa5f9-159">b.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-159">b.</span></span> <span data-ttu-id="aa5f9-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:</span><span class="sxs-lookup"><span data-stu-id="aa5f9-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > <span data-ttu-id="aa5f9-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-161">These values are not real.</span></span> <span data-ttu-id="aa5f9-162">Deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="aa5f9-163">Neem contact op met [BeeLine ondersteuningsteam](https://www.beeline.com/contact-us/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-163">Contact [BeeLine support team](https://www.beeline.com/contact-us/) to get these values.</span></span>
 
4. <span data-ttu-id="aa5f9-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_certificate.png) 

5. <span data-ttu-id="aa5f9-166">Uw toepassing Beeline verwacht de SAML-asserties in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-166">Your Beeline application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="aa5f9-167">Neem contact op met [BeeLine ondersteuningsteam](https://www.beeline.com/contact-us/) eerst om te identificeren van de juiste gebruikers-id die in de toepassing worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-167">Please work with [BeeLine support team](https://www.beeline.com/contact-us/) first to identify the correct user identifier which will be mapped into the application.</span></span> <span data-ttu-id="aa5f9-168">Ook moet rekening houden met de richtlijnen van [BeeLine ondersteuningsteam](https://www.beeline.com/contact-us/) over het kenmerk dat moet worden gebruikt voor deze toewijzing.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-168">Also please take the guidance from [BeeLine support team](https://www.beeline.com/contact-us/) about the attribute which they want to use for this mapping.</span></span> <span data-ttu-id="aa5f9-169">U kunt beheren de waarde van dit kenmerk van de **gebruikerskenmerken** tabblad van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-169">You can manage the value of this attribute from the **User Attributes** tab of the application.</span></span> <span data-ttu-id="aa5f9-170">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-170">The following screenshot shows an example for this.</span></span> <span data-ttu-id="aa5f9-171">We hebben hier toegewezen de **gebruikers-id** claim met de **userprincipalname** kenmerk unieke gebruikers-ID, die worden verzonden naar de toepassing Beeline in het elke geslaagde SAML-antwoord bevat.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-171">Here we have mapped the **User Identifier** claim with the **userprincipalname** attribute, which provides unique user ID, which will be sent to the Beeline application in the every successful SAML Response.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-beeline-tutorial/tutorial_attribute.png)  

6. <span data-ttu-id="aa5f9-173">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-173">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-beeline-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="aa5f9-175">Op de **BeeLine configuratie** sectie, klikt u op **configureren BeeLine** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-175">On the **BeeLine Configuration** section, click **Configure BeeLine** to open **Configure sign-on** window.</span></span> <span data-ttu-id="aa5f9-176">Kopieer de **Sign-Out URL** en **SAML entiteit-ID** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="aa5f9-176">Copy the **Sign-Out URL** and **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_configure.png) 

8. <span data-ttu-id="aa5f9-178">Eenmalige aanmelding configureren op **BeeLine** zijde, moet u de gedownloade verzenden **Metadata XML** en **SAML entiteit-ID**, **Sign-Out URL** naar [BeeLine ondersteuningsteam](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="aa5f9-178">To configure single sign-on on **BeeLine** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID**, **Sign-Out URL** to [BeeLine support team](https://www.beeline.com/contact-us/).</span></span>

> [!TIP]
> <span data-ttu-id="aa5f9-179">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="aa5f9-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="aa5f9-180">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="aa5f9-181">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="aa5f9-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aa5f9-182">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="aa5f9-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="aa5f9-183">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="aa5f9-185">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="aa5f9-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="aa5f9-186">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-beeline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aa5f9-188">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-beeline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aa5f9-190">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aa5f9-192">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="aa5f9-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aa5f9-194">a.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-194">a.</span></span> <span data-ttu-id="aa5f9-195">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aa5f9-196">b.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-196">b.</span></span> <span data-ttu-id="aa5f9-197">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aa5f9-198">c.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-198">c.</span></span> <span data-ttu-id="aa5f9-199">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="aa5f9-200">d.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-200">d.</span></span> <span data-ttu-id="aa5f9-201">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-201">Click **Create**.</span></span>
 
### <a name="creating-a-beeline-test-user"></a><span data-ttu-id="aa5f9-202">Een testgebruiker BeeLine maken</span><span class="sxs-lookup"><span data-stu-id="aa5f9-202">Creating a BeeLine test user</span></span>

<span data-ttu-id="aa5f9-203">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Beeline maken.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-203">In this section, you create a user called Britta Simon in Beeline.</span></span> <span data-ttu-id="aa5f9-204">Beeline toepassing moet de gebruikers moeten worden ingericht in de toepassing voordat u eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-204">Beeline application needs all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="aa5f9-205">Zo werken met de [BeeLine ondersteuningsteam](https://www.beeline.com/contact-us/) voor het inrichten van al deze gebruikers in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-205">So work with the [BeeLine support team](https://www.beeline.com/contact-us/) to provision all these users into the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="aa5f9-206">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa5f9-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="aa5f9-207">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan BeeLine.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BeeLine.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="aa5f9-209">**Britta Simon om aan te wijzen BeeLine, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="aa5f9-209">**To assign Britta Simon to BeeLine, perform the following steps:**</span></span>

1. <span data-ttu-id="aa5f9-210">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="aa5f9-212">Selecteer in de lijst met toepassingen **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-212">In the applications list, select **BeeLine**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_app.png) 

3. <span data-ttu-id="aa5f9-214">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="aa5f9-216">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-216">Click **Add** button.</span></span> <span data-ttu-id="aa5f9-217">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="aa5f9-219">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="aa5f9-220">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aa5f9-221">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="aa5f9-222">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="aa5f9-222">Testing single sign-on</span></span>

<span data-ttu-id="aa5f9-223">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="aa5f9-224">Als u op de tegel Beeline in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Beeline.</span><span class="sxs-lookup"><span data-stu-id="aa5f9-224">When you click the Beeline tile in the Access Panel, you should get automatically signed-on to your Beeline application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aa5f9-225">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="aa5f9-225">Additional resources</span></span>

* [<span data-ttu-id="aa5f9-226">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa5f9-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aa5f9-227">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aa5f9-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_203.png

