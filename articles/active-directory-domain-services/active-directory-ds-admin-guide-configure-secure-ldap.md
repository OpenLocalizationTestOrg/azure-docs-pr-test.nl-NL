---
title: Beveiligde LDAP (LDAPS) in Azure AD Domain Services configureren | Microsoft Docs
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
ms.openlocfilehash: 93afa49166c5b31d23237c308b9d34f6d6f3507d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="49a93-103">Beveiligde LDAP (LDAPS) voor een beheerd domein van Azure AD Domain Services configureren</span><span class="sxs-lookup"><span data-stu-id="49a93-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="49a93-104">Dit artikel laat zien hoe u beveiligde Lightweight Directory Access Protocol (LDAPS) kunt inschakelen voor uw beheerde domein van Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="49a93-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="49a93-105">Beveiligde LDAP wordt ook wel ' Lightweight Directory Access Protocol (LDAP) via Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span><span class="sxs-lookup"><span data-stu-id="49a93-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="49a93-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="49a93-106">Before you begin</span></span>
<span data-ttu-id="49a93-107">Als u wilt uitvoeren van de taken worden in dit artikel worden vermeld, hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="49a93-107">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="49a93-108">Een geldige **Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="49a93-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="49a93-109">Een **Azure AD-directory** -ofwel gesynchroniseerd met een on-premises adreslijst of een map alleen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="49a93-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="49a93-110">**Azure AD Domain Services** moet zijn ingeschakeld voor de Azure AD-directory.</span><span class="sxs-lookup"><span data-stu-id="49a93-110">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="49a93-111">Als u dit nog niet hebt gedaan, volgt u alle taken die worden beschreven in de [handleiding](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="49a93-111">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="49a93-112">Een **certificaat moet worden gebruikt voor het inschakelen van beveiligde LDAP**.</span><span class="sxs-lookup"><span data-stu-id="49a93-112">A **certificate to be used to enable secure LDAP**.</span></span>

   * <span data-ttu-id="49a93-113">**Aanbevolen** -een certificaat verkrijgen van een betrouwbare, openbare certificeringsinstantie.</span><span class="sxs-lookup"><span data-stu-id="49a93-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="49a93-114">Deze configuratieoptie is veiliger.</span><span class="sxs-lookup"><span data-stu-id="49a93-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="49a93-115">U kunt ook u kunt ook [een zelfondertekend certificaat maken](#task-1---obtain-a-certificate-for-secure-ldap) zoals verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="49a93-115">Alternately, you may also choose to [create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-the-secure-ldap-certificate"></a><span data-ttu-id="49a93-116">Vereisten voor de beveiligde LDAP-certificaat</span><span class="sxs-lookup"><span data-stu-id="49a93-116">Requirements for the secure LDAP certificate</span></span>
<span data-ttu-id="49a93-117">Een geldig certificaat per de volgende richtlijnen te verkrijgen voordat u beveiligde LDAP inschakelen.</span><span class="sxs-lookup"><span data-stu-id="49a93-117">Acquire a valid certificate per the following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="49a93-118">Er optreden fouten als u probeert in te schakelen beveiligde LDAP voor uw beheerde domein met een ongeldig/onjuist certificaat.</span><span class="sxs-lookup"><span data-stu-id="49a93-118">You encounter failures if you try to enable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="49a93-119">**Vertrouwde uitgevers** -het certificaat moet worden uitgegeven door een instantie wordt vertrouwd door computers verbinding maken met het beheerde domein met behulp van beveiligde LDAP.</span><span class="sxs-lookup"><span data-stu-id="49a93-119">**Trusted issuer** - The certificate must be issued by an authority trusted by computers connecting to the managed domain using secure LDAP.</span></span> <span data-ttu-id="49a93-120">Deze instantie is mogelijk een openbare certificeringsinstantie wordt vertrouwd door deze computers.</span><span class="sxs-lookup"><span data-stu-id="49a93-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="49a93-121">**Levensduur** -het certificaat moet geldig zijn ten minste de komende 3-6 maanden.</span><span class="sxs-lookup"><span data-stu-id="49a93-121">**Lifetime** - The certificate must be valid for at least the next 3-6 months.</span></span> <span data-ttu-id="49a93-122">Beveiligde LDAP-toegang tot uw beheerde domein wordt onderbroken wanneer het certificaat is verlopen.</span><span class="sxs-lookup"><span data-stu-id="49a93-122">Secure LDAP access to your managed domain is disrupted when the certificate expires.</span></span>
3. <span data-ttu-id="49a93-123">**Onderwerpnaam** -de onderwerpnaam op het certificaat moet een jokerteken voor uw beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="49a93-123">**Subject name** - The subject name on the certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="49a93-124">Bijvoorbeeld, als uw domein met de naam, contoso100.com', de onderwerpnaam van het certificaat moet ' *. contoso100.com'.</span><span class="sxs-lookup"><span data-stu-id="49a93-124">For instance, if your domain is named 'contoso100.com', the certificate's subject name must be '*.contoso100.com'.</span></span> <span data-ttu-id="49a93-125">De DNS-naam (alternatieve onderwerpnaam) ingesteld op deze jokertekennaam.</span><span class="sxs-lookup"><span data-stu-id="49a93-125">Set the DNS name (subject alternate name) to this wildcard name.</span></span>
4. <span data-ttu-id="49a93-126">**Sleutelgebruik** -het certificaat moet worden geconfigureerd voor het volgende gebruikt - digitale handtekeningen en sleutelcodering.</span><span class="sxs-lookup"><span data-stu-id="49a93-126">**Key usage** - The certificate must be configured for the following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="49a93-127">**Doel van het certificaat** -het certificaat moet geldig zijn voor SSL-serververificatie.</span><span class="sxs-lookup"><span data-stu-id="49a93-127">**Certificate purpose** - The certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="49a93-128">**Ondernemings-CA's:** Azure AD Domain Services biedt geen ondersteuning voor het gebruik van beveiligde LDAP certificaten uitgegeven door een certificeringsinstantie voor ondernemingen van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="49a93-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="49a93-129">Deze beperking is omdat de service de ondernemings-CA als een basiscertificeringsinstantie niet vertrouwt.</span><span class="sxs-lookup"><span data-stu-id="49a93-129">This restriction is because the service does not trust your enterprise CA as a root certification authority.</span></span> 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="49a93-130">Taak 1: een certificaat verkrijgen voor beveiligde LDAP</span><span class="sxs-lookup"><span data-stu-id="49a93-130">Task 1 - obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="49a93-131">De eerste taak omvat het verkrijgen van een certificaat gebruikt voor beveiligde LDAP-toegang tot het beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="49a93-131">The first task involves obtaining a certificate used for secure LDAP access to the managed domain.</span></span> <span data-ttu-id="49a93-132">U hebt hiervoor twee opties:</span><span class="sxs-lookup"><span data-stu-id="49a93-132">You have two options:</span></span>

* <span data-ttu-id="49a93-133">Een certificaat verkrijgen van een certificeringsinstantie (CA).</span><span class="sxs-lookup"><span data-stu-id="49a93-133">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="49a93-134">De instantie is mogelijk een openbare certificeringsinstantie.</span><span class="sxs-lookup"><span data-stu-id="49a93-134">The authority may be a public certification authority.</span></span>
* <span data-ttu-id="49a93-135">Een zelfondertekend certificaat maken.</span><span class="sxs-lookup"><span data-stu-id="49a93-135">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="49a93-136">Optie een (aanbevolen) - een beveiligde LDAP-certificaat verkrijgen van een certificeringsinstantie (CA)</span><span class="sxs-lookup"><span data-stu-id="49a93-136">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="49a93-137">Als uw organisatie de certificaten van een openbare certificeringsinstantie verkrijgt, moet u de beveiligde LDAP-certificaat verkrijgen van een openbare certificeringsinstantie.</span><span class="sxs-lookup"><span data-stu-id="49a93-137">If your organization obtains its certificates from a public certification authority, you need to obtain the secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="49a93-138">Wanneer u een certificaat aanvraagt, zorg ervoor dat u voldoen aan alle vereisten die worden beschreven in [vereisten voor de LDAP om certificaten veilig](#requirements-for-the-secure-ldap-certificate).</span><span class="sxs-lookup"><span data-stu-id="49a93-138">When requesting a certificate, ensure that you satisfy all the requirements outlined in [Requirements for the secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="49a93-139">Clientcomputers die verbinding moeten maken met het beheerde domein met behulp van beveiligde LDAP moeten de verlener van het beveiligde LDAP-certificaat vertrouwen.</span><span class="sxs-lookup"><span data-stu-id="49a93-139">Client computers that need to connect to the managed domain using secure LDAP must trust the issuer of the secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="49a93-140">Optie B - een zelfondertekend certificaat maken voor beveiligde LDAP</span><span class="sxs-lookup"><span data-stu-id="49a93-140">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="49a93-141">Als u niet van plan bent om een certificaat van een openbare certificeringsinstantie te gebruiken, kunt u een zelfondertekend certificaat maken voor beveiligde LDAP.</span><span class="sxs-lookup"><span data-stu-id="49a93-141">If you do not expect to use a certificate from a public certification authority, you may choose to create a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="49a93-142">**Maak een zelfondertekend certificaat met behulp van PowerShell**</span><span class="sxs-lookup"><span data-stu-id="49a93-142">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="49a93-143">Open op uw Windows-computer als een nieuwe PowerShell-venster **beheerder** en typ de volgende opdrachten, een nieuw zelfondertekend certificaat maken.</span><span class="sxs-lookup"><span data-stu-id="49a93-143">On your Windows computer, open a new PowerShell window as **Administrator** and type the following commands, to create a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="49a93-144">Vervang in het voorgaande voorbeeld, '*. contoso100.com' met de DNS-domeinnaam van uw beheerde domein. For example, als u een beheerd domein 'contoso100.onmicrosoft.com' genoemd, vervangen door '*. contoso100.com' in het bovenstaande script met ' *. contoso100.onmicrosoft.com').</span><span class="sxs-lookup"><span data-stu-id="49a93-144">In the preceding sample, replace '*.contoso100.com' with the DNS domain name of your managed domain. For example, if you created a managed domain called 'contoso100.onmicrosoft.com', replace '*.contoso100.com' in the above script with '*.contoso100.onmicrosoft.com').</span></span>

![Azure AD-directory selecteren](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="49a93-146">De zojuist gemaakte zelf-ondertekend certificaat wordt geplaatst in het certificaatarchief van de lokale machine.</span><span class="sxs-lookup"><span data-stu-id="49a93-146">The newly created self-signed certificate is placed in the local machine's certificate store.</span></span>


## <a name="next-step"></a><span data-ttu-id="49a93-147">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="49a93-147">Next step</span></span>
[<span data-ttu-id="49a93-148">Taak 2: het beveiligde LDAP-certificaat te exporteren een. PFX-bestand</span><span class="sxs-lookup"><span data-stu-id="49a93-148">Task 2 - export the secure LDAP certificate to a .PFX file</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
