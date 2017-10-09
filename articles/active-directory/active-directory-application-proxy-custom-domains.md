---
title: aaaCustom domeinen in Azure AD-toepassingsproxy | Microsoft Docs
description: Aangepaste domeinen in Azure AD-toepassingsproxy beheren zodat die Hallo-URL voor Hallo app is dezelfde Hallo ongeacht waar uw gebruikers toegang toe.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7a433c411976077210a2435c3c087991c7430755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="df1ee-103">Werken met aangepaste domeinen in Azure AD-toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="df1ee-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="df1ee-104">Wanneer u een toepassing via Azure Active Directory-toepassingsproxy publiceert, maakt u een externe URL voor uw gebruikers toogo toowhen die ze extern werken.</span><span class="sxs-lookup"><span data-stu-id="df1ee-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users toogo toowhen they're working remotely.</span></span> <span data-ttu-id="df1ee-105">Deze URL opgehaald Hallo standaarddomein *yourtenant.msappproxy.net*.</span><span class="sxs-lookup"><span data-stu-id="df1ee-105">This URL gets hello default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="df1ee-106">Bijvoorbeeld, als u gepubliceerd een app met de naam uitgaven en uw tenant is met de naam Contoso en vervolgens de externe URL Hallo https://expenses-contoso.msappproxy.net zou zijn.</span><span class="sxs-lookup"><span data-stu-id="df1ee-106">For example, if you published an app named Expenses and your tenant is named Contoso, then hello external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="df1ee-107">Als u toouse op uw eigen domeinnaam wilt, kunt u een aangepast domein voor uw toepassing configureren.</span><span class="sxs-lookup"><span data-stu-id="df1ee-107">If you want toouse your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="df1ee-108">Het is raadzaam dat u instelt aangepaste domeinen voor uw toepassingen indien mogelijk.</span><span class="sxs-lookup"><span data-stu-id="df1ee-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="df1ee-109">Hallo voordelen van aangepaste domeinen onder andere:</span><span class="sxs-lookup"><span data-stu-id="df1ee-109">Some of hello benefits of custom domains include:</span></span>

- <span data-ttu-id="df1ee-110">Uw gebruikers toegang krijgen tot de toepassing toohello met dezelfde URL Hallo of ze binnen of buiten uw netwerk werken.</span><span class="sxs-lookup"><span data-stu-id="df1ee-110">Your users can get toohello application with hello same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="df1ee-111">Als al uw toepassingen hebben dezelfde interne en externe URL hello, blijven toowork zelfs buiten het bedrijfsnetwerk Hallo met koppelingen in één toepassing die tooanother verwijzen.</span><span class="sxs-lookup"><span data-stu-id="df1ee-111">If all of your applications have hello same internal and external URLs, then links in one application that point tooanother continue toowork even outside hello corporate network.</span></span> 
- <span data-ttu-id="df1ee-112">U uw huisstijl beheren en Hallo-URL's die u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="df1ee-112">You control your branding, and create hello URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="df1ee-113">Een aangepast domein configureren</span><span class="sxs-lookup"><span data-stu-id="df1ee-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="df1ee-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="df1ee-114">Prerequisites</span></span>

<span data-ttu-id="df1ee-115">Voordat u een aangepast domein configureren, zorg ervoor dat er Hallo volgens de vereisten die zijn voorbereid:</span><span class="sxs-lookup"><span data-stu-id="df1ee-115">Before you configure a custom domain, make sure that you have hello following requirements prepared:</span></span> 
- <span data-ttu-id="df1ee-116">Een [geverifieerd domein toegevoegd tooAzure Active Directory](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="df1ee-116">A [verified domain added tooAzure Active Directory](active-directory-domains-add-azure-portal.md).</span></span>
- <span data-ttu-id="df1ee-117">Een aangepaste certificaat voor Hallo-domein in Hallo vorm van een PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="df1ee-117">A custom certificate for hello domain, in hello form of a PFX file.</span></span> 
- <span data-ttu-id="df1ee-118">Een lokale app [gepubliceerd via toepassingsproxy](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="df1ee-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="df1ee-119">Uw aangepaste domein configureren</span><span class="sxs-lookup"><span data-stu-id="df1ee-119">Configure your custom domain</span></span>

<span data-ttu-id="df1ee-120">Wanneer u deze drie vereisten gereed hebt, volgt u deze stappen tooset van uw aangepaste domein:</span><span class="sxs-lookup"><span data-stu-id="df1ee-120">When you have those three requirements ready, follow these steps tooset up your custom domain:</span></span>

1. <span data-ttu-id="df1ee-121">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="df1ee-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="df1ee-122">Navigeer te**Azure Active Directory** > **bedrijfstoepassingen** > **alle toepassingen** en kies Hallo app gewenste toomanage.</span><span class="sxs-lookup"><span data-stu-id="df1ee-122">Navigate too**Azure Active Directory** > **Enterprise applications** > **All applications** and choose hello app you want toomanage.</span></span>
3. <span data-ttu-id="df1ee-123">Selecteer **toepassingsproxy**.</span><span class="sxs-lookup"><span data-stu-id="df1ee-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="df1ee-124">Gebruik in het veld van de externe URL hello, Hallo dropdown lijst tooselect uw aangepaste domein.</span><span class="sxs-lookup"><span data-stu-id="df1ee-124">In hello External URL field, use hello dropdown list tooselect your custom domain.</span></span> <span data-ttu-id="df1ee-125">Als u uw domein in de lijst Hallo niet ziet, nog niet klikt u vervolgens deze geverifieerd nog.</span><span class="sxs-lookup"><span data-stu-id="df1ee-125">If you don't see your domain in hello list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="df1ee-126">Selecteer **opslaan**</span><span class="sxs-lookup"><span data-stu-id="df1ee-126">Select **Save**</span></span>
5. <span data-ttu-id="df1ee-127">Hallo **certificaat** veld dat is uitgeschakeld, wordt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="df1ee-127">hello **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="df1ee-128">Selecteer dit veld.</span><span class="sxs-lookup"><span data-stu-id="df1ee-128">Select this field.</span></span> 

   ![Klik op tooupload een certificaat](./media/active-directory-application-proxy-custom-domains/certificate.png)

   <span data-ttu-id="df1ee-130">Als u al een certificaat voor dit domein hebt geüpload, wordt in het certificaatveld Hallo geeft Hallo-certificaatinformatie weer.</span><span class="sxs-lookup"><span data-stu-id="df1ee-130">If you already uploaded a certificate for this domain, hello Certificate field displays hello certificate information.</span></span> 

6. <span data-ttu-id="df1ee-131">Hallo PFX-certificaat uploaden en Hallo wachtwoord invoeren voor Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="df1ee-131">Upload hello PFX certificate and enter hello password for hello certificate.</span></span> 
7. <span data-ttu-id="df1ee-132">Selecteer **opslaan** toosave uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="df1ee-132">Select **Save** toosave your changes.</span></span> 
8. <span data-ttu-id="df1ee-133">Voeg een [DNS-record](../dns/dns-operations-recordsets-portal.md) dat omleidingen Hallo nieuwe externe URL toohello msappproxy.net-domein.</span><span class="sxs-lookup"><span data-stu-id="df1ee-133">Add a [DNS record](../dns/dns-operations-recordsets-portal.md) that redirects hello new external URL toohello msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="df1ee-134">U hoeft slechts één certificaat tooupload per aangepast domein.</span><span class="sxs-lookup"><span data-stu-id="df1ee-134">You only need tooupload one certificate per custom domain.</span></span> <span data-ttu-id="df1ee-135">Wanneer u een certificaat uploaden, kunt u aangepast domein Hallo wanneer u een nieuwe app publiceert en geen aanvullende configuratie toodo, met uitzondering van Hallo DNS-record.</span><span class="sxs-lookup"><span data-stu-id="df1ee-135">Once you upload a certificate, you can choose hello custom domain when you publish a new app and not have toodo additional configuration except for hello DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="df1ee-136">Certificaten beheren</span><span class="sxs-lookup"><span data-stu-id="df1ee-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="df1ee-137">De indeling van certificaat</span><span class="sxs-lookup"><span data-stu-id="df1ee-137">Certificate format</span></span>
<span data-ttu-id="df1ee-138">Er is geen beperking op Hallo certificaat handtekening methoden.</span><span class="sxs-lookup"><span data-stu-id="df1ee-138">There is no restriction on hello certificate signature methods.</span></span> <span data-ttu-id="df1ee-139">Alle worden Elliptic Curve Cryptography (ECC), SAN Subject Alternative Name () en andere algemene typen certificaten ondersteund.</span><span class="sxs-lookup"><span data-stu-id="df1ee-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="df1ee-140">U kunt een jokertekencertificaat, zolang Hallo jokertekens overeenkomt met de externe URL Hallo gewenst.</span><span class="sxs-lookup"><span data-stu-id="df1ee-140">You can use a wildcard certificate as long as hello wildcard matches hello desired external URL.</span></span> 

<span data-ttu-id="df1ee-141">U kunt zelf-ondertekende certificaten, evenals gebruiken.</span><span class="sxs-lookup"><span data-stu-id="df1ee-141">You can use self-signed certificates, as well.</span></span> <span data-ttu-id="df1ee-142">Als u een persoonlijke certificeringsinstantie, moet Hallo CDP (certificaat intrekken point-distributiepunt) voor Hallo certificaat openbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="df1ee-142">If you’re using a private certificate authority, hello CDP (certificate revocation point distribution point) for hello certificate should be public.</span></span>

### <a name="changing-hello-domain"></a><span data-ttu-id="df1ee-143">Hallo domein wijzigen</span><span class="sxs-lookup"><span data-stu-id="df1ee-143">Changing hello domain</span></span>
<span data-ttu-id="df1ee-144">Alle geverifieerde domeinen weergegeven in de vervolgkeuzelijst van Hallo externe URL voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="df1ee-144">All verified domains appear in hello External URL dropdown list for your application.</span></span> <span data-ttu-id="df1ee-145">toochange Hallo-domein alleen update die voor de toepassing hello veld.</span><span class="sxs-lookup"><span data-stu-id="df1ee-145">toochange hello domain, just update that field for hello application.</span></span> <span data-ttu-id="df1ee-146">Als Hallo domein u wilt niet in de lijst Hallo [toevoegen als een geverifieerde domeinnaam](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="df1ee-146">If hello domain you want isn't in hello list, [add it as a verified domain](active-directory-domains-add-azure-portal.md).</span></span> <span data-ttu-id="df1ee-147">Als u een domein dat een bijbehorend certificaat nog geen selecteert, volgt u stap 5-7 tooadd Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="df1ee-147">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 tooadd hello certificate.</span></span> <span data-ttu-id="df1ee-148">Controleer vervolgens of dat u Hallo DNS-record tooredirect van nieuwe externe URL Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="df1ee-148">Then, make sure you update hello DNS record tooredirect from hello new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="df1ee-149">Certificaatbeheer</span><span class="sxs-lookup"><span data-stu-id="df1ee-149">Certificate management</span></span>
<span data-ttu-id="df1ee-150">U kunt hetzelfde voor meerdere toepassingen certificaat tenzij Hallo toepassingen een externe host delen hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="df1ee-150">You can use hello same certificate for multiple applications unless hello applications share an external host.</span></span> 

<span data-ttu-id="df1ee-151">Ontvangt u een waarschuwing wanneer een certificaat is verlopen, dat u tooupload een ander certificaat via Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="df1ee-151">You get a warning when a certificate expires, telling you tooupload another certificate through hello portal.</span></span> <span data-ttu-id="df1ee-152">Als het Hallo-certificaat is ingetrokken, kunnen uw gebruikers een beveiligingswaarschuwing zien bij het openen van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="df1ee-152">If hello certificate is revoked, your users may see a security warning when accessing hello application.</span></span> <span data-ttu-id="df1ee-153">We uitvoeren geen intrekkingscontroles voor certificaten.</span><span class="sxs-lookup"><span data-stu-id="df1ee-153">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="df1ee-154">tooupdate hello certificaat voor een bepaalde toepassing toohello toepassing navigeren en volg de stappen 5 tot en met 7 voor het configureren van aangepaste domeinen op gepubliceerde toepassingen tooupload een nieuw certificaat.</span><span class="sxs-lookup"><span data-stu-id="df1ee-154">tooupdate hello certificate for a given application, navigate toohello application and follow steps 5-7 for configuring custom domains on published applications tooupload a new certificate.</span></span> <span data-ttu-id="df1ee-155">Als het oude certificaat Hallo niet door andere toepassingen wordt gebruikt, wordt deze automatisch verwijderd.</span><span class="sxs-lookup"><span data-stu-id="df1ee-155">If hello old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="df1ee-156">Alle Certificaatbeheer is momenteel door afzonderlijke toepassing pagina's er daarom toomanage certificaten in de context Hallo van relevante Hallo-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="df1ee-156">Currently all certificate management is through individual application pages so you need toomanage certificates in hello context of hello relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="df1ee-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="df1ee-157">Next steps</span></span>
* <span data-ttu-id="df1ee-158">[Eenmalige aanmelding inschakelen](active-directory-application-proxy-sso-using-kcd.md) tooyour gepubliceerde apps met Azure AD-verificatie.</span><span class="sxs-lookup"><span data-stu-id="df1ee-158">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) tooyour published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="df1ee-159">[Inschakelen van voorwaardelijke toegang](active-directory-application-proxy-conditional-access.md) tooyour gepubliceerde apps.</span><span class="sxs-lookup"><span data-stu-id="df1ee-159">[Enable conditional access](active-directory-application-proxy-conditional-access.md) tooyour published apps.</span></span>
* [<span data-ttu-id="df1ee-160">Uw aangepaste domein naam tooAzure AD toevoegen</span><span class="sxs-lookup"><span data-stu-id="df1ee-160">Add your custom domain name tooAzure AD</span></span>](active-directory-domains-add-azure-portal.md)


