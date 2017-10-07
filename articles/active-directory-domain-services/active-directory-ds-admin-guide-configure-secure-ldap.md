---
title: aaaConfigure Secure LDAP (LDAPS) in Azure AD Domain Services | Microsoft Docs
description: Beveiligde LDAP (LDAPS) voor een beheerd domein van Azure AD Domain Services configureren
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="41200-103">Beveiligde LDAP (LDAPS) voor een beheerd domein van Azure AD Domain Services configureren</span><span class="sxs-lookup"><span data-stu-id="41200-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="41200-104">Dit artikel laat zien hoe u beveiligde Lightweight Directory Access Protocol (LDAPS) kunt inschakelen voor uw beheerde domein van Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="41200-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="41200-105">Beveiligde LDAP wordt ook wel ' Lightweight Directory Access Protocol (LDAP) via Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span><span class="sxs-lookup"><span data-stu-id="41200-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="41200-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="41200-106">Before you begin</span></span>
<span data-ttu-id="41200-107">tooperform hello taken die in dit artikel worden vermeld, hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="41200-107">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="41200-108">Een geldige **Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="41200-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="41200-109">Een **Azure AD-directory** -ofwel gesynchroniseerd met een on-premises adreslijst of een map alleen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="41200-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="41200-110">**Azure AD Domain Services** moet zijn ingeschakeld voor hello Azure AD-directory.</span><span class="sxs-lookup"><span data-stu-id="41200-110">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="41200-111">Als u dit nog niet hebt gedaan, volgt u alle Hallo taken die worden beschreven in Hallo [handleiding](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="41200-111">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="41200-112">Een **certificaat toobe gebruikt tooenable beveiligde LDAP**.</span><span class="sxs-lookup"><span data-stu-id="41200-112">A **certificate toobe used tooenable secure LDAP**.</span></span>

   * <span data-ttu-id="41200-113">**Aanbevolen** -een certificaat verkrijgen van een betrouwbare, openbare certificeringsinstantie.</span><span class="sxs-lookup"><span data-stu-id="41200-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="41200-114">Deze configuratieoptie is veiliger.</span><span class="sxs-lookup"><span data-stu-id="41200-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="41200-115">U kunt ook u kunt ook te[een zelfondertekend certificaat maken](#task-1---obtain-a-certificate-for-secure-ldap) zoals verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="41200-115">Alternately, you may also choose too[create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a><span data-ttu-id="41200-116">Vereisten voor Hallo beveiligde LDAP-certificaat</span><span class="sxs-lookup"><span data-stu-id="41200-116">Requirements for hello secure LDAP certificate</span></span>
<span data-ttu-id="41200-117">Verkrijgen van een geldig certificaat per Hallo richtlijnen te volgen voordat u beveiligde LDAP inschakelen.</span><span class="sxs-lookup"><span data-stu-id="41200-117">Acquire a valid certificate per hello following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="41200-118">Er fouten optreden als u tooenable probeert beveiligde LDAP voor uw beheerde domein met een ongeldig/onjuist certificaat.</span><span class="sxs-lookup"><span data-stu-id="41200-118">You encounter failures if you try tooenable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="41200-119">**Vertrouwde uitgevers** -Hallo certificaat moet zijn uitgegeven door een instantie wordt vertrouwd door computers die verbinding maken toohello beheerde domein met behulp van beveiligde LDAP.</span><span class="sxs-lookup"><span data-stu-id="41200-119">**Trusted issuer** - hello certificate must be issued by an authority trusted by computers connecting toohello managed domain using secure LDAP.</span></span> <span data-ttu-id="41200-120">Deze instantie is mogelijk een openbare certificeringsinstantie wordt vertrouwd door deze computers.</span><span class="sxs-lookup"><span data-stu-id="41200-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="41200-121">**Levensduur** -Hallo certificaat moet geldig zijn ten minste Hallo komende 3-6 maanden.</span><span class="sxs-lookup"><span data-stu-id="41200-121">**Lifetime** - hello certificate must be valid for at least hello next 3-6 months.</span></span> <span data-ttu-id="41200-122">Beveiligde LDAP toegang tooyour beheerd domein wordt onderbroken wanneer Hallo het certificaat verloopt.</span><span class="sxs-lookup"><span data-stu-id="41200-122">Secure LDAP access tooyour managed domain is disrupted when hello certificate expires.</span></span>
3. <span data-ttu-id="41200-123">**Onderwerpnaam** -Hallo onderwerpnaam op Hallo certificaat moet een jokerteken voor uw beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="41200-123">**Subject name** - hello subject name on hello certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="41200-124">Bijvoorbeeld, als uw domein is, contoso100.com' genoemd, Hallo de naam van de certificaathouder moet ' *. contoso100.com'.</span><span class="sxs-lookup"><span data-stu-id="41200-124">For instance, if your domain is named 'contoso100.com', hello certificate's subject name must be '*.contoso100.com'.</span></span> <span data-ttu-id="41200-125">Hallo DNS-naam (alternatieve onderwerpnaam) toothis jokertekennaam instellen.</span><span class="sxs-lookup"><span data-stu-id="41200-125">Set hello DNS name (subject alternate name) toothis wildcard name.</span></span>
4. <span data-ttu-id="41200-126">**Sleutelgebruik** - Hallo-certificaat moet worden geconfigureerd voor Hallo na gebruikt - digitale handtekeningen en sleutelcodering.</span><span class="sxs-lookup"><span data-stu-id="41200-126">**Key usage** - hello certificate must be configured for hello following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="41200-127">**Doel van het certificaat** -Hallo moet geldig zijn voor SSL-serververificatie.</span><span class="sxs-lookup"><span data-stu-id="41200-127">**Certificate purpose** - hello certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="41200-128">**Ondernemings-CA's:** Azure AD Domain Services biedt geen ondersteuning voor het gebruik van beveiligde LDAP certificaten uitgegeven door een certificeringsinstantie voor ondernemingen van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="41200-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="41200-129">Deze beperking is omdat het Hallo-service de ondernemings-CA als een basiscertificeringsinstantie niet vertrouwt.</span><span class="sxs-lookup"><span data-stu-id="41200-129">This restriction is because hello service does not trust your enterprise CA as a root certification authority.</span></span> 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="41200-130">Taak 1: een certificaat verkrijgen voor beveiligde LDAP</span><span class="sxs-lookup"><span data-stu-id="41200-130">Task 1 - obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="41200-131">de eerste taak Hallo omvat het verkrijgen van een certificaat wordt gebruikt voor beveiligde LDAP toegang toohello beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="41200-131">hello first task involves obtaining a certificate used for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="41200-132">U hebt hiervoor twee opties:</span><span class="sxs-lookup"><span data-stu-id="41200-132">You have two options:</span></span>

* <span data-ttu-id="41200-133">Een certificaat verkrijgen van een certificeringsinstantie (CA).</span><span class="sxs-lookup"><span data-stu-id="41200-133">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="41200-134">Hallo-instantie is mogelijk een openbare certificeringsinstantie.</span><span class="sxs-lookup"><span data-stu-id="41200-134">hello authority may be a public certification authority.</span></span>
* <span data-ttu-id="41200-135">Een zelfondertekend certificaat maken.</span><span class="sxs-lookup"><span data-stu-id="41200-135">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="41200-136">Optie een (aanbevolen) - een beveiligde LDAP-certificaat verkrijgen van een certificeringsinstantie (CA)</span><span class="sxs-lookup"><span data-stu-id="41200-136">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="41200-137">Als uw organisatie de certificaten van een openbare certificeringsinstantie verkrijgt, moet u tooobtain Hallo beveiligde LDAP-certificaat van een openbare certificeringsinstantie.</span><span class="sxs-lookup"><span data-stu-id="41200-137">If your organization obtains its certificates from a public certification authority, you need tooobtain hello secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="41200-138">Wanneer u een certificaat aanvraagt, zorg ervoor dat u voldoen aan alle Hallo vereisten die worden beschreven in [vereisten voor beveiligde LDAP-certificaat Hallo](#requirements-for-the-secure-ldap-certificate).</span><span class="sxs-lookup"><span data-stu-id="41200-138">When requesting a certificate, ensure that you satisfy all hello requirements outlined in [Requirements for hello secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="41200-139">Clientcomputers die tooconnect toohello beheerde domein met behulp van beveiligde LDAP moeten moeten Hallo-uitgever van Hallo beveiligde LDAP-certificaat vertrouwen.</span><span class="sxs-lookup"><span data-stu-id="41200-139">Client computers that need tooconnect toohello managed domain using secure LDAP must trust hello issuer of hello secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="41200-140">Optie B - een zelfondertekend certificaat maken voor beveiligde LDAP</span><span class="sxs-lookup"><span data-stu-id="41200-140">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="41200-141">Als u niet van plan toouse een certificaat van een openbare certificeringsinstantie bent, kunt u toocreate een zelfondertekend certificaat voor beveiligde LDAP.</span><span class="sxs-lookup"><span data-stu-id="41200-141">If you do not expect toouse a certificate from a public certification authority, you may choose toocreate a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="41200-142">**Maak een zelfondertekend certificaat met behulp van PowerShell**</span><span class="sxs-lookup"><span data-stu-id="41200-142">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="41200-143">Open op uw Windows-computer als een nieuwe PowerShell-venster **beheerder** en type Hallo-opdrachten, toocreate een nieuw zelfondertekend certificaat te volgen.</span><span class="sxs-lookup"><span data-stu-id="41200-143">On your Windows computer, open a new PowerShell window as **Administrator** and type hello following commands, toocreate a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="41200-144">Vervang in Hallo voorgaande voorbeeld, '*. contoso100.com' met Hallo DNS-domeinnaam van uw beheerde domein. For example, als u een beheerd domein 'contoso100.onmicrosoft.com' genoemd, vervangen door '*. contoso100.com' in hello boven het script dat ' *. contoso100.onmicrosoft.com').</span><span class="sxs-lookup"><span data-stu-id="41200-144">In hello preceding sample, replace '*.contoso100.com' with hello DNS domain name of your managed domain. For example, if you created a managed domain called 'contoso100.onmicrosoft.com', replace '*.contoso100.com' in hello above script with '*.contoso100.onmicrosoft.com').</span></span>

![Azure AD-directory selecteren](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="41200-146">Hallo nieuw gemaakt zelfondertekend certificaat wordt geplaatst in het certificaatarchief Hallo van de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="41200-146">hello newly created self-signed certificate is placed in hello local machine's certificate store.</span></span>


## <a name="next-step"></a><span data-ttu-id="41200-147">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="41200-147">Next step</span></span>
[<span data-ttu-id="41200-148">Taak 2: Hallo beveiligde LDAP certificaat tooa exporteren. PFX-bestand</span><span class="sxs-lookup"><span data-stu-id="41200-148">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
