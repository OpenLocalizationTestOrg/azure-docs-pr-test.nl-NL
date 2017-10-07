---
title: aaaOverview van beveiliging in Data Lake Store | Microsoft Docs
description: Begrijpen hoe Azure Data Lake Store is een veiligere big data-archief
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ebd5b2ac-c5cc-46d4-9cfd-1a1ee70024c2
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 69e20bd046a9427202074baf59bff13f5b6a83ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-in-azure-data-lake-store"></a>Beveiliging in Azure Data Lake Store
Veel bedrijven profiteert van big data-analyses voor zakelijke inzichten toohelp die ze beslissingen van smartcard maken. Een organisatie kan een complex en gereglementeerde omgeving met een toenemend aantal diverse gebruikers hebben. Is het essentieel is voor een enterprise-toomake zeker van te zijn dat cruciale bedrijfsgegevens wordt meer veilig opgeslagen met Hallo juiste toegangsniveau tooindividual gebruikers verleend. Azure Data Lake Store is ontworpen toohelp voldoen aan deze beveiligingsvereisten. In dit artikel meer informatie over de beveiligingsmogelijkheden Hallo van Data Lake Store, met inbegrip van:

* Authentication
* Autorisatie
* Netwerkisolatie
* Gegevensbeveiliging
* Controleren

## <a name="authentication-and-identity-management"></a>Authenticatie en identiteit management
Verificatie is Hallo-proces waarmee de identiteit van een gebruiker wordt geverifieerd wanneer Hallo gebruiker werkt met Data Lake Store of met alle services die verbinding tooData Lake Store maakt. Voor identiteits- en verificatie, het gebruik van Data Lake Store [Azure Active Directory](../active-directory/active-directory-whatis.md), een uitgebreide identiteits- en toegangsbeheer cloud beheeroplossing die vereenvoudigt het beheer van gebruikers en groepen Hallo.

Elk Azure-abonnement kan worden gekoppeld aan een exemplaar van Azure Active Directory. Alleen gebruikers en service-identiteiten die zijn gedefinieerd in uw Azure Active Directory-service toegang tot uw Data Lake Store-account met behulp van hello Azure-portal, opdrachtregelprogramma's of via de clienttoepassingen die uw organisatie worden gebouwd met behulp van hello Azure-gegevens Lake Store SDK. Belangrijkste voordelen van het gebruik van Azure Active Directory als een gecentraliseerde mechanisme voor toegangsbeheer zijn:

* Identity lifecycle beheer vereenvoudigd. Hallo-identiteit van een gebruiker of een service (een service principal identiteit) worden snel gemaakt en snel door gewoon verwijderen of uitschakelen van de account in de map Hallo Hallo ingetrokken.
* Multi-factor authentication-server. [Multi-factorauthenticatie](../multi-factor-authentication/multi-factor-authentication.md) biedt een extra beveiligingslaag voor gebruikersaanmeldingen en transacties.
* Verificatie van elke client via een open standaardprotocol, zoals OAuth of OpenID.
* Federatie met enterprise directoryservices en cloud-id-providers.

## <a name="authorization-and-access-control"></a>Autorisatie en toegangsbeheer
Nadat u Azure Active Directory wordt een gebruiker geverifieerd zodat hello gebruiker toegang Azure Data Lake Store tot, toegangsmachtigingen autorisatie besturingselementen voor Data Lake Store. Data Lake Store scheidt autorisatie voor account gerelateerd en -gegevens activiteiten in Hallo manier te volgen:

* [Toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-what-is.md) (RBAC) opgegeven door de Azure voor accountbeheer
* POSIX ACL voor toegang tot gegevens in Hallo store

### <a name="rbac-for-account-management"></a>RBAC voor accountbeheer
Vier eenvoudige rollen worden standaard gedefinieerd voor Data Lake Store. Hallo rollen toestaan dat verschillende bewerkingen op een Data Lake Store-account via hello Azure-portal, PowerShell-cmdlets en REST-API's. Hallo eigenaar en Inzender rollen kunnen tal van functies voor beheer op Hallo account uitvoeren. U kunt toewijzen Hallo lezer rol toousers die alleen met gegevens werken.

![RBAC-rollen](./media/data-lake-store-security-overview/rbac-roles.png "RBAC-rollen")

Bedenk dat hoewel rollen zijn toegewezen voor accountbeheer, sommige rollen toegang toodata beïnvloeden. U moet toouse ACL's toocontrol toegang toooperations die een gebruiker op Hallo-bestandssysteem uitvoeren kan. Hallo volgende tabel bevat een overzicht van de rights management en data access-rechten voor Hallo standaardrollen.

| Rollen | Rights management | Data access-rechten | Uitleg |
| --- | --- | --- | --- |
| Er is geen rol die is toegewezen |Geen |Beheerst door de ACL |Hallo-gebruiker kan geen hello Azure portal of Azure PowerShell cmdlets toobrowse Data Lake Store gebruiken. Hallo-gebruiker kan alleen de opdrachtregelprogramma's gebruiken. |
| Eigenaar |Alle |Alle |rol van eigenaar Hallo is een beheerder. Deze rol kan alles beheren en toodata volledige toegang heeft. |
| Lezer |alleen-lezen |Beheerst door de ACL |de rol Lezer Hallo kan alles weergeven met betrekking tot accountbeheer, zoals welke gebruiker toowhich rol is toegewezen. de rol Lezer Hallo kunt geen wijzigingen aanbrengen. |
| Inzender |Alles behalve rollen toevoegen en verwijderen |Beheerst door de ACL |rol van Inzender Hallo kunt bepaalde aspecten van een account, zoals implementaties en bij het maken en beheren van waarschuwingen beheren. de rol Inzender Hallo kunt toevoegen of verwijderen van rollen. |
| Beheerder van gebruikerstoegang |Toevoegen en verwijderen van rollen |Beheerst door de ACL |Hallo beheerder voor gebruikerstoegang rol kan de gebruiker toegang tooaccounts beheren. |

Zie voor instructies [toewijzen van gebruikers of beveiligingsgroepen tooData Lake Store-accounts](data-lake-store-secure-data.md#assign-users-or-security-groups-to-azure-data-lake-store-accounts).

### <a name="using-acls-for-operations-on-file-systems"></a>Met behulp van ACL's voor bewerkingen voor bestandssystemen
Data Lake Store is een hiërarchische bestandssysteem zoals Hadoop Distributed File System (HDFS) en het ondersteunt [POSIX-ACL's](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists). Hiermee kunt u lezen (r), (b) schrijven en uitvoeren (x) tooresources machtigingen voor de rol van eigenaar hello, Hallo Eigenaar Groepsbeleid, en voor andere gebruikers en groepen. In Hallo openbare Preview van Data Lake Store (Hallo huidige release), kunnen de ACL's worden ingeschakeld in de hoofdmap hello, submappen en afzonderlijke bestanden. Zie voor meer informatie over de werking van ACL's in de context van Data Lake Store [Toegangsbeheer in Data Lake Store](data-lake-store-access-control.md).

Het is raadzaam dat u voor meerdere gebruikers met behulp van ACL's definiëren [beveiligingsgroepen](../active-directory/active-directory-accessmanagement-manage-groups.md). Beveiligingsgroep voor gebruikers tooa toevoegen en vervolgens Hallo ACL's voor een bestand of map toothat beveiligingsgroep toewijzen. Dit is handig als u wilt dat tooprovide aangepaste toegang, omdat u beperkte tooadding maximaal negen items voor aangepaste toegang. Zie voor meer informatie over hoe de gegevens die zijn opgeslagen in Data Lake Store met Azure Active Directory-beveiligingsgroepen voor het beveiligen van toobetter [gebruikers of beveiligingsgroep toewijzen als ACL's toohello Azure Data Lake Store-bestandssysteem](data-lake-store-secure-data.md#filepermissions).

![Standaard- en aangepaste toegang lijst](./media/data-lake-store-security-overview/adl.acl.2.png "lijst standaard en aangepaste toegang")

## <a name="network-isolation"></a>Netwerkisolatie
Gebruik Data Lake Store toohelp beheer toegang tot tooyour gegevens opslaan op netwerkniveau Hallo. U kunt tot stand brengen van firewalls en een IP-adresbereik opgeven voor uw vertrouwde clients. Alleen clients met een IP-adres binnen het bereik van Hallo gedefinieerd kunnen tooData Lake Store verbinding maken met een IP-adresbereik.

![Firewall-instellingen en IP-toegang tot](./media/data-lake-store-security-overview/firewall-ip-access.png "Firewall-instellingen en IP-adres")

## <a name="data-protection"></a>Gegevensbeveiliging
Azure Data Lake Store beschermt u uw gegevens tijdens de levenscyclus. Voor gegevens tijdens de overdracht gebruikt Data Lake Store Hallo industriestandaard-Transport Layer Security (TLS)-protocol toosecure gegevens via Hallo-netwerk.

![Codering in Data Lake Store](./media/data-lake-store-security-overview/adls-encryption.png "versleuteling in Data Lake Store")

Data Lake Store biedt ook versleuteling voor gegevens die zijn opgeslagen in Hallo-account. U hebt gekozen toohave uw gegevens versleuteld of kiezen voor geen versleuteling. Als u zich voor versleuteling aanmelden is opgeslagen gegevens in Data Lake Store versleutelde voorafgaande toostoring op permanente media. In dat geval Data Lake Store automatisch gecodeerd voorafgaande toopersisting gegevens en gedecodeerd gegevens voorafgaande tooretrieval, dus is het volledig transparant toohello client Hallo gegevenstoegang. Er is geen codewijziging vereist op Hallo tooencrypt/ontsleutelen clientgegevens.

Voor sleutelbeheer biedt Data Lake Store twee modi voor het beheren van uw master versleutelingssleutels (MEKs), die vereist zijn voor het ontsleutelen van gegevens die zijn opgeslagen in Data Lake Store Hallo zijn. U kunt ofwel Data Lake Store Hallo MEKs voor u beheert, of kies tooretain eigendom van Hallo MEKs met uw account voor Azure Sleutelkluis. U opgeven Hallo-modus van Sleutelbeheer terwijl tijdens het maken van een Data Lake Store-account. Voor meer informatie over het tooprovide versleuteling-gerelateerde configuratie, Zie [aan de slag met Azure Data Lake Store met Azure Portal Hallo](data-lake-store-get-started-portal.md).

## <a name="auditing-and-diagnostic-logs"></a>Controle en diagnostische logboeken
U kunt controleren of diagnostische logboeken, afhankelijk van of u op zoek naar de logboeken voor incidentbeheer activiteiten of gegevens-gerelateerde activiteiten.

* Management-gerelateerde activiteiten gebruik van Azure Resource Manager-API's en worden opgehaald in hello Azure-portal via controlelogboeken.
* Data-gerelateerde activiteiten gebruik van WebHDFS REST-API's en in hello Azure-portal via Logboeken met diagnostische gegevens worden opgehaald.

### <a name="auditing-logs"></a>Controlelogboeken
toocomply aan voorschriften een organisatie mogelijk voldoende audittrails als toodig naar specifieke incidenten. Data Lake Store is ingebouwde bewaking en controle en registreert alle account beheeractiviteiten.

Voor audittrails account management, weergeven en Hallo kolommen kiezen die u toolog wilt. U kunt ook audit logboeken tooAzure opslag exporteren.

![Controlelogboeken](./media/data-lake-store-security-overview/audit-logs.png "Controlelogboeken")

### <a name="diagnostic-logs"></a>Diagnostische logboeken
U kunt toegang tot gegevens audittrails in hello Azure-portal (in de diagnostische instellingen) en maken van een Azure Blob storage-account waarin Hallo logboeken worden opgeslagen.

![Diagnostische logboeken](./media/data-lake-store-security-overview/diagnostic-logs.png "diagnostische logboeken")

Nadat u de diagnostische instellingen configureert, kunt u Hallo logboeken weergeven op Hallo **diagnostische logboeken** tabblad.

Zie voor meer informatie over het werken met Logboeken met diagnostische gegevens met Azure Data Lake Store [toegang tot diagnoselogboeken voor Data Lake Store](data-lake-store-diagnostic-logs.md).

## <a name="summary"></a>Samenvatting
Enterprise-klanten vereisen een cloud-platform voor gegevens analytics is veiliger en gemakkelijk toouse. Azure Data Lake Store is ontworpen toohelp deze vereisten via identiteits- en verificatie via Azure Active Directory-integratie, op basis van ACL-autorisatie, netwerkisolatie, gegevensversleuteling onderweg en at-rest (binnenkort in hello te houden toekomstige) en controle.

Als u toosee nieuwe functies in Data Lake Store wilt, stuur ons uw feedback in Hallo [Data Lake Store UserVoice forum](https://feedback.azure.com/forums/327234-data-lake).

## <a name="see-also"></a>Zie ook
* [Overzicht van Azure Data Lake Store](data-lake-store-overview.md)
* [Aan de slag met Data Lake Store](data-lake-store-get-started-portal.md)
* [Gegevens in Data Lake Store beveiligen](data-lake-store-secure-data.md)

