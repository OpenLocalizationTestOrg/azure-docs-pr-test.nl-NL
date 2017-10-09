---
title: 'Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen | Microsoft Docs'
description: Legt uit hoe Azure AD Connect-synchronisatie werkt en hoe toocustomize.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ee4bf802-045b-4da0-986e-90aba2de58d6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2016
ms.author: markvi
ms.openlocfilehash: 97e4bd9904b077f2628e5f8dcbaa6f1a76168a12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understand-and-customize-synchronization"></a>Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen
Hello Azure Active Directory Connect-Synchronisatieservices (Azure AD Connect sync) is een belangrijkste onderdeel van Azure AD Connect. Dit zorgt voor alle Hallo-bewerkingen die gerelateerde toosynchronize identiteitsgegevens tussen uw on-premises omgeving en Azure AD. Azure AD Connect-synchronisatie is Hallo opvolger van DirSync, Azure AD Sync en Forefront Identity Manager Hello die Azure Active Directory-Connector is geconfigureerd.

Dit onderwerp is Hallo thuis voor **Azure AD Connect-synchronisatie** (ook wel **synchronisatie-engine**) en een lijst met koppelingen tooall andere gerelateerde tooit onderwerpen. Voor koppelingen tooAzure AD Connect, Zie [uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).

Hallo-sync-service bestaat uit twee componenten, Hallo lokale **Azure AD Connect-synchronisatie** onderdeel en Hallo servicezijde in Azure AD aangeroepen **Azure AD Connect-synchronisatieservice**. Hallo-service is gebruikelijk voor DirSync, Azure AD Sync en Azure AD Connect.

## <a name="azure-ad-connect-sync-topics"></a>Azure AD Connect sync-onderwerpen
| Onderwerp | Er wordt aangegeven en wanneer tooread |
| --- | --- |
| **Grondbeginselen van Azure AD Connect-synchronisatie** | |
| [Understanding Hallo-architectuur](active-directory-aadconnectsync-understanding-architecture.md) |Voor de nieuwe toohello synchronisatie-engine zijn wie en wilt toolearn over Hallo-architectuur en het Hallo-termen die worden gebruikt. |
| [Technische concepten](active-directory-aadconnectsync-technical-concepts.md) |Een korte versie van Hallo architectuur onderwerp en een korte wordt uitgelegd Hallo termen die worden gebruikt. |
| [Topologieën voor Azure AD Connect](active-directory-aadconnect-topologies.md) |Hierin wordt beschreven Hallo verschillende scenario's en topologieën Hallo sync engine ondersteunt. |
| **Aangepaste configuratie** | |
| [Actieve Hallo installatiewizard opnieuw](active-directory-aadconnectsync-installation-wizard.md) |Wordt uitgelegd wat u opties beschikbaar zijn wanneer u hello Azure AD Connect-installatiewizard opnieuw uitvoert. |
| [Informatie over declaratieve inrichting](active-directory-aadconnectsync-understanding-declarative-provisioning.md) |Hierin wordt beschreven Hallo configuratiemodel aangeroepen declaratieve inrichting. |
| [Inzicht in expressies declaratieve inrichting](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |Hallo-syntaxis voor het Hallo-expressie die wordt gebruikt in de declaratieve inrichting beschrijft. |
| [Understanding Hallo standaardconfiguratie](active-directory-aadconnectsync-understanding-default-configuration.md) |Hallo out-of-box-regels en de standaardconfiguratie Hallo beschrijft. Beschrijft ook hoe regels Hallo samenwerken voor Hallo out-of-box-scenario's toowork. |
| [Inzicht krijgen in gebruikers en contactpersonen](active-directory-aadconnectsync-understanding-users-and-contacts.md) |Van de vorige onderwerp hello wordt voortgezet en wordt beschreven hoe Hallo-configuratie voor gebruikers en contactpersonen werkt samen met name in een omgeving met meerdere forests. |
| [Hoe een wijziging toohello toomake standaard configuratie](active-directory-aadconnectsync-change-the-configuration.md) |Begeleidt u bij hoe toomake een algemene configuratie wijzigen-tooattribute loopt. |
| [Aanbevolen procedures voor het wijzigen van de standaardconfiguratie Hallo](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) |Beperkingen voor de ondersteuning en voor het maken van wijzigingen toohello out-of-box-configuratie. |
| [Filteren configureren](active-directory-aadconnectsync-configure-filtering.md) |Hallo verschillende opties voor hoe toolimit die objecten worden gesynchroniseerd tooAzure AD en stapsgewijze procedure beschrijft tooconfigure deze opties. |
| **Scenario's en onderdelen** | |
| [Onopzettelijke verwijderingen voorkomen](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) |Hierin wordt beschreven Hallo *onopzettelijk verwijderen voorkomen* functie en hoe tooconfigure deze. |
| [Scheduler](active-directory-aadconnectsync-feature-scheduler.md) |Beschrijving van de ingebouwde scheduler hello, die is importeren, synchroniseren en exporteren van gegevens. |
| [Wachtwoordsynchronisatie implementeren](active-directory-aadconnectsync-implement-password-synchronization.md) |Hierin wordt beschreven hoe werkt Wachtwoordsynchronisatie, hoe tooimplement, en hoe toooperate en op te lossen. |
| [Write-back van apparaat](active-directory-aadconnect-feature-device-writeback.md) |Hierin wordt beschreven hoe Write-back van apparaat werkt in Azure AD Connect. |
| [Uitbreidingen van de directory](active-directory-aadconnectsync-feature-directory-extensions.md) |Hierin wordt beschreven hoe tooextend hello Azure AD-schema met uw eigen aangepaste kenmerken. |
| **Sync-Service** | |
| [Azure AD Connect sync-service-functies](active-directory-aadconnectsyncservice-features.md) |Beschrijft servicezijde Hallo-synchronisatie en hoe toochange instellingen in Azure AD synchroniseren. |
| [Dubbel kenmerk tolerantie](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) |Hierin wordt beschreven hoe tooenable en gebruik **userPrincipalName** en **proxyAddresses** dubbel kenmerk waarden tolerantie. |
| **Bewerkingen en gebruikersinterface** | |
| [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md) |Hierin wordt beschreven Hallo Synchronization Service Manager-UI, met inbegrip van [Operations](active-directory-aadconnectsync-service-manager-ui-operations.md), [Connectors](active-directory-aadconnectsync-service-manager-ui-connectors.md), [Metaverse Designer](active-directory-aadconnectsync-service-manager-ui-mvdesigner.md), en [Metaverse zoeken](active-directory-aadconnectsync-service-manager-ui-mvsearch.md) tabbladen. |
| [Operationele taken en overwegingen](active-directory-aadconnectsync-operations.md) |Beschrijving van operationele problemen, zoals herstel na noodgevallen. |
| **Procedures...** | |
| [Hello Azure AD-account opnieuw instellen](active-directory-aadconnectsync-howto-azureadaccount.md) |Hoe gebruikt tooreset Hallo referenties van het serviceaccount Hallo tooconnect van Azure AD Connect-synchronisatie tooAzure AD. |
| **Meer informatie en verwijzingen** | |
| [Poorten](active-directory-aadconnect-ports.md) |Een lijst die u poorten moet tooopen tussen Hallo synchronisatie-engine en uw on-premises adreslijsten en Azure AD. |
| [Kenmerken gesynchroniseerd tooAzure Active Directory](active-directory-aadconnectsync-attributes-synchronized.md) |Hier worden alle kenmerken worden gesynchroniseerd tussen on-premises AD en Azure AD. |
| [Functieverwijzing](active-directory-aadconnectsync-functions-reference.md) |Een lijst met alle beschikbare functies in declaratieve inrichting. |

## <a name="additional-resources"></a>Aanvullende resources
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)

