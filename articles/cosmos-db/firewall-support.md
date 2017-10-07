---
title: aaaAzure Cosmos DB firewallondersteuning & IP-toegangsbeheer | Microsoft Docs
description: Meer informatie over hoe toouse IP-beleid voor toegangsbeheer voor firewall ondersteuning bieden voor Azure Cosmos DB database accounts.
keywords: Toegangsbeheer voor IP-, firewallondersteuning
services: cosmos-db
author: shahankur11
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: c1b9ede0-ed93-411a-ac9a-62c113a8e887
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ankshah
ms.openlocfilehash: b5cdbdb28e9d7ee0fd0ea54aad277167b699929f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-firewall-support"></a>Ondersteuning van Azure DB Cosmos-firewall
toosecure gegevens opgeslagen in een databaseaccount Azure Cosmos DB, Azure Cosmos DB heeft biedt ondersteuning voor een geheim op basis van [autorisatie model](https://msdn.microsoft.com/library/azure/dn783368.aspx) die gebruikmaakt van een sterke Hash-based message authentication code (HMAC). Nu bovendien autorisatie-model op basis van toohello geheim, Azure Cosmos DB beleid aangestuurd IP gebaseerd toegangsbeheer voor binnenkomende firewallondersteuning ondersteunt. Dit model is heel vergelijkbaar toohello firewallregels van een systeem van traditionele databases en biedt een extra verificatieniveau beveiliging toohello databaseaccount Azure Cosmos DB. Met dit model, u kunt nu een alleen toegankelijk vanuit een goedgekeurde set machines van Azure DB die Cosmos database account toobe configureren en/of cloudservices. Toegang tot tooAzure Cosmos DB bronnen van deze goedgekeurde sets machines en services vereisen nog steeds Hallo aanroeper toopresent een geldige verificatietoken.

## <a name="ip-access-control-overview"></a>IP-Toegangsbeheer-overzicht
Een Azure DB die Cosmos-databaseaccount is standaard toegankelijk is vanaf het openbare internet, zolang het Hallo-aanvraag vergezeld gaat van een geldige verificatietoken. tooconfigure IP op basis van beleid voor toegangsbeheer, Hallo gebruiker moet Hallo reeks IP-adressen of IP-adresbereiken in CIDR-formulier toobe opgenomen als Hallo toegestane lijst met client-IP-adressen voor een bepaalde database-account opgeven. Nadat deze configuratie is toegepast, worden alle aanvragen die afkomstig zijn van computers buiten deze lijst met toegestane wordt geblokkeerd door Hallo-server.  Hallo verbinding verwerking van de stroom voor Hallo toegangsbeheer op basis van IP is beschreven in het volgende diagram Hallo.

![Diagram van Hallo verbindingsproces voor toegangsbeheer op basis van IP](./media/firewall-support/firewall-support-flow.png)

## <a name="connections-from-cloud-services"></a>Verbindingen met cloudservices
Cloudservices zijn in Azure, een veelgebruikte manier voor het hosten van de middelste laag service logica met behulp van Azure Cosmos DB. tooenable toegang tooan Azure Cosmos DB databaseaccount van een cloudservice, openbare IP-adres van de cloudservice Hallo Hallo moet toegevoegde toohello toegestane lijst met IP-adressen die zijn gekoppeld aan uw Azure DB die Cosmos-databaseaccount door [configureren IP-beleid voor toegangsbeheer Hallo](#configure-ip-policy).  Dit zorgt ervoor dat alle rolexemplaren van cloud-services toegang tooyour databaseaccount Azure Cosmos DB. U kunt IP-adressen ophalen voor uw cloudservices in hello Azure-portal, zoals wordt weergegeven in de volgende schermafbeelding Hallo.

![Schermopname van het openbare IP-adres Hallo voor een cloudservice die worden weergegeven in hello Azure-portal](./media/firewall-support/public-ip-addresses.png)

Wanneer u uw cloudservice uitbreiden door aanvullende rol exemplaren toe te voegen, die nieuwe exemplaren automatisch toegang toohello Azure DB die Cosmos-databaseaccount hebt omdat ze deel van Hallo uitmaken dezelfde cloudservice.

## <a name="connections-from-virtual-machines"></a>Verbindingen van virtuele machines
[Virtuele machines](https://azure.microsoft.com/services/virtual-machines/) of [virtuele-machineschaalsets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) kan ook worden gebruikt toohost middelste laag services met behulp van Azure Cosmos DB.  tooconfigure hello Azure Cosmos DB account tooallow toegang tot de database van virtuele machines, openbare IP-adressen van virtuele machine en/of de virtuele-machineschaalset moet worden geconfigureerd als een toegestane IP-adressen voor het account van uw Azure DB die Cosmos-database door Hallo [Hallo IP-beleid voor toegangsbeheer configureren](#configure-ip-policy). Zoals wordt weergegeven in de volgende schermafbeelding Hallo, kunt u IP-adressen voor virtuele machines in Azure-portal Hallo ophalen.

![Schermopname van een openbaar IP-adres voor een virtuele machine weergegeven in hello Azure-portal](./media/firewall-support/public-ip-addresses-dns.png)

Wanneer u aanvullende virtuele machine-exemplaren toohello groep toevoegt, worden ze automatisch toegang tooyour Azure DB die Cosmos-databaseaccount opgegeven.

## <a name="connections-from-hello-internet"></a>Verbindingen van internet Hallo
Wanneer u toegang tot een Cosmos Azure DB database account vanaf een computer op internet hello, moet hello client IP-adres of IP-adresbereik van de machine Hallo toegevoegde toohello lijst met IP-adres voor hello Azure DB die Cosmos-databaseaccount toegestaan. 

## <a id="configure-ip-policy"></a>Hallo IP-beleid voor toegangsbeheer configureren
Hallo IP-beleid voor toegangsbeheer kunt u instellen in hello Azure-portal of programmatisch via [Azure CLI](cli-samples.md), [Azure Powershell](powershell-samples.md), of Hallo [REST-API](/rest/api/documentdb/) door Hallo bijwerken`ipRangeFilter` eigenschap. IP-adressen of-adresbereiken moet door komma's gescheiden en mag geen spaties bevatten. Voorbeeld: '13.91.6.132,13.91.6.1/24'. Wanneer uw databaseaccount wordt bijgewerkt via deze methoden, worden toopopulate ervoor dat alle Hallo eigenschappen tooprevent toodefault instellingen herstellen.

> [!NOTE]
> Als u een IP-toegangsbeleid voor het account van uw Azure DB die Cosmos-database, toegestaan alle toegang tooyour Azure Cosmos DB databaseaccount vanaf computers buiten Hallo geconfigureerd lijst met IP-adresbereiken worden geblokkeerd. Doordat dit model Hallo gegevensbewerking vlak van Hallo portal bladeren worden ook geblokkeerde tooensure Hallo integriteit van toegangsbeheer.

toosimplify ontwikkeling, hello Azure-portal helpt u te identificeren en Hallo IP-adres van uw client machine toohello lijst toegestaan toevoegen zodat apps die worden uitgevoerd van de computer toegang heeft tot hello Azure DB die Cosmos-account. Houd er rekening mee dat Hallo IP-clientadres Hier wordt gedetecteerd, zoals weergegeven door het Hallo-portal. Hallo client-IP-adres van uw computer is mogelijk, maar dit kan ook worden Hallo IP-adres van de gateway van uw netwerk. Vergeet niet tooremove het eerder tooproduction gaat.

tooset hello IP-beleid voor toegangsbeheer in hello Azure-portal navigeert blade toohello Azure DB die Cosmos-account, klikt u op **Firewall** in het navigatiemenu hello, klik vervolgens op **ON** 

![Schermopname die laat zien hoe tooopen Hallo Firewall blade in hello Azure-portal](./media/firewall-support/azure-portal-firewall.png)

Opgeven of hello Azure-portal kunt toegang Hallo-account tot, en voeg desgewenst andere adressen en -bereiken toe en klik vervolgens in het nieuwe deelvenster hello, **opslaan**.  

> [!NOTE]
> Wanneer u een IP-beleid voor toegangsbeheer inschakelt, moet u tooadd Hallo IP-adres voor hello Azure portal toomaintain toegang. Hallo portal IP-adressen zijn:
> |Regio|IP-adres|
> |------|----------|
> |Alle regio's die zijn opgegeven behalve hieronder| 104.42.195.92|
> |Duitsland|51.4.229.218|
> |China|139.217.8.252|
> |VS (overheid) - Arizona|52.244.48.71|
>

![Schermopname die laat zien hoe u een tooconfigure firewall-instellingen in hello Azure-portal](./media/firewall-support/azure-portal-firewall-configure.png)

## <a name="troubleshooting-hello-ip-access-control-policy"></a>Het oplossen van problemen Hallo IP-beleid voor toegangsbeheer
### <a name="portal-operations"></a>Portal-bewerkingen
Als u een IP-toegangsbeleid voor het account van uw Azure DB die Cosmos-database, toegestaan alle toegang tooyour Azure Cosmos DB databaseaccount vanaf computers buiten Hallo geconfigureerd lijst met IP-adresbereiken worden geblokkeerd. Als u tooenable portal gegevens vlak bewerkingen wilt zoals het bladeren door verzamelingen en query-documenten, moet u daarom tooexplicitly toestaan van Azure portal-toegang met behulp van Hallo **Firewall** blade in Hallo-portal. 

![Schermopname die laat zien hoe u een tooenable toegang toohello Azure-portal](./media/firewall-support/azure-portal-access-firewall.png)

### <a name="sdk--rest-api"></a>SDK & Rest-API
Voor toegang via SDK of REST-API van computers niet in de lijst met toegestane Hallo uit veiligheidsoverwegingen het resultaat van algemene 404 niet gevonden zonder extra details. Controleer of dat Hallo IP toegestane lijst die zijn geconfigureerd voor Azure Cosmos DB database tooensure Hallo juiste beleid voor configuratie van uw account is toegepaste tooyour databaseaccount Azure Cosmos DB.

## <a name="next-steps"></a>Volgende stappen
Zie voor informatie over het netwerk gerelateerde prestatietips [tips voor betere prestaties](performance-tips.md).

