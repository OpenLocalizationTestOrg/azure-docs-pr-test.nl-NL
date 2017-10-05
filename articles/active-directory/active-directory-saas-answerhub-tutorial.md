---
title: 'Zelfstudie: Azure Active Directory-integratie met AnswerHub | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en AnswerHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 3a1c9cc5d7a2ebe28e9fb7e0e6ed8e3d393873ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="b8dae-103">Zelfstudie: Azure Active Directory-integratie met AnswerHub</span><span class="sxs-lookup"><span data-stu-id="b8dae-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="b8dae-104">In deze zelfstudie leert u hoe AnswerHub integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b8dae-104">In this tutorial, you learn how to integrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b8dae-105">AnswerHub integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b8dae-105">Integrating AnswerHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b8dae-106">U kunt beheren in Azure AD die toegang tot AnswerHub heeft</span><span class="sxs-lookup"><span data-stu-id="b8dae-106">You can control in Azure AD who has access to AnswerHub</span></span>
- <span data-ttu-id="b8dae-107">U kunt uw gebruikers automatisch ophalen aangemeld bij AnswerHub (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="b8dae-107">You can enable your users to automatically get signed-on to AnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b8dae-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b8dae-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b8dae-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b8dae-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8dae-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b8dae-110">Prerequisites</span></span>

<span data-ttu-id="b8dae-111">Voor het configureren van Azure AD-integratie met AnswerHub, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b8dae-111">To configure Azure AD integration with AnswerHub, you need the following items:</span></span>

- <span data-ttu-id="b8dae-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b8dae-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b8dae-113">Een AnswerHub eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b8dae-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b8dae-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b8dae-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b8dae-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b8dae-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b8dae-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b8dae-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b8dae-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b8dae-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b8dae-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b8dae-118">Scenario description</span></span>
<span data-ttu-id="b8dae-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b8dae-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b8dae-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b8dae-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b8dae-121">AnswerHub uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b8dae-121">Adding AnswerHub from the gallery</span></span>
2. <span data-ttu-id="b8dae-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b8dae-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-the-gallery"></a><span data-ttu-id="b8dae-123">AnswerHub uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b8dae-123">Adding AnswerHub from the gallery</span></span>
<span data-ttu-id="b8dae-124">Voor het configureren van de integratie van AnswerHub in Azure AD, moet u AnswerHub uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b8dae-124">To configure the integration of AnswerHub into Azure AD, you need to add AnswerHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b8dae-125">**Als u wilt toevoegen AnswerHub uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b8dae-125">**To add AnswerHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b8dae-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b8dae-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b8dae-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b8dae-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="b8dae-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b8dae-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="b8dae-133">Typ in het zoekvak **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-133">In the search box, type **AnswerHub**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="b8dae-135">Selecteer in het deelvenster resultaten **AnswerHub**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b8dae-135">In the results panel, select **AnswerHub**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b8dae-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b8dae-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b8dae-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met AnswerHub op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b8dae-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b8dae-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in AnswerHub is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8dae-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AnswerHub is to a user in Azure AD.</span></span> <span data-ttu-id="b8dae-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in AnswerHub tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="b8dae-140">In other words, a link relationship between an Azure AD user and the related user in AnswerHub needs to be established.</span></span>

<span data-ttu-id="b8dae-141">Wijs in AnswerHub, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="b8dae-141">In AnswerHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b8dae-142">Om te configureren en testen van Azure AD eenmalige aanmelding met AnswerHub, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="b8dae-142">To configure and test Azure AD single sign-on with AnswerHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b8dae-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b8dae-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b8dae-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8dae-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b8dae-145">**[Maken van een testgebruiker AnswerHub](#creating-an-answerhub-test-user)**  - AnswerHub die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="b8dae-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - to have a counterpart of Britta Simon in AnswerHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b8dae-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b8dae-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b8dae-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b8dae-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b8dae-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b8dae-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b8dae-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing AnswerHub configureren.</span><span class="sxs-lookup"><span data-stu-id="b8dae-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="b8dae-150">**Voor het configureren van Azure AD eenmalige aanmelding met AnswerHub, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b8dae-150">**To configure Azure AD single sign-on with AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="b8dae-151">In de Azure-portal op de **AnswerHub** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-151">In the Azure portal, on the **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b8dae-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b8dae-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="b8dae-155">Op de **AnswerHub domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b8dae-155">On the **AnswerHub Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="b8dae-157">a.</span><span class="sxs-lookup"><span data-stu-id="b8dae-157">a.</span></span> <span data-ttu-id="b8dae-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="b8dae-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="b8dae-159">b.</span><span class="sxs-lookup"><span data-stu-id="b8dae-159">b.</span></span> <span data-ttu-id="b8dae-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="b8dae-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b8dae-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="b8dae-161">These values are not real.</span></span> <span data-ttu-id="b8dae-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="b8dae-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b8dae-163">Neem contact op met [AnswerHub Client ondersteuningsteam](mailto:success@answerhub.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="b8dae-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) to get these values.</span></span> 
 
4. <span data-ttu-id="b8dae-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b8dae-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="b8dae-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b8dae-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b8dae-168">Op de **AnswerHub configuratie** sectie, klikt u op **configureren AnswerHub** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="b8dae-168">On the **AnswerHub Configuration** section, click **Configure AnswerHub** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b8dae-169">Kopieer de **Sign-Out URL's, en SAML Single Sign-On Service** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="b8dae-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="b8dae-171">In een ander browservenster, meld u bij uw bedrijf AnswerHub site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b8dae-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="b8dae-172">Als u nodig hebt bij het configureren van AnswerHub, neem dan contact op met [ondersteuningsteam van AnswerHub](mailto:success@answerhub.com.).</span><span class="sxs-lookup"><span data-stu-id="b8dae-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="b8dae-173">Ga naar **beheer**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-173">Go to **Administration**.</span></span>

9. <span data-ttu-id="b8dae-174">Klik op de **gebruikers en groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="b8dae-174">Click the **User and Group** tab.</span></span>

10. <span data-ttu-id="b8dae-175">Klik in het navigatievenster aan de linkerkant in de **sociale instellingen** sectie, klikt u op **SAML Setup**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-175">In the navigation pane on the left side, in the **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="b8dae-176">Klik op **IDP Config** tabblad.</span><span class="sxs-lookup"><span data-stu-id="b8dae-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="b8dae-177">Op de **IDP Config** tabblad, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b8dae-177">On the **IDP Config** tab, perform the following steps:</span></span>

     <span data-ttu-id="b8dae-178">![Setup van SAML](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span><span class="sxs-lookup"><span data-stu-id="b8dae-178">![SAML Setup](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="b8dae-179">a.</span><span class="sxs-lookup"><span data-stu-id="b8dae-179">a.</span></span> <span data-ttu-id="b8dae-180">In **IDP aanmeldings-URL** textbox plakken **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b8dae-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="b8dae-181">b.</span><span class="sxs-lookup"><span data-stu-id="b8dae-181">b.</span></span> <span data-ttu-id="b8dae-182">In **IDP afmelding URL** textbox plakken **Sign-Out URL** waarde die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b8dae-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="b8dae-183">c.</span><span class="sxs-lookup"><span data-stu-id="b8dae-183">c.</span></span> <span data-ttu-id="b8dae-184">In **IDP-naamnotatie id** textbox, voert u de gebruiker id dezelfde waarde als de geselecteerde in Azure-portal op **gebruikerskenmerken** sectie.</span><span class="sxs-lookup"><span data-stu-id="b8dae-184">In **IDP Name Identifier Format** textbox, enter the user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="b8dae-185">d.</span><span class="sxs-lookup"><span data-stu-id="b8dae-185">d.</span></span> <span data-ttu-id="b8dae-186">Klik op **sleutels en certificaten**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="b8dae-187">Voer de volgende stappen uit op het tabblad sleutels en certificaten:</span><span class="sxs-lookup"><span data-stu-id="b8dae-187">On the Keys and Certificates tab, perform the following steps:</span></span>
    
     <span data-ttu-id="b8dae-188">![Sleutels en certificaten](./media/active-directory-saas-answerhub-tutorial/ic785173.png "sleutels en certificaten")</span><span class="sxs-lookup"><span data-stu-id="b8dae-188">![Keys and Certificates](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="b8dae-189">a.</span><span class="sxs-lookup"><span data-stu-id="b8dae-189">a.</span></span> <span data-ttu-id="b8dae-190">Open uw base-64 gecodeerde certificaat dat u hebt gedownload vanuit Azure-portal in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **IDP openbare sleutel (x 509-indeling)** textbox.</span><span class="sxs-lookup"><span data-stu-id="b8dae-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="b8dae-191">b.</span><span class="sxs-lookup"><span data-stu-id="b8dae-191">b.</span></span> <span data-ttu-id="b8dae-192">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-192">Click **Save**.</span></span>

14. <span data-ttu-id="b8dae-193">Op de **IDP Config** tabblad **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-193">On the **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b8dae-194">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="b8dae-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b8dae-195">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="b8dae-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b8dae-196">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b8dae-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b8dae-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b8dae-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="b8dae-198">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b8dae-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="b8dae-200">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b8dae-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b8dae-201">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b8dae-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b8dae-203">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b8dae-205">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b8dae-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b8dae-207">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b8dae-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b8dae-209">a.</span><span class="sxs-lookup"><span data-stu-id="b8dae-209">a.</span></span> <span data-ttu-id="b8dae-210">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b8dae-211">b.</span><span class="sxs-lookup"><span data-stu-id="b8dae-211">b.</span></span> <span data-ttu-id="b8dae-212">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b8dae-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b8dae-213">c.</span><span class="sxs-lookup"><span data-stu-id="b8dae-213">c.</span></span> <span data-ttu-id="b8dae-214">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b8dae-215">d.</span><span class="sxs-lookup"><span data-stu-id="b8dae-215">d.</span></span> <span data-ttu-id="b8dae-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="b8dae-217">Een testgebruiker AnswerHub maken</span><span class="sxs-lookup"><span data-stu-id="b8dae-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="b8dae-218">Om Azure AD-gebruikers zich aanmelden bij AnswerHub, moeten ze worden ingericht in AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="b8dae-218">To enable Azure AD users to log in to AnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="b8dae-219">In het geval van AnswerHub is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="b8dae-219">In the case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="b8dae-220">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b8dae-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="b8dae-221">Meld u aan bij uw **AnswerHub** bedrijf site als administrator.</span><span class="sxs-lookup"><span data-stu-id="b8dae-221">Log in to your **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="b8dae-222">Ga naar **beheer**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-222">Go to **Administration**.</span></span>

3. <span data-ttu-id="b8dae-223">Klik op de **gebruikers en groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="b8dae-223">Click the **Users & Groups** tab.</span></span>

4. <span data-ttu-id="b8dae-224">Klik in het navigatievenster aan de linkerkant in de **gebruikers beheren** sectie, klikt u op **maken of importeren gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-224">In the navigation pane on the left side, in the **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="b8dae-225">![Gebruikers en groepen](./media/active-directory-saas-answerhub-tutorial/ic785175.png "gebruikers en groepen")</span><span class="sxs-lookup"><span data-stu-id="b8dae-225">![Users & Groups](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="b8dae-226">Typ de **e-mailadres**, **gebruikersnaam** en **wachtwoord** van een geldige Azure Active Directory-account die u wilt inrichten in de bijbehorende tekstvakken en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-226">Type the **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want to provision into the related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="b8dae-227">U kunt andere AnswerHub gebruiker account hulpmiddelen voor het maken of API's die is geleverd door AnswerHub aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="b8dae-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b8dae-228">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8dae-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b8dae-229">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="b8dae-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AnswerHub.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b8dae-231">**Britta Simon om aan te wijzen AnswerHub, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b8dae-231">**To assign Britta Simon to AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="b8dae-232">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b8dae-234">Selecteer in de lijst met toepassingen **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-234">In the applications list, select **AnswerHub**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="b8dae-236">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b8dae-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="b8dae-238">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b8dae-238">Click **Add** button.</span></span> <span data-ttu-id="b8dae-239">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b8dae-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="b8dae-241">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b8dae-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b8dae-242">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b8dae-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b8dae-243">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b8dae-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b8dae-244">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b8dae-244">Testing single sign-on</span></span>

<span data-ttu-id="b8dae-245">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b8dae-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b8dae-246">Als u op de tegel AnswerHub in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="b8dae-246">When you click the AnswerHub tile in the Access Panel, you should get automatically signed-on to your AnswerHub application.</span></span>
<span data-ttu-id="b8dae-247">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b8dae-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b8dae-248">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b8dae-248">Additional resources</span></span>

* [<span data-ttu-id="b8dae-249">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b8dae-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b8dae-250">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b8dae-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

