---
title: aaaAzure AD Connect en Federatie | Microsoft Docs
description: Deze pagina is Hallo centrale locatie voor alle documentatie over AD FS-bewerkingen die gebruikmaken van Azure AD Connect.
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: f9107cf5-0131-499a-9edf-616bf3afef4d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: anandy
ms.openlocfilehash: dc70206eee2296c2320712ef2ade48ccebcc912d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-and-federation"></a>Azure AD Connect en federatie
Azure Active Directory (Azure AD) Connect kunt configureren van Federatie met lokale Active Directory Federation Services (AD FS) en Azure AD. Met federation aanmelden, kunt u gebruikers toosign in tooAzure AD gebaseerde services met hun on-premises wachtwoorden-- en, terwijl op het bedrijfsnetwerk hello, zonder tooenter hun wachtwoord opnieuw inschakelen. Hallo federation optie met AD FS gebruikt, kunt u een nieuwe installatie van AD FS implementeren of u kunt een bestaande installatie opgeven in een farm met Windows Server 2012 R2.

Dit onderwerp is Hallo thuis voor informatie over de federation-gerelateerde functies voor Azure AD Connect. Geeft een lijst van koppelingen tooall Verwante onderwerpen. Voor koppelingen tooAzure AD Connect, Zie [uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).

## <a name="azure-ad-connect-federation-topics"></a>Azure AD Connect: federation-onderwerpen
| Onderwerp | Er wordt aangegeven en wanneer tooread deze |
|:--- |:--- |
| **Azure AD Connect gebruiker aanmeldingsopties** | |
| [Opties aanmelden gebruiker begrijpen](active-directory-aadconnect-user-signin.md) |Meer informatie over de verschillende gebruiker aanmeldingsopties en hoe deze gebruikerservaring hello Azure aanmeldingspagina beïnvloeden. |
| **AD FS installeren met behulp van Azure AD Connect** | |
| [Vereisten](active-directory-aadconnect-get-started-custom.md#ad-fs-configuration-pre-requisites) |Zie Hallo-vereisten voor een geslaagde installatie van AD FS via Azure AD Connect. |
| [Een AD FS-farm configureren](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs) |Installeer een nieuwe AD FS-farm met behulp van Azure AD Connect. |
| [Gefedereerd met Azure AD met behulp van alternatieve aanmeldings-ID](active-directory-aadconnect-federation-management.md#alternateid) | Federatie met behulp van alternatieve aanmeldings-ID configureren  |
| **Hallo AD FS-configuratie wijzigen** | |
| [Hallo-vertrouwensrelatie repareren](active-directory-aadconnect-federation-management.md#repairthetrust) |Reparatie Hallo huidige vertrouwensrelatie tussen lokale AD FS en Office 365/Azure. |
| [Een nieuwe AD FS-server toevoegen](active-directory-aadconnect-federation-management.md#addadfsserver) |Vouw een AD FS-farm met een extra AD FS-server na de eerste installatie. |
| [Een nieuwe AD FS WAP-server toevoegen](active-directory-aadconnect-federation-management.md#addwapserver) |Vouw een AD FS-farm met een extra Webtoepassingsproxy (WAP)-server na de eerste installatie. |
| [Een nieuwe federatieve domein toevoegen](active-directory-aadconnect-federation-management.md#addfeddomain) |Voeg een ander domein toobe gefedereerd met Azure AD. |
| [Hallo SSL-certificaat bijwerken](active-directory-aadconnectfed-ssl-update.md)| Hallo SSL-certificaat voor AD FS-farm bijwerken. |
| **Andere federatieconfiguratie** | |
| [Meerdere exemplaren van Azure AD federeren met één exemplaar van AD FS](active-directory-aadconnectfed-single-adfs-multitenant-federation.md) | Federeren van meerdere Azure AD met één AD FS-farm| 
| [Een aangepaste bedrijfsportal logo/afbeelding toevoegen](active-directory-aadconnect-federation-management.md#customlogo) |Hallo-aanmeldingservaring aanpast wijzigen door op te geven Hallo aangepaste logo dat wordt weergegeven op Hallo AD FS-aanmeldingspagina. |
| [Een beschrijving van de aanmeldingspagina toevoegen](active-directory-aadconnect-federation-management.md#addsignindescription) |Hallo aanmelden omschrijving op Hallo AD FS-aanmeldingspagina wijzigen. |
| [Wijzigen van de claimregels van AD FS](active-directory-aadconnect-federation-management.md#modclaims) |Wijzigen of toevoegen van claimregels in AD FS die overeenkomen met de configuratie van tooAzure AD Connect-synchronisatie. |


## <a name="additional-resources"></a>Aanvullende bronnen
* [Federatie twee Azure AD met één AD FS](active-directory-aadconnectfed-single-adfs-multitenant-federation.md)
* [AD FS-implementatie in Azure](active-directory-aadconnect-azure-adfs.md)
* [Hoge beschikbaarheid cross-geografische AD FS-implementatie in Azure met Azure Traffic Manager](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)
