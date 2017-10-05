---
title: 'Zelfstudie: Azure Active Directory-integratie met de beheerportal Cloud voor Microsoft Azure | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Cloud-Management-Portal voor Microsoft Azure.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4ea9f47c-25ca-42b0-a878-9e7aa6f34973
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: bae5f05a161b2730bf662bcb47f20ab3e1799951
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloud-management-portal-for-microsoft-azure"></a><span data-ttu-id="6e62d-103">Zelfstudie: Azure Active Directory-integratie met de beheerportal Cloud voor Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="6e62d-103">Tutorial: Azure Active Directory integration with Cloud Management Portal for Microsoft Azure</span></span>

<span data-ttu-id="6e62d-104">In deze zelfstudie leert u hoe Cloud Management-Portal voor Microsoft Azure integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6e62d-104">In this tutorial, you learn how to integrate Cloud Management Portal for Microsoft Azure with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6e62d-105">Cloud-Management-Portal voor Microsoft Azure integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6e62d-105">Integrating Cloud Management Portal for Microsoft Azure with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6e62d-106">U kunt beheren in Azure AD die toegang hebben tot Cloud-beheerportal voor Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="6e62d-106">You can control in Azure AD who has access to Cloud Management Portal for Microsoft Azure</span></span>
- <span data-ttu-id="6e62d-107">U kunt uw gebruikers automatisch ophalen aangemeld bij de beheerportal Cloud voor Microsoft Azure (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="6e62d-107">You can enable your users to automatically get signed-on to Cloud Management Portal for Microsoft Azure (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6e62d-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="6e62d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6e62d-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6e62d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e62d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6e62d-110">Prerequisites</span></span>

<span data-ttu-id="6e62d-111">Voor het configureren van Azure AD-integratie met de beheerportal Cloud voor Microsoft Azure, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="6e62d-111">To configure Azure AD integration with Cloud Management Portal for Microsoft Azure, you need the following items:</span></span>

- <span data-ttu-id="6e62d-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6e62d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6e62d-113">Een Cloud-Management-Portal voor Microsoft Azure-eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6e62d-113">A Cloud Management Portal for Microsoft Azure single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6e62d-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6e62d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6e62d-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6e62d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6e62d-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6e62d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6e62d-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6e62d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6e62d-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6e62d-118">Scenario description</span></span>
<span data-ttu-id="6e62d-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6e62d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6e62d-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6e62d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6e62d-121">Cloud-Management-Portal voor Microsoft Azure uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6e62d-121">Adding Cloud Management Portal for Microsoft Azure from the gallery</span></span>
2. <span data-ttu-id="6e62d-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6e62d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloud-management-portal-for-microsoft-azure-from-the-gallery"></a><span data-ttu-id="6e62d-123">Cloud-Management-Portal voor Microsoft Azure uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6e62d-123">Adding Cloud Management Portal for Microsoft Azure from the gallery</span></span>
<span data-ttu-id="6e62d-124">Voor het configureren van de integratie van Cloud-Management-Portal voor Microsoft Azure met Azure AD, moet u Cloud-Management-Portal voor Microsoft Azure uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6e62d-124">To configure the integration of Cloud Management Portal for Microsoft Azure into Azure AD, you need to add Cloud Management Portal for Microsoft Azure from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6e62d-125">**Als u wilt toevoegen Cloud Management-Portal voor Microsoft Azure uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6e62d-125">**To add Cloud Management Portal for Microsoft Azure from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6e62d-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6e62d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6e62d-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6e62d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6e62d-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6e62d-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6e62d-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e62d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6e62d-133">Typ in het zoekvak **Cloud Management-Portal voor Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="6e62d-133">In the search box, type **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_search.png)

5. <span data-ttu-id="6e62d-135">Selecteer in het deelvenster resultaten **Cloud Management-Portal voor Microsoft Azure**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="6e62d-135">In the results panel, select **Cloud Management Portal for Microsoft Azure**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6e62d-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6e62d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6e62d-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met de beheerportal Cloud voor Microsoft Azure op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="6e62d-138">In this section, you configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6e62d-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in de beheerportal Cloud voor Microsoft Azure is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e62d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cloud Management Portal for Microsoft Azure is to a user in Azure AD.</span></span> <span data-ttu-id="6e62d-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de beheerportal Cloud voor Microsoft Azure tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="6e62d-140">In other words, a link relationship between an Azure AD user and the related user in Cloud Management Portal for Microsoft Azure needs to be established.</span></span>

<span data-ttu-id="6e62d-141">Wijs in het beheerportal voor Microsoft Azure Cloud, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="6e62d-141">In Cloud Management Portal for Microsoft Azure, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6e62d-142">Om te configureren en testen van Azure AD eenmalige aanmelding met de beheerportal Cloud voor Microsoft Azure, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="6e62d-142">To configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6e62d-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6e62d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6e62d-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e62d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6e62d-145">**[Maken van een Cloud-Management-Portal voor Microsoft Azure-testgebruiker](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)**  - Cloud-Management-Portal voor Microsoft Azure die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="6e62d-145">**[Creating a Cloud Management Portal for Microsoft Azure test user](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)** - to have a counterpart of Britta Simon in Cloud Management Portal for Microsoft Azure that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6e62d-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6e62d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6e62d-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6e62d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6e62d-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6e62d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6e62d-149">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw Cloud-Management-Portal voor Microsoft Azure-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6e62d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="6e62d-150">**Voor het configureren van Azure AD eenmalige aanmelding met de beheerportal Cloud voor Microsoft Azure, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6e62d-150">**To configure Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, perform the following steps:**</span></span>

1. <span data-ttu-id="6e62d-151">In de Azure-portal op de **Cloud Management-Portal voor Microsoft Azure** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6e62d-151">In the Azure portal, on the **Cloud Management Portal for Microsoft Azure** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6e62d-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6e62d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_samlbase.png)

3. <span data-ttu-id="6e62d-155">Op de **Cloud Management-Portal voor Microsoft Azure-domein en URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6e62d-155">On the **Cloud Management Portal for Microsoft Azure Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_url.png)

    <span data-ttu-id="6e62d-157">a.</span><span class="sxs-lookup"><span data-stu-id="6e62d-157">a.</span></span> <span data-ttu-id="6e62d-158">In de **aanmeldings-URL** textbox, typ een URL met de volgende patronen:</span><span class="sxs-lookup"><span data-stu-id="6e62d-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    
    | |
    |--|
    | `https://portal.newsignature.com/<instancename>` |   
    | `https://portal.igcm.com/<instancename>` |
    
    <span data-ttu-id="6e62d-159">b.</span><span class="sxs-lookup"><span data-stu-id="6e62d-159">b.</span></span> <span data-ttu-id="6e62d-160">In de **id** textbox, typ een URL met de volgende patronen:</span><span class="sxs-lookup"><span data-stu-id="6e62d-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com` |
    | `https://<subdomain>.newsignature.com` |

    <span data-ttu-id="6e62d-161">c.</span><span class="sxs-lookup"><span data-stu-id="6e62d-161">c.</span></span> <span data-ttu-id="6e62d-162">In de **antwoord-URL** textbox, typ een URL met de volgende patronen:</span><span class="sxs-lookup"><span data-stu-id="6e62d-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com/<instancename>` |
    | `https://<subdomain>.newsignature.com` |
    | `https://<subdomain>.newsignature.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="6e62d-163">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="6e62d-163">These values are not real.</span></span> <span data-ttu-id="6e62d-164">Deze waarden bijwerken met de werkelijke aanmeldings-URL, -id en antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="6e62d-164">Update these values with the actual Sign-On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="6e62d-165">Neem contact op met [Cloud Management-Portal voor Microsoft Azure Client ondersteuningsteam](mailto:jczernuszka@newsignature.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="6e62d-165">Contact [Cloud Management Portal for Microsoft Azure Client support team](mailto:jczernuszka@newsignature.com) to get these values.</span></span> 
 
4. <span data-ttu-id="6e62d-166">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6e62d-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_certificate.png) 

5. <span data-ttu-id="6e62d-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6e62d-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-newsignature-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6e62d-170">Op de **Cloud Management-Portal voor Microsoft Azure Configuration** sectie, klikt u op **Cloud-beheerportal configureren voor Microsoft Azure** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="6e62d-170">On the **Cloud Management Portal for Microsoft Azure Configuration** section, click **Configure Cloud Management Portal for Microsoft Azure** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6e62d-171">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="6e62d-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_configure.png) 

7. <span data-ttu-id="6e62d-173">Eenmalige aanmelding configureren op **Cloud Management-Portal voor Microsoft Azure** zijde, moet u de gedownloade verzenden **certificaat**, **Sign-Out URL**, **SAML Single Sign-On Service-URL** en **SAML entiteit-ID** naar [Cloud Management-Portal voor Microsoft Azure-ondersteuningsteam](mailto:jczernuszka@newsignature.com).</span><span class="sxs-lookup"><span data-stu-id="6e62d-173">To configure single sign-on on **Cloud Management Portal for Microsoft Azure** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Single Sign-On Service URL** and **SAML Entity ID** to [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com).</span></span> <span data-ttu-id="6e62d-174">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6e62d-174">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="6e62d-175">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="6e62d-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6e62d-176">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="6e62d-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6e62d-177">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6e62d-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6e62d-178">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6e62d-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="6e62d-179">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6e62d-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6e62d-181">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6e62d-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6e62d-182">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6e62d-182">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-newsignature-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6e62d-184">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6e62d-184">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-newsignature-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6e62d-186">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e62d-186">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-newsignature-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6e62d-188">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6e62d-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-newsignature-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6e62d-190">a.</span><span class="sxs-lookup"><span data-stu-id="6e62d-190">a.</span></span> <span data-ttu-id="6e62d-191">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6e62d-191">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6e62d-192">b.</span><span class="sxs-lookup"><span data-stu-id="6e62d-192">b.</span></span> <span data-ttu-id="6e62d-193">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6e62d-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6e62d-194">c.</span><span class="sxs-lookup"><span data-stu-id="6e62d-194">c.</span></span> <span data-ttu-id="6e62d-195">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6e62d-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6e62d-196">d.</span><span class="sxs-lookup"><span data-stu-id="6e62d-196">d.</span></span> <span data-ttu-id="6e62d-197">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6e62d-197">Click **Create**.</span></span>
 
### <a name="creating-a-cloud-management-portal-for-microsoft-azure-test-user"></a><span data-ttu-id="6e62d-198">Een Cloud-Management-Portal voor Microsoft Azure-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6e62d-198">Creating a Cloud Management Portal for Microsoft Azure test user</span></span>

<span data-ttu-id="6e62d-199">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in de beheerportal Cloud voor Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6e62d-199">The objective of this section is to create a user called Britta Simon in Cloud Management Portal for Microsoft Azure.</span></span> <span data-ttu-id="6e62d-200">Neem contact op met [Cloud Management-Portal voor Microsoft Azure-ondersteuningsteam](mailto:jczernuszka@newsignature.com) de gebruikers in de Cloud-Management-Portal voor Microsoft Azure-account toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6e62d-200">Please work with [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com) to add the users in the Cloud Management Portal for Microsoft Azure account.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6e62d-201">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e62d-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6e62d-202">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Cloud Management-Portal voor Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6e62d-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cloud Management Portal for Microsoft Azure.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6e62d-204">**Als u wilt toewijzen Britta Simon Cloud Management Portal voor Microsoft Azure, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6e62d-204">**To assign Britta Simon to Cloud Management Portal for Microsoft Azure, perform the following steps:**</span></span>

1. <span data-ttu-id="6e62d-205">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6e62d-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6e62d-207">Selecteer in de lijst met toepassingen **Cloud Management-Portal voor Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="6e62d-207">In the applications list, select **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_app.png) 

3. <span data-ttu-id="6e62d-209">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6e62d-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6e62d-211">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6e62d-211">Click **Add** button.</span></span> <span data-ttu-id="6e62d-212">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e62d-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6e62d-214">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6e62d-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6e62d-215">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e62d-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6e62d-216">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6e62d-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6e62d-217">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6e62d-217">Testing single sign-on</span></span>

<span data-ttu-id="6e62d-218">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="6e62d-218">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="6e62d-219">Als u op de Cloud-beheerportal voor Microsoft Azure-tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw Cloud-Management-Portal voor Microsoft Azure-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6e62d-219">When you click the Cloud Management Portal for Microsoft Azure tile in the Access Panel, you should get automatically signed-on to your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="6e62d-220">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6e62d-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6e62d-221">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6e62d-221">Additional resources</span></span>

* [<span data-ttu-id="6e62d-222">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e62d-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6e62d-223">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6e62d-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_203.png

