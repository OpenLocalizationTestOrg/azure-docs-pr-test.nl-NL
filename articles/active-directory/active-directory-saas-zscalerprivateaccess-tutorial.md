---
title: 'Zelfstudie: Azure Active Directory-integratie met Zscaler persoonlijke toegang (ZPA) | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Zscaler persoonlijke toegang (ZPA).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 5c598bfa5b6725d21a89df54dbcb3314cc631d80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a><span data-ttu-id="e8950-103">Zelfstudie: Azure Active Directory-integratie met Zscaler persoonlijke toegang (ZPA)</span><span class="sxs-lookup"><span data-stu-id="e8950-103">Tutorial: Azure Active Directory integration with Zscaler Private Access (ZPA)</span></span>

<span data-ttu-id="e8950-104">In deze zelfstudie leert u hoe Zscaler persoonlijke toegang (ZPA) integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e8950-104">In this tutorial, you learn how to integrate Zscaler Private Access (ZPA) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e8950-105">Zscaler persoonlijke toegang (ZPA) integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e8950-105">Integrating Zscaler Private Access (ZPA) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e8950-106">U kunt beheren in Azure AD met toegang op Zscaler persoonlijke toegang (ZPA)</span><span class="sxs-lookup"><span data-stu-id="e8950-106">You can control in Azure AD who has access to Zscaler Private Access (ZPA)</span></span>
- <span data-ttu-id="e8950-107">U kunt uw gebruikers automatisch ophalen aangemelde naar Zscaler persoonlijke toegang (ZPA) (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="e8950-107">You can enable your users to automatically get signed-on to Zscaler Private Access (ZPA) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e8950-108">U kunt uw accounts op één centrale locatie - en de Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="e8950-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="e8950-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e8950-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8950-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e8950-110">Prerequisites</span></span>

<span data-ttu-id="e8950-111">Voor het configureren van Azure AD-integratie met Zscaler persoonlijke toegang (ZPA), moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="e8950-111">To configure Azure AD integration with Zscaler Private Access (ZPA), you need the following items:</span></span>

- <span data-ttu-id="e8950-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="e8950-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e8950-113">Een Zscaler persoonlijke toegang (ZPA) eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="e8950-113">A Zscaler Private Access (ZPA) single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="e8950-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e8950-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="e8950-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="e8950-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e8950-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="e8950-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="e8950-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e8950-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="e8950-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="e8950-118">Scenario description</span></span>
<span data-ttu-id="e8950-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e8950-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e8950-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="e8950-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e8950-121">Zscaler persoonlijke toegang (ZPA) uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e8950-121">Adding Zscaler Private Access (ZPA) from the gallery</span></span>
2. <span data-ttu-id="e8950-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e8950-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zscaler-private-access-zpa-from-the-gallery"></a><span data-ttu-id="e8950-123">Zscaler persoonlijke toegang (ZPA) uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e8950-123">Adding Zscaler Private Access (ZPA) from the gallery</span></span>
<span data-ttu-id="e8950-124">Voor het configureren van de integratie van Zscaler persoonlijke toegang (ZPA) in Azure AD, moet u Zscaler persoonlijke toegang (ZPA) uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="e8950-124">To configure the integration of Zscaler Private Access (ZPA) into Azure AD, you need to add Zscaler Private Access (ZPA) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e8950-125">**Als u wilt toevoegen Zscaler persoonlijke toegang (ZPA) uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e8950-125">**To add Zscaler Private Access (ZPA) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e8950-126">In de  **[Azure Management Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e8950-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e8950-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e8950-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e8950-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e8950-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="e8950-131">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e8950-131">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="e8950-133">Typ in het zoekvak **Zscaler persoonlijke toegang (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="e8950-133">In the search box, type **Zscaler Private Access (ZPA)**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. <span data-ttu-id="e8950-135">Selecteer in het deelvenster resultaten **Zscaler persoonlijke toegang (ZPA)**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e8950-135">In the results panel, select **Zscaler Private Access (ZPA)**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e8950-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e8950-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e8950-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Zscaler persoonlijke toegang (ZPA) op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="e8950-138">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access (ZPA) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e8950-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Zscaler persoonlijke toegang (ZPA) is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8950-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Private Access (ZPA) is to a user in Azure AD.</span></span> <span data-ttu-id="e8950-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Zscaler persoonlijke toegang (ZPA) tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="e8950-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler Private Access (ZPA) needs to be established.</span></span>

<span data-ttu-id="e8950-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Zscaler persoonlijke toegang (ZPA).</span><span class="sxs-lookup"><span data-stu-id="e8950-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zscaler Private Access (ZPA).</span></span>

<span data-ttu-id="e8950-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Zscaler persoonlijke toegang (ZPA), moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="e8950-142">To configure and test Azure AD single sign-on with Zscaler Private Access (ZPA), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e8950-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e8950-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e8950-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e8950-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e8950-145">**[Maken van een testgebruiker Zscaler persoonlijke toegang (ZPA)](#creating-a-zscaler-private-access-(zpa)-test-user)**  - hebben een equivalent van Britta Simon in Zscaler persoonlijke toegang (ZPA) die is gekoppeld aan de Azure AD-representatie van haar.</span><span class="sxs-lookup"><span data-stu-id="e8950-145">**[Creating a Zscaler Private Access (ZPA) test user](#creating-a-zscaler-private-access-(zpa)-test-user)** - to have a counterpart of Britta Simon in Zscaler Private Access (ZPA) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="e8950-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e8950-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e8950-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="e8950-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e8950-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="e8950-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e8950-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing Zscaler persoonlijke toegang (ZPA).</span><span class="sxs-lookup"><span data-stu-id="e8950-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Zscaler Private Access (ZPA) application.</span></span>

<span data-ttu-id="e8950-150">**Voor het configureren van Azure AD eenmalige aanmelding met Zscaler persoonlijke toegang (ZPA), moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e8950-150">**To configure Azure AD single sign-on with Zscaler Private Access (ZPA), perform the following steps:**</span></span>

1. <span data-ttu-id="e8950-151">In de Azure-beheerportal op de **Zscaler persoonlijke toegang (ZPA)** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="e8950-151">In the Azure Management portal, on the **Zscaler Private Access (ZPA)** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="e8950-153">Op de **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** eenmalige aanmelding inschakelen op.</span><span class="sxs-lookup"><span data-stu-id="e8950-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="e8950-155">Op de **Zscaler persoonlijke toegang (ZPA)-domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e8950-155">On the **Zscaler Private Access (ZPA) Domain and URLs** section, perform the following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    <span data-ttu-id="e8950-157">a.</span><span class="sxs-lookup"><span data-stu-id="e8950-157">a.</span></span> <span data-ttu-id="e8950-158">In de **aanmelding op URL** textbox, typ een URL met het volgende patroon volgen:`https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span><span class="sxs-lookup"><span data-stu-id="e8950-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span></span>

    <span data-ttu-id="e8950-159">b.</span><span class="sxs-lookup"><span data-stu-id="e8950-159">b.</span></span> <span data-ttu-id="e8950-160">In de **id** textbox, type:`https://samlsp.private.zscaler.com/auth/metadata`</span><span class="sxs-lookup"><span data-stu-id="e8950-160">In the **Identifier** textbox, type: `https://samlsp.private.zscaler.com/auth/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e8950-161">Houd er rekening mee dat deze niet de werkelijke waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="e8950-161">Please note that these are not the real values.</span></span> <span data-ttu-id="e8950-162">U hebt deze waarden bijwerken met het werkelijke aanmelding op de URL en de id.</span><span class="sxs-lookup"><span data-stu-id="e8950-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="e8950-163">Hier raden we u voor het gebruik van de unieke waarde van de URL in de id.</span><span class="sxs-lookup"><span data-stu-id="e8950-163">Here we suggest you to use the unique value of URL in the Identifier.</span></span> <span data-ttu-id="e8950-164">Neem contact op met [Zscaler persoonlijke toegang (ZPA) ondersteuningsteam](https://help.zscaler.com/zpa-submit-ticket) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="e8950-164">Contact [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) to get these values.</span></span>

4. <span data-ttu-id="e8950-165">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **nieuw certificaat maken**.</span><span class="sxs-lookup"><span data-stu-id="e8950-165">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. <span data-ttu-id="e8950-167">Op de **nieuw certificaat maken** dialoogvenster, klikt u op het pictogram van de kalender en selecteer een **vervaldatum**.</span><span class="sxs-lookup"><span data-stu-id="e8950-167">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="e8950-168">Klik vervolgens op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e8950-168">Then click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="e8950-170">Op de **SAML-certificaat voor ondertekening van** sectie **nieuwe certificaat activeren** en klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e8950-170">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. <span data-ttu-id="e8950-172">In het pop-upvenster **rollovercertificaat** venster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8950-172">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="e8950-174">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e8950-174">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. <span data-ttu-id="e8950-176">In een ander browservenster, meld u bij uw bedrijf Zscaler persoonlijke toegang (ZPA) site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e8950-176">In a different web browser window, log into your Zscaler Private Access (ZPA) company site as an administrator.</span></span>

10. <span data-ttu-id="e8950-177">Navigeer naar **beheerder** en klik vervolgens op **Idp configuratie**.</span><span class="sxs-lookup"><span data-stu-id="e8950-177">Navigate to **Administrator** and then click **Idp Configuration**.</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. <span data-ttu-id="e8950-179">In de **Idp configuratie** sectie, klikt u op **nieuwe IDP-configuratie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e8950-179">In the **Idp Configuration** section, click **Add New IDP Configuration**.</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. <span data-ttu-id="e8950-181">In de **nieuwe IDP configuratie** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e8950-181">In the **New IDP Configuration** section, perform the following steps:</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    <span data-ttu-id="e8950-183">a.</span><span class="sxs-lookup"><span data-stu-id="e8950-183">a.</span></span> <span data-ttu-id="e8950-184">Klik op **bestand selecteren** en uw van het gedownloade metagegevensbestand te uploaden.</span><span class="sxs-lookup"><span data-stu-id="e8950-184">Click **Select File** and upload your downloaded metadata file.</span></span>

    <span data-ttu-id="e8950-185">b.</span><span class="sxs-lookup"><span data-stu-id="e8950-185">b.</span></span> <span data-ttu-id="e8950-186">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="e8950-186">Click **Save** button.</span></span>
    


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e8950-187">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="e8950-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="e8950-188">Het doel van deze sectie is het een testgebruiker maken in Azure Management portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e8950-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="e8950-190">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e8950-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e8950-191">In de **Azure Management portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="e8950-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e8950-193">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="e8950-193">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e8950-195">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e8950-195">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e8950-197">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e8950-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e8950-199">a.</span><span class="sxs-lookup"><span data-stu-id="e8950-199">a.</span></span> <span data-ttu-id="e8950-200">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e8950-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e8950-201">b.</span><span class="sxs-lookup"><span data-stu-id="e8950-201">b.</span></span> <span data-ttu-id="e8950-202">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e8950-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e8950-203">c.</span><span class="sxs-lookup"><span data-stu-id="e8950-203">c.</span></span> <span data-ttu-id="e8950-204">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e8950-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e8950-205">d.</span><span class="sxs-lookup"><span data-stu-id="e8950-205">d.</span></span> <span data-ttu-id="e8950-206">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="e8950-206">Click **Create**.</span></span> 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a><span data-ttu-id="e8950-207">Maken van een testgebruiker Zscaler persoonlijke toegang (ZPA)</span><span class="sxs-lookup"><span data-stu-id="e8950-207">Creating a Zscaler Private Access (ZPA) test user</span></span>

<span data-ttu-id="e8950-208">In deze sectie maakt u een gebruiker met de naam Britta Simon in Zscaler persoonlijke toegang (ZPA).</span><span class="sxs-lookup"><span data-stu-id="e8950-208">In this section, you create a user called Britta Simon in Zscaler Private Access (ZPA).</span></span> <span data-ttu-id="e8950-209">Neem contact op met [Zscaler persoonlijke toegang (ZPA) ondersteuningsteam](https://help.zscaler.com/zpa-submit-ticket) om toe te voegen de gebruikers van het platform Zscaler persoonlijke toegang (ZPA).</span><span class="sxs-lookup"><span data-stu-id="e8950-209">Please work with [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) to add the users in the Zscaler Private Access (ZPA) platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e8950-210">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8950-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e8950-211">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan Zscaler persoonlijke toegang (ZPA).</span><span class="sxs-lookup"><span data-stu-id="e8950-211">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Zscaler Private Access (ZPA).</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="e8950-213">**Als u wilt toewijzen Britta Simon naar Zscaler persoonlijke toegang (ZPA), moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="e8950-213">**To assign Britta Simon to Zscaler Private Access (ZPA), perform the following steps:**</span></span>

1. <span data-ttu-id="e8950-214">In de Azure-beheerportal, opent u de weergave toepassingen en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e8950-214">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="e8950-216">Selecteer in de lijst met toepassingen **Zscaler persoonlijke toegang (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="e8950-216">In the applications list, select **Zscaler Private Access (ZPA)**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. <span data-ttu-id="e8950-218">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e8950-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="e8950-220">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e8950-220">Click **Add** button.</span></span> <span data-ttu-id="e8950-221">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e8950-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="e8950-223">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e8950-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e8950-224">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e8950-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e8950-225">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e8950-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="e8950-226">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="e8950-226">Testing single sign-on</span></span>

<span data-ttu-id="e8950-227">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="e8950-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e8950-228">Als u op de tegel Zscaler persoonlijke toegang (ZPA) in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Zscaler persoonlijke toegang (ZPA).</span><span class="sxs-lookup"><span data-stu-id="e8950-228">When you click the Zscaler Private Access (ZPA) tile in the Access Panel, you should get automatically signed-on to your Zscaler Private Access (ZPA) application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="e8950-229">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e8950-229">Additional resources</span></span>

* [<span data-ttu-id="e8950-230">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e8950-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e8950-231">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e8950-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png