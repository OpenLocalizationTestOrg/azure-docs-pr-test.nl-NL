---
title: Kenmerken die zijn gesynchroniseerd met Azure AD Connect | Microsoft Docs
description: Een lijst met Hallo kenmerken die zijn gesynchroniseerd tooAzure Active Directory.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c2bb36e0-5205-454c-b9b6-f4990bcedf51
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 2fe5b944a7fc832f245631416c265fb82eedeb15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-attributes-synchronized-tooazure-active-directory"></a>Azure AD Connect-synchronisatie: kenmerken gesynchroniseerd tooAzure Active Directory
Dit onderwerp staan Hallo kenmerken die worden gesynchroniseerd door Azure AD Connect-synchronisatie.  
Hallo kenmerken worden gegroepeerd Hallo gerelateerde Azure AD-app.

## <a name="attributes-toosynchronize"></a>Kenmerken toosynchronize
Een algemene vraag is *Hallo-lijst van kenmerken toosynchronize*. Hallo standaard en de aanbevolen aanpak is tookeep Hallo standaardkenmerken zodat een volledige GAL (globale adreslijst) kan worden gemaakt in Hallo cloud en tooget alle functies in Office 365-werkbelastingen. In sommige gevallen, er zijn een aantal kenmerken dat uw organisatie wil niet gesynchroniseerde toohello cloud omdat deze kenmerken bevatten gevoelige of persoonlijke (persoonsgegevens) gegevens, zoals in dit voorbeeld:  
![ongeldige kenmerken](./media/active-directory-aadconnectsync-attributes-synchronized/badextensionattribute.png)

In dit geval beginnen met Hallo lijst met kenmerken in dit onderwerp en identificeren van de kenmerken die gevoelige of persoonlijke gegevens bevatten zou en kunnen niet worden gesynchroniseerd. Deselecteer tijdens de installatie met deze kenmerken [Azure AD-app en kenmerkfilters](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering).

> [!WARNING]
> Wanneer kenmerken uitschakelt, moet u voorzichtig zijn en alleen de kenmerken absoluut niet mogelijk toosynchronize Hef de selectie. Selectie opheffen van andere kenmerken, kan een nadelige invloed op onderdelen hebben.
>
>

## <a name="office-365-proplus"></a>Office 365 ProPlus
| Naam van kenmerk | Gebruiker | Opmerking |
| --- |:---:| --- |
| accountEnabled |X |Hiermee worden gedefinieerd als een account is ingeschakeld. |
| algemene naam |X | |
| Weergavenaam |X | |
| objectSID |X |mechanische eigenschap. AD-gebruikers-id gebruikt toomaintain synchronisatie tussen Azure AD en AD. |
| pwdLastSet |X |mechanische eigenschap. Gebruikte tooknow wanneer tooinvalidate al zijn uitgegeven tokens. Door Wachtwoordsynchronisatie en Federatie gebruikt. |
| sourceAnchor |X |mechanische eigenschap. Onveranderbare id toomaintain relatie tussen ADDS en Azure AD. |
| usageLocation |X |mechanische eigenschap. Hallo van de gebruiker het land. Gebruikt voor de licentietoewijzing. |
| UserPrincipalName |X |UPN is Hallo aanmeldings-ID voor Hallo-gebruiker. Hallo vaak hetzelfde als de waarde [e]. |

## <a name="exchange-online"></a>Exchange Online
| Naam van kenmerk | Gebruiker | Contact | Groep | Opmerking |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Hiermee worden gedefinieerd als een account is ingeschakeld. |
| assistent |X |X | | |
| altRecipient |X | | |Azure AD Connect build 1.1.552.0 vereist of na. |
| authOrig |X |X |X | |
| C |X |X | | |
| algemene naam |X | |X | |
| CO |X |X | | |
| Bedrijf |X |X | | |
| CountryCode |X |X | | |
| Afdeling |X |X | | |
| description |X |X |X | |
| Weergavenaam |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| Voornaam |X |X | | |
| HomePhone |X |X | | |
| Info |X |X |X |Dit kenmerk is momenteel niet worden gebruikt voor groepen. |
| initialen |X |X | | |
| L |X |X | | |
| LegacyExchangeDN |X |X |X | |
| mailNickname |X |X |X | |
| mangedBy | | |X | |
| Manager |X |X | | |
| Lid | | |X | |
| mobiele |X |X | | |
| msDS-HABSeniorityIndex |X |X |X | |
| msDS-PhoneticDisplayName |X |X |X | |
| msExchArchiveGUID |X | | | |
| msExchArchiveName |X | | | |
| msExchAssistantName |X |X | | |
| msExchAuditAdmin |X | | | |
| msExchAuditDelegate |X | | | |
| msExchAuditDelegateAdmin |X | | | |
| msExchAuditOwner |X | | | |
| msExchBlockedSendersHash |X |X | | |
| msExchBypassAudit |X | | | |
| msExchBypassModerationLink | | |X |Beschikbaar in Azure AD Connect versie 1.1.524.0 |
| msExchCoManagedByLink | | |X | |
| msExchDelegateListLink |X | | | |
| msExchELCExpirySuspensionEnd |X | | | |
| msExchELCExpirySuspensionStart |X | | | |
| msExchELCMailboxFlags |X | | | |
| msExchEnableModeration |X | |X | |
| msExchExtensionCustomAttribute1 |X |X |X |Dit kenmerk is momenteel niet worden gebruikt door Exchange Online. |
| msExchExtensionCustomAttribute2 |X |X |X |Dit kenmerk is momenteel niet worden gebruikt door Exchange Online. |
| msExchExtensionCustomAttribute3 |X |X |X |Dit kenmerk is momenteel niet worden gebruikt door Exchange Online. |
| msExchExtensionCustomAttribute4 |X |X |X |Dit kenmerk is momenteel niet worden gebruikt door Exchange Online. |
| msExchExtensionCustomAttribute5 |X |X |X |Dit kenmerk is momenteel niet worden gebruikt door Exchange Online. |
| msExchHideFromAddressLists |X |X |X | |
| msExchImmutableID |X | | | |
| msExchLitigationHoldDate |X |X |X | |
| msExchLitigationHoldOwner |X |X |X | |
| msExchMailboxAuditEnable |X | | | |
| msExchMailboxAuditLogAgeLimit |X | | | |
| msExchMailboxGuid |X | | | |
| msExchModeratedByLink |X |X |X | |
| msExchModerationFlags |X |X |X | |
| msExchRecipientDisplayType |X |X |X | |
| msExchRecipientTypeDetails |X |X |X | |
| msExchRemoteRecipientType |X | | | |
| msExchRequireAuthToSendTo |X |X |X | |
| msExchResourceCapacity |X | | | |
| msExchResourceDisplay |X | | | |
| msExchResourceMetaData |X | | | |
| msExchResourceSearchProperties |X | | | |
| msExchRetentionComment |X |X |X | |
| msExchRetentionURL |X |X |X | |
| msExchSafeRecipientsHash |X |X | | |
| msExchSafeSendersHash |X |X | | |
| msExchSenderHintTranslations |X |X |X | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| msExchUserHoldPolicies |X | | | |
| msOrg IsOrganizational | | |X | |
| objectSID |X | |X |mechanische eigenschap. AD-gebruikers-id gebruikt toomaintain synchronisatie tussen Azure AD en AD. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherTelephone |X |X | | |
| Pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| Postcode |X |X | | |
| proxyAddresses |X |X |X | |
| publicDelegates |X |X |X | |
| pwdLastSet |X | | |mechanische eigenschap. Gebruikte tooknow wanneer tooinvalidate al zijn uitgegeven tokens. Door Wachtwoordsynchronisatie en Federatie gebruikt. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityenabled moet | | |X |Afgeleid van groupType |
| SN |X |X | | |
| sourceAnchor |X |X |X |mechanische eigenschap. Onveranderbare id toomaintain relatie tussen ADDS en Azure AD. |
| St |X |X | | |
| StreetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| titel |X |X | | |
| unauthOrig |X |X |X | |
| usageLocation |X | | |mechanische eigenschap. Hallo van de gebruiker het land. Gebruikt voor de licentietoewijzing. |
| userCertificate |X |X | | |
| UserPrincipalName |X | | |UPN is Hallo aanmeldings-ID voor Hallo-gebruiker. Hallo vaak hetzelfde als de waarde [e]. |
| userSMIMECertificates |X |X | | |
| wWWHomePage |X |X | | |

## <a name="sharepoint-online"></a>SharePoint Online
| Naam van kenmerk | Gebruiker | Contact | Groep | Opmerking |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Hiermee worden gedefinieerd als een account is ingeschakeld. |
| authOrig |X |X |X | |
| C |X |X | | |
| algemene naam |X | |X | |
| CO |X |X | | |
| Bedrijf |X |X | | |
| CountryCode |X |X | | |
| Afdeling |X |X | | |
| description |X |X |X | |
| Weergavenaam |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| Voornaam |X |X | | |
| hideDLMembership | | |X | |
| homephone |X |X | | |
| Info |X |X |X | |
| initialen |X |X | | |
| ipPhone |X |X | | |
| L |X |X | | |
| E-mail |X |X |X | |
| mailnickname |X |X |X | |
| Door | | |X | |
| Manager |X |X | | |
| Lid | | |X | |
| Afzonderlijk |X |X | | |
| mobiele |X |X | | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointLinkedBy |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| objectSID |X | |X |mechanische eigenschap. AD-gebruikers-id gebruikt toomaintain synchronisatie tussen Azure AD en AD. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherIpPhone |X |X | | |
| OtherMobile |X |X | | |
| otherPager |X |X | | |
| otherTelephone |X |X | | |
| Pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| Postcode |X |X | | |
| postOfficeBox |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |mechanische eigenschap. Gebruikte tooknow wanneer tooinvalidate al zijn uitgegeven tokens. Door Wachtwoordsynchronisatie en Federatie gebruikt. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityenabled moet | | |X |Afgeleid van groupType |
| SN |X |X | | |
| sourceAnchor |X |X |X |mechanische eigenschap. Onveranderbare id toomaintain relatie tussen ADDS en Azure AD. |
| St |X |X | | |
| StreetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| titel |X |X | | |
| unauthOrig |X |X |X | |
| URL |X |X | | |
| usageLocation |X | | |mechanische eigenschap. Hallo van de gebruiker het land. Gebruikt voor de licentietoewijzing. |
| UserPrincipalName |X | | |UPN is Hallo aanmeldings-ID voor Hallo-gebruiker. Hallo vaak hetzelfde als de waarde [e]. |
| wWWHomePage |X |X | | |

## <a name="lync-online"></a>Lync Online
| Naam van kenmerk | Gebruiker | Contact | Groep | Opmerking |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Hiermee worden gedefinieerd als een account is ingeschakeld. |
| C |X |X | | |
| algemene naam |X | |X | |
| CO |X |X | | |
| Bedrijf |X |X | | |
| Afdeling |X |X | | |
| description |X |X |X | |
| Weergavenaam |X |X |X | |
| facsimiletelephonenumber |X |X |X | |
| Voornaam |X |X | | |
| homephone |X |X | | |
| ipPhone |X |X | | |
| L |X |X | | |
| E-mail |X |X |X | |
| mailNickname |X |X |X | |
| Door | | |X | |
| Manager |X |X | | |
| Lid | | |X | |
| mobiele |X |X | | |
| msExchHideFromAddressLists |X |X |X | |
| msRTCSIP-ApplicationOptions |X | | | |
| msRTCSIP-DeploymentLocator |X |X | | |
| msRTCSIP-Line |X |X | | |
| msRTCSIP-OptionFlags |X |X | | |
| msRTCSIP-OwnerUrn |X | | | |
| msRTCSIP-PrimaryUserAddress |X |X | | |
| msRTCSIP-UserEnabled |X |X | | |
| objectSID |X | |X |mechanische eigenschap. AD-gebruikers-id gebruikt toomaintain synchronisatie tussen Azure AD en AD. |
| otherTelephone |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| Postcode |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |mechanische eigenschap. Gebruikte tooknow wanneer tooinvalidate al zijn uitgegeven tokens. Door Wachtwoordsynchronisatie en Federatie gebruikt. |
| securityenabled moet | | |X |Afgeleid van groupType |
| SN |X |X | | |
| sourceAnchor |X |X |X |mechanische eigenschap. Onveranderbare id toomaintain relatie tussen ADDS en Azure AD. |
| St |X |X | | |
| StreetAddress |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| titel |X |X | | |
| usageLocation |X | | |mechanische eigenschap. Hallo van de gebruiker het land. Gebruikt voor de licentietoewijzing. |
| UserPrincipalName |X | | |UPN is Hallo aanmeldings-ID voor Hallo-gebruiker. Hallo vaak hetzelfde als de waarde [e]. |
| wWWHomePage |X |X | | |

## <a name="azure-rms"></a>Azure RMS
| Naam van kenmerk | Gebruiker | Contact | Groep | Opmerking |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Hiermee worden gedefinieerd als een account is ingeschakeld. |
| algemene naam |X | |X |Algemene naam of alias. Meest Hallo voorvoegsel van de waarde [e]. |
| Weergavenaam |X |X |X |Een tekenreeks met Hallo naam vaak weergegeven als Hallo beschrijvende naam (voornaam achternaam). |
| E-mail |X |X |X |volledige e-mailadres. |
| Lid | | |X | |
| objectSID |X | |X |mechanische eigenschap. AD-gebruikers-id gebruikt toomaintain synchronisatie tussen Azure AD en AD. |
| proxyAddresses |X |X |X |mechanische eigenschap. Gebruikt door Azure AD. Alle secundaire e-mailadressen voor Hallo gebruiker bevat. |
| pwdLastSet |X | | |mechanische eigenschap. Gebruikte tooknow wanneer tooinvalidate al zijn uitgegeven tokens. |
| securityenabled moet | | |X |GroupType is afgeleid. |
| sourceAnchor |X |X |X |mechanische eigenschap. Onveranderbare id toomaintain relatie tussen ADDS en Azure AD. |
| usageLocation |X | | |mechanische eigenschap. Hallo van de gebruiker het land. Gebruikt voor de licentietoewijzing. |
| UserPrincipalName |X | | |De UPN is Hallo aanmeldings-ID voor Hallo-gebruiker. Hallo vaak hetzelfde als de waarde [e]. |

## <a name="intune"></a>Intune
| Naam van kenmerk | Gebruiker | Contact | Groep | Opmerking |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Hiermee worden gedefinieerd als een account is ingeschakeld. |
| C |X |X | | |
| algemene naam |X | |X | |
| description |X |X |X | |
| Weergavenaam |X |X |X | |
| E-mail |X |X |X | |
| mailnickname |X |X |X | |
| Lid | | |X | |
| objectSID |X | |X |mechanische eigenschap. AD-gebruikers-id gebruikt toomaintain synchronisatie tussen Azure AD en AD. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |mechanische eigenschap. Gebruikte tooknow wanneer tooinvalidate al zijn uitgegeven tokens. Door Wachtwoordsynchronisatie en Federatie gebruikt. |
| securityenabled moet | | |X |Afgeleid van groupType |
| sourceAnchor |X |X |X |mechanische eigenschap. Onveranderbare id toomaintain relatie tussen ADDS en Azure AD. |
| usageLocation |X | | |mechanische eigenschap. Hallo van de gebruiker het land. Gebruikt voor de licentietoewijzing. |
| UserPrincipalName |X | | |UPN is Hallo aanmeldings-ID voor Hallo-gebruiker. Hallo vaak hetzelfde als de waarde [e]. |

## <a name="dynamics-crm"></a>Dynamics CRM
| Naam van kenmerk | Gebruiker | Contact | Groep | Opmerking |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Hiermee worden gedefinieerd als een account is ingeschakeld. |
| C |X |X | | |
| algemene naam |X | |X | |
| CO |X |X | | |
| Bedrijf |X |X | | |
| CountryCode |X |X | | |
| description |X |X |X | |
| Weergavenaam |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| Voornaam |X |X | | |
| L |X |X | | |
| Door | | |X | |
| Manager |X |X | | |
| Lid | | |X | |
| mobiele |X |X | | |
| objectSID |X | |X |mechanische eigenschap. AD-gebruikers-id gebruikt toomaintain synchronisatie tussen Azure AD en AD. |
| physicalDeliveryOfficeName |X |X | | |
| Postcode |X |X | | |
| preferredLanguage |X | | | |
| pwdLastSet |X | | |mechanische eigenschap. Gebruikte tooknow wanneer tooinvalidate al zijn uitgegeven tokens. Door Wachtwoordsynchronisatie en Federatie gebruikt. |
| securityenabled moet | | |X |Afgeleid van groupType |
| SN |X |X | | |
| sourceAnchor |X |X |X |mechanische eigenschap. Onveranderbare id toomaintain relatie tussen ADDS en Azure AD. |
| St |X |X | | |
| StreetAddress |X |X | | |
| telephoneNumber |X |X | | |
| titel |X |X | | |
| usageLocation |X | | |mechanische eigenschap. Hallo van de gebruiker het land. Gebruikt voor de licentietoewijzing. |
| UserPrincipalName |X | | |UPN is Hallo aanmeldings-ID voor Hallo-gebruiker. Hallo vaak hetzelfde als de waarde [e]. |

## <a name="3rd-party-applications"></a>3e toepassingen van derden
Deze groep is een set kenmerken die worden gebruikt als Hallo minimale kenmerken die nodig zijn voor een algemene werkbelasting of toepassing. Het kan worden gebruikt voor een werkbelasting die niet wordt vermeld in een andere sectie of voor een niet-Microsoft-app. Het wordt expliciet voor Hallo volgende gebruikt:

* Yammer (alleen gebruiker wordt gebruikt)
* [Hybride Business-to-Business (B2B) cross-org samenwerking scenario's die worden aangeboden door bronnen zoals SharePoint](http://go.microsoft.com/fwlink/?LinkId=747036)

Deze groep is een set kenmerken die kunnen worden gebruikt als hello Azure AD-directory niet toosupport Office 365, Dynamics of Intune gebruikt. Er is een klein aantal belangrijke kenmerken.

| Naam van kenmerk | Gebruiker | Contact | Groep | Opmerking |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Hiermee worden gedefinieerd als een account is ingeschakeld. |
| algemene naam |X | |X | |
| Weergavenaam |X |X |X | |
| Voornaam |X |X | | |
| E-mail |X | |X | |
| Door | | |X | |
| mailNickName |X |X |X | |
| Lid | | |X | |
| objectSID |X | | |mechanische eigenschap. AD-gebruikers-id gebruikt toomaintain synchronisatie tussen Azure AD en AD. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |mechanische eigenschap. Gebruikte tooknow wanneer tooinvalidate al zijn uitgegeven tokens. Door Wachtwoordsynchronisatie en Federatie gebruikt. |
| SN |X |X | | |
| sourceAnchor |X |X |X |mechanische eigenschap. Onveranderbare id toomaintain relatie tussen ADDS en Azure AD. |
| usageLocation |X | | |mechanische eigenschap. Hallo van de gebruiker het land. Gebruikt voor de licentietoewijzing. |
| UserPrincipalName |X | | |UPN is Hallo aanmeldings-ID voor Hallo-gebruiker. Hallo vaak hetzelfde als de waarde [e]. |

## <a name="windows-10"></a>Windows 10
Een Windows 10 domein computer(device) worden bepaalde kenmerken tooAzure AD gesynchroniseerd. Zie voor meer informatie over scenario's Hallo [domeinapparaten tooAzure AD Connect voor Windows 10 optreedt](../active-directory-azureadjoin-devices-group-policy.md). Deze kenmerken altijd te synchroniseren en Windows 10 wordt niet weergegeven als een app die kunt u het vakje. Domein Windows 10-computer wordt geïdentificeerd door Hallo kenmerk userCertificate ingevuld.

| Naam van kenmerk | Apparaat | Opmerking |
| --- |:---:| --- |
| accountEnabled |X | |
| deviceTrustType |X |De waarde van de hardcoded voor domeincomputers. |
| Weergavenaam |X | |
| DS-MS-CreatorSID |X |Ook wel registeredOwnerReference genoemd. |
| objectGUID |X |Ook wel de apparaat-id genoemd. |
| objectSID |X |Ook wel onPremisesSecurityIdentifier genoemd. |
| operatingSystem |X |Ook wel deviceOSType genoemd. |
| operatingSystemVersion |X |Ook wel deviceOSVersion genoemd. |
| userCertificate |X | |

Deze kenmerken voor **gebruiker** zijn bovendien toohello andere apps die u hebt geselecteerd.  

| Naam van kenmerk | Gebruiker | Opmerking |
| --- |:---:| --- |
| domainFQDN |X |Ook wel een DNS-domeinnaam genoemd. Bijvoorbeeld contoso.com. |
| domainNetBios |X |Ook wel netBiosName genoemd. Bijvoorbeeld CONTOSO. |

## <a name="exchange-hybrid-writeback"></a>Exchange hybride Write-back
Deze kenmerken worden opgeslagen in Azure AD tooon-premises Active Directory wanneer u tooenable selecteert **Exchange hybride**. Afhankelijk van uw versie van Exchange mogelijk minder kenmerken worden gesynchroniseerd.

| Naam van kenmerk | Gebruiker | Contact | Groep | Opmerking |
| --- |:---:|:---:|:---:| --- |
| msDS-ExternalDirectoryObjectID |X | | |Afgeleid van cloudAnchor in Azure AD. Dit kenmerk is nieuw in Exchange 2016 en Windows Server 2016 AD. |
| msExchArchiveStatus |X | | |Online archief: Kunnen klanten tooarchive mail. |
| msExchBlockedSendersHash |X | | |Filteren: Schrijft terug on-premises filteren en online veilige en geblokkeerde afzender gegevens van clients. |
| msExchSafeRecipientsHash |X | | |Filteren: Schrijft terug on-premises filteren en online veilige en geblokkeerde afzender gegevens van clients. |
| msExchSafeSendersHash |X | | |Filteren: Schrijft terug on-premises filteren en online veilige en geblokkeerde afzender gegevens van clients. |
| msExchUCVoiceMailSettings |X | | |Unified Messaging (UM) - Online voicemail inschakelen: gebruikt door Microsoft Lync Server integratie tooindicate tooLync Server lokale die Hallo de gebruiker heeft voicemail in onlineservices. |
| msExchUserHoldPolicies |X | | |Geschil wachtstand: Hiermee schakelt u cloud services toodetermine die gebruikers onder geschil houdt. |
| proxyAddresses |X |X |X |Alleen Hallo x500 adres vanuit Exchange Online wordt ingevoegd. |
| publicDelegates |X | | |Hiermee kunt dat een Exchange Online-Postvak toobe verleend SendOnBehalfTo rechten toousers met lokale Exchange-postvak. Azure AD Connect build 1.1.552.0 vereist of na. |

## <a name="exchange-mail-public-folder"></a>Exchange Mail openbare map
Deze kenmerken worden gesynchroniseerd vanuit de lokale Active Directory tooAzure AD wanneer u tooenable selecteert **Exchange Mail openbare map**.

| Naam van kenmerk | PublicFolder | Opmerking |
| --- | :---:| --- |
| Weergavenaam | X |  |
| E-mail | X |  |
| msExchRecipientTypeDetails | X |  |
| objectGUID | X |  |
| proxyAddresses | X |  |
| targetAddress | X |  |

## <a name="device-writeback"></a>Apparaat terugschrijven
Apparaatobjecten zijn gemaakt in Active Directory. Deze objecten kunnen lid zijn van apparaten tooAzure AD of domein Windows 10-computers.

| Naam van kenmerk | Apparaat | Opmerking |
| --- |:---:| --- |
| altSecurityIdentities |X | |
| Weergavenaam |X | |
| DN-naam |X | |
| msDS-CloudAnchor |X | |
| msDS-apparaat-id |X | |
| msDS-DeviceObjectVersion |X | |
| msDS-DeviceOSType |X | |
| msDS-DeviceOSVersion |X | |
| msDS-DevicePhysicalIDs |X | |
| msDS-KeyCredentialLink |X |Alleen met Windows Server 2016 AD-schema |
| msDS-IsCompliant |X | |
| msDS-IsEnabled |X | |
| msDS-IsManaged |X | |
| msDS-RegisteredOwner |X | |

## <a name="notes"></a>Opmerkingen
* Gebruik een alternatieve ID hello on-premises is kenmerk userPrincipalName gesynchroniseerd met hello Azure AD-kenmerk onPremisesUserPrincipalName. Hallo alternatieve ID-kenmerk, bijvoorbeeld e-mail, is gesynchroniseerd met het kenmerk userPrincipalName van hello Azure AD.
* Hallo objecttype in Hallo lijsten bovenstaande **gebruiker** toohello objecttype is ook van toepassing **iNetOrgPerson**.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over Hallo [Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md) configuratie.

Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory ](active-directory-aadconnect.md).
