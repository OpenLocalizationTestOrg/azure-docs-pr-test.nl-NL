---
title: "Hybride identiteit: vergelijking van hulpprogramma’s voor directory-integratie | Microsoft Docs"
description: Deze pagina bevat een uitgebreide tabel waarin Hallo vergelijkt verschillende hulpprogramma die kunnen worden gebruikt voor directory-integratie is.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 1e62a4bd-4d55-4609-895e-70131dedbf52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 18ac0a0f58726eceb85510df516e8db71429b313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-directory-integration-tools-comparison"></a>Vergelijking van hulpprogramma’s voor directory-integratie voor hybride identiteit
Hallo jaren hulpprogramma Hallo toegenomen en ontwikkeld.  Dit document is toohelp bieden een geconsolideerde weergave van deze hulpprogramma's en een vergelijking van Hallo-functies die beschikbaar in elk zijn.

<!-- hello hardcoded link is a workaround for campaign ids not working in acom links-->

> [!NOTE]
> Azure AD Connect bevat Hallo-onderdelen en functionaliteit die eerder is uitgebracht als Dirsync en AAD Sync. Deze hulpprogramma's zijn niet meer afzonderlijk uitgebracht en alle toekomstige verbeteringen worden opgenomen in updates tooAzure AD verbinding kan maken, zodat u altijd weet waar tooget Hallo meest recente functionaliteit.
> 
> DirSync en Azure AD Sync zijn afgeschaft. Meer informatie vindt u [hier](active-directory-aadconnect-dirsync-deprecated.md).
> 
> 

Hallo sleutel volgen voor elk van de tabellen hello gebruiken.

● = Nu beschikbaar  
FR = Toekomstige release  
PP = Openbare preview  

## <a name="on-premises-toocloud-synchronization"></a>On-Premises tooCloud synchronisatie
| Functie | Azure Active Directory Connect | Azure Active Directory-synchronisatieservices (AAD Sync) | Hulpprogramma voor Azure Active Directory-synchronisatie (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Verbinding maken met toosingle on-premises AD-forest |● |● |● |● |● |
| Verbinding maken met toomultiple on-premises AD-forests |● |● | |● |● |
| Verbinding maken met toomultiple lokale Exchange-organisaties |● | | | | |
| Verbinding maken met on-premises LDAP-adreslijst toosingle |FR | | |● |● |
| Verbinding maken met on-premises LDAP-adreslijsten toomultiple |FR | | |● |● |
| Verbinding maken met tooon-premises AD en on-premises LDAP-adreslijsten |FR | | |● |● |
| Verbinding maken met toocustom systemen (dat wil zeggen SQL, Oracle, MySQL, enz.) |FR | | |● |● |
| Door de klant gedefinieerde kenmerken synchroniseren (directory-extensies) |● | | | | |
| Verbinding maken met tooon-premises HR (SAP, Oracle eBusiness, PeopleSoft) |FR | | |● |● |
| Ondersteunt de FIM-synchronisatieregels en -connectors voor het inrichten van tooon-premises systemen. | | | |● |● |

## <a name="cloud-tooon-premises-synchronization"></a>Synchronisatie van cloud-tooOn-Premises
| Functie | Azure Active Directory Connect | Azure Active Directory-synchronisatieservices | Hulpprogramma voor Azure Active Directory-synchronisatie (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Write-back van apparaten |● | |● | | |
| Write-back van kenmerken (voor de hybride implementatie voor Exchange) |● |● |● |● |● |
| Write-back van groepsobjecten |● | | | | |
| Write-back van wachtwoorden (van de selfservice voor wachtwoordherstel (SSPR) en het wijzigen van wachtwoorden) |● |● | | | |

## <a name="authentication-feature-support"></a>Ondersteuning van verificatiefuncties
| Functie | Azure Active Directory Connect | Azure Active Directory-synchronisatieservices | Hulpprogramma voor Azure Active Directory-synchronisatie (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Wachtwoordsynchronisatie voor één on-premises AD-forest |● |● |● | | |
| Wachtwoordsynchronisatie voor meerdere on-premises AD-forests |● |● | | | |
| Eenmalige aanmelding met federatie |● |● |● |● |● |
| Write-back van wachtwoorden (van SSPR en het wijzigen van wachtwoorden) |● |● | | | |

## <a name="set-up-and-installation"></a>Instellingen en installatie
| Functie | Azure Active Directory Connect | Azure Active Directory-synchronisatieservices | Hulpprogramma voor Azure Active Directory-synchronisatie (DirSync) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|
| Biedt ondersteuning voor installatie op een domeincontroller |● |● |● | |
| Biedt ondersteuning voor installatie met SQL Express |● |● |● | |
| Eenvoudig upgraden van DirSync |● | | | |
| Lokalisatie van Admin UX tooWindows Server-talen |● |● |● | |
| Lokalisatie van eindgebruiker-UX tooWindows Server-talen | | | |● |
| Ondersteuning voor Windows Server 2008 en Windows Server 2008 R2 |● voor synchronisatie, niet voor federatie |● |● |● |
| Ondersteuning voor Windows Server 2012 en Windows Server 2012 R2 |● |● |● |● |

## <a name="filtering-and-configuration"></a>Filteren en configuratie
| Functie | Azure Active Directory Connect | Azure Active Directory-synchronisatieservices | Hulpprogramma voor Azure Active Directory-synchronisatie (DirSync) | Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Filteren op domeinen en organisatie-eenheden |● |● |● |● |● |
| Filteren op kenmerkwaarden van objecten |● |● |● |● |● |
| Toestaan dat minimale set kenmerken toobe gesynchroniseerd (MinSync) |● |● | | | |
| Verschillende sjablonen toobe toegepast voor kenmerkstromen toestaan |● |● | | | |
| Toestaan dat het verwijderen van kenmerken van AD tooAzure AD stroomt |● |● | | | |
| Geavanceerd aanpassen voor kenmerkstromen toestaan |● |● | |● |● |

## <a name="next-steps"></a>Volgende stappen
Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory](active-directory-aadconnect.md).

