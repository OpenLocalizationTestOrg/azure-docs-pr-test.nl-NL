---
title: aaaWhat is Azure Sleutelkluis? | Microsoft Docs
description: Met Azure Key Vault kunt u de cryptografische sleutels en geheimen beveiligen die door cloudtoepassingen en -services worden gebruikt. Klanten kunnen met Azure Key Vault sleutels en geheimen versleutelen (zoals verificatiesleutels, opslagaccountsleutels, gegevensversleutelingssleutels, PFX-bestanden en wachtwoorden) door gebruik te maken van sleutels die worden beveiligd met HSM's.
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e759df6f-0638-43b1-98ed-30b3913f9b82
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 296fcce03658b96b84afab299b73681bbe8ac9fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-key-vault"></a>Wat is Azure Sleutelkluis?
Azure Sleutelkluis is beschikbaar in de meeste regio's. Zie voor meer informatie, Hallo [pagina prijzen van Sleutelkluis](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Inleiding
Met Azure Sleutelkluis kunt u de cryptografische sleutels en geheimen beveiligen die door cloudtoepassingen en -services worden gebruikt. U kunt met Key Vault sleutels en geheimen versleutelen (zoals verificatiesleutels, opslagaccountsleutels, gegevensversleutelingssleutels, PFX-bestanden en wachtwoorden) door gebruik te maken van sleutels die worden beveiligd met HSM's. Voor extra zekerheid kunt u de sleutels importeren of genereren in HSM's. Als u kiest toodo deze, processen Microsoft uw sleutels in FIPS 140-2 op niveau 2 gevalideerde HSM (hardware en firmware).  

Sleutelkluis stroomlijnt het beheerproces Hallo en kunt u toomaintain beheer van sleutels die toegang tot en uw gegevens te versleutelen. Ontwikkelaars kunnen maken van sleutels voor het ontwikkelen en testen in minuten en deze vervolgens probleemloos migreren tooproduction sleutels. Administrators voor rapportbeveiliging kunnen verlenen (en intrekken) machtiging tookeys, indien nodig.

Gebruik Hallo na tabel toobetter begrijpen hoe Sleutelkluis toomeet Hallo behoeften van ontwikkelaars en beveiligingsadministrators kan helpen.

| Rol | Probleemformulering | Opgelost door Azure Key Vault |
| --- | --- | --- |
| Ontwikkelaar voor een Azure-toepassing |"Ik wil toowrite een toepassing voor Azure die gebruikmaakt van sleutels voor ondertekening en versleuteling, maar ik wil deze sleutels toobe externe van mijn toepassing zodat Hallo oplossing geschikt voor een toepassing die geografisch wordt gedistribueerd. <br/><br/>Ik wil ook dat deze sleutels en geheimen toobe beveiligd, zonder dat toowrite Hallo code zelf. Ik is ook raadzaam deze sleutels en geheimen toobe gemakkelijk voor mij toouse vanuit Mijn toepassingen kunnen met optimale prestaties." |√ De sleutels worden opgeslagen in een kluis en wanneer dit nodig is, aangeroepen via een URI.<br/><br/> √ De sleutels worden beveiligd door Azure. Hiervoor wordt gebruikgemaakt van algoritmen, sleutellengten en HSM's die voldoen aan de industriestandaard).<br/><br/> √ Sleutels worden verwerkt in HSM's die zich in Hallo dezelfde Azure-datacenters als Hallo-toepassingen. Dit biedt betere betrouwbaarheid en lagere latentie mogelijk dan als Hallo sleutels zich op een afzonderlijke locatie, bijvoorbeeld on-premises. |
| SaaS-ontwikkelaar (Software as a Service) |"Ik wil niet Hallo verantwoordelijk of potentiële aansprakelijkheid voor mijn klant tenant-sleutels en geheimen. <br/><br/>Ik Hallo klanten tooown wilt en hun sleutels beheren, zodat ik mij concentreren kan op hetgeen waar ik beste, namelijk het leveren van Hallo belangrijkste softwarefuncties." |√ Klanten kunnen hun eigen sleutels in Azure importeren en beheren. Wanneer een SaaS-toepassing tooperform cryptografische bewerkingen moet met behulp van hun klanten sleutels, biedt Sleutelkluis deze bewerkingen namens Hallo-toepassing. Hallo-toepassing hello klanten sleutels niet te zien. |
| Chief Security Officer (CSO) |"Ik wil tooknow die onze toepassingen aan de FIPS 140-2 Level 2 HSM's voor beveiligd Sleutelbeheer voldoen. <br/><br/>Ik wilt toomake ervoor dat mijn organisatie wordt controle over de levenscyclus van de Hallo-sleutel en het sleutelgebruik kan controleren. <br/><br/>En hoewel we meerdere Azure-services en bronnen gebruiken, ik wil toomanage Hallo sleutels vanaf één locatie in Azure." |√ HSM's zijn FIPS 140-2 Level 2-gevalideerde modules.<br/><br/>√ Key Vault is zodanig ontworpen dat Microsoft uw sleutels niet kan zien of extraheren.<br/><br/>√ Het sleutelgebruik wordt vrijwel in realtime geregistreerd in een logboek.<br/><br/>√ hello kluis biedt één interface, ongeacht het aantal kluizen hebt u in Azure, welke regio's ze ondersteuning en welke toepassingen ze worden gebruikt. |

Iedereen met een Azure-abonnement kan sleutelkluizen maken en gebruiken. Hoewel Key Vault voordelen biedt voor ontwikkelaars en beveiligingsadministrators, kan de service worden geïmplementeerd en beheerd door een beheerder die ook andere Azure-services voor een organisatie beheert. Deze beheerder zou bijvoorbeeld aanmelden met een Azure-abonnement, een kluis voor Hallo organisatie in welke toostore-sleutels maken en vervolgens verantwoordelijk zijn voor operationele taken, zoals:

* Een sleutel of geheim maken of importeren.
* Een sleutel of geheim intrekken of verwijderen.
* Autoriseren van gebruikers of toepassingen tooaccess hello sleutelkluis, zodat ze kunnen beheren of gebruiken van de sleutels en geheimen
* Sleutelgebruik configureren (bijvoorbeeld ondertekenen of versleutelen).
* Sleutelgebruik bewaken.

Deze beheerder zou vervolgens ontwikkelaars voorzien van URI's toocall in hun toepassingen en bieden hun beveiligingsbeheerder sleutelgebruik logboekinformatie. 

   ![Overzicht van Azure Key Vault][1]

Ontwikkelaars kunnen ook beheren Hallo sleutels rechtstreeks met behulp van API's. Zie voor meer informatie [Sleutelkluis ontwikkelaarshandleiding Hallo](key-vault-developers-guide.md).

## <a name="next-steps"></a>Volgende stappen
Zie [Aan de slag met Azure Key Vault](key-vault-get-started.md) voor een inleidende zelfstudie voor beheerders.

Zie [Logboekregistratie van Azure Key Vault](key-vault-logging.md) voor meer informatie over de gebruiksregistratie voor Key Vault.

Zie [Over sleutels, geheimen en certificaten](https://msdn.microsoft.com/library/azure/dn903623\(v=azure.1\).aspx) voor meer informatie over het gebruik van sleutels en geheimen met Azure Key Vault.

<!--Image references-->
[1]: ./media/key-vault-whatis/AzureKeyVault_overview.png
