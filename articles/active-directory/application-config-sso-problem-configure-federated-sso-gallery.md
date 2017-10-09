---
title: aaaProblem federatieve eenmalige aanmelding voor een toepassing-galerie van Azure AD configureren | Microsoft Docs
description: Adres aantal Hallo veelvoorkomende problemen optreden kunnen bij het configureren van federatieve eenmalige aanmelding via SAML voor toepassingen die worden vermeld in hello Azure AD-Toepassingsgalerie
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
ms.openlocfilehash: 2ae1e511bd49b19159e1ab83cf79a7db5403b9a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="b603b-103">Probleem federatieve eenmalige aanmelding voor een toepassing-galerie van Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b603b-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="b603b-104">Als u een probleem ondervindt bij het configureren van een toepassing.</span><span class="sxs-lookup"><span data-stu-id="b603b-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="b603b-105">Controleer of dat u alle Hallo stappen hebt gevolgd in de zelfstudie Hallo voor Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b603b-105">Verify you have followed all hello steps in hello tutorial for hello application.</span></span> <span data-ttu-id="b603b-106">In de configuratie van de toepassing hello hebt u inline-documentatie over hoe tooconfigure toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="b603b-106">In hello application’s configuration, you have inline documentation on how tooconfigure hello application.</span></span> <span data-ttu-id="b603b-107">U kunt ook openen Hallo [lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) voor een stapsgewijze instructies voor details.</span><span class="sxs-lookup"><span data-stu-id="b603b-107">Also, you can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="b603b-108">Een ander exemplaar van de toepassing hello toevoegen niet</span><span class="sxs-lookup"><span data-stu-id="b603b-108">Can’t add another instance of hello application</span></span>

<span data-ttu-id="b603b-109">tooadd een tweede exemplaar van een toepassing, moet u toobe kunnen:</span><span class="sxs-lookup"><span data-stu-id="b603b-109">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="b603b-110">Een unieke id voor de tweede instantie Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="b603b-110">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="b603b-111">U kunt tooconfigure Hallo dezelfde id voor de eerste instantie Hallo gebruikt niet.</span><span class="sxs-lookup"><span data-stu-id="b603b-111">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="b603b-112">Configureer een ander certificaat dan Hallo gebruikt voor de eerste instantie Hallo.</span><span class="sxs-lookup"><span data-stu-id="b603b-112">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="b603b-113">Als hello toepassing biedt geen ondersteuning voor een van bovenstaande Hallo.</span><span class="sxs-lookup"><span data-stu-id="b603b-113">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="b603b-114">Vervolgens niet kunnen tooconfigure een tweede exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b603b-114">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="cant-add-hello-identifier-or-hello-reply-url"></a><span data-ttu-id="b603b-115">Kan geen Hallo id toevoegen of Hallo antwoord-URL</span><span class="sxs-lookup"><span data-stu-id="b603b-115">Can’t add hello Identifier or hello Reply URL</span></span>

<span data-ttu-id="b603b-116">Als u niet kunt tooconfigure Hallo id of Hallo antwoord-URL, Hallo id bevestigen en antwoord-URL waarden Hallo patronen vooraf is geconfigureerd voor de toepassing hello overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="b603b-116">If you’re not able tooconfigure hello Identifier or hello Reply URL, confirm hello Identifier and Reply URL values match hello patterns pre-configured for hello application.</span></span>

<span data-ttu-id="b603b-117">tooknow hello patronen vooraf is geconfigureerd voor de toepassing hello:</span><span class="sxs-lookup"><span data-stu-id="b603b-117">tooknow hello patterns pre-configured for hello application:</span></span>

1.  <span data-ttu-id="b603b-118">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.** Ga toostep 7.</span><span class="sxs-lookup"><span data-stu-id="b603b-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.** Go toostep 7.</span></span> <span data-ttu-id="b603b-119">Als u al Hallo toepassing configuratie blade op Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b603b-119">If you are already in hello application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="b603b-120">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="b603b-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b603b-121">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="b603b-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b603b-122">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="b603b-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b603b-123">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b603b-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="b603b-124">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="b603b-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b603b-125">Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="b603b-125">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="b603b-126">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="b603b-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b603b-127">Selecteer **op basis van SAML aanmelding** van Hallo **modus** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="b603b-127">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="b603b-128">Ga toohello **id** of **antwoord-URL** textbox onder Hallo **sectie domein en URL's.**</span><span class="sxs-lookup"><span data-stu-id="b603b-128">Go toohello **Identifier** or **Reply URL** textbox, under hello **Domain and URLs section.**</span></span>

10. <span data-ttu-id="b603b-129">Er zijn drie manieren tooknow Hallo ondersteund patronen voor Hallo toepassing:</span><span class="sxs-lookup"><span data-stu-id="b603b-129">There are three ways tooknow hello supported patterns for hello application:</span></span>

   * <span data-ttu-id="b603b-130">Hallo textbox u ziet Hallo ondersteund patroon of patronen als tijdelijke aanduiding *voorbeeld:* <https://contoso.com>.</span><span class="sxs-lookup"><span data-stu-id="b603b-130">In hello textbox, you see hello supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="b603b-131">Als het Hallo-patroon wordt niet ondersteund, ziet u een rood uitroepteken wanneer u tooenter Hallo waarde in Hallo textbox probeert.</span><span class="sxs-lookup"><span data-stu-id="b603b-131">if hello pattern is not supported, you see a red exclamation mark when you try tooenter hello value in hello textbox.</span></span> <span data-ttu-id="b603b-132">Als u de muisaanwijzer op Hallo rood uitroepteken, ziet u Hallo ondersteund patronen.</span><span class="sxs-lookup"><span data-stu-id="b603b-132">If you hover your mouse over hello red exclamation mark, you see hello supported patterns.</span></span>

   * <span data-ttu-id="b603b-133">In de zelfstudie Hallo voor toepassing hello, kunt u ook informatie ophalen over Hallo ondersteund patronen.</span><span class="sxs-lookup"><span data-stu-id="b603b-133">In hello tutorial for hello application, you can also get information about hello supported patterns.</span></span> <span data-ttu-id="b603b-134">Onder Hallo **eenmalige aanmelding configureren Azure AD** sectie.</span><span class="sxs-lookup"><span data-stu-id="b603b-134">Under hello **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="b603b-135">Ga toohello stap voor het geconfigureerde Hallo waarden onder Hallo **domein en de URL's** sectie.</span><span class="sxs-lookup"><span data-stu-id="b603b-135">Go toohello step for configured hello values under hello **Domain and URLs** section.</span></span>

<span data-ttu-id="b603b-136">Als de waarden Hallo komen niet met Hallo patronen vooraf is geconfigureerd op Azure AD overeen.</span><span class="sxs-lookup"><span data-stu-id="b603b-136">If hello values don’t match with hello patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="b603b-137">U kunt:</span><span class="sxs-lookup"><span data-stu-id="b603b-137">You can:</span></span>

-   <span data-ttu-id="b603b-138">Werken met Hallo toepassing leverancier tooget waarden die overeenkomen met Hallo patroon vooraf is geconfigureerd op Azure AD</span><span class="sxs-lookup"><span data-stu-id="b603b-138">Work with hello application vendor tooget values that match hello pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="b603b-139">U kunt ook contact opnemen met Azure AD-team via < aadapprequest@microsoft.com > of u een reactie in Hallo zelfstudie toorequest Hallo bijwerken van de patronen voor Hallo toepassing hello ondersteund</span><span class="sxs-lookup"><span data-stu-id="b603b-139">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in hello tutorial toorequest hello update of hello supported patterns for hello application</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="b603b-140">Waar kan ik Hallo id (gebruiker Identifier) van de entiteit indeling instellen</span><span class="sxs-lookup"><span data-stu-id="b603b-140">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="b603b-141">U kunt tooselect Hallo id (gebruiker Identifier) van de entiteit indeling Azure AD toohello toepassing hello als antwoord verzendt na verificatie van gebruiker niet.</span><span class="sxs-lookup"><span data-stu-id="b603b-141">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="b603b-142">Azure AD Selecteer Hallo-indeling voor Hallo NameID kenmerk (gebruikers-id) op basis van geselecteerde Hallo-waarde of Hallo aangevraagd door de toepassing hello in Hallo SAML AuthRequest indeling.</span><span class="sxs-lookup"><span data-stu-id="b603b-142">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="b603b-143">Voor meer informatie gaat u naar Hallo artikel [Single Sign-On SAML-protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) onder sectie Hallo NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="b603b-143">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="cant-find-hello-azure-ad-metadata-toocomplete-hello-configuration-with-hello-application"></a><span data-ttu-id="b603b-144">Kan hello Azure AD metagegevens toocomplete Hallo configuratie met Hallo toepassing niet vinden</span><span class="sxs-lookup"><span data-stu-id="b603b-144">Can’t find hello Azure AD metadata toocomplete hello configuration with hello application</span></span>

<span data-ttu-id="b603b-145">de metagegevens van de toepassing hello toodownload of het certificaat van Azure AD stappen Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="b603b-145">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="b603b-146">Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**</span><span class="sxs-lookup"><span data-stu-id="b603b-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b603b-147">Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.</span><span class="sxs-lookup"><span data-stu-id="b603b-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b603b-148">Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="b603b-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b603b-149">Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="b603b-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b603b-150">Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b603b-150">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="b603b-151">Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**</span><span class="sxs-lookup"><span data-stu-id="b603b-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b603b-152">Selecteer Hallo-toepassing die u hebt geconfigureerd eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b603b-152">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="b603b-153">Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="b603b-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b603b-154">Ga te**SAML-certificaat voor ondertekening van** sectie en klik vervolgens op **downloaden** waarde in de kolom.</span><span class="sxs-lookup"><span data-stu-id="b603b-154">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="b603b-155">Afhankelijk van welke toepassing hello configureren van eenmalige aanmelding vereist, ziet u beide Hallo optie toodownload Hallo Metadata XML of Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="b603b-155">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="b603b-156">Azure AD biedt een URL tooget Hallo metagegevens niet.</span><span class="sxs-lookup"><span data-stu-id="b603b-156">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="b603b-157">Hallo metagegevens kan alleen worden opgehaald als een XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="b603b-157">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="b603b-158">Niet weet hoe toocustomize SAML claims tooan toepassing verzonden</span><span class="sxs-lookup"><span data-stu-id="b603b-158">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="b603b-159">toolearn hoe toocustomize Hallo SAML kenmerk claims verzonden tooyour toepassing, Zie [toewijzen in Azure Active Directory-Claims](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b603b-159">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b603b-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b603b-160">Next steps</span></span>
[<span data-ttu-id="b603b-161">Toepassingen beheren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b603b-161">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
