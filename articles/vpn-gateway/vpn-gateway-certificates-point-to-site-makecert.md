---
title: 'Genereren en exporteren van certificaten voor punt-naar-Site: MakeCert: Azure | Microsoft Docs'
description: Dit artikel bevat stappen toocreate een zelfondertekend basiscertificaat, Hallo openbare sleutel niet exporteren en met MakeCert clientcertificaten te genereren.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 0b795ccf74f1f97fbd3de8a0dc339f9cb0b48183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-makecert"></a>Genereren en exporteren van certificaten voor punt-naar-Site-verbindingen met het MakeCert

Punt-naar-Site-verbindingen gebruiken certificaten tooauthenticate. In dit artikel leest u hoe toocreate een zelfondertekend basiscertificaat en clientcertificaten met MakeCert genereren. Als u configuratiestappen voor punt-naar-Site, zoekt zoals hoe tooupload basiscertificaten, selecteert u een van de Hallo ' configureren punt-naar-Site' artikelen van Hallo volgende lijst:

> [!div class="op_single_selector"]
> * [Zelfondertekende certificaten - PowerShell maken](vpn-gateway-certificates-point-to-site.md)
> * [Zelfondertekende certificaten - MakeCert maken](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Punt-naar-Site - Resource Manager - Azure-portal configureren](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [Punt-naar-Site - Resource Manager - PowerShell configureren](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Punt-naar-Site - Classic - Azure-portal configureren](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 

Terwijl het is raadzaam Hallo [Windows 10 PowerShell stappen](vpn-gateway-certificates-point-to-site.md) toocreate uw certificaten, bieden we deze instructies MakeCert als een optionele methode. Hallo-certificaten die u genereren met behulp van beide methoden kunnen worden geïnstalleerd op [een ondersteunde client-besturingssysteem](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq). MakeCert heeft echter Hallo beperking te volgen:

* MakeCert is afgeschaft. Dit betekent dat dit hulpprogramma op elk moment kan worden verwijderd. Certificaten die u al hebt gegenereerd met MakeCert worden niet beïnvloed wanneer MakeCert niet meer beschikbaar is. MakeCert is alleen gebruikte toogenerate Hallo certificaten niet als een mechanisme voor het valideren.

## <a name="rootcert"></a>Een zelfondertekend basiscertificaat maken

Hallo stappen ziet u hoe toocreate een zelfondertekend certificaat met MakeCert. Deze stappen zijn niet specifiek implementatiemodel. Ze zijn geldig voor zowel Resource Manager en classic.

1. Download en installeer [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx).
2. Na de installatie vindt u doorgaans Hallo makecert.exe hulpprogramma onder dit pad: ' C:\Program Files (x86) \Windows Kits\10\bin\<arch >'. Hoewel het is mogelijk dat het was geïnstalleerd tooanother locatie. Open een opdrachtprompt als beheerder en navigeren toohello locatie Hallo MakeCert-hulpprogramma. U kunt Hallo voorbeeld te volgen, aanpassen voor de juiste locatie hello gebruiken:

  ```cmd
  cd C:\Program Files (x86)\Windows Kits\10\bin\x64
  ```
3. Maken en een certificaat op Hallo persoonlijke certificaatarchief op uw computer installeren. Hallo volgende voorbeeld wordt een bijbehorende *.cer* bestand dat u uploadt tooAzure bij het configureren van P2S. Vervangen door 'P2SRootCert' en 'P2SRootCert.cer' hello naam wilt u toouse voor Hallo certificaat. Hallo certificaat bevindt zich in uw 'Certificaten - Huidige gebruiker\Persoonlijk\Certificaten'.

  ```cmd
  makecert -sky exchange -r -n "CN=P2SRootCert" -pe -a sha256 -len 2048 -ss My
  ```

## <a name="cer"></a>Hallo openbare sleutel (.cer) exporteren

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

Hallo exported.cer bestand moet geüploade tooAzure. Zie voor instructies [een punt-naar-Site-verbinding configureren](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile). Zie voor een vertrouwd basiscertificaat aanvullende tooadd [in deze sectie](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add) van Hallo artikel.

### <a name="export-hello-self-signed-certificate-and-private-key-toostore-it-optional"></a>Hallo zelf-ondertekend certificaat en de persoonlijke sleutel toostore exporteren deze (optioneel)

U kunt tooexport Hallo zelfondertekend basiscertificaat en veilig opslaan. Indien nodig zijn, u kunt later op een andere computer installeren en meer clientcertificaten te genereren of een andere cer-bestand exporteren. tooexport hello zelfondertekend basiscertificaat als een .pfx, selecteer Hallo-basiscertificaat en gebruik dezelfde stappen Hallo zoals beschreven in [exporteren van een clientcertificaat](#clientexport).

## <a name="create-and-install-client-certificates"></a>Maken en clientcertificaten te installeren

Installeer rechtstreeks op de clientcomputer Hallo niet Hallo zelf-ondertekend certificaat. U moet een clientcertificaat van een zelfondertekend certificaat Hallo toogenerate. U en vervolgens exporteren en Hallo client certificate toohello-clientcomputer installeren. Hallo stappen te volgen zijn geen specifieke implementatie-model. Ze zijn geldig voor zowel Resource Manager en classic.

### <a name="clientcert"></a>Een clientcertificaat genereren

Elke clientcomputer die verbinding tooa maakt VNet met punt-naar-Site moet beschikken over een clientcertificaat dat is geïnstalleerd. U een clientcertificaat genereren uit het zelfondertekende basiscertificaat hello, en vervolgens exporteren en installeren van Hallo clientcertificaat. Als het Hallo-clientcertificaat niet is geïnstalleerd, mislukt de verificatie. 

Hallo volgende stappen maakt u een clientcertificaat van een zelfondertekend basiscertificaat genereren. U kunt meerdere clientcertificaten genereren van Hallo hetzelfde basiscertificaat. Als u clientcertificaten gebruik Hallo stappen hieronder genereert, wordt Hallo clientcertificaat automatisch geïnstalleerd op Hallo-computer die u hebt toogenerate Hallo certificaat gebruikt. Als u een certificaat op een andere clientcomputer tooinstall wilt, kunt u Hallo certificaat exporteren.
 
1. Op Hallo dezelfde computer die u hebt gebruikt toocreate Hallo zelfondertekend certificaat, open een opdrachtprompt als beheerder.
2. Wijzigen en Voer Hallo voorbeeld toogenerate een clientcertificaat.
  * Wijziging *'P2SRootCert'* toohello-naam van Hallo zelfondertekend basiscertificaat die u het clientcertificaat Hallo van genereren. Controleer of gebruikt u de naam van de basiscertificaat hello, die elk Hallo Hallo "CN =' waarde is die u hebt opgegeven toen u Hallo zelfondertekende basiscertificaat hebt gemaakt.
  * Wijziging *P2SChildCert* toohello-naam die u wilt dat een client certificate toobe toogenerate.

  Als u Hallo voorbeeld te volgen zonder het te wijzigen uitvoert, is het Hallo resultaat een certificaat met de naam P2SChildcert in uw persoonlijke certificaatarchief die is gegenereerd op basis van het basiscertificaat P2SRootCert.

  ```cmd
  makecert.exe -n "CN=P2SChildCert" -pe -sky exchange -m 96 -ss My -in "P2SRootCert" -is my -a sha256
  ```

### <a name="clientexport"></a>Een clientcertificaat exporteren

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

### <a name="install"></a>Een geëxporteerde certificaat installeren

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>Volgende stappen

Ga door met de punt-naar-Site-configuratie. 

* Voor **Resource Manager** model implementatiestappen Zie [configureren van een punt-naar-Site-verbinding tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).
* Voor **klassieke** model implementatiestappen Zie [configureren van een punt-naar-Site VPN-verbinding tooa VNet (klassiek)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
