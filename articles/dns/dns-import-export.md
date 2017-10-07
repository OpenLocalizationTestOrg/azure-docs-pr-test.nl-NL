---
title: aaaImport en exporteren van een domeinzone tooAzure DNS met Azure CLI 1.0-bestand | Microsoft Docs
description: Meer informatie over hoe tooimport en een DNS-server exporteren bestand tooAzure DNS-zone met behulp van Azure CLI 1.0
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a>Importeren en exporteren van een DNS-zonebestand met hello Azure CLI 1.0 

In dit artikel leert u hoe tooimport en exporteren DNS-zone-bestanden voor het gebruik van Azure DNS hello Azure CLI 1.0.

## <a name="introduction-toodns-zone-migration"></a>Inleiding tooDNS zone migratie

Een DNS-zonebestand is een tekstbestand met de details van elke record System DNS (Domain Name) in Hallo zone. Volgt een standaardindeling, waardoor het geschikt is voor de DNS-records overbrengen tussen DNS-systemen. Met behulp van een zonebestand is een snelle, betrouwbare, en een handige manier tootransfer een DNS-zone van of naar Azure DNS.

Azure DNS ondersteunt importeren en exporteren van de zone-bestanden met behulp van hello Azure-opdrachtregelinterface (CLI). Zone-bestand importeren is **niet** momenteel ondersteund via Azure PowerShell of hello Azure-portal.

Hello Azure CLI 1.0 is een platformoverschrijdende opdrachtregel-hulpprogramma gebruikt voor het beheer van Azure-services. Is beschikbaar voor Windows, Mac en Linux platforms Hallo van Hallo [pagina Azure downloads](https://azure.microsoft.com/downloads/). Ondersteuning voor meerdere platforms is belangrijk voor importeren en exporteren van zonebestanden, omdat de meest voorkomende naam serversoftware Hallo [BINDEN](https://www.isc.org/downloads/bind/), doorgaans op Linux wordt uitgevoerd.

> [!NOTE]
> Er zijn twee versies van hello Azure CLI. CLI1.0 is gebaseerd op Node.js en opdrachten die beginnen met 'azure' is.
> CLI2.0 is gebaseerd op Python en opdrachten die beginnen met 'az' heeft. Zone-bestand importeren in beide versies wordt ondersteund, wordt u aangeraden Hallo CLI1.0 opdrachten, zoals beschreven in deze pagina.

## <a name="obtain-your-existing-dns-zone-file"></a>Verkrijgen van uw bestaande DNS-zonebestand

Voordat u een DNS-zone-bestand in Azure DNS importeren, moet u een kopie van het Hallo-zonebestand tooobtain. Hallo-bron van dit bestand is afhankelijk van waar momenteel Hallo DNS-zone wordt gehost.

* Als uw DNS-zone wordt gehost door een partner-service (zoals een domeinregistrar, specifieke DNS-hostingprovider of alternatieve cloudprovider), leveren die service DNS-zonebestand voor Hallo mogelijkheid toodownload Hallo.
* Als uw DNS-zone wordt gehost op Windows DNS, Hallo standaard wordt de map voor Hallo zonebestanden **%systemroot%\system32\dns**. Hallo volledig pad tooeach zone-bestand bevat ook op Hallo **algemene** tabblad van Hallo DNS-console.
* Als uw DNS-zone wordt gehost met behulp van BIND, Hallo-locatie van Hallo-zonebestand voor elke zone wordt opgegeven in het configuratiebestand voor BIND Hallo **named.conf**.

> [!NOTE]
> Zone-bestanden die zijn gedownload van GoDaddy hebben een iets andere indeling. U moet toocorrect dit voordat u deze zonebestanden in Azure DNS importeren.
>
> DNS-namen in Hallo RDATA van elke DNS-record zijn opgegeven als FQDN-namen, maar ze niet beschikken over een afsluitende '. ' Dit betekent dat ze worden geïnterpreteerd door andere DNS-systemen als relatieve namen. U moet tooedit Hallo zone bestand tooappend Hallo beëindigd '. ' tootheir namen voordat u ze in Azure DNS importeren.
>
> Bijvoorbeeld, CNAME-record 'www 3600 IN CNAME contoso.com' hello te moet worden gewijzigd 'www 3600 IN CNAME contoso.com'.
> (met een afsluitende '. ').

## <a name="import-a-dns-zone-file-into-azure-dns"></a>Een DNS-zone-bestand importeren in Azure DNS

Maakt een nieuwe zone een zonebestand te importeren in Azure DNS, als deze niet al bestaat. Als de zone Hallo al bestaat, moeten hello recordsets in Hallo zonebestand worden samengevoegd met de bestaande recordsets Hallo.

### <a name="merge-behavior"></a>Samenvoegen van gedrag

* Standaard worden bestaande en nieuwe recordsets samengevoegd. Identieke records binnen een samengevoegde Recordset zijn ongedaan gedupliceerde.
* U kunt ook door op te geven Hallo `--force` optie, Hallo importeren proces vervangt bestaande recordsets met nieuwe recordsets. Bestaande recordsets waarvoor geen overeenkomende recordset in de geïmporteerde zonebestand Hallo worden niet verwijderd.
* Als recordsets worden samengevoegd, wordt hello toolive TTL (time) van de bestaande recordsets gebruikt. Wanneer `--force` wordt gebruikt, Hallo TTL van de nieuwe recordset hello wordt gebruikt.
* Parameters Authority (SOA) is gestart (behalve `host`) altijd onttrokken Hallo geïmporteerde zone-bestand, ongeacht of `--force` wordt gebruikt. Op deze manier voor Hallo naamserverrecord ingesteld in het toppunt zone hello, hello TTL altijd overgenomen uit Hallo geïmporteerde zone-bestand.
* Een geïmporteerde CNAME-record is geen vervanging voor een bestaande CNAME record met dezelfde naam tenzij Hallo Hallo `--force` parameter wordt opgegeven.
* Als een conflict optreedt tussen een CNAME-record en een andere record Hallo dezelfde naam maar een ander type (ongeacht die is bestaande of nieuwe), Hallo bestaande record wordt bewaard. Dit is onafhankelijk van het gebruik van Hallo `--force`.

### <a name="additional-information-about-importing"></a>Als u meer informatie over het importeren

Hallo bieden opmerkingen bij de volgende aanvullende technische gegevens over Hallo zone importeren.

* Hallo `$TTL` richtlijn is optioneel en wordt ondersteund. Als er geen `$TTL` richtlijn krijgt, records zonder een expliciete TTL worden geïmporteerd tooa standaard TTL 3600 seconden instellen. Wanneer twee registreert in hello dezelfde recordset Geef andere TTLs, Hallo lagere waarde wordt gebruikt.
* Hallo `$ORIGIN` richtlijn is optioneel en wordt ondersteund. Als er geen `$ORIGIN` is ingesteld, Hallo standaard gebruikte waarde is de zonenaam Hallo die is opgegeven op de opdrachtregel Hallo (plus hello wordt beëindigd '. ').
* Hallo `$INCLUDE` en `$GENERATE` richtlijnen worden niet ondersteund.
* Deze typen worden ondersteund: A, AAAA, CNAME, MX, NS, SOA, SRV en TXT.
* Hallo SOA-record wordt automatisch gemaakt door Azure DNS wanneer u een zone wordt gemaakt. Wanneer u een zonebestand importeert, alle SOA-parameters zijn afkomstig uit Hallo zonebestand *behalve* hello `host` parameter. Hallo-waarde die door Azure DNS maakt gebruik van deze parameter. Dit is omdat deze parameter moet toohello de naam van de primaire server is verstrekt door Azure DNS verwijzen.
* Hallo naamserverrecord ingesteld in het toppunt Hallo zone wordt ook automatisch gemaakt door Azure DNS als Hallo zone wordt gemaakt. Alleen is hello TTL van deze recordset geïmporteerd. Deze records bevatten Hallo naamservernamen verstrekt door Azure DNS. Hallo gegevens niet wordt overschreven door de waarden in de geïmporteerde zonebestand Hallo Hallo.
* Azure DNS biedt ondersteuning voor slechts één tekenreeks TXT-records tijdens de openbare Preview. Multistring TXT-records zijn aaneengeschakelde en afgekapte too255 tekens zijn.

### <a name="cli-format-and-values"></a>CLI-indeling en waarden

Hallo-indeling van hello Azure CLI opdracht tooimport een DNS-zone is:

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

Waarden:

* `<resource group>`Hallo naam van resourcegroep Hallo Hallo zone in Azure DNS is.
* `<zone name>`Hallo-naam van Hallo zone is.
* `<zone file name>`Hallo padnaam van Hallo zone bestand toobe geïmporteerd is.

Als een zone met deze naam niet in de resourcegroep hello bestaat, wordt deze voor u gemaakt. Als hello zone al bestaat, worden hello geïmporteerde recordsets samengevoegd met bestaande recordsets. toooverwrite hello bestaande recordsets, gebruik Hallo `--force` optie.

tooverify hello indeling van een zonebestand zonder het, gebruik Hallo daadwerkelijk geïmporteerd `--parse-only` optie.

### <a name="step-1-import-a-zone-file"></a>Step 1. Een zonebestand importeren

een zonebestand voor Hallo zone tooimport **contoso.com**.

1. Meld u tooyour Azure-abonnement met behulp van hello Azure CLI 1.0.

    ```azurecli
    azure login
    ```

2. Selecteer waar u toocreate uw nieuwe DNS-zone Hallo-abonnement.

    ```azurecli
    azure account set <subscription name>
    ```

3. Azure DNS is een Azure Resource Manager alleen-lezen-service zodat hello Azure CLI uitgeschakeld tooResource Manager-modus zijn moet.

    ```azurecli
    azure config mode arm
    ```

4. Voordat u hello Azure DNS-service gebruiken, moet u uw abonnement toouse hello Microsoft.Network-resourceprovider registreren. (Dit is een eenmalige bewerking voor elk abonnement.)

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. Als u nog geen een hebt, moet u ook toocreate een Resource Manager-resourcegroep.

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. tooimport hello zone **contoso.com** uit bestand Hallo **contoso.com.txt** in een nieuwe DNS-zone in de resourcegroep Hallo **myresourcegroup**, Voer Hallo opdracht `azure network dns zone import`.<BR>Met deze opdracht wordt geladen Hallo zone-bestand en het parseren. Hallo-opdracht wordt een reeks opdrachten uitgevoerd op Hallo Azure DNS-service toocreate Hallo zone en alle Hallo recordsets in Hallo zone. Hallo opdracht rapporten voortgang in Hallo-consolevenster, samen met eventuele fouten of waarschuwingen. Omdat recordsets zijn gemaakt in de reeks, duurt het enkele minuten tooimport een grote zone-bestand.

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a>Stap 2. Controleer of de zone Hallo

tooverify hello DNS-zone nadat u Hallo-bestand importeren, kunt u een van de volgende methoden Hallo:

* U kunt Hallo records weergeven met behulp van hello Azure CLI-opdracht te volgen:

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* U kunt Hallo records weergeven met behulp van PowerShell-cmdlet Hallo `Get-AzureRmDnsRecordSet`.
* U kunt `nslookup` tooverify naamomzetting voor Hallo records. Omdat Hallo zone nog niet is toegewezen, moet u toospecify Hallo juiste Azure DNS-naamservers expliciet. Hallo volgende voorbeeld toont hoe tooretrieve hello naamservernamen toohello zone toegewezen. IT ook ziet u hoe tooquery Hallo 'www' vastleggen met behulp van `nslookup`.

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a>Stap 3. DNS-delegering bijwerken

Nadat u hebt gecontroleerd dat Hallo zone correct is geïmporteerd, moet u tooupdate Hallo DNS-delegering toopoint toohello naamservers Azure DNS. Zie voor meer informatie artikel Hallo [Hallo DNS-delegering bijwerken](dns-domain-delegation.md).

## <a name="export-a-dns-zone-file-from-azure-dns"></a>Een DNS-zone-bestand exporteren uit Azure DNS

Hallo-indeling van hello Azure CLI opdracht tooimport een DNS-zone is:

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

Waarden:

* `<resource group>`Hallo naam van resourcegroep Hallo Hallo zone in Azure DNS is.
* `<zone name>`Hallo-naam van Hallo zone is.
* `<zone file name>`Hallo padnaam van Hallo zone bestand toobe geëxporteerd is.

Zoals met Hallo zone importeren, moet u eerst toosign in, kiest u uw abonnement en configureer hello Azure CLI toouse Resource Manager-modus.

### <a name="tooexport-a-zone-file"></a>tooexport een zonebestand

1. Meld u tooyour Azure-abonnement met behulp van hello Azure CLI.

    ```azurecli
    azure login
    ```

2. Selecteer waar u toocreate uw DNS-zone Hallo-abonnement.

    ```azurecli
    azure account set <subscription name>
    ```

3. Azure DNS is een Azure Resource Manager alleen-lezen-service. Hello Azure CLI moet geschakelde tooResource Manager-modus.

    ```azurecli
    azure config mode arm
    ```

4. tooexport Hallo bestaande Azure DNS-zone **contoso.com** in de resourcegroep **myresourcegroup** toohello bestand **contoso.com.txt** (in Hallo huidige map), voert u `azure network dns zone export`. Deze opdracht aanroepen hello Azure DNS-service tooenumerate recordsets in Hallo zone en Hallo resultaten tooa BIND-compatibele zone-bestand exporteren.

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
