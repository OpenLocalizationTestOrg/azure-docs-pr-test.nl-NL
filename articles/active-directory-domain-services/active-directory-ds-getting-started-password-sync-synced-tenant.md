---
title: 'Azure AD Domain Services: wachtwoordsynchronisatie inschakelen | Microsoft Docs'
description: Aan de slag met Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8731f2b2-661c-4f3d-adba-2c9e06344537
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: a7a6ee0f83d3d9bdaf236717efb39155a26934e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="0e407-103">Wachtwoord synchronisatie tooAzure Active Directory Domain Services inschakelen</span><span class="sxs-lookup"><span data-stu-id="0e407-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="0e407-104">Tijdens de vorige taken hebt u Azure Active Directory Domain Services ingeschakeld voor uw Azure Active Directory-tenant (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0e407-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="0e407-105">de volgende taak Hallo is tooenable synchronisatie van referentie-hashes die vereist zijn voor NT LAN Manager (NTLM) en Kerberos-verificatie tooAzure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="0e407-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="0e407-106">Nadat u een referentie-synchronisatie hebt ingesteld, kunnen gebruikers zich aanmelden in toohello beheerde domein met hun bedrijfsreferenties.</span><span class="sxs-lookup"><span data-stu-id="0e407-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="0e407-107">Hallo stappen die nodig zijn verschillend voor de gebruiker alleen in de cloud accounts tegenover gebruikersaccounts die worden gesynchroniseerd vanuit uw lokale directory met Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="0e407-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="0e407-108">Als uw Azure AD-tenant een combinatie van heeft cloud alleen gebruikers en gebruikers van uw on-premises AD, moet u tooperform na beide stappen.</span><span class="sxs-lookup"><span data-stu-id="0e407-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="0e407-109">**Alleen in de cloud gebruikersaccounts**: [wachtwoorden synchroniseren voor alleen in de cloud gebruikersaccounts tooyour beheerd domein](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="0e407-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="0e407-110">**Lokale gebruikersaccounts**: [wachtwoorden synchroniseren voor gebruikersaccounts die zijn gesynchroniseerd vanuit uw on-premises AD tooyour beheerd domein](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="0e407-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a><span data-ttu-id="0e407-111">Taak 5: inschakelen wachtwoord synchronisatie tooyour beheerd domein voor gebruikersaccounts die zijn gesynchroniseerd met uw on-premises AD</span><span class="sxs-lookup"><span data-stu-id="0e407-111">Task 5: enable password synchronization tooyour managed domain for user accounts synced with your on-premises AD</span></span>
<span data-ttu-id="0e407-112">Een gesynchroniseerde Azure AD-tenant toosynchronize met van uw organisatie on-premises directory via Azure AD Connect is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="0e407-112">A synced Azure AD tenant is set toosynchronize with your organization's on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="0e407-113">Azure AD Connect wordt standaard NTLM en Kerberos-referentie-hashes tooAzure AD niet gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="0e407-113">By default, Azure AD Connect does not synchronize NTLM and Kerberos credential hashes tooAzure AD.</span></span> <span data-ttu-id="0e407-114">toouse Azure AD Domain Services, moet u tooconfigure Azure AD Connect toosynchronize referentie-hashes voor NTLM en Kerberos-verificatie.</span><span class="sxs-lookup"><span data-stu-id="0e407-114">toouse Azure AD Domain Services, you need tooconfigure Azure AD Connect toosynchronize credential hashes required for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="0e407-115">Hallo stappen te volgen inschakelen synchronisatie van referentie-hashes Hallo vereist vanuit uw lokale directory tooyour Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="0e407-115">hello following steps enable synchronization of hello required credential hashes from your on-premises directory tooyour Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="0e407-116">Als uw organisatie gebruikersaccounts die worden gesynchroniseerd vanuit uw on-premises directory, moet synchronisatie van NTLM en Kerberos-hashes in volgorde toouse Hallo beheerde domein inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0e407-116">If your organization has user accounts that are synchronized from your on-premises directory, your must enable synchronization of NTLM and Kerberos hashes in order toouse hello managed domain.</span></span> <span data-ttu-id="0e407-117">Een gesynchroniseerde gebruikersaccount is een account dat is gemaakt in uw on-premises directory en is gesynchroniseerd tooyour Azure AD-tenant met Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="0e407-117">A synced user account is an account that was created in your on-premises directory and is synchronized tooyour Azure AD tenant using Azure AD Connect.</span></span>
>
>

### <a name="install-or-update-azure-ad-connect"></a><span data-ttu-id="0e407-118">Azure AD Connect installeren of bijwerken</span><span class="sxs-lookup"><span data-stu-id="0e407-118">Install or update Azure AD Connect</span></span>
<span data-ttu-id="0e407-119">Installeren van de meest recente aanbevolen Hallo versie van Azure AD Connect op een domein die lid zijn van de computer.</span><span class="sxs-lookup"><span data-stu-id="0e407-119">Install hello latest recommended release of Azure AD Connect on a domain joined computer.</span></span> <span data-ttu-id="0e407-120">Als u een bestaand exemplaar van Azure AD Connect-installatie hebt, moet u tooupdate deze toouse Hallo meest recente versie van Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="0e407-120">If you have an existing instance of Azure AD Connect setup, you need tooupdate it toouse hello latest version of Azure AD Connect.</span></span> <span data-ttu-id="0e407-121">tooavoid bekende problemen/fouten optreden die mogelijk al zijn opgelost, zorg ervoor dat u altijd de meest recente versie Hallo van Azure AD Connect gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0e407-121">tooavoid known issues/bugs that may have already been fixed, ensure you always use hello latest version of Azure AD Connect.</span></span>

<span data-ttu-id="0e407-122">**[Azure AD Connect downloaden](http://www.microsoft.com/download/details.aspx?id=47594)**</span><span class="sxs-lookup"><span data-stu-id="0e407-122">**[Download Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span></span>

<span data-ttu-id="0e407-123">Aanbevolen versie: **1.1.553.0** - gepubliceerd op 27 juni 2017.</span><span class="sxs-lookup"><span data-stu-id="0e407-123">Recommended version: **1.1.553.0** - published on June 27, 2017.</span></span>

> [!WARNING]
> <span data-ttu-id="0e407-124">U moet installeren Hallo meest recente versie van Azure AD Connect tooenable hello toosynchronize tooyour Azure AD-tenant oude wachtwoord referenties (vereist voor NTLM en Kerberos-verificatie) aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="0e407-124">You MUST install hello latest recommended release of Azure AD Connect tooenable hello legacy password credentials (required for NTLM and Kerberos authentication) toosynchronize tooyour Azure AD tenant.</span></span> <span data-ttu-id="0e407-125">Deze functionaliteit is niet beschikbaar in eerdere versies van Azure AD Connect of met Hallo oudere DirSync-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="0e407-125">This functionality is not available in prior releases of Azure AD Connect or with hello legacy DirSync tool.</span></span>
>
>

<span data-ttu-id="0e407-126">Installatie-instructies voor Azure AD Connect zijn beschikbaar in de volgende Hallo artikel - [aan de slag met Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="0e407-126">Installation instructions for Azure AD Connect are available in hello following article - [Getting started with Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span></span>

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a><span data-ttu-id="0e407-127">Synchronisatie van NTLM en Kerberos-referentie-hashes tooAzure AD inschakelen</span><span class="sxs-lookup"><span data-stu-id="0e407-127">Enable synchronization of NTLM and Kerberos credential hashes tooAzure AD</span></span>
<span data-ttu-id="0e407-128">Hallo volgende PowerShell-script op elk AD-forest tooforce volledige Wachtwoordsynchronisatie, uitvoeren en schakel alle on-premises gebruikers de referentie-hashes toosync tooyour Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="0e407-128">Execute hello following PowerShell script on each AD forest, tooforce full password synchronization, and enable all on-premises users’ credential hashes toosync tooyour Azure AD tenant.</span></span> <span data-ttu-id="0e407-129">Dit script kunt Hallo referentie-hashes voor NTLM of Kerberos-verificatie toobe gesynchroniseerde tooyour Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="0e407-129">This script enables hello credential hashes required for NTLM/Kerberos authentication toobe synchronized tooyour Azure AD tenant.</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"  
$azureadConnector = "<CASE SENSITIVE AZURE AD CONNECTOR NAME>"  
Import-Module adsync  
$c = Get-ADSyncConnector -Name $adConnector  
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1  
$c.GlobalParameters.Remove($p.Name)  
$c.GlobalParameters.Add($p)  
$c = Add-ADSyncConnector -Connector $c  
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $false   
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $true  
```

<span data-ttu-id="0e407-130">Afhankelijk van Hallo grootte van uw directory (aantal gebruikers, groepen enzovoort), synchronisatie van de referentie-hashes tooAzure AD tijd in beslag neemt.</span><span class="sxs-lookup"><span data-stu-id="0e407-130">Depending on hello size of your directory (number of users, groups etc.), synchronization of credential hashes tooAzure AD takes time.</span></span> <span data-ttu-id="0e407-131">Hallo wachtwoorden, worden gebruikt op Hallo Azure AD Domain Services beheerd domein kort nadat Hallo referentie-hashes zijn tooAzure AD gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="0e407-131">hello passwords will be usable on hello Azure AD Domain Services managed domain shortly after hello credential hashes have synchronized tooAzure AD.</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="0e407-132">Gerelateerde inhoud</span><span class="sxs-lookup"><span data-stu-id="0e407-132">Related Content</span></span>
* [<span data-ttu-id="0e407-133">Inschakelen wachtwoord synchronisatie tooAAD Domain Services voor een alleen-Azure AD-directory</span><span class="sxs-lookup"><span data-stu-id="0e407-133">Enable password synchronization tooAAD Domain Services for a cloud-only Azure AD directory</span></span>](active-directory-ds-getting-started-password-sync.md)
* [<span data-ttu-id="0e407-134">Een beheerd domein van Azure AD Domain Services beheren</span><span class="sxs-lookup"><span data-stu-id="0e407-134">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="0e407-135">Deelnemen aan een Windows virtuele machine tooan Azure AD Domain Services beheerd domein</span><span class="sxs-lookup"><span data-stu-id="0e407-135">Join a Windows virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="0e407-136">Deelnemen aan een Red Hat Enterprise Linux virtuele machine tooan Azure AD Domain Services beheerd domein</span><span class="sxs-lookup"><span data-stu-id="0e407-136">Join a Red Hat Enterprise Linux virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
