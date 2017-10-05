---
title: 'Zelfstudie: Azure Active Directory-integratie met samenwerking innovatie | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en gezamenlijke innovatie.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bba95df3-75a4-4a93-8805-b3a8aa3d4861
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 5706ba9f4e7c92de77a0edc5146aa150de379c9f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a><span data-ttu-id="0cea8-103">Zelfstudie: Azure Active Directory-integratie met samenwerking innovatie</span><span class="sxs-lookup"><span data-stu-id="0cea8-103">Tutorial: Azure Active Directory integration with Collaborative Innovation</span></span>

<span data-ttu-id="0cea8-104">In deze zelfstudie leert u hoe samenwerking innovatie integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0cea8-104">In this tutorial, you learn how to integrate Collaborative Innovation with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0cea8-105">Samenwerking innovatie integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="0cea8-105">Integrating Collaborative Innovation with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0cea8-106">U kunt beheren in Azure AD die toegang tot de collectieve innovatie heeft</span><span class="sxs-lookup"><span data-stu-id="0cea8-106">You can control in Azure AD who has access to Collaborative Innovation</span></span>
- <span data-ttu-id="0cea8-107">U kunt uw gebruikers automatisch ophalen aangemeld bij gezamenlijke innovatie (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="0cea8-107">You can enable your users to automatically get signed-on to Collaborative Innovation (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0cea8-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="0cea8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0cea8-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0cea8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0cea8-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0cea8-110">Prerequisites</span></span>

<span data-ttu-id="0cea8-111">Voor het configureren van Azure AD-integratie met samenwerking innovatie, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="0cea8-111">To configure Azure AD integration with Collaborative Innovation, you need the following items:</span></span>

- <span data-ttu-id="0cea8-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="0cea8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0cea8-113">Een gezamenlijke innovatie eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="0cea8-113">A Collaborative Innovation single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0cea8-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="0cea8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0cea8-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="0cea8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0cea8-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="0cea8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0cea8-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0cea8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0cea8-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="0cea8-118">Scenario description</span></span>
<span data-ttu-id="0cea8-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="0cea8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0cea8-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="0cea8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0cea8-121">Samenwerking innovatie uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="0cea8-121">Adding Collaborative Innovation from the gallery</span></span>
2. <span data-ttu-id="0cea8-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0cea8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-collaborative-innovation-from-the-gallery"></a><span data-ttu-id="0cea8-123">Samenwerking innovatie uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="0cea8-123">Adding Collaborative Innovation from the gallery</span></span>
<span data-ttu-id="0cea8-124">Voor het configureren van de integratie van samenwerking innovatie in Azure AD, moet u samenwerken innovatie uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="0cea8-124">To configure the integration of Collaborative Innovation into Azure AD, you need to add Collaborative Innovation from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0cea8-125">**Als u wilt samenwerken innovatie uit de galerie toevoegt, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0cea8-125">**To add Collaborative Innovation from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0cea8-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0cea8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0cea8-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0cea8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0cea8-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0cea8-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="0cea8-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0cea8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="0cea8-133">Typ in het zoekvak **gezamenlijke innovatie**.</span><span class="sxs-lookup"><span data-stu-id="0cea8-133">In the search box, type **Collaborative Innovation**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

5. <span data-ttu-id="0cea8-135">Selecteer in het deelvenster resultaten **gezamenlijke innovatie**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="0cea8-135">In the results panel, select **Collaborative Innovation**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0cea8-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0cea8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0cea8-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met samenwerking vernieuwing op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="0cea8-138">In this section, you configure and test Azure AD single sign-on with Collaborative Innovation based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0cea8-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in samenwerking innovatie is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0cea8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Collaborative Innovation is to a user in Azure AD.</span></span> <span data-ttu-id="0cea8-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in samenwerking vernieuwing tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="0cea8-140">In other words, a link relationship between an Azure AD user and the related user in Collaborative Innovation needs to be established.</span></span>

<span data-ttu-id="0cea8-141">Wijs in samenwerking innovatie, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="0cea8-141">In Collaborative Innovation, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0cea8-142">Om te configureren en testen van Azure AD eenmalige aanmelding met samenwerking innovatie, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="0cea8-142">To configure and test Azure AD single sign-on with Collaborative Innovation, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0cea8-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0cea8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0cea8-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0cea8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0cea8-145">**[Maken van een gezamenlijke innovatie testgebruiker](#creating-a-collaborative-innovation-test-user)**  - samenwerking innovatie die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="0cea8-145">**[Creating a Collaborative Innovation test user](#creating-a-collaborative-innovation-test-user)** - to have a counterpart of Britta Simon in Collaborative Innovation that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0cea8-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0cea8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0cea8-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="0cea8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0cea8-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="0cea8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0cea8-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing gezamenlijke innovatie configureren.</span><span class="sxs-lookup"><span data-stu-id="0cea8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Collaborative Innovation application.</span></span>

<span data-ttu-id="0cea8-150">**Voor het configureren van Azure AD eenmalige aanmelding met samenwerking innovatie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0cea8-150">**To configure Azure AD single sign-on with Collaborative Innovation, perform the following steps:**</span></span>

1. <span data-ttu-id="0cea8-151">In de Azure-portal op de **gezamenlijke innovatie** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="0cea8-151">In the Azure portal, on the **Collaborative Innovation** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="0cea8-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0cea8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

3. <span data-ttu-id="0cea8-155">Op de **gezamenlijke innovatie domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="0cea8-155">On the **Collaborative Innovation Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    <span data-ttu-id="0cea8-157">a.</span><span class="sxs-lookup"><span data-stu-id="0cea8-157">a.</span></span> <span data-ttu-id="0cea8-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<instancename>.foundry.<companyname>.com/`</span><span class="sxs-lookup"><span data-stu-id="0cea8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.foundry.<companyname>.com/`</span></span>

    <span data-ttu-id="0cea8-159">b.</span><span class="sxs-lookup"><span data-stu-id="0cea8-159">b.</span></span> <span data-ttu-id="0cea8-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<instancename>.foundry.<companyname>.com`</span><span class="sxs-lookup"><span data-stu-id="0cea8-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.foundry.<companyname>.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="0cea8-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="0cea8-161">These values are not real.</span></span> <span data-ttu-id="0cea8-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="0cea8-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0cea8-163">Neem contact op met [gezamenlijke innovatie Client ondersteuningsteam](https://www.unilever.com/contact/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="0cea8-163">Contact [Collaborative Innovation Client support team](https://www.unilever.com/contact/) to get these values.</span></span>  

4. <span data-ttu-id="0cea8-164">De SAML-asserties verwacht gezamenlijk innovatie toepassingen in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="0cea8-164">Collaborative Innovation application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="0cea8-165">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="0cea8-165">Please configure the following claims for this application.</span></span> <span data-ttu-id="0cea8-166">U kunt beheren de waarden van deze kenmerken van de '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="0cea8-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="0cea8-167">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="0cea8-167">The following screenshot shows an example for this.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-collaborativeinnovation-tutorial/attribute.png)
    
5. <span data-ttu-id="0cea8-169">Klik op **weergeven en bewerken van alle andere gebruikerskenmerken** selectievakje in de **gebruikerskenmerken** sectie uit te breiden, de kenmerken.</span><span class="sxs-lookup"><span data-stu-id="0cea8-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="0cea8-170">Voer de volgende stappen uit op elk van de kenmerken weergegeven-</span><span class="sxs-lookup"><span data-stu-id="0cea8-170">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="0cea8-171">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="0cea8-171">Attribute Name</span></span> | <span data-ttu-id="0cea8-172">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="0cea8-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="0cea8-173">Voornaam</span><span class="sxs-lookup"><span data-stu-id="0cea8-173">givenname</span></span> | <span data-ttu-id="0cea8-174">User.givenName</span><span class="sxs-lookup"><span data-stu-id="0cea8-174">user.givenname</span></span> |
    | <span data-ttu-id="0cea8-175">Achternaam</span><span class="sxs-lookup"><span data-stu-id="0cea8-175">surname</span></span> | <span data-ttu-id="0cea8-176">User.surname</span><span class="sxs-lookup"><span data-stu-id="0cea8-176">user.surname</span></span> |
    | <span data-ttu-id="0cea8-177">EmailAddress</span><span class="sxs-lookup"><span data-stu-id="0cea8-177">emailaddress</span></span> | <span data-ttu-id="0cea8-178">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="0cea8-178">user.userprincipalname</span></span> |
    | <span data-ttu-id="0cea8-179">naam</span><span class="sxs-lookup"><span data-stu-id="0cea8-179">name</span></span> | <span data-ttu-id="0cea8-180">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="0cea8-180">user.userprincipalname</span></span> |

    <span data-ttu-id="0cea8-181">a.</span><span class="sxs-lookup"><span data-stu-id="0cea8-181">a.</span></span> <span data-ttu-id="0cea8-182">Klik op het kenmerk openen de **kenmerk bewerken** venster.</span><span class="sxs-lookup"><span data-stu-id="0cea8-182">Click the attribute to open the **Edit Attribute** window.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-collaborativeinnovation-tutorial/url_update.png)

    <span data-ttu-id="0cea8-184">b.</span><span class="sxs-lookup"><span data-stu-id="0cea8-184">b.</span></span> <span data-ttu-id="0cea8-185">Verwijder de URL-waarde van de **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="0cea8-185">Delete the URL value from the **Namespace**.</span></span>
    
    <span data-ttu-id="0cea8-186">c.</span><span class="sxs-lookup"><span data-stu-id="0cea8-186">c.</span></span> <span data-ttu-id="0cea8-187">Klik op **Ok** om op te slaan van de instelling.</span><span class="sxs-lookup"><span data-stu-id="0cea8-187">Click **Ok** to save the setting.</span></span>

6. <span data-ttu-id="0cea8-188">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="0cea8-188">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

7. <span data-ttu-id="0cea8-190">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="0cea8-190">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0cea8-192">Eenmalige aanmelding configureren op **gezamenlijke innovatie** zijde, moet u de gedownloade verzenden **Metadata XML** naar [gezamenlijke innovatie ondersteuningsteam](https://www.unilever.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="0cea8-192">To configure single sign-on on **Collaborative Innovation** side, you need to send the downloaded **Metadata XML** to [Collaborative Innovation support team](https://www.unilever.com/contact/).</span></span> <span data-ttu-id="0cea8-193">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="0cea8-193">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0cea8-194">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="0cea8-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0cea8-195">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="0cea8-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0cea8-196">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0cea8-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0cea8-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="0cea8-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="0cea8-198">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0cea8-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="0cea8-200">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0cea8-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0cea8-201">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="0cea8-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0cea8-203">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="0cea8-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0cea8-205">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0cea8-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0cea8-207">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="0cea8-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0cea8-209">a.</span><span class="sxs-lookup"><span data-stu-id="0cea8-209">a.</span></span> <span data-ttu-id="0cea8-210">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0cea8-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0cea8-211">b.</span><span class="sxs-lookup"><span data-stu-id="0cea8-211">b.</span></span> <span data-ttu-id="0cea8-212">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0cea8-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0cea8-213">c.</span><span class="sxs-lookup"><span data-stu-id="0cea8-213">c.</span></span> <span data-ttu-id="0cea8-214">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="0cea8-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0cea8-215">d.</span><span class="sxs-lookup"><span data-stu-id="0cea8-215">d.</span></span> <span data-ttu-id="0cea8-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0cea8-216">Click **Create**.</span></span>
 
### <a name="creating-a-collaborative-innovation-test-user"></a><span data-ttu-id="0cea8-217">Maken van een gezamenlijke innovatie testgebruiker</span><span class="sxs-lookup"><span data-stu-id="0cea8-217">Creating a Collaborative Innovation test user</span></span>

<span data-ttu-id="0cea8-218">Om Azure AD-gebruikers zich aanmelden bij gezamenlijke innovatie, moeten ze worden ingericht in samenwerking innovatie.</span><span class="sxs-lookup"><span data-stu-id="0cea8-218">To enable Azure AD users to log in to Collaborative Innovation, they must be provisioned into Collaborative Innovation.</span></span>  

<span data-ttu-id="0cea8-219">In geval van deze toepassing is inrichting automatische als de toepassing alleen bij tijd gebruikersaanvragen ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="0cea8-219">In case of this application provisioning is automatic as the application supports just in time user provisioning.</span></span> <span data-ttu-id="0cea8-220">Zo hoeft niet hier alle stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="0cea8-220">So there is no need to perform any steps here.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0cea8-221">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="0cea8-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0cea8-222">In deze sectie maakt inschakelen u Britta Simon gebruiken Azure eenmalige aanmelding toegang verleent tot samenwerking innovatie.</span><span class="sxs-lookup"><span data-stu-id="0cea8-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Collaborative Innovation.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="0cea8-224">**Britta Simon om aan te wijzen gezamenlijke innovatie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="0cea8-224">**To assign Britta Simon to Collaborative Innovation, perform the following steps:**</span></span>

1. <span data-ttu-id="0cea8-225">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="0cea8-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="0cea8-227">Selecteer in de lijst met toepassingen **gezamenlijke innovatie**.</span><span class="sxs-lookup"><span data-stu-id="0cea8-227">In the applications list, select **Collaborative Innovation**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

3. <span data-ttu-id="0cea8-229">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="0cea8-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="0cea8-231">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="0cea8-231">Click **Add** button.</span></span> <span data-ttu-id="0cea8-232">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0cea8-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="0cea8-234">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="0cea8-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0cea8-235">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0cea8-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0cea8-236">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0cea8-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0cea8-237">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="0cea8-237">Testing single sign-on</span></span>

<span data-ttu-id="0cea8-238">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="0cea8-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0cea8-239">Als u op de tegel gezamenlijke innovatie in het deelvenster toegang, krijgt u de aanmeldingspagina van samenwerking innovatie toepassing.</span><span class="sxs-lookup"><span data-stu-id="0cea8-239">When you click the Collaborative Innovation tile in the Access Panel, you should get login page of Collaborative Innovation application.</span></span>
<span data-ttu-id="0cea8-240">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0cea8-240">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0cea8-241">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="0cea8-241">Additional resources</span></span>

* [<span data-ttu-id="0cea8-242">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0cea8-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0cea8-243">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0cea8-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_203.png

