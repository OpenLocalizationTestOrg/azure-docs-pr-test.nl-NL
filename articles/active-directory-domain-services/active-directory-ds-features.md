---
title: 'Azure Active Directory Domain Services: Functies | Microsoft Docs'
description: Functies van Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8d1c3eb3-1022-4add-a919-c98cc6584af1
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1a9417bafa35959d280eabf3db6ad8530db4ea45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services"></a>Azure AD Domain Services
## <a name="features"></a>Functies
Hallo volgende functies zijn beschikbaar in Azure AD Domain Services beheerd domeinen.

* **Eenvoudige implementatie-ervaring:** u Azure AD Domain Services voor uw Azure AD-tenant met behulp van een paar klikken kunt inschakelen. Ongeacht of uw Azure AD-tenant is van een cloud-tenant of gesynchroniseerd met uw on-premises directory, kan uw beheerde domein snel worden ingericht.
* **Ondersteuning voor het lid van domein:** kunt u gemakkelijk computers in uw beheerde domein is beschikbaar in virtuele Azure-netwerk Hallo lid van een domein. Hallo domein ervaring op Windows-client en Server-besturingssystemen werkt naadloos met domeinen die door Azure AD Domain Services zijn verwerkt. U kunt ook geautomatiseerde domein tooling tegen die domeinen.
* **Exemplaar van één domein per Azure AD-adreslijst:** kunt u één Active Directory-domein voor elke Azure AD-directory.
* **Domeinen met aangepaste namen maken:** kunt u domeinen met aangepaste namen (bijvoorbeeld, contoso100.com') met behulp van Azure AD Domain Services. U kunt beide geverifieerde of niet-geverifieerde domeinnamen gebruiken. Eventueel u ook een domein kunt maken met de ingebouwde domeinachtervoegsel hello (dat wil zeggen, ' *. onmicrosoft.com') die worden aangeboden door uw Azure AD-directory.
* **Geïntegreerd met Azure AD:** u niet moet tooconfigure of beheren van replicatie tooAzure AD Domain Services. Gebruikersaccounts, groepslidmaatschappen en referenties van gebruiker (wachtwoorden) van uw Azure AD-directory zijn automatisch beschikbaar zijn in Azure AD Domain Services. Nieuwe gebruikers, groepen of wijzigingen tooattributes van uw Azure AD-tenant of uw on-premises directory worden automatisch gesynchroniseerd tooAzure AD Domain Services.
* **NTLM en Kerberos-verificatie:** met ondersteuning voor NTLM en Kerberos-verificatie, kunt u toepassingen die afhankelijk van geïntegreerde Windows-verificatie zijn implementeren.
* **Gebruik uw zakelijke referenties/wachtwoorden:** wachtwoorden voor gebruikers in uw Azure AD-tenant werken met Azure AD Domain Services. Gebruikers kunnen hun zakelijke referenties toodomain-join-machines gebruiken, aanmelden, interactief of via Extern bureaublad en verificatie uitvoeren tegen Hallo beheerd domein.
* **LDAP-binding & LDAP lezen ondersteuning:** kunt u toepassingen die afhankelijk van LDAP-bindingen tooauthenticate gebruikers in domeinen die door Azure AD Domain Services zijn verwerkt zijn. Bovendien leesbewerkingen toepassingen die gebruikmaken van LDAP tooquery gebruiker of computer kenmerken uit Hallo directory kunnen ook worden gebruikt op basis van Azure AD Domain Services.
* **Beveiligde LDAP (LDAPS):** kunt u access toohello directory via beveiligde LDAP (LDAPS) inschakelen. Beveiligde LDAP-toegang is beschikbaar in het virtuele netwerk Hallo standaard. Echter, kunt u eventueel ook beveiligde LDAP toegang inschakelen via Hallo internet.
* **Groepsbeleid:** kunt u één ingebouwde GPO elke voor Hallo-gebruikers en computers containers tooenforce naleving vereist beveiligingsbeleid voor gebruikersaccounts en domeincomputers. U kunt ook uw eigen aangepaste GPO's maken en hieraan toocustom organisatie-eenheden te[beheren van Groepsbeleid](active-directory-ds-admin-guide-administer-group-policy.md).
* **DNS beheren:** leden van Hallo ' AAD DC' beheerdersgroep DNS kunnen beheren voor uw beheerde domein met behulp van bekende DNS-beheer, hulpprogramma's zoals Hallo DNS-beheer MMC-module.
* **Aangepaste organisatie-eenheden (OE's) maken:** kunnen leden van Hallo ' AAD DC' beheerdersgroep aangepaste OE's maken in Hallo beheerde domein. Deze gebruikers worden volledige beheerdersrechten verleend via aangepaste OE's, zodat ze kunnen toevoegen of verwijderen serviceaccounts voor groepen, computers, groepen enzovoort binnen deze aangepaste organisatie-eenheden.
* **Beschikbaar in meerdere Azure-regio's:** Zie Hallo [Azure-services per regio](https://azure.microsoft.com/regions/#services/) pagina tooknow hello Azure-regio's waar Azure AD Domain Services beschikbaar is.
* **Hoge beschikbaarheid:** Azure AD Domain Services biedt hoge beschikbaarheid voor uw domein. Deze functie biedt Hallo garantie van hogere service uptime en herstelmogelijkheden toofailures. Ingebouwde voor health monitoring aanbiedingen automatisch doorvoeren van fouten door draaien nieuwe exemplaren van de exemplaren tooreplace is mislukt en tooprovide steeds service voor uw domein.
* **Bekend beheerhulpprogramma's gebruiken:** kunt u vertrouwde hulpprogramma's voor Windows Server Active Directory-beheer zoals Hallo Active Directory-beheercentrum of Active Directory PowerShell tooadminister beheerde domeinen.
