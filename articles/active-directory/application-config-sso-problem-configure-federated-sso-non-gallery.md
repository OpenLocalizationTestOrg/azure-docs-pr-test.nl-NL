---
title: Probleem federatieve eenmalige aanmelding voor een toepassing niet galerie configureren | Microsoft Docs
description: Adres van een aantal veelvoorkomende problemen die optreden kunnen bij het configureren van federatieve eenmalige aanmelding voor uw aangepaste SAML-toepassing die niet wordt vermeld in de Azure AD-Toepassingsgalerie
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4eb2c04c940dd6ad15a491a331aed76c237f0387
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="c485c-103">Probleem federatieve eenmalige aanmelding voor een toepassing niet galerie configureren</span><span class="sxs-lookup"><span data-stu-id="c485c-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="c485c-104">Als u een probleem ondervindt bij het configureren van een toepassing.</span><span class="sxs-lookup"><span data-stu-id="c485c-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="c485c-105">Controleer of u alle stappen in het artikel hebt gevolgd [eenmalige aanmelding tot toepassingen die zich niet in de Azure Active Directory-toepassingsgalerie configureren.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span><span class="sxs-lookup"><span data-stu-id="c485c-105">Verify you have followed all the steps in the article [Configuring single sign-on to applications that are not in the Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="c485c-106">Een ander exemplaar van de toepassing toevoegen niet</span><span class="sxs-lookup"><span data-stu-id="c485c-106">Can’t add another instance of the application</span></span>

<span data-ttu-id="c485c-107">Als u wilt een tweede exemplaar van een toepassing toevoegt, moet u mogelijk:</span><span class="sxs-lookup"><span data-stu-id="c485c-107">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="c485c-108">Configureer een unieke id voor de tweede instantie.</span><span class="sxs-lookup"><span data-stu-id="c485c-108">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="c485c-109">Het niet mogelijk om te configureren voor het eerste exemplaar gebruikt dezelfde id.</span><span class="sxs-lookup"><span data-stu-id="c485c-109">You won’t be able to configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="c485c-110">Configureer een ander certificaat dan de versie die wordt gebruikt voor het eerste exemplaar.</span><span class="sxs-lookup"><span data-stu-id="c485c-110">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="c485c-111">Als de toepassing biedt geen ondersteuning voor een van de bovenstaande.</span><span class="sxs-lookup"><span data-stu-id="c485c-111">If the application doesn’t support any of the above.</span></span> <span data-ttu-id="c485c-112">Vervolgens het niet mogelijk voor het configureren van een tweede exemplaar.</span><span class="sxs-lookup"><span data-stu-id="c485c-112">Then, you won’t be able to configure a second instance.</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="c485c-113">Waar kan ik de id van de entiteit (gebruikers-id)-indeling instellen</span><span class="sxs-lookup"><span data-stu-id="c485c-113">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="c485c-114">Het niet mogelijk om de id van de entiteit (gebruikers-id)-indeling die Azure AD naar de toepassing in het antwoord na verificatie van gebruikers verzendt te selecteren.</span><span class="sxs-lookup"><span data-stu-id="c485c-114">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="c485c-115">Azure AD selecteren de indeling voor het kenmerk NameID (gebruikers-id) op basis van de waarde geselecteerd of de indeling die is aangevraagd door de toepassing in de SAML-AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="c485c-115">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="c485c-116">Raadpleeg voor meer informatie het artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder de sectie NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="c485c-116">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="where-do-i-get-the-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="c485c-117">Waar vind ik de metagegevens van de toepassing of het certificaat van Azure AD</span><span class="sxs-lookup"><span data-stu-id="c485c-117">Where do I get the application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="c485c-118">Voor het downloaden van de metagegevens van de toepassing of het certificaat van Azure AD, de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="c485c-118">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="c485c-119">Open de [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="c485c-119">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c485c-120">Open de **Azure Active Directory-extensie** door te klikken op **meer services** onderaan in het navigatiemenu belangrijkste linkerkant.</span><span class="sxs-lookup"><span data-stu-id="c485c-120">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c485c-121">Typ in **' Azure Active Directory**' in het zoekvak filter en selecteer de **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="c485c-121">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c485c-122">Klik op **bedrijfstoepassingen** in het menu van Azure Active Directory linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="c485c-122">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c485c-123">Klik op **alle toepassingen** om een lijst met al uw toepassingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="c485c-123">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="c485c-124">Als u de toepassing die u wilt weergeven die hier niet ziet, gebruikt u de **Filter** besturingselement aan de bovenkant van de **lijst met alle toepassingen** en stel de **weergeven** optie naar **alle toepassingen.**</span><span class="sxs-lookup"><span data-stu-id="c485c-124">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="c485c-125">Selecteer de toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="c485c-125">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="c485c-126">Nadat de toepassing wordt geladen, klikt u op de **eenmalige aanmelding** van navigatiemenu links aan de van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c485c-126">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c485c-127">Ga naar **SAML-certificaat voor ondertekening van** sectie en klik vervolgens op **downloaden** waarde in de kolom.</span><span class="sxs-lookup"><span data-stu-id="c485c-127">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="c485c-128">Afhankelijk van wat de toepassing configureren van eenmalige aanmelding vereist, ziet u ofwel de optie voor het downloaden van de Metadata XML of het certificaat.</span><span class="sxs-lookup"><span data-stu-id="c485c-128">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="c485c-129">Azure AD biedt een URL als u de metagegevens niet.</span><span class="sxs-lookup"><span data-stu-id="c485c-129">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="c485c-130">De metagegevens kan alleen worden opgehaald als een XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="c485c-130">The metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-to-customize-saml-claims-sent-to-an-application"></a><span data-ttu-id="c485c-131">Weet u niet het aanpassen van SAML-claims verzonden naar een toepassing</span><span class="sxs-lookup"><span data-stu-id="c485c-131">Don't know how to customize SAML claims sent to an application</span></span>

<span data-ttu-id="c485c-132">Zie voor meer informatie over het aanpassen van de SAML-kenmerk claims verzonden naar uw toepassing, [toewijzen in Azure Active Directory-Claims](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c485c-132">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c485c-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c485c-133">Next steps</span></span>
[<span data-ttu-id="c485c-134">Toepassingen beheren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c485c-134">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
