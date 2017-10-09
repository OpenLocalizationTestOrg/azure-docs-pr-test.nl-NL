---
title: een aangepaste domeinnaam voor uw Azure Blob storage-eindpunt aaaConfigure | Microsoft Docs
description: Hello Azure portal toomap eindpunt van de eigen canonieke naam (CNAME) toohello Blob storage in een Azure Storage-account gebruiken.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: aaafd8c5-eacb-49dc-8c8b-3f7011ad5e92
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: marsma
ms.openlocfilehash: bfee6d28039f389ba2e2ed6b28d43894b6e15469
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-for-your-blob-storage-endpoint"></a>Een aangepaste domeinnaam configureren voor het eindpunt voor Blob Storage

U kunt een aangepast domein voor toegang tot blobgegevens in uw Azure storage-account configureren. Hallo eindpunt voor Blob-opslag is `<storage-account-name>.blob.core.windows.net`. Als u een aangepaste domeinen en subdomeinen zoals toewijst **www.contoso.com** blobeindpunt toohello voor uw opslagaccount, uw gebruikers krijgen vervolgens toegang tot blob-gegevens in uw storage-account met behulp van dat domein.

> [!IMPORTANT]
> Azure-opslag ondersteunt nog systeemeigen geen HTTPS met aangepaste domeinen. U kunt momenteel [hello Azure CDN tooaccess blobs gebruiken met aangepaste domeinen via HTTPS](storage-https-custom-domain-cdn.md).
>

Hallo volgende tabel ziet u enkele voorbeeld-URL's voor blob-gegevens die zich in een opslagaccount met de naam **mystorageaccount**. aangepast domein Hallo geregistreerd voor Hallo storage-account is **www.contoso.com**:

| Resourcetype | Standaard-URL | Aangepast domein-URL |
| --- | --- | --- |
| Storage-account | http://mystorageaccount.BLOB.Core.Windows.NET | http://www.contoso.com |
| Blob |http://mystorageaccount.BLOB.Core.Windows.NET/mycontainer/myblob | http://www.contoso.com/mycontainer/myblob |
| Hoofdcontainer | http://mystorageaccount.BLOB.Core.Windows.NET/myblob of http://mystorageaccount.blob.core.windows.net/$ root/myblob| http://www.contoso.com/myblob of http://www.contoso.com/$ root/myblob |

## <a name="direct-vs-intermediary-domain-mapping"></a>Directe versus tussenliggend domein toewijzing

Er zijn twee manieren toopoint uw aangepaste domein toohello blob-eindpunt voor uw opslagaccount: directe CNAME toewijzing en het gebruik van Hallo *asverify* tussenliggende subdomein.

### <a name="direct-cname-mapping"></a>Directe CNAME-toewijzing

Hallo-methode voor eerste en eenvoudigste, is toocreate een canonieke naam (CNAME)-record dat kan worden toegewezen van uw aangepaste domeinen en subdomeinen direct toohello blob-eindpunt. Een CNAME-record is een domain name system (DNS)-functie die een brondomein domein tooa bestemming wordt toegewezen. In dit geval Hallo brondomein is uw eigen aangepaste domeinen en subdomeinen, bijvoorbeeld *www.contoso.com*. Hallo doeldomein is uw eindpunt Blob-service bijvoorbeeld  *mystorageaccount.BLOB.Core.Windows.NET*.

Hallo directe methode wordt beschreven in [registreren van een aangepast domein](#register-a-custom-domain).

### <a name="intermediary-mapping-with-asverify"></a>Tussenliggende toewijzing met *asverify*

Hallo tweede methode gebruikt ook CNAME-records, maar eerst de veiligheidsmaatregelen voor een speciale subdomein dat wordt herkend door Azure tooavoid uitvaltijd: **asverify**.

Hallo-proces voor het toewijzen van uw aangepaste domein tooa blob-eindpunt kan resulteren in een korte periode van uitvaltijd voor Hallo domein terwijl u deze in Hallo registreert [Azure-portal](https://portal.azure.com). Als uw aangepaste domein wordt momenteel ondersteund door een toepassing met een service level agreement (SLA) waarvoor uitvaltijd, dan kunt u hello Azure *asverify* subdomein als een tussenliggende registratiestap. Deze tussenliggende stap zorgt ervoor dat gebruikers zijn kunnen tooaccess terwijl Hallo DNS-toewijzing plaats vindt uw domein.

Hallo tussenliggende methode wordt beschreven in [registreren van een aangepast domein met Hallo *asverify* subdomein](#register-a-custom-domain-using-the-asverify-subdomain).

## <a name="register-a-custom-domain"></a>Registreren van een aangepast domein
Gebruik deze procedure tooregister uw aangepaste domein als u zich geen zorgen over Hallo domein wordt kort niet beschikbaar tooyour gebruikers, of als uw aangepaste domein is momenteel geen host voor een toepassing.

Als uw aangepaste domein wordt momenteel ondersteund door een toepassing die geen uitvaltijd, volgt u Hallo-procedure beschreven in [registreren van een aangepast domein met Hallo *asverify* subdomein](#register-a-custom-domain-using-the-asverify-subdomain).

een aangepaste domeinnaam tooconfigure, moet u een nieuwe CNAME-record in DNS. Hallo CNAME-record bevat een alias voor een domeinnaam. In dit geval het Hallo-adres van uw aangepaste domein toohello eindpunt Blob-opslag voor uw opslagaccount wordt toegewezen.

Doorgaans kunt u uw domein-DNS-instellingen op uw domeinregistrar website beheren. Elke registrar heeft een methode vergelijkbaar maar enigszins verschillen van het opgeven van een CNAME-record, maar Hallo concept is hetzelfde Hallo. Sommige pakketten van de registratie basic domein bieden geen DNS-configuratie, dus u tooupgrade moet misschien uw registratiepakket domein voordat u kunt Hallo CNAME-record maken.

1. Navigeer tooyour storage-account in Hallo [Azure-portal](https://portal.azure.com).
1. Onder **BLOB-SERVICE** selecteren op Hallo menu blade **aangepaste domeinen** tooopen hello *aangepaste domeinen* blade.
1. Meld u op de website van tooyour domeinregistrar en ga toohello pagina voor het beheren van DNS. U vindt dit in een gedeelte zoals **Domeinnaam**, **DNS** of **Serverbeheernaam**.
1. Hallo sectie voor het beheren van CNAME-records vinden. U kunt toogo tooan geavanceerde instellingenpagina hebben en zoekt u naar Hallo woorden **CNAME**, **Alias**, of **subdomeinen**.
1. Maak een nieuwe CNAME-record en geef een alias voor een subdomein zoals **www** of **foto's**. Geef een host-naam, uw eindpunt Blob-service in de indeling Hallo **mystorageaccount.blob.core.windows.net** (waar *mystorageaccount* Hallo-naam van uw storage-account). Hallo host naam toouse wordt weergegeven in item #1 Hallo *aangepaste domeinen* blade in Hallo [Azure-portal](https://portal.azure.com).
1. In het tekstvak Hallo op Hallo *aangepaste domeinen* blade in Hallo [Azure-portal](https://portal.azure.com), Voer Hallo-naam van uw aangepaste domein, met inbegrip van Hallo subdomein. Als uw domein bijvoorbeeld **contoso.com** en je alias subdomein is **www**, voer **www.contoso.com**. Als een subdomein is **foto's**, voer **photos.contoso.com**. Hallo subdomein is *vereist*.
1. Selecteer **opslaan** op Hallo *aangepaste domeinen* blade tooregister uw aangepaste domein. Als het Hallo-registratie is gelukt, ziet u een portal melding uw storage-account is bijgewerkt.

Als uw nieuwe CNAME-record is doorgegeven via DNS is vastgesteld, kunnen uw gebruikers blob-gegevens met behulp van uw aangepaste domein bekijken, zolang ze Hallo geschikte machtigingen hebben.

## <a name="register-a-custom-domain-using-hello-asverify-subdomain"></a>Registreren van een aangepast domein met Hallo *asverify* subdomein
Gebruik deze procedure tooregister uw aangepaste domein als uw aangepaste domein wordt momenteel ondersteund door een toepassing met een SLA die dat vereist er geen uitvaltijd. Door het maken van een CNAME die vanaf `asverify.<subdomain>.<customdomain>` te`asverify.<storageaccount>.blob.core.windows.net`, kunt u uw domein met Azure vooraf registreren. Vervolgens kunt u een tweede CNAME die vanaf maken `<subdomain>.<customdomain>` te`<storageaccount>.blob.core.windows.net`, waarna de clientzijdebewaking verkeer tooyour aangepast domein gerichte tooyour blobeindpunt worden.

Hallo **asverify** subdomein is een speciale subdomein dat wordt herkend door Azure. Door voorafgaand `asverify` tooyour eigen subdomein, u toestaan Azure toorecognize uw aangepaste domein zonder Hallo DNS-record voor Hallo domein wijzigen. Wanneer u Hallo DNS-record voor Hallo domein wijzigt, worden toegewezen toohello blobeindpunt zonder uitvaltijd.

1. Navigeer tooyour storage-account in Hallo [Azure-portal](https://portal.azure.com).
1. Onder **BLOB-SERVICE** selecteren op Hallo menu blade **aangepaste domeinen** tooopen hello *aangepaste domeinen* blade.
1. Meld u aan de website van tooyour DNS-provider en ga toohello pagina voor het beheren van DNS. U vindt dit in een gedeelte zoals **Domeinnaam**, **DNS** of **Serverbeheernaam**.
1. Hallo sectie voor het beheren van CNAME-records vinden. U kunt toogo tooan geavanceerde instellingenpagina hebben en zoekt u naar Hallo woorden **CNAME**, **Alias**, of **subdomeinen**.
1. Maak een nieuwe CNAME-record en geef een alias voor een subdomein met Hallo *asverify* subdomein. Bijvoorbeeld: **asverify.www** of **asverify.photos**. Geef een host-naam, uw eindpunt Blob-service in de indeling Hallo **asverify.mystorageaccount.blob.core.windows.net** (waar **mystorageaccount** Hallo-naam van uw storage-account). Hallo host naam toouse wordt weergegeven in item #2 Hallo *aangepaste domeinen* blade in Hallo [Azure-portal](https://portal.azure.com).
1. In het tekstvak Hallo op Hallo *aangepaste domeinen* blade in Hallo [Azure-portal](https://portal.azure.com), Voer Hallo-naam van uw aangepaste domein, met inbegrip van Hallo subdomein. Neem geen *asverify*. Als uw domein bijvoorbeeld **contoso.com** en je alias subdomein is **www**, voer **www.contoso.com**. Als een subdomein is **foto's**, voer **photos.contoso.com**. Hallo subdomein is vereist.
1. Selecteer Hallo **indirecte CNAME-validatie gebruiken** selectievakje.
1. Selecteer **opslaan** op Hallo *aangepaste domeinen* blade tooregister uw aangepaste domein. Als het Hallo-registratie is gelukt, ziet u een portal melding uw storage-account is bijgewerkt. Op dit moment uw aangepaste domein is geverifieerd door Azure, maar verkeer tooyour domein is nog niet tooyour storage-account worden gerouteerd.
1. Retourneert de website van tooyour DNS-provider en een andere CNAME-record maken die uw eindpunt subdomein tooyour Blob-service wordt toegewezen. Geef bijvoorbeeld Hallo subdomein als **www** of **foto's** (zonder Hallo *asverify*), en de hostnaam als Hallo  **mystorageaccount.BLOB.Core.Windows.NET** (waarbij **mystorageaccount** Hallo-naam van uw storage-account). Hallo-registratie van uw aangepaste domein is met deze stap is voltooid.
1. Ten slotte kunt u Hallo CNAME-record die u hebt gemaakt met Hallo verwijderen **asverify** subdomein, zoals deze is alleen als een tussenliggende stap nodig.

Als uw nieuwe CNAME-record is doorgegeven via DNS is vastgesteld, kunnen uw gebruikers blob-gegevens met behulp van uw aangepaste domein bekijken, zolang ze Hallo geschikte machtigingen hebben.

## <a name="test-your-custom-domain"></a>Testen van uw aangepaste domein

tooconfirm die uw aangepaste domein is toegewezen inderdaad tooyour eindpunt voor Blob-service, maakt u een blob in een openbare container in uw opslagaccount. Gebruik vervolgens een URI in een webbrowser in Hallo indeling tooaccess Hallo blob te volgen:

`http://<subdomain.customdomain>/<mycontainer>/<myblob>`

Bijvoorbeeld, kunt u na URI tooaccess een webformulier in Hallo Hallo **myforms** container in Hallo **photos.contoso.com** aangepast subdomein:

`http://photos.contoso.com/myforms/applicationform.htm`

## <a name="deregister-a-custom-domain"></a>Een aangepast domein opgeheven

een aangepast domein voor uw eindpunt Blob-opslag tooderegister gebruik een van de Hallo procedures te volgen.

### <a name="azure-portal"></a>Azure Portal

De volgende Hallo in hello Azure portal tooremove Hallo aangepast domeininstelling uitvoeren:

1. Navigeer tooyour storage-account in Hallo [Azure-portal](https://portal.azure.com).
1. Onder **BLOB-SERVICE** selecteren op Hallo menu blade **aangepaste domeinen** tooopen hello *aangepaste domeinen* blade.
1. Schakel Hallo inhoud van Hallo-vak met uw aangepaste domeinnaam.
1. Selecteer Hallo **opslaan** knop.

Wanneer Hallo aangepaste domein is verwijderd, ziet u een portal melding uw storage-account is bijgewerkt.

### <a name="azure-cli-20"></a>Azure CLI 2.0

Gebruik Hallo [az storage account bijwerken](https://docs.microsoft.com/cli/azure/storage/account#update) CLI opdracht in en geef een lege tekenreeks (`""`) voor Hallo `--custom-domain` argument waarde tooremove de registratie van een aangepast domein.

* De opdrachtindeling van de:

  ```azurecli
  az storage account update \
      --name <storage-account-name> \
      --resource-group <resource-group-name> \
      --custom-domain ""
  ```

* Voorbeeld van de opdracht:

  ```azurecli
  az storage account update \
      --name mystorageaccount \
      --resource-group myresourcegroup \
      --custom-domain ""
  ```

### <a name="powershell"></a>PowerShell

Gebruik Hallo [Set AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) PowerShell-cmdlet en geef een lege tekenreeks (`""`) voor Hallo `-CustomDomainName` argument waarde tooremove de registratie van een aangepast domein.

* De opdrachtindeling van de:

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "<resource-group-name>" `
      -AccountName "<storage-account-name>" `
      -CustomDomainName ""
  ```

* Voorbeeld van de opdracht:

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "myresourcegroup" `
      -AccountName "mystorageaccount" `
      -CustomDomainName ""
  ```

## <a name="next-steps"></a>Volgende stappen
* [Toewijzen van een aangepast domein tooan Azure Content Delivery Network (CDN)-eindpunt](../../cdn/cdn-map-content-to-custom-domain.md)
* [Met behulp van hello Azure CDN tooaccess blobs via HTTPS met aangepaste domeinen](storage-https-custom-domain-cdn.md)
