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
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Beveiligde LDAP (LDAPS) voor een beheerd domein van Azure AD Domain Services configureren
Dit artikel laat zien hoe u beveiligde Lightweight Directory Access Protocol (LDAPS) kunt inschakelen voor uw beheerde domein van Azure AD Domain Services. Beveiligde LDAP wordt ook wel ' Lightweight Directory Access Protocol (LDAP) via Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.

## <a name="before-you-begin"></a>Voordat u begint
tooperform hello taken die in dit artikel worden vermeld, hebt u nodig:

1. Een geldige **Azure-abonnement**.
2. Een **Azure AD-directory** -ofwel gesynchroniseerd met een on-premises adreslijst of een map alleen in de cloud.
3. **Azure AD Domain Services** moet zijn ingeschakeld voor hello Azure AD-directory. Als u dit nog niet hebt gedaan, volgt u alle Hallo taken die worden beschreven in Hallo [handleiding](active-directory-ds-getting-started.md).
4. Een **certificaat toobe gebruikt tooenable beveiligde LDAP**.

   * **Aanbevolen** -een certificaat verkrijgen van een betrouwbare, openbare certificeringsinstantie. Deze configuratieoptie is veiliger.
   * U kunt ook u kunt ook te[een zelfondertekend certificaat maken](#task-1---obtain-a-certificate-for-secure-ldap) zoals verderop in dit artikel.

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a>Vereisten voor Hallo beveiligde LDAP-certificaat
Verkrijgen van een geldig certificaat per Hallo richtlijnen te volgen voordat u beveiligde LDAP inschakelen. Er fouten optreden als u tooenable probeert beveiligde LDAP voor uw beheerde domein met een ongeldig/onjuist certificaat.

1. **Vertrouwde uitgevers** -Hallo certificaat moet zijn uitgegeven door een instantie wordt vertrouwd door computers die verbinding maken toohello beheerde domein met behulp van beveiligde LDAP. Deze instantie is mogelijk een openbare certificeringsinstantie wordt vertrouwd door deze computers.
2. **Levensduur** -Hallo certificaat moet geldig zijn ten minste Hallo komende 3-6 maanden. Beveiligde LDAP toegang tooyour beheerd domein wordt onderbroken wanneer Hallo het certificaat verloopt.
3. **Onderwerpnaam** -Hallo onderwerpnaam op Hallo certificaat moet een jokerteken voor uw beheerde domein. Bijvoorbeeld, als uw domein is, contoso100.com' genoemd, Hallo de naam van de certificaathouder moet ' *. contoso100.com'. Hallo DNS-naam (alternatieve onderwerpnaam) toothis jokertekennaam instellen.
4. **Sleutelgebruik** - Hallo-certificaat moet worden geconfigureerd voor Hallo na gebruikt - digitale handtekeningen en sleutelcodering.
5. **Doel van het certificaat** -Hallo moet geldig zijn voor SSL-serververificatie.

> [!NOTE]
> **Ondernemings-CA's:** Azure AD Domain Services biedt geen ondersteuning voor het gebruik van beveiligde LDAP certificaten uitgegeven door een certificeringsinstantie voor ondernemingen van uw organisatie. Deze beperking is omdat het Hallo-service de ondernemings-CA als een basiscertificeringsinstantie niet vertrouwt. 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a>Taak 1: een certificaat verkrijgen voor beveiligde LDAP
de eerste taak Hallo omvat het verkrijgen van een certificaat wordt gebruikt voor beveiligde LDAP toegang toohello beheerde domein. U hebt hiervoor twee opties:

* Een certificaat verkrijgen van een certificeringsinstantie (CA). Hallo-instantie is mogelijk een openbare certificeringsinstantie.
* Een zelfondertekend certificaat maken.

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a>Optie een (aanbevolen) - een beveiligde LDAP-certificaat verkrijgen van een certificeringsinstantie (CA)
Als uw organisatie de certificaten van een openbare certificeringsinstantie verkrijgt, moet u tooobtain Hallo beveiligde LDAP-certificaat van een openbare certificeringsinstantie.

Wanneer u een certificaat aanvraagt, zorg ervoor dat u voldoen aan alle Hallo vereisten die worden beschreven in [vereisten voor beveiligde LDAP-certificaat Hallo](#requirements-for-the-secure-ldap-certificate).

> [!NOTE]
> Clientcomputers die tooconnect toohello beheerde domein met behulp van beveiligde LDAP moeten moeten Hallo-uitgever van Hallo beveiligde LDAP-certificaat vertrouwen.
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a>Optie B - een zelfondertekend certificaat maken voor beveiligde LDAP
Als u niet van plan toouse een certificaat van een openbare certificeringsinstantie bent, kunt u toocreate een zelfondertekend certificaat voor beveiligde LDAP.

**Maak een zelfondertekend certificaat met behulp van PowerShell**

Open op uw Windows-computer als een nieuwe PowerShell-venster **beheerder** en type Hallo-opdrachten, toocreate een nieuw zelfondertekend certificaat te volgen.

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

Vervang in Hallo voorgaande voorbeeld, '*. contoso100.com' met Hallo DNS-domeinnaam van uw beheerde domein. For example, als u een beheerd domein 'contoso100.onmicrosoft.com' genoemd, vervangen door '*. contoso100.com' in hello boven het script dat ' *. contoso100.onmicrosoft.com').

![Azure AD-directory selecteren](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

Hallo nieuw gemaakt zelfondertekend certificaat wordt geplaatst in het certificaatarchief Hallo van de lokale computer.


## <a name="next-step"></a>Volgende stap
[Taak 2: Hallo beveiligde LDAP certificaat tooa exporteren. PFX-bestand](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
