---
title: aaaSQL VM verbinding tooAzure zoeken | Microsoft Docs
description: Versleutelde verbindingen inschakelen en configureren van Hallo firewall tooallow verbindingen tooSQL Server op Azure een virtuele machine (VM) van een indexeerfunctie op Azure Search.
services: search
documentationcenter: 
author: HeidiSteen
manager: pablocas
editor: 
ms.assetid: 46e42e0e-c8de-4fec-b11a-ed132db7e7bc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: heidist
ms.openlocfilehash: 1f0db8a2812b0a7d012e58bb873c4b2b29fa1338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-connection-from-an-azure-search-indexer-toosql-server-on-an-azure-vm"></a>Een verbinding van een Azure Search-indexeerfunctie tooSQL Server configureren op een virtuele machine in Azure
Zoals vermeld in [verbinding maken met Azure SQL Database tooAzure zoeken met de indexeerfuncties](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md#faq), maken indexeerfuncties tegen **SQL Server op Azure Virtual machines** (of **SQL Azure Virtual machines** voor korte) is ondersteund door Azure Search, maar er zijn enkele vereisten met betrekking tot beveiliging tootake antwoord eerste. 

**De duur van de taak:** ongeveer 30 minuten, ervan uitgaande dat u al een certificaat geïnstalleerd op Hallo VM.

## <a name="enable-encrypted-connections"></a>Versleutelde verbindingen inschakelen
Azure Search is een versleuteld kanaal voor alle aanvragen van de indexeerfunctie via een openbare internetverbinding vereist. Deze sectie vindt Hallo stappen toomake dit werk.

1. Controleer Hallo eigenschappen van Hallo tooverify Hallo naam van de certificaathouder Hallo volledig gekwalificeerde domeinnaam (FQDN) van hello Azure VM. U kunt een hulpprogramma zoals CertUtils gebruiken of Hallo certificaten module tooview Hallo eigenschappen. Kunt u Hallo FQDN krijgen via Hallo VM service blade van Essentials sectie in Hallo **openbare IP-adres/DNS-naamlabel** veld in Hallo [Azure-portal](https://portal.azure.com/).
   
   * Voor virtuele machines die zijn gemaakt met behulp van Hallo nieuwere **Resource Manager** sjabloon Hallo FQDN is geformatteerd als `<your-VM-name>.<region>.cloudapp.azure.com`. 
   * Voor oudere virtuele machines die zijn gemaakt als een **klassieke** VM, Hallo FQDN is geformatteerd als `<your-cloud-service-name.cloudapp.net>`. 
2. Hallo Register-Editor (regedit) met behulp van SQL Server toouse Hallo-certificaat configureren. 
   
    Hoewel SQL Server Configuration Manager vaak voor deze taak gebruikt wordt, kunt u deze niet gebruiken voor dit scenario. Vindt niet Hallo geïmporteerd certificaat omdat de FQDN-naam van de VM op Azure Hallo Hallo komt niet overeen met de Hallo FQDN zoals wordt bepaald door Hallo VM (het identificeert Hallo domein als de lokale computer Hallo of Hallo netwerk domein toowhich die deze is gekoppeld). Als namen niet overeenkomen, moet u regedit toospecify Hallo certificaat gebruiken.
   
   * Blader in regedit toothis registersleutel: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\[MSSQL13.MSSQLSERVER]\MSSQLServer\SuperSocketNetLib\Certificate`.
     
     Hallo `[MSSQL13.MSSQLSERVER]` onderdeel varieert op basis van de versie en exemplaarnaam. 
   * Hallo-waarde van Hallo **certificaat** key toohello **vingerafdruk** van Hallo SSL-certificaat geïmporteerd van toohello VM.
     
     Er zijn verschillende manieren tooget Hallo vingerafdruk, sommige beter dan andere. Als u het kopiëren van Hallo **certificaten** -module in MMC, u waarschijnlijk opgehaald een onzichtbare toonaangevende teken [zoals beschreven in dit ondersteuningsartikel](https://support.microsoft.com/kb/2023869/), wat resulteert in een fout wanneer u probeert een de verbinding. Er bestaan verschillende oplossingen voor het oplossen van dit probleem. Hallo eenvoudigste toobackspace is voltooid, en typ nogmaals Hallo eerste teken van Hallo vingerafdruk tooremove Hallo toonaangevende teken in Hallo sleutelwaardeveld in regedit. U kunt ook een ander hulpprogramma toocopy Hallo vingerafdruk gebruiken.
3. Machtigingen toohello-serviceaccount. 
   
    Zorg ervoor dat Hallo SQL Server-serviceaccount is gemachtigd juiste op Hallo persoonlijke sleutel van Hallo SSL-certificaat. Als u deze stap laten corrigeren, worden SQL Server niet gestart. U kunt Hallo **certificaten** -module of **CertUtils** voor deze taak.
4. Hallo SQL Server-service opnieuw starten.

## <a name="configure-sql-server-connectivity-in-hello-vm"></a>SQL Server-connectiviteit in Hallo VM configureren
Nadat u Hallo versleutelde verbinding vereist voor Azure Search hebt ingesteld, zijn er aanvullende configuratie stappen intrinsieke tooSQL Server op Azure Virtual machines. Als u dit nog niet hebt gedaan, is de volgende stap Hallo toofinish-configuratie met behulp van een van deze artikelen:

* Voor een **Resource Manager** VM, Zie [verbinding maken met virtuele Machine van SQL Server op Azure Resource Manager met tooa](../virtual-machines/windows/sql/virtual-machines-windows-sql-connect.md). 
* Voor een **klassieke** VM, Zie [tooa virtuele Machine van SQL Server op de klassieke Azure-verbinding](../virtual-machines/windows/classic/sql-connect.md).

Controleer in het bijzonder Hallo-sectie in elk artikel voor "verbinding maken via internet Hallo".

## <a name="configure-hello-network-security-group-nsg"></a>Hallo Netwerkbeveiligingsgroep (NSG) configureren
Het is niet ongebruikelijk tooconfigure Hallo NSG en de bijbehorende Azure-eindpunt of de lijst met ACL (Access Control) toomake uw Azure VM toegankelijk tooother partijen. Waarschijnlijk hebben dat u eerder hebt uitgevoerd dit tooallow uw eigen toepassing logica tooconnect tooyour SQL Azure VM. Het gaat niet anders voor een Azure Search verbinding tooyour SQL Azure VM. 

Hallo onderstaande koppelingen bieden instructies over het NSG-configuratie voor VM-implementaties. Volg deze instructies dat tooacl een Azure SEarch-eindpunt op basis van het IP-adres.

> [!NOTE]
> Zie voor achtergrondinformatie, [wat is er een Netwerkbeveiligingsgroep?](../virtual-network/virtual-networks-nsg.md)
> 
> 

* Voor een **Resource Manager** VM, Zie [hoe toocreate nsg's voor ARM implementaties](../virtual-network/virtual-networks-create-nsg-arm-pportal.md). 
* Voor een **klassieke** VM, Zie [hoe toocreate nsg's voor klassieke implementaties](../virtual-network/virtual-networks-create-nsg-classic-ps.md).

IP-adressering kan opleveren voor enkele uitdagingen die gemakkelijk te overwinnen zijn als u zich bewust bent van Hallo probleem en mogelijke oplossingen. Hallo resterende secties vindt u de aanbevelingen voor het verwerken van problemen met gerelateerde tooIP adressen in Hallo ACL.

#### <a name="restrict-access-toohello-search-service-ip-address"></a>Beperken van toegang toohello search service IP-adres
Wij raden u Hallo toegang toohello IP-adres van uw zoekservice in Hallo ACL beperken in plaats van het maken van uw SQL Azure VM's breed open tooany verbindingsaanvragen. U kunt eenvoudig hello IP ontdekken adres door te pingen Hallo FQDN-naam (bijvoorbeeld `<your-search-service-name>.search.windows.net`) van uw zoekservice.

#### <a name="managing-ip-address-fluctuations"></a>IP-adres schommelingen beheren
Als uw search-service heeft slechts één zoekeenheid (dat wil zeggen, één replica en één partitie), wordt tijdens het opstarten wordt periodiek onderhoud, ongeldig te maken van een bestaande ACL met IP-adres van uw zoekservice Hallo IP-adres wijzigen.

Eenzijdige tooavoid Hallo volgende verbindingsfout is toouse meer dan één replica en een partitie in Azure Search. In dat geval Hallo kosten verhoogt, maar deze ook Hallo IP-adres probleem is opgelost. In Azure Search worden IP-adressen niet gewijzigd wanneer u meer dan één zoekeenheid hebt.

Een tweede aanpak is tooallow Hallo verbinding toofail en Hallo ACL's in Hallo NSG vervolgens opnieuw te configureren. Gemiddeld, kunt u verwachten IP-adressen toochange om de paar weken. Voor klanten die gecontroleerde indexeren op basis van incidentele, kan deze benadering levensvatbaar zijn.

Een derde levensvatbaar (maar niet met name veilig) aanpak is toospecify Hallo IP-adresbereik van hello Azure-regio waar uw search-service is ingericht. Hallo-lijst met IP-adresbereiken waarvan openbare IP-adressen tooAzure resources worden toegewezen wordt gepubliceerd op [Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653). 

#### <a name="include-hello-azure-search-portal-ip-addresses"></a>Hello Azure Search portal IP-adressen bevatten
Als u Azure portal toocreate een indexeerfunctie Hallo gebruikt, moet Azure Search portal logica ook toegang tooyour SQL Azure VM tijdens de aanmaakfase. Azure search portal IP-adressen kunnen u vinden door te pingen `stamp2.search.ext.azure.com`.

## <a name="next-steps"></a>Volgende stappen
Met configuratie buiten het Hallo manier kunt u nu een SQL Server op Azure VM als de gegevensbron Hallo voor een Azure Search-indexeerfunctie opgeven. Zie [verbinding maken met Azure SQL Database tooAzure zoeken met de indexeerfuncties](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md) voor meer informatie.

