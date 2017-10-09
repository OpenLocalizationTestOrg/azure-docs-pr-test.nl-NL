---
title: aaaAccess Sleutelkluis achter een firewall | Microsoft Docs
description: Meer informatie over hoe tooaccess Azure Key Vault van een toepassing achter een firewall
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 50d21774-2ee1-4212-8995-570c9de603c5
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: ab4bb0c27a41fef878a20dace6cab203df04e579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-key-vault-behind-a-firewall"></a>Toegang tot Azure Key Vault achter een firewall
### <a name="q-my-key-vault-client-application-needs-toobe-behind-a-firewall-what-ports-hosts-or-ip-addresses-should-i-open-tooenable-access-tooa-key-vault"></a>V: Mijn clienttoepassing sleutelkluis moet toobe achter een firewall. Welke poorten, hosts of IP-adressen is het openen van tooenable toegang tooa sleutelkluis?
een sleutelkluis tooaccess, uw clienttoepassing sleutelkluis heeft tooaccess meerdere eindpunten voor verschillende functies:

* Verificatie via Azure Active Directory (Azure AD).
* Beheer van Azure Key Vault. Dit omvat het maken, lezen, bijwerken, verwijderen en instellen van toegangsbeleid via Azure Resource Manager.
* Toegang tot en beheer van objecten (sleutels en geheimen) die zijn opgeslagen in de Sleutelkluis zelf, gaan via Hallo Key Vault-specifieke eindpunt (bijvoorbeeld [https://yourvaultname.vault.azure.net](https://yourvaultname.vault.azure.net)).  

Er zijn enkele verschillen, afhankelijk van uw configuratie en omgeving.   

## <a name="ports"></a>Poorten
Alle verkeer tooa sleutelkluis voor alle drie functies (verificatie-, beheer- en vlak toegang) gaat via HTTPS: poort 443. Voor CRL gaat het verkeer soms echter via HTTP (poort 80). Clients die ondersteuning bieden voor OCSP, mogen CRL niet bereiken, maar kunnen soms [http://cdp1.public-trust.com/CRL/Omniroot2025.crl](http://cdp1.public-trust.com/CRL/Omniroot2025.crl) bereiken.  

## <a name="authentication"></a>Authentication
Sleutelkluis-clienttoepassingen moet tooaccess eindpunten voor Azure Active Directory voor verificatie. Hallo eindpunt dat wordt gebruikt afhankelijk van Hallo configuratie van Azure AD-tenant, Hallo type principal (UPN of service-principal) en Hallo type-account, bijvoorbeeld een Microsoft-account of een werk- of schoolaccount.  

| Type principal | Eindpunt:poort |
| --- | --- |
| Gebruiker gebruikt Microsoft-account<br> (bijvoorbeeld user@hotmail.com) |**Wereldwijd:**<br> login.microsoftonline.com:443<br><br> **Azure China:**<br> login.chinacloudapi.cn:443<br><br>**Azure van de Amerikaanse overheid:**<br> login-us.microsoftonline.com:443<br><br>**Azure Duitsland:**<br> login.microsoftonline.de:443<br><br> en <br>login.live.com:443 |
| Gebruiker of service-principal met een werk- of schoolaccount met Azure AD (bijvoorbeeld user@contoso.com) |**Wereldwijd:**<br> login.microsoftonline.com:443<br><br> **Azure China:**<br> login.chinacloudapi.cn:443<br><br>**Azure van de Amerikaanse overheid:**<br> login-us.microsoftonline.com:443<br><br>**Azure Duitsland:**<br> login.microsoftonline.de:443 |
| Gebruiker of service-principal maken met werk of schoolaccount, plus Active Directory Federation Services (AD FS) of andere federatieve eindpunt (bijvoorbeeld user@contoso.com) |Alle eindpunten voor een werk- of schoolaccount, plus AD FS- of andere federatieve eindpunten |

Er zijn andere, mogelijk complexe scenario's. Raadpleeg te[Azure Active Directory-verificatie stromen](/documentation/articles/active-directory-authentication-scenarios/), [toepassingen integreren met Azure Active Directory](/documentation/articles/active-directory-integrating-applications/), en [Active Directory-verificatieprotocollen](https://msdn.microsoft.com/library/azure/dn151124.aspx) voor meer informatie.  

## <a name="key-vault-management"></a>Key Vault-beheer
Voor Sleutelkluis-beheer (CRUD en toegangsbeleid instellen), moet Hallo sleutelkluis clienttoepassing tooaccess een Azure Resource Manager-eindpunt.  

| Type bewerking | Eindpunt:poort |
| --- | --- |
| Bewerkingen voor de controlelaag van Key Vault<br> via Azure Resource Manager |**Wereldwijd:**<br> management.azure.com:443<br><br> **Azure China:**<br> management.chinacloudapi.cn:443<br><br> **Azure van de Amerikaanse overheid:**<br> management.usgovcloudapi.net:443<br><br> **Azure Duitsland:**<br> management.microsoftazure.de:443 |
| Azure Active Directory Graph API |**Wereldwijd:**<br> graph.windows.net:443<br><br> **Azure China:**<br> graph.chinacloudapi.cn:443<br><br> **Azure van de Amerikaanse overheid:**<br> graph.windows.net:443<br><br> **Azure Duitsland:**<br> graph.cloudapi.de:443 |

## <a name="key-vault-operations"></a>Key Vault-bewerkingen
Hallo sleutelkluis client moet voor alle beheer van de sleutelkluis-object (sleutels en geheimen) en cryptografische bewerkingen tooaccess hello sleutelkluis-eindpunt. Hallo eindpunt DNS-achtervoegsel is afhankelijk van Hallo-locatie van de sleutelkluis. Hallo sleutelkluis eindpunt heeft een indeling Hallo *kluisnaam*. *regio specifieke-DNS-achtervoegsel*, zoals beschreven in de volgende tabel Hallo.  

| Type bewerking | Eindpunt:poort |
| --- | --- |
| Bewerkingen waaronder cryptografiebewerkingen voor sleutels, het maken, lezen, bijwerken en verwijderen van sleutels en geheimen, instellen of ophalen van tags en andere kenmerken voor key vault-objecten (sleutels of geheimen) |**Wereldwijd:**<br> &lt;kluisnaam&gt;.vault.azure.net:443<br><br> **Azure China:**<br> &lt;kluisnaam&gt;.vault.azure.cn:443<br><br> **Azure van de Amerikaanse overheid:**<br> &lt;kluisnaam&gt;.vault.usgovcloudapi.net:443<br><br> **Azure Duitsland:**<br> &lt;kluisnaam&gt;.vault.microsoftazure.de:443 |

## <a name="ip-address-ranges"></a>IP-adresbereiken
Hallo Sleutelkluis-service maakt gebruik van andere Azure-resources zoals PaaS-infrastructuur. Zodat het niet mogelijk tooprovide een specifiek bereik van IP-adressen die Sleutelkluis-service-eindpunten op een willekeurig moment hebben. Als uw firewall alleen IP-adresbereiken ondersteunt, raadpleeg dan toohello [Microsoft Azure Datacenter IP-adresbereiken](https://www.microsoft.com/download/details.aspx?id=41653) document. Voor verificatie en -identiteit (Azure Active Directory), moet uw toepassing kunnen tooconnect toohello eindpunten die worden beschreven [authenticatie en identiteit adressen](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

## <a name="next-steps"></a>Volgende stappen
Als u vragen over Sleutelkluis hebt, gaat u naar Hallo [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).

