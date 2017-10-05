---
title: Aangepaste domeinen in Azure AD-toepassingsproxy | Microsoft Docs
description: Aangepaste domeinen in Azure AD-toepassingsproxy beheren zodat de URL voor de app hetzelfde is, ongeacht waar uw gebruikers toegang toe.
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
ms.openlocfilehash: 1dde300780c8d1f7ea9eee4c92de06bcf70a1f12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="0ade7-103">Werken met aangepaste domeinen in Azure AD-toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="0ade7-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="0ade7-104">Wanneer u een toepassing via Azure Active Directory-toepassingsproxy publiceert, maakt u een externe URL voor uw gebruikers gaan wanneer ze extern werken.</span><span class="sxs-lookup"><span data-stu-id="0ade7-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users to go to when they're working remotely.</span></span> <span data-ttu-id="0ade7-105">Deze URL wordt het standaarddomein *yourtenant.msappproxy.net*.</span><span class="sxs-lookup"><span data-stu-id="0ade7-105">This URL gets the default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="0ade7-106">Bijvoorbeeld, als u een app met de naam uitgaven en uw tenant gepubliceerd is met de naam Contoso, de externe URL https://expenses-contoso.msappproxy.net zou zijn.</span><span class="sxs-lookup"><span data-stu-id="0ade7-106">For example, if you published an app named Expenses and your tenant is named Contoso, then the external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="0ade7-107">Als u wilt om uw eigen domeinnaam te gebruiken, moet u een aangepast domein voor uw toepassing configureren.</span><span class="sxs-lookup"><span data-stu-id="0ade7-107">If you want to use your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="0ade7-108">Het is raadzaam dat u instelt aangepaste domeinen voor uw toepassingen indien mogelijk.</span><span class="sxs-lookup"><span data-stu-id="0ade7-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="0ade7-109">Enkele van de voordelen van aangepaste domeinen:</span><span class="sxs-lookup"><span data-stu-id="0ade7-109">Some of the benefits of custom domains include:</span></span>

- <span data-ttu-id="0ade7-110">Uw gebruikers toegang krijgen tot de toepassing met dezelfde URL, of ze binnen of buiten uw netwerk werken.</span><span class="sxs-lookup"><span data-stu-id="0ade7-110">Your users can get to the application with the same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="0ade7-111">Als al uw toepassingen dezelfde interne en externe URL's hebt, klikt u vervolgens blijven koppelingen in één toepassing die naar een andere verwijzen werken zelfs buiten het bedrijfsnetwerk.</span><span class="sxs-lookup"><span data-stu-id="0ade7-111">If all of your applications have the same internal and external URLs, then links in one application that point to another continue to work even outside the corporate network.</span></span> 
- <span data-ttu-id="0ade7-112">U uw huisstijl beheren en de URL's die u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="0ade7-112">You control your branding, and create the URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="0ade7-113">Een aangepast domein configureren</span><span class="sxs-lookup"><span data-stu-id="0ade7-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0ade7-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0ade7-114">Prerequisites</span></span>

<span data-ttu-id="0ade7-115">Voordat u een aangepast domein configureren, zorg ervoor dat u de volgende vereisten voorbereid hebt:</span><span class="sxs-lookup"><span data-stu-id="0ade7-115">Before you configure a custom domain, make sure that you have the following requirements prepared:</span></span> 
- <span data-ttu-id="0ade7-116">Een [gecontroleerde domein is toegevoegd aan Azure Active Directory](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0ade7-116">A [verified domain added to Azure Active Directory](active-directory-domains-add-azure-portal.md).</span></span>
- <span data-ttu-id="0ade7-117">Een aangepaste certificaat voor het domein, in de vorm van een PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="0ade7-117">A custom certificate for the domain, in the form of a PFX file.</span></span> 
- <span data-ttu-id="0ade7-118">Een lokale app [gepubliceerd via toepassingsproxy](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0ade7-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="0ade7-119">Uw aangepaste domein configureren</span><span class="sxs-lookup"><span data-stu-id="0ade7-119">Configure your custom domain</span></span>

<span data-ttu-id="0ade7-120">Wanneer u deze drie vereisten gereed hebt, volg deze stappen voor het instellen van uw aangepaste domein:</span><span class="sxs-lookup"><span data-stu-id="0ade7-120">When you have those three requirements ready, follow these steps to set up your custom domain:</span></span>

1. <span data-ttu-id="0ade7-121">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0ade7-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0ade7-122">Navigeer naar **Azure Active Directory** > **bedrijfstoepassingen** > **alle toepassingen** en kies de app die u wilt beheren.</span><span class="sxs-lookup"><span data-stu-id="0ade7-122">Navigate to **Azure Active Directory** > **Enterprise applications** > **All applications** and choose the app you want to manage.</span></span>
3. <span data-ttu-id="0ade7-123">Selecteer **toepassingsproxy**.</span><span class="sxs-lookup"><span data-stu-id="0ade7-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="0ade7-124">Gebruik de vervolgkeuzelijst om uw aangepaste domein in het veld externe URL.</span><span class="sxs-lookup"><span data-stu-id="0ade7-124">In the External URL field, use the dropdown list to select your custom domain.</span></span> <span data-ttu-id="0ade7-125">Als u uw domein in de lijst niet ziet, nog niet klikt u vervolgens deze geverifieerd nog.</span><span class="sxs-lookup"><span data-stu-id="0ade7-125">If you don't see your domain in the list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="0ade7-126">Selecteer **opslaan**</span><span class="sxs-lookup"><span data-stu-id="0ade7-126">Select **Save**</span></span>
5. <span data-ttu-id="0ade7-127">De **certificaat** veld dat is uitgeschakeld, wordt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="0ade7-127">The **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="0ade7-128">Selecteer dit veld.</span><span class="sxs-lookup"><span data-stu-id="0ade7-128">Select this field.</span></span> 

   ![Klik hier om een certificaat te uploaden](./media/active-directory-application-proxy-custom-domains/certificate.png)

   <span data-ttu-id="0ade7-130">Als u al een certificaat voor dit domein hebt geüpload, geeft de certificaatinformatie in het certificaatveld weer.</span><span class="sxs-lookup"><span data-stu-id="0ade7-130">If you already uploaded a certificate for this domain, the Certificate field displays the certificate information.</span></span> 

6. <span data-ttu-id="0ade7-131">Het PFX-certificaat uploaden en voer het wachtwoord voor het certificaat.</span><span class="sxs-lookup"><span data-stu-id="0ade7-131">Upload the PFX certificate and enter the password for the certificate.</span></span> 
7. <span data-ttu-id="0ade7-132">Selecteer **opslaan** uw wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="0ade7-132">Select **Save** to save your changes.</span></span> 
8. <span data-ttu-id="0ade7-133">Voeg een [DNS-record](../dns/dns-operations-recordsets-portal.md) die de nieuwe externe URL leidt om naar het domein msappproxy.net.</span><span class="sxs-lookup"><span data-stu-id="0ade7-133">Add a [DNS record](../dns/dns-operations-recordsets-portal.md) that redirects the new external URL to the msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="0ade7-134">U hoeft alleen te uploaden één certificaat per aangepast domein.</span><span class="sxs-lookup"><span data-stu-id="0ade7-134">You only need to upload one certificate per custom domain.</span></span> <span data-ttu-id="0ade7-135">Wanneer u een certificaat uploaden, kunt u het aangepaste domein wanneer u een nieuwe app publiceert en geen aanvullende instellingen, met uitzondering van de DNS-record.</span><span class="sxs-lookup"><span data-stu-id="0ade7-135">Once you upload a certificate, you can choose the custom domain when you publish a new app and not have to do additional configuration except for the DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="0ade7-136">Certificaten beheren</span><span class="sxs-lookup"><span data-stu-id="0ade7-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="0ade7-137">De indeling van certificaat</span><span class="sxs-lookup"><span data-stu-id="0ade7-137">Certificate format</span></span>
<span data-ttu-id="0ade7-138">Er is geen beperking voor de methoden van de handtekening certificaat.</span><span class="sxs-lookup"><span data-stu-id="0ade7-138">There is no restriction on the certificate signature methods.</span></span> <span data-ttu-id="0ade7-139">Alle worden Elliptic Curve Cryptography (ECC), SAN Subject Alternative Name () en andere algemene typen certificaten ondersteund.</span><span class="sxs-lookup"><span data-stu-id="0ade7-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="0ade7-140">U kunt een jokertekencertificaat, zolang het jokerteken overeenkomt met de gewenste externe URL.</span><span class="sxs-lookup"><span data-stu-id="0ade7-140">You can use a wildcard certificate as long as the wildcard matches the desired external URL.</span></span> 

<span data-ttu-id="0ade7-141">U kunt zelf-ondertekende certificaten, evenals gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0ade7-141">You can use self-signed certificates, as well.</span></span> <span data-ttu-id="0ade7-142">Als u een persoonlijke certificeringsinstantie, moet het CRL-Distributiepunt (certificaat intrekken point-distributiepunt) voor het certificaat openbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="0ade7-142">If you’re using a private certificate authority, the CDP (certificate revocation point distribution point) for the certificate should be public.</span></span>

### <a name="changing-the-domain"></a><span data-ttu-id="0ade7-143">Het wijzigen van het domein</span><span class="sxs-lookup"><span data-stu-id="0ade7-143">Changing the domain</span></span>
<span data-ttu-id="0ade7-144">Alle geverifieerde domeinen worden weergegeven in de vervolgkeuzelijst van de externe URL voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="0ade7-144">All verified domains appear in the External URL dropdown list for your application.</span></span> <span data-ttu-id="0ade7-145">Om te wijzigen van het domein, moet u zojuist hebt dat veld voor de toepassing bijwerken.</span><span class="sxs-lookup"><span data-stu-id="0ade7-145">To change the domain, just update that field for the application.</span></span> <span data-ttu-id="0ade7-146">Als het domein dat u wilt dat niet in de lijst [toevoegen als een geverifieerde domeinnaam](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0ade7-146">If the domain you want isn't in the list, [add it as a verified domain](active-directory-domains-add-azure-portal.md).</span></span> <span data-ttu-id="0ade7-147">Als u een domein dat niet heeft een bijbehorende certificaat nog stap 5-7 het certificaat toevoegen Volg selecteert.</span><span class="sxs-lookup"><span data-stu-id="0ade7-147">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 to add the certificate.</span></span> <span data-ttu-id="0ade7-148">Controleer vervolgens of dat u de DNS-record om te leiden van de nieuwe externe URL bijwerken.</span><span class="sxs-lookup"><span data-stu-id="0ade7-148">Then, make sure you update the DNS record to redirect from the new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="0ade7-149">Certificaatbeheer</span><span class="sxs-lookup"><span data-stu-id="0ade7-149">Certificate management</span></span>
<span data-ttu-id="0ade7-150">U kunt hetzelfde certificaat gebruiken voor meerdere toepassingen, tenzij de toepassingen een externe host delen.</span><span class="sxs-lookup"><span data-stu-id="0ade7-150">You can use the same certificate for multiple applications unless the applications share an external host.</span></span> 

<span data-ttu-id="0ade7-151">U krijgt een waarschuwing wanneer een certificaat is verlopen, dat u een ander certificaat via de portal uploaden.</span><span class="sxs-lookup"><span data-stu-id="0ade7-151">You get a warning when a certificate expires, telling you to upload another certificate through the portal.</span></span> <span data-ttu-id="0ade7-152">Als het certificaat is ingetrokken, kunnen uw gebruikers een beveiligingswaarschuwing zien bij het openen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="0ade7-152">If the certificate is revoked, your users may see a security warning when accessing the application.</span></span> <span data-ttu-id="0ade7-153">We uitvoeren geen intrekkingscontroles voor certificaten.</span><span class="sxs-lookup"><span data-stu-id="0ade7-153">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="0ade7-154">Navigeer naar de toepassing en volg de stappen 5 tot en met 7 voor het configureren van aangepaste domeinen op gepubliceerde toepassingen voor het uploaden van een nieuw certificaat voor het bijwerken van het certificaat voor een bepaalde toepassing.</span><span class="sxs-lookup"><span data-stu-id="0ade7-154">To update the certificate for a given application, navigate to the application and follow steps 5-7 for configuring custom domains on published applications to upload a new certificate.</span></span> <span data-ttu-id="0ade7-155">Als het oude certificaat niet door andere toepassingen gebruikt wordt, wordt deze automatisch verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0ade7-155">If the old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="0ade7-156">Alle Certificaatbeheer is momenteel door afzonderlijke toepassing pagina's er daarom voor het beheren van certificaten in de context van de relevante toepassingen.</span><span class="sxs-lookup"><span data-stu-id="0ade7-156">Currently all certificate management is through individual application pages so you need to manage certificates in the context of the relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0ade7-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0ade7-157">Next steps</span></span>
* <span data-ttu-id="0ade7-158">[Eenmalige aanmelding inschakelen](active-directory-application-proxy-sso-using-kcd.md) naar uw gepubliceerde apps met Azure AD-verificatie.</span><span class="sxs-lookup"><span data-stu-id="0ade7-158">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) to your published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="0ade7-159">[Inschakelen van voorwaardelijke toegang](active-directory-application-proxy-conditional-access.md) naar uw gepubliceerde apps.</span><span class="sxs-lookup"><span data-stu-id="0ade7-159">[Enable conditional access](active-directory-application-proxy-conditional-access.md) to your published apps.</span></span>
* [<span data-ttu-id="0ade7-160">Uw aangepaste domeinnaam toevoegen aan Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ade7-160">Add your custom domain name to Azure AD</span></span>](active-directory-domains-add-azure-portal.md)


