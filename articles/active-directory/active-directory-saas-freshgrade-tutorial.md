---
title: 'Zelfstudie: Azure Active Directory-integratie met FreshGrade | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en FreshGrade.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1055bba6-f4df-462e-bc9b-1ad5ada0f638
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 3ff3e5aab679f8ee610c98f8a4089308adcce48f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshgrade"></a><span data-ttu-id="1f2b8-103">Zelfstudie: Azure Active Directory-integratie met FreshGrade</span><span class="sxs-lookup"><span data-stu-id="1f2b8-103">Tutorial: Azure Active Directory integration with FreshGrade</span></span>

<span data-ttu-id="1f2b8-104">In deze zelfstudie leert u hoe FreshGrade integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1f2b8-104">In this tutorial, you learn how to integrate FreshGrade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1f2b8-105">FreshGrade integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="1f2b8-105">Integrating FreshGrade with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1f2b8-106">U kunt beheren in Azure AD die toegang tot FreshGrade heeft</span><span class="sxs-lookup"><span data-stu-id="1f2b8-106">You can control in Azure AD who has access to FreshGrade</span></span>
- <span data-ttu-id="1f2b8-107">U kunt uw gebruikers automatisch ophalen aangemeld bij FreshGrade (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="1f2b8-107">You can enable your users to automatically get signed-on to FreshGrade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1f2b8-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="1f2b8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1f2b8-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1f2b8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f2b8-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1f2b8-110">Prerequisites</span></span>

<span data-ttu-id="1f2b8-111">Voor het configureren van Azure AD-integratie met FreshGrade, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="1f2b8-111">To configure Azure AD integration with FreshGrade, you need the following items:</span></span>

- <span data-ttu-id="1f2b8-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="1f2b8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1f2b8-113">Een FreshGrade eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="1f2b8-113">A FreshGrade single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1f2b8-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1f2b8-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="1f2b8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1f2b8-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1f2b8-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f2b8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1f2b8-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="1f2b8-118">Scenario description</span></span>
<span data-ttu-id="1f2b8-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1f2b8-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="1f2b8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1f2b8-121">FreshGrade uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1f2b8-121">Adding FreshGrade from the gallery</span></span>
2. <span data-ttu-id="1f2b8-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1f2b8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshgrade-from-the-gallery"></a><span data-ttu-id="1f2b8-123">FreshGrade uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="1f2b8-123">Adding FreshGrade from the gallery</span></span>
<span data-ttu-id="1f2b8-124">Voor het configureren van de integratie van FreshGrade in Azure AD, moet u FreshGrade uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-124">To configure the integration of FreshGrade into Azure AD, you need to add FreshGrade from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1f2b8-125">**Als u wilt toevoegen FreshGrade uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1f2b8-125">**To add FreshGrade from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1f2b8-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1f2b8-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1f2b8-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="1f2b8-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="1f2b8-133">Typ in het zoekvak **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-133">In the search box, type **FreshGrade**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_search.png)

5. <span data-ttu-id="1f2b8-135">Selecteer in het deelvenster resultaten **FreshGrade**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-135">In the results panel, select **FreshGrade**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1f2b8-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1f2b8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1f2b8-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met FreshGrade op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-138">In this section, you configure and test Azure AD single sign-on with FreshGrade based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1f2b8-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in FreshGrade is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshGrade is to a user in Azure AD.</span></span> <span data-ttu-id="1f2b8-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in FreshGrade tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-140">In other words, a link relationship between an Azure AD user and the related user in FreshGrade needs to be established.</span></span>

<span data-ttu-id="1f2b8-141">Wijs in FreshGrade, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-141">In FreshGrade, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1f2b8-142">Om te configureren en testen van Azure AD eenmalige aanmelding met FreshGrade, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="1f2b8-142">To configure and test Azure AD single sign-on with FreshGrade, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1f2b8-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1f2b8-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1f2b8-145">**[Maken van een testgebruiker FreshGrade](#creating-a-freshgrade-test-user)**  - FreshGrade die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-145">**[Creating a FreshGrade test user](#creating-a-freshgrade-test-user)** - to have a counterpart of Britta Simon in FreshGrade that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1f2b8-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1f2b8-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1f2b8-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="1f2b8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1f2b8-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing FreshGrade configureren.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FreshGrade application.</span></span>

<span data-ttu-id="1f2b8-150">**Voor het configureren van Azure AD eenmalige aanmelding met FreshGrade, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1f2b8-150">**To configure Azure AD single sign-on with FreshGrade, perform the following steps:**</span></span>

1. <span data-ttu-id="1f2b8-151">In de Azure-portal op de **FreshGrade** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-151">In the Azure portal, on the **FreshGrade** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="1f2b8-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_samlbase.png)

3. <span data-ttu-id="1f2b8-155">Op de **FreshGrade domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1f2b8-155">On the **FreshGrade Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_url.png)

    <span data-ttu-id="1f2b8-157">a.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-157">a.</span></span> <span data-ttu-id="1f2b8-158">In de **aanmeldings-URL** textbox, typ een URL met de volgende patronen:</span><span class="sxs-lookup"><span data-stu-id="1f2b8-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
      | |
      |--|
      | `https://<subdomain>.freshgrade.com/login` |    
      | `https://<subdomain>.onboarding.freshgrade.com/login` |

    <span data-ttu-id="1f2b8-159">b.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-159">b.</span></span> <span data-ttu-id="1f2b8-160">In de **id** textbox, typ een URL met de volgende patronen:</span><span class="sxs-lookup"><span data-stu-id="1f2b8-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
      | |
      |--|
      | `https://login.onboarding.freshgrade.com:443/saml/metadata/alias/<instancename>` |      
      | `https://login.freshgrade.com:443/saml/metadata/alias/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="1f2b8-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-161">These values are not real.</span></span> <span data-ttu-id="1f2b8-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1f2b8-163">Neem contact op met [FreshGrade Client ondersteuningsteam](mailTo:support@freshgrade.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-163">Contact [FreshGrade Client support team](mailTo:support@freshgrade.com) to get these values.</span></span> 
 


4. <span data-ttu-id="1f2b8-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_certificate.png) 

5. <span data-ttu-id="1f2b8-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshgrade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1f2b8-168">Op de **FreshGrade configuratie** sectie, klikt u op **configureren FreshGrade** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-168">On the **FreshGrade Configuration** section, click **Configure FreshGrade** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1f2b8-169">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="1f2b8-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_configure.png) 

7. <span data-ttu-id="1f2b8-171">Voor het genereren van de **metagegevens** -url, de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1f2b8-171">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="1f2b8-172">a.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-172">a.</span></span> <span data-ttu-id="1f2b8-173">Klik op **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-173">Click **App registrations**.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appregistrations.png)
   
    <span data-ttu-id="1f2b8-175">b.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-175">b.</span></span> <span data-ttu-id="1f2b8-176">Klik op **eindpunten** openen **eindpunten** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-176">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpointicon.png)

    <span data-ttu-id="1f2b8-178">c.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-178">c.</span></span> <span data-ttu-id="1f2b8-179">Klik op de knop kopiëren om te kopiëren **DOCUMENT met federatieve metagegevens** url en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-179">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpoint.png)
     
    <span data-ttu-id="1f2b8-181">d.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-181">d.</span></span> <span data-ttu-id="1f2b8-182">Nu gaat u naar de eigenschappenpagina van **FreshGrade** en kopieer de **toepassings-Id** met **kopie** knop en plak deze in Kladblok.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-182">Now go to the property page of **FreshGrade** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appid.png)

    <span data-ttu-id="1f2b8-184">e.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-184">e.</span></span> <span data-ttu-id="1f2b8-185">Genereren van de **metagegevens-URL** met het volgende patroon volgen:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="1f2b8-185">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

8. <span data-ttu-id="1f2b8-186">Eenmalige aanmelding configureren op **FreshGrade** kant die u wilt verzenden de **metagegevens-URL** en **SAML Single Sign-On Service-URL** naar [FreshGrade ondersteuningsteam](mailTo:support@freshgrade.com).</span><span class="sxs-lookup"><span data-stu-id="1f2b8-186">To configure single sign-on on **FreshGrade** side, you need to send the **Metadata URL** and **SAML Single Sign-On Service URL** to [FreshGrade support team](mailTo:support@freshgrade.com).</span></span> <span data-ttu-id="1f2b8-187">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-187">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1f2b8-188">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="1f2b8-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1f2b8-189">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1f2b8-190">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1f2b8-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1f2b8-191">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="1f2b8-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="1f2b8-192">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="1f2b8-194">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1f2b8-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1f2b8-195">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1f2b8-197">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1f2b8-199">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1f2b8-201">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1f2b8-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1f2b8-203">a.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-203">a.</span></span> <span data-ttu-id="1f2b8-204">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1f2b8-205">b.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-205">b.</span></span> <span data-ttu-id="1f2b8-206">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1f2b8-207">c.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-207">c.</span></span> <span data-ttu-id="1f2b8-208">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1f2b8-209">d.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-209">d.</span></span> <span data-ttu-id="1f2b8-210">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-210">Click **Create**.</span></span>
 
### <a name="creating-a-freshgrade-test-user"></a><span data-ttu-id="1f2b8-211">Een testgebruiker FreshGrade maken</span><span class="sxs-lookup"><span data-stu-id="1f2b8-211">Creating a FreshGrade test user</span></span>

<span data-ttu-id="1f2b8-212">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in FreshGrade maken.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-212">In this section, you create a user called Britta Simon in FreshGrade.</span></span> <span data-ttu-id="1f2b8-213">Neem contact op met [FreshGrade ondersteuningsteam](mailTo:support@freshgrade.com) de gebruikers van het platform FreshGrade toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-213">Please work with [FreshGrade support team](mailTo:support@freshgrade.com) to add the users in the FreshGrade platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1f2b8-214">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f2b8-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1f2b8-215">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FreshGrade.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="1f2b8-217">**Britta Simon om aan te wijzen FreshGrade, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="1f2b8-217">**To assign Britta Simon to FreshGrade, perform the following steps:**</span></span>

1. <span data-ttu-id="1f2b8-218">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="1f2b8-220">Selecteer in de lijst met toepassingen **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-220">In the applications list, select **FreshGrade**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_app.png) 

3. <span data-ttu-id="1f2b8-222">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="1f2b8-224">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-224">Click **Add** button.</span></span> <span data-ttu-id="1f2b8-225">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="1f2b8-227">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1f2b8-228">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1f2b8-229">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1f2b8-230">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1f2b8-230">Testing single sign-on</span></span>

<span data-ttu-id="1f2b8-231">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1f2b8-232">Als u op de tegel FreshGrade in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="1f2b8-232">When you click the FreshGrade tile in the Access Panel, you should get automatically signed-on to your FreshGrade application.</span></span>
<span data-ttu-id="1f2b8-233">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1f2b8-233">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1f2b8-234">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="1f2b8-234">Additional resources</span></span>

* [<span data-ttu-id="1f2b8-235">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f2b8-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1f2b8-236">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1f2b8-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_203.png

