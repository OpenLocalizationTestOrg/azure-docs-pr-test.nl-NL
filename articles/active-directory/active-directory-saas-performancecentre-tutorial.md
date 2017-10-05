---
title: 'Zelfstudie: Azure Active Directory-integratie met PerformanceCentre | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en PerformanceCentre.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: e86adaf4bd9b4752f2aece8207a8a423ec5590a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a><span data-ttu-id="38de5-103">Zelfstudie: Azure Active Directory-integratie met PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="38de5-103">Tutorial: Azure Active Directory integration with PerformanceCentre</span></span>

<span data-ttu-id="38de5-104">In deze zelfstudie leert u hoe PerformanceCentre integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="38de5-104">In this tutorial, you learn how to integrate PerformanceCentre with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="38de5-105">PerformanceCentre integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="38de5-105">Integrating PerformanceCentre with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="38de5-106">U kunt beheren in Azure AD die toegang tot PerformanceCentre heeft</span><span class="sxs-lookup"><span data-stu-id="38de5-106">You can control in Azure AD who has access to PerformanceCentre</span></span>
- <span data-ttu-id="38de5-107">U kunt uw gebruikers automatisch ophalen aangemeld bij PerformanceCentre (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="38de5-107">You can enable your users to automatically get signed-on to PerformanceCentre (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="38de5-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="38de5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="38de5-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="38de5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38de5-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="38de5-110">Prerequisites</span></span>

<span data-ttu-id="38de5-111">Voor het configureren van Azure AD-integratie met PerformanceCentre, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="38de5-111">To configure Azure AD integration with PerformanceCentre, you need the following items:</span></span>

- <span data-ttu-id="38de5-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="38de5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="38de5-113">Een PerformanceCentre eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="38de5-113">A PerformanceCentre single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="38de5-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="38de5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="38de5-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="38de5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="38de5-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="38de5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="38de5-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="38de5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="38de5-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="38de5-118">Scenario description</span></span>
<span data-ttu-id="38de5-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="38de5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="38de5-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="38de5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="38de5-121">PerformanceCentre uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="38de5-121">Adding PerformanceCentre from the gallery</span></span>
2. <span data-ttu-id="38de5-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="38de5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-performancecentre-from-the-gallery"></a><span data-ttu-id="38de5-123">PerformanceCentre uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="38de5-123">Adding PerformanceCentre from the gallery</span></span>
<span data-ttu-id="38de5-124">Voor het configureren van de integratie van PerformanceCentre in Azure AD, moet u PerformanceCentre uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="38de5-124">To configure the integration of PerformanceCentre into Azure AD, you need to add PerformanceCentre from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="38de5-125">**Als u wilt toevoegen PerformanceCentre uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="38de5-125">**To add PerformanceCentre from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="38de5-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="38de5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="38de5-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="38de5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="38de5-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="38de5-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="38de5-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="38de5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="38de5-133">Typ in het zoekvak **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="38de5-133">In the search box, type **PerformanceCentre**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_search.png)

5. <span data-ttu-id="38de5-135">Selecteer in het deelvenster resultaten **PerformanceCentre**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="38de5-135">In the results panel, select **PerformanceCentre**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="38de5-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="38de5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="38de5-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met PerformanceCentre op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="38de5-138">In this section, you configure and test Azure AD single sign-on with PerformanceCentre based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="38de5-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in PerformanceCentre is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38de5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PerformanceCentre is to a user in Azure AD.</span></span> <span data-ttu-id="38de5-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in PerformanceCentre tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="38de5-140">In other words, a link relationship between an Azure AD user and the related user in PerformanceCentre needs to be established.</span></span>

<span data-ttu-id="38de5-141">Wijs in PerformanceCentre, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="38de5-141">In PerformanceCentre, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="38de5-142">Om te configureren en testen van Azure AD eenmalige aanmelding met PerformanceCentre, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="38de5-142">To configure and test Azure AD single sign-on with PerformanceCentre, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="38de5-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="38de5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="38de5-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="38de5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="38de5-145">**[Maken van een testgebruiker PerformanceCentre](#creating-a-performancecentre-test-user)**  - PerformanceCentre die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="38de5-145">**[Creating a PerformanceCentre test user](#creating-a-performancecentre-test-user)** - to have a counterpart of Britta Simon in PerformanceCentre that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="38de5-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="38de5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="38de5-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="38de5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="38de5-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="38de5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="38de5-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing PerformanceCentre configureren.</span><span class="sxs-lookup"><span data-stu-id="38de5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PerformanceCentre application.</span></span>

<span data-ttu-id="38de5-150">**Voor het configureren van Azure AD eenmalige aanmelding met PerformanceCentre, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="38de5-150">**To configure Azure AD single sign-on with PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="38de5-151">In de Azure-portal op de **PerformanceCentre** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="38de5-151">In the Azure portal, on the **PerformanceCentre** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="38de5-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="38de5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_samlbase.png)

3. <span data-ttu-id="38de5-155">Op de **PerformanceCentre domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="38de5-155">On the **PerformanceCentre Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_url.png)

    <span data-ttu-id="38de5-157">a.</span><span class="sxs-lookup"><span data-stu-id="38de5-157">a.</span></span> <span data-ttu-id="38de5-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`http://companyname.performancecentre.com/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="38de5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://companyname.performancecentre.com/saml/SSO`</span></span>

    <span data-ttu-id="38de5-159">b.</span><span class="sxs-lookup"><span data-stu-id="38de5-159">b.</span></span> <span data-ttu-id="38de5-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`http://companyname.performancecentre.com`</span><span class="sxs-lookup"><span data-stu-id="38de5-160">In the **Identifier** textbox, type a URL using the following pattern: `http://companyname.performancecentre.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="38de5-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="38de5-161">These values are not real.</span></span> <span data-ttu-id="38de5-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="38de5-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="38de5-163">Neem contact op met [PerformanceCentre Client ondersteuningsteam](https://www.performancecentre.com/contact-us/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="38de5-163">Contact [PerformanceCentre Client support team](https://www.performancecentre.com/contact-us/) to get these values.</span></span> 

4. <span data-ttu-id="38de5-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="38de5-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_certificate.png) 

5. <span data-ttu-id="38de5-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="38de5-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-performancecentre-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="38de5-168">Op de **PerformanceCentre configuratie** sectie, klikt u op **configureren PerformanceCentre** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="38de5-168">On the **PerformanceCentre Configuration** section, click **Configure PerformanceCentre** to open **Configure sign-on** window.</span></span> <span data-ttu-id="38de5-169">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="38de5-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_configure.png) 

7. <span data-ttu-id="38de5-171">Aanmelding bij uw **PerformanceCentre** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="38de5-171">Sign-on to your **PerformanceCentre** company site as administrator.</span></span>

8. <span data-ttu-id="38de5-172">Klik op het tabblad aan de linkerkant **configureren**.</span><span class="sxs-lookup"><span data-stu-id="38de5-172">In the tab on the left side, click **Configure**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][10]

9. <span data-ttu-id="38de5-174">Klik op het tabblad aan de linkerkant **overige**, en klik vervolgens op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="38de5-174">In the tab on the left side, click **Miscellaneous**, and then click **Single Sign On**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][11]

10. <span data-ttu-id="38de5-176">Als **Protocol**, selecteer **SAML**.</span><span class="sxs-lookup"><span data-stu-id="38de5-176">As **Protocol**, select **SAML**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][12]

11. <span data-ttu-id="38de5-178">Open de van het gedownloade metagegevensbestand in Kladblok, Kopieer de inhoud, plakt u deze in de **identiteit Provider metagegevens** tekstvak en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="38de5-178">Open your downloaded metadata file in notepad, copy the content, paste it into the **Identity Provider Metadata** textbox, and then click **Save**.</span></span>
   
    ![Azure AD voor eenmalige aanmelding][13]

12. <span data-ttu-id="38de5-180">Controleer de waarden voor de **entiteit basis-URL** en **entiteit-ID URL** juist zijn.</span><span class="sxs-lookup"><span data-stu-id="38de5-180">Verify that the values for the **Entity Base URL** and **Entity ID URL** are correct.</span></span>
    
     ![Azure AD voor eenmalige aanmelding][14]

> [!TIP]
> <span data-ttu-id="38de5-182">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="38de5-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="38de5-183">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="38de5-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="38de5-184">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="38de5-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="38de5-185">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="38de5-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="38de5-186">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="38de5-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="38de5-188">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="38de5-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="38de5-189">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="38de5-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="38de5-191">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="38de5-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="38de5-193">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="38de5-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="38de5-195">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="38de5-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="38de5-197">a.</span><span class="sxs-lookup"><span data-stu-id="38de5-197">a.</span></span> <span data-ttu-id="38de5-198">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="38de5-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="38de5-199">b.</span><span class="sxs-lookup"><span data-stu-id="38de5-199">b.</span></span> <span data-ttu-id="38de5-200">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="38de5-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="38de5-201">c.</span><span class="sxs-lookup"><span data-stu-id="38de5-201">c.</span></span> <span data-ttu-id="38de5-202">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="38de5-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="38de5-203">d.</span><span class="sxs-lookup"><span data-stu-id="38de5-203">d.</span></span> <span data-ttu-id="38de5-204">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="38de5-204">Click **Create**.</span></span>
 
### <a name="creating-a-performancecentre-test-user"></a><span data-ttu-id="38de5-205">Een testgebruiker PerformanceCentre maken</span><span class="sxs-lookup"><span data-stu-id="38de5-205">Creating a PerformanceCentre test user</span></span>

<span data-ttu-id="38de5-206">Het doel van deze sectie is het maken van een gebruiker Britta Simon in PerformanceCentre genoemd.</span><span class="sxs-lookup"><span data-stu-id="38de5-206">The objective of this section is to create a user called Britta Simon in PerformanceCentre.</span></span>

<span data-ttu-id="38de5-207">**Als u wilt een gebruiker Britta Simon aangeroepen in PerformanceCentre maakt, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="38de5-207">**To create a user called Britta Simon in PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="38de5-208">Meld u op met uw bedrijf PerformanceCentre site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="38de5-208">Sign on to your PerformanceCentre company site as administrator.</span></span>

2. <span data-ttu-id="38de5-209">Klik in het menu aan de linkerkant op **Interrelate**, en klik vervolgens op **maken deelnemer**.</span><span class="sxs-lookup"><span data-stu-id="38de5-209">In the menu on the left, click **Interrelate**, and then click **Create Participant**.</span></span>
   
    ![Gebruiker maken][400]

3. <span data-ttu-id="38de5-211">Op de **is de relatie tussen - deelnemer maken** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="38de5-211">On the **Interrelate - Create Participant** dialog, perform the following steps:</span></span>
   
    ![Gebruiker maken][401]
    
    <span data-ttu-id="38de5-213">a.</span><span class="sxs-lookup"><span data-stu-id="38de5-213">a.</span></span> <span data-ttu-id="38de5-214">Typ de vereiste kenmerken voor Britta Simon in de bijbehorende tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="38de5-214">Type the required attributes for Britta Simon into related textboxes.</span></span>
    
    >[!IMPORTANT]
    ><span data-ttu-id="38de5-215">Kenmerk van de gebruikersnaam van Britta in PerformanceCentre moet hetzelfde zijn als de gebruikersnaam in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38de5-215">Britta's User Name attribute in PerformanceCentre must be the same as the User Name in Azure AD.</span></span>
    
    <span data-ttu-id="38de5-216">b.</span><span class="sxs-lookup"><span data-stu-id="38de5-216">b.</span></span> <span data-ttu-id="38de5-217">Selecteer **Client Administrator** als **Kies rol**.</span><span class="sxs-lookup"><span data-stu-id="38de5-217">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="38de5-218">c.</span><span class="sxs-lookup"><span data-stu-id="38de5-218">c.</span></span> <span data-ttu-id="38de5-219">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="38de5-219">Click **Save**.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="38de5-220">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="38de5-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="38de5-221">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="38de5-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PerformanceCentre.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="38de5-223">**Britta Simon om aan te wijzen PerformanceCentre, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="38de5-223">**To assign Britta Simon to PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="38de5-224">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="38de5-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="38de5-226">Selecteer in de lijst met toepassingen **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="38de5-226">In the applications list, select **PerformanceCentre**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_app.png) 

3. <span data-ttu-id="38de5-228">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="38de5-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="38de5-230">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="38de5-230">Click **Add** button.</span></span> <span data-ttu-id="38de5-231">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="38de5-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="38de5-233">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="38de5-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="38de5-234">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="38de5-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="38de5-235">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="38de5-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="38de5-236">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="38de5-236">Testing single sign-on</span></span>

<span data-ttu-id="38de5-237">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="38de5-237">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="38de5-238">Als u op de tegel PerformanceCentre in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="38de5-238">When you click the PerformanceCentre tile in the Access Panel, you should get automatically signed-on to your PerformanceCentre application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="38de5-239">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="38de5-239">Additional resources</span></span>

* [<span data-ttu-id="38de5-240">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="38de5-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="38de5-241">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="38de5-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png

[100]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png

