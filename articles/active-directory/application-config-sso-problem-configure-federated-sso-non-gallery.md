---
title: configureren van federatieve eenmalige aanmelding voor een toepassing niet galerie aaaProblem | Microsoft Docs
description: Aantal Hallo veelvoorkomende problemen die optreden kunnen bij het configureren van federatieve eenmalige aanmelding tooyour aangepaste SAML-toepassing die niet wordt vermeld in de galerie van Azure AD-toepassing hello adres
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
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="ac553-103">Probleem federatieve eenmalige aanmelding voor een toepassing niet galerie configureren</span><span class="sxs-lookup"><span data-stu-id="ac553-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="ac553-104">Als u een probleem ondervindt bij het configureren van een toepassing.</span><span class="sxs-lookup"><span data-stu-id="ac553-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="ac553-105">Controleer of u alle stappen van Hallo in Hallo artikel hebt gevolgd [eenmalige aanmelding tooapplications die zich niet in de Azure Active Directory-toepassingsgalerie Hallo configureren.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span><span class="sxs-lookup"><span data-stu-id="ac553-105">Verify you have followed all hello steps in hello article [Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="ac553-106">Een ander exemplaar van de toepassing hello toevoegen niet</span><span class="sxs-lookup"><span data-stu-id="ac553-106">Can’t add another instance of hello application</span></span>

<span data-ttu-id="ac553-107">tooadd een tweede exemplaar van een toepassing, moet u toobe kunnen:</span><span class="sxs-lookup"><span data-stu-id="ac553-107">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="ac553-108">Een unieke id voor de tweede instantie Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="ac553-108">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="ac553-109">U kunt tooconfigure Hallo dezelfde id voor de eerste instantie Hallo gebruikt niet.</span><span class="sxs-lookup"><span data-stu-id="ac553-109">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="ac553-110">Configureer een ander certificaat dan Hallo gebruikt voor de eerste instantie Hallo.</span><span class="sxs-lookup"><span data-stu-id="ac553-110">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="ac553-111">Als hello toepassing biedt geen ondersteuning voor een van bovenstaande Hallo.</span><span class="sxs-lookup"><span data-stu-id="ac553-111">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="ac553-112">Vervolgens niet kunnen tooconfigure een tweede exemplaar.</span><span class="sxs-lookup"><span data-stu-id="ac553-112">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="ac553-113">Waar kan ik Hallo id (gebruiker Identifier) van de entiteit indeling instellen</span><span class="sxs-lookup"><span data-stu-id="ac553-113">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="ac553-114">U kunt tooselect Hallo id (gebruiker Identifier) van de entiteit indeling Azure AD toohello toepassing hello als antwoord verzendt na verificatie van gebruiker niet.</span><span class="sxs-lookup"><span data-stu-id="ac553-114">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="ac553-115">Azure AD Selecteer Hallo-indeling voor Hallo NameID kenmerk (gebruikers-id) op basis van geselecteerde Hallo-waarde of Hallo aangevraagd door de toepassing hello in Hallo SAML AuthRequest indeling.</span><span class="sxs-lookup"><span data-stu-id="ac553-115">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="ac553-116">Voor meer informatie gaat u naar Hallo artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder sectie Hallo NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="ac553-116">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="ac553-117">Waar vind ik metagegevens van de toepassing hello of een certificaat van Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac553-117">Where do I get hello application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="ac553-118">de metagegevens van de toepassing hello toodownload of het certificaat van Azure AD stappen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="ac553-118">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="ac553-119">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="ac553-119">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ac553-120">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="ac553-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ac553-121">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="ac553-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ac553-122">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="ac553-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ac553-123">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="ac553-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="ac553-124">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="ac553-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ac553-125">Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ac553-125">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="ac553-126">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="ac553-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ac553-127">Ga te**SAML-certificaat voor ondertekening van** sectie en klik vervolgens op **downloaden** waarde in de kolom.</span><span class="sxs-lookup"><span data-stu-id="ac553-127">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="ac553-128">Afhankelijk van welke toepassing hello configureren van eenmalige aanmelding vereist, ziet u beide Hallo optie toodownload Hallo Metadata XML of Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="ac553-128">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="ac553-129">Azure AD biedt een URL tooget Hallo metagegevens niet.</span><span class="sxs-lookup"><span data-stu-id="ac553-129">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="ac553-130">Hallo metagegevens kan alleen worden opgehaald als een XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="ac553-130">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="ac553-131">Niet weet hoe toocustomize SAML claims tooan toepassing verzonden</span><span class="sxs-lookup"><span data-stu-id="ac553-131">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="ac553-132">toolearn hoe toocustomize Hallo SAML kenmerk claims verzonden tooyour toepassing, Zie [toewijzen in Azure Active Directory-Claims](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ac553-132">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac553-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ac553-133">Next steps</span></span>
[<span data-ttu-id="ac553-134">Toepassingen beheren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ac553-134">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
