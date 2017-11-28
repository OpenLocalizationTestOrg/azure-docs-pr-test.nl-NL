---
title: 'Zelfstudie: Azure Active Directory-integratie met Proofpoint op verzoek | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Proofpoint op aanvraag.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: b4c8d8c187fc865a905016f04a41843894249f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="90ad6-103">Zelfstudie: Azure Active Directory-integratie met Proofpoint op aanvraag</span><span class="sxs-lookup"><span data-stu-id="90ad6-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="90ad6-104">In deze zelfstudie leert u hoe Proofpoint op verzoek integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="90ad6-104">In this tutorial, you learn how to integrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="90ad6-105">Proofpoint op verzoek integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="90ad6-105">Integrating Proofpoint on Demand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="90ad6-106">U kunt beheren in Azure AD die toegang tot Proofpoint op aanvraag heeft</span><span class="sxs-lookup"><span data-stu-id="90ad6-106">You can control in Azure AD who has access to Proofpoint on Demand</span></span>
- <span data-ttu-id="90ad6-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Proofpoint op verzoek (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="90ad6-107">You can enable your users to automatically get signed-on to Proofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="90ad6-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="90ad6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="90ad6-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="90ad6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90ad6-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="90ad6-110">Prerequisites</span></span>

<span data-ttu-id="90ad6-111">Voor het configureren van Azure AD-integratie met Proofpoint op verzoek, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="90ad6-111">To configure Azure AD integration with Proofpoint on Demand, you need the following items:</span></span>

- <span data-ttu-id="90ad6-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="90ad6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="90ad6-113">Een Proofpoint op verzoek-eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="90ad6-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="90ad6-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="90ad6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="90ad6-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="90ad6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="90ad6-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="90ad6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="90ad6-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="90ad6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="90ad6-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="90ad6-118">Scenario description</span></span>
<span data-ttu-id="90ad6-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="90ad6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="90ad6-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="90ad6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="90ad6-121">Proofpoint op verzoek vanuit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="90ad6-121">Adding Proofpoint on Demand from the gallery</span></span>
2. <span data-ttu-id="90ad6-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="90ad6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-the-gallery"></a><span data-ttu-id="90ad6-123">Proofpoint op verzoek vanuit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="90ad6-123">Adding Proofpoint on Demand from the gallery</span></span>
<span data-ttu-id="90ad6-124">Als u wilt de integratie van Proofpoint op verzoek configureren in Azure AD, moet u Proofpoint op verzoek vanuit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="90ad6-124">To configure the integration of Proofpoint on Demand into Azure AD, you need to add Proofpoint on Demand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="90ad6-125">**Als u wilt toevoegen Proofpoint op verzoek vanuit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="90ad6-125">**To add Proofpoint on Demand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="90ad6-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="90ad6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="90ad6-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="90ad6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="90ad6-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="90ad6-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="90ad6-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="90ad6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="90ad6-133">Typ in het zoekvak **Proofpoint op verzoek**.</span><span class="sxs-lookup"><span data-stu-id="90ad6-133">In the search box, type **Proofpoint on Demand**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="90ad6-135">Selecteer in het deelvenster resultaten **Proofpoint op verzoek**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="90ad6-135">In the results panel, select **Proofpoint on Demand**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="90ad6-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="90ad6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="90ad6-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Proofpoint op verzoek op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="90ad6-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="90ad6-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Proofpoint op verzoek is naar een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90ad6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Proofpoint on Demand is to a user in Azure AD.</span></span> <span data-ttu-id="90ad6-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Proofpoint op verzoek tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="90ad6-140">In other words, a link relationship between an Azure AD user and the related user in Proofpoint on Demand needs to be established.</span></span>

<span data-ttu-id="90ad6-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Proofpoint op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="90ad6-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="90ad6-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Proofpoint op verzoek, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="90ad6-142">To configure and test Azure AD single sign-on with Proofpoint on Demand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="90ad6-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="90ad6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="90ad6-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="90ad6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="90ad6-145">**[Maken van een Proofpoint op aanvraag testgebruiker](#creating-a-proofpoint-on-demand-test-user)**  - Proofpoint op aanvraag die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="90ad6-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - to have a counterpart of Britta Simon in Proofpoint on Demand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="90ad6-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="90ad6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="90ad6-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="90ad6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="90ad6-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="90ad6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="90ad6-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw Proofpoint op verzoek-toepassing.</span><span class="sxs-lookup"><span data-stu-id="90ad6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="90ad6-150">**Voor het configureren van Azure AD eenmalige aanmelding met Proofpoint op verzoek, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="90ad6-150">**To configure Azure AD single sign-on with Proofpoint on Demand, perform the following steps:**</span></span>

1. <span data-ttu-id="90ad6-151">In de Azure-portal op de **Proofpoint op verzoek** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="90ad6-151">In the Azure portal, on the **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="90ad6-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="90ad6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
  
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="90ad6-155">Op de **Proofpoint op verzoek-domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="90ad6-155">On the **Proofpoint on Demand Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="90ad6-157">a.In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<hostname>.pphosted.com/ppssamlsp_hostname`</span><span class="sxs-lookup"><span data-stu-id="90ad6-157">a.In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="90ad6-158">b.</span><span class="sxs-lookup"><span data-stu-id="90ad6-158">b.</span></span> <span data-ttu-id="90ad6-159">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="90ad6-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="90ad6-160">c.</span><span class="sxs-lookup"><span data-stu-id="90ad6-160">c.</span></span>  <span data-ttu-id="90ad6-161">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span><span class="sxs-lookup"><span data-stu-id="90ad6-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="90ad6-162">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="90ad6-162">These values are not the real.</span></span> <span data-ttu-id="90ad6-163">Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL.</span><span class="sxs-lookup"><span data-stu-id="90ad6-163">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="90ad6-164">Neem contact op met [Proofpoint op aanvraag Client ondersteuningsteam](https://www.proofpoint.com/us/support-services) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="90ad6-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to get these values.</span></span> 

4. <span data-ttu-id="90ad6-165">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="90ad6-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="90ad6-167">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="90ad6-167">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="90ad6-169">Op de **Proofpoint op verzoek-configuratie** sectie, klikt u op **Proofpoint op verzoek configureren** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="90ad6-169">On the **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="90ad6-170">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="90ad6-170">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="90ad6-172">Eenmalige aanmelding configureren op **Proofpoint op verzoek** zijde, moet u de gedownloade verzenden **Certificate(Base64)**,**SAML entiteit-ID**, en **SAML Single Sign-On Service-URL** naar [Proofpoint op aanvraag Client ondersteuningsteam](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="90ad6-172">To configure single sign-on on **Proofpoint on Demand** side, you need to send the downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** to [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="90ad6-173">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="90ad6-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="90ad6-174">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="90ad6-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="90ad6-175">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="90ad6-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="90ad6-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="90ad6-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="90ad6-177">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="90ad6-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="90ad6-179">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="90ad6-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="90ad6-180">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="90ad6-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="90ad6-182">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="90ad6-182">These values are not the real.</span></span> <span data-ttu-id="90ad6-183">Deze waarden bijwerken met de werkelijke</span><span class="sxs-lookup"><span data-stu-id="90ad6-183">Update these values with the actual</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="90ad6-185">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="90ad6-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="90ad6-187">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="90ad6-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="90ad6-189">a.</span><span class="sxs-lookup"><span data-stu-id="90ad6-189">a.</span></span> <span data-ttu-id="90ad6-190">In de **naam** textbox type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="90ad6-190">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="90ad6-191">b.</span><span class="sxs-lookup"><span data-stu-id="90ad6-191">b.</span></span> <span data-ttu-id="90ad6-192">In de **gebruikersnaam** textbox type de **e-mailadres** van Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="90ad6-192">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="90ad6-193">c.</span><span class="sxs-lookup"><span data-stu-id="90ad6-193">c.</span></span> <span data-ttu-id="90ad6-194">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="90ad6-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="90ad6-195">d.</span><span class="sxs-lookup"><span data-stu-id="90ad6-195">d.</span></span> <span data-ttu-id="90ad6-196">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="90ad6-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="90ad6-197">Maken van een Proofpoint op aanvraag testgebruiker</span><span class="sxs-lookup"><span data-stu-id="90ad6-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="90ad6-198">In deze sectie maakt u Britta Simon aangeroepen in Proofpoint op verzoek van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="90ad6-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="90ad6-199">Werken met [Proofpoint op aanvraag Client ondersteuningsteam](https://www.proofpoint.com/us/support-services) gebruikers toevoegen in de Proofpoint op verzoek-platform.</span><span class="sxs-lookup"><span data-stu-id="90ad6-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to add users in the Proofpoint on Demand platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="90ad6-200">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="90ad6-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="90ad6-201">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Proofpoint op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="90ad6-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Proofpoint on Demand.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="90ad6-203">**Britta Simon om aan te wijzen Proofpoint op verzoek, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="90ad6-203">**To assign Britta Simon to Proofpoint on Demand, perform the following steps:**</span></span>

1. <span data-ttu-id="90ad6-204">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="90ad6-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="90ad6-206">Selecteer in de lijst met toepassingen **Proofpoint op verzoek**.</span><span class="sxs-lookup"><span data-stu-id="90ad6-206">In the applications list, select **Proofpoint on Demand**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="90ad6-208">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="90ad6-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="90ad6-210">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="90ad6-210">Click **Add** button.</span></span> <span data-ttu-id="90ad6-211">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="90ad6-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="90ad6-213">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="90ad6-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="90ad6-214">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="90ad6-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="90ad6-215">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="90ad6-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="90ad6-216">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="90ad6-216">Testing single sign-on</span></span>

<span data-ttu-id="90ad6-217">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="90ad6-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="90ad6-218">Wanneer u klikt op de **Proofpoint op verzoek** tegel op het toegangsvenster u moet ook automatisch aangemeld op naar uw Proofpoint op verzoek-toepassing.</span><span class="sxs-lookup"><span data-stu-id="90ad6-218">When you click the **Proofpoint on Demand** tile on the Access Panel, you should be automatically signed on to your Proofpoint on Demand application.</span></span>
<span data-ttu-id="90ad6-219">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="90ad6-219">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="90ad6-220">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="90ad6-220">Additional resources</span></span>

* [<span data-ttu-id="90ad6-221">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90ad6-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="90ad6-222">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="90ad6-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

