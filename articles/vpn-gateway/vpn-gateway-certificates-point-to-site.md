---
title: 'Genereren en exporteren van certificaten voor punt-naar-Site: PowerShell: Azure | Microsoft Docs'
description: Dit artikel bevat stappen toocreate een zelfondertekend basiscertificaat, Hallo openbare sleutel niet exporteren en met PowerShell op Windows 10 clientcertificaten te genereren.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 11dda015368cda5ce9799fcc4f01d7c542b84fe8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a>Genereren en exporteren van certificaten voor punt-naar-Site-verbindingen op Windows 10 met behulp van PowerShell

Punt-naar-Site-verbindingen gebruiken certificaten tooauthenticate. In dit artikel leest u hoe toocreate een zelfondertekend basiscertificaat en genereren met behulp van PowerShell op Windows 10 clientcertificaten. Als u configuratiestappen voor punt-naar-Site, zoekt zoals hoe tooupload basiscertificaten, selecteert u een van de Hallo ' configureren punt-naar-Site' artikelen van Hallo volgende lijst:

> [!div class="op_single_selector"]
> * [Zelfondertekende certificaten - PowerShell maken](vpn-gateway-certificates-point-to-site.md)
> * [Zelfondertekende certificaten - MakeCert maken](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Punt-naar-Site - Resource Manager - Azure-portal configureren](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [Punt-naar-Site - Resource Manager - PowerShell configureren](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Punt-naar-Site - Classic - Azure-portal configureren](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


In dit artikel op een computer met Windows 10, moet u Hallo stappen uitvoeren. Hallo PowerShell-cmdlets is dat u toogenerate certificaten deel uitmaken van Hallo Windows 10-besturingssysteem en werken niet op andere versies van Windows. Hallo Windows 10-computer is alleen nodig toogenerate Hallo certificaten. Zodra het Hallo-certificaten worden gegenereerd, kunt u deze uploaden of installeren op een ondersteunde client-besturingssysteem. 

Als u geen toegang tot tooa Windows 10-computer, kunt u [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificaten. Hallo-certificaten die u genereren met behulp van beide methoden kunnen worden geïnstalleerd op een [ondersteund](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) clientbesturingssysteem.

## <a name="rootcert"></a>Een zelfondertekend basiscertificaat maken

Hallo nieuw SelfSignedCertificate cmdlet toocreate een zelfondertekend basiscertificaat gebruiken. Zie voor informatie over de extra parameters, [nieuw SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

1. Open vanaf een computer met Windows 10, Windows PowerShell-console met verhoogde bevoegdheden.
2. Gebruik hello voorbeeld toocreate Hallo zelfondertekende basiscertificaat te volgen. Hallo wordt volgende voorbeeld een zelfondertekend basiscertificaat met de naam 'P2SRootCert', die automatisch wordt geïnstalleerd in 'Certificaten-Huidige gebruiker\Persoonlijk\Certificaten'. U kunt Hallo certificaat weergeven door het openen van *certmgr.msc*, of *Gebruikerscertificaten beheren*.

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <a name="cer"></a>Hallo openbare sleutel (.cer) exporteren

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

Hallo exported.cer bestand moet geüploade tooAzure. Zie voor instructies [een punt-naar-Site-verbinding configureren](vpn-gateway-howto-point-to-site-rm-ps.md#upload). een vertrouwd basiscertificaat aanvullende tooadd [in deze sectie](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) van Hallo artikel.

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a>Het zelfondertekende basiscertificaat Hallo en openbare sleutel toostore exporteren deze (optioneel)

U kunt tooexport Hallo zelfondertekend basiscertificaat en veilig opslaan. Indien nodig zijn, u kunt later op een andere computer installeren en meer clientcertificaten te genereren of een andere cer-bestand exporteren. tooexport hello zelfondertekend basiscertificaat als een .pfx, selecteer Hallo-basiscertificaat en gebruik dezelfde stappen Hallo zoals beschreven in [exporteren van een clientcertificaat](#clientexport).

## <a name="clientcert"></a>Een clientcertificaat genereren

Elke clientcomputer die verbinding tooa maakt VNet met punt-naar-Site moet beschikken over een clientcertificaat dat is geïnstalleerd. U een clientcertificaat genereren uit het zelfondertekende basiscertificaat hello, en vervolgens exporteren en installeren van Hallo clientcertificaat. Als het Hallo-clientcertificaat niet is geïnstalleerd, mislukt de verificatie. 

Hallo volgende stappen maakt u een clientcertificaat van een zelfondertekend basiscertificaat genereren. U kunt meerdere clientcertificaten genereren van Hallo hetzelfde basiscertificaat. Als u clientcertificaten gebruik Hallo stappen hieronder genereert, wordt Hallo clientcertificaat automatisch geïnstalleerd op Hallo-computer die u hebt toogenerate Hallo certificaat gebruikt. Als u een certificaat op een andere clientcomputer tooinstall wilt, kunt u Hallo certificaat exporteren.

Hallo voorbeelden gebruikt Hallo nieuw SelfSignedCertificate cmdlet toogenerate een clientcertificaat dat na één jaar verloopt. Zie voor aanvullende parameterinformatie, zoals het instellen van een andere verlopen waarde voor het clientcertificaat Hallo [nieuw SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

### <a name="example-1"></a>Voorbeeld 1

In dit voorbeeld wordt de variabele '$cert' uit de vorige sectie Hallo gedeclareerd Hallo. Als u de PowerShell-console Hallo gesloten nadat het maken van zelfondertekende basiscertificaat Hallo of zijn extra client certificaten in een nieuwe sessie van de PowerShell-console, gebruiken Hallo stappen in [voorbeeld 2](#ex2).

Wijzigen en Voer Hallo voorbeeld toogenerate een clientcertificaat. Als u Hallo voorbeeld te volgen zonder het te wijzigen uitvoert, is het Hallo resultaat een certificaat met de naam 'P2SChildCert'.  Als u tooname Hallo onderliggende certificaat iets anders wilt, wijzigt u Hallo CN-waarde. Hallo TextExtension niet wijzigt wanneer u dit voorbeeld uitvoert. Hallo-clientcertificaat dat u genereren wordt automatisch geïnstalleerd in 'Certificaten - Huidige gebruiker\Persoonlijk\Certificaten' op uw computer.

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <a name="ex2"></a>Voorbeeld 2

Als u extra client certificaten maakt of worden niet met behulp van Hallo dezelfde PowerShell-sessie die u hebt gebruikt toocreate uw zelfondertekende basiscertificaat gebruik Hallo stappen te volgen:

1. Hallo zelfondertekende basiscertificaat dat is geïnstalleerd op de computer Hallo identificeren. Deze cmdlet retourneert een lijst met certificaten die zijn geïnstalleerd op uw computer.

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. Hallo-naam voor onderwerp van de geretourneerde lijst en klik vervolgens kopiëren Hallo vingerafdruk die is gevonden volgende tooit tooa tekst hello vinden bestand. In de Hallo voorbeeld te volgen, zijn er twee certificaten. Hallo CN-naam is Hallo-naam van zelfondertekende basiscertificaat Hallo van waaruit u wilt dat een certificaat van de onderliggende toogenerate. In dit geval 'P2SRootCert'.

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. Een variabele voor het basiscertificaat Hallo met vingerafdruk van de vorige stap Hallo Hallo declareren. Vervang de VINGERAFDRUK Hallo vingerafdruk van waaruit u wilt dat een certificaat van de onderliggende toogenerate Hallo-basiscertificaat.

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  Met de vingerafdruk van het Hallo voor P2SRootCert in de vorige stap hello, Hallo variabele ziet er bijvoorbeeld als volgt:

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  Wijzigen en Voer Hallo voorbeeld toogenerate een clientcertificaat. Als u Hallo voorbeeld te volgen zonder het te wijzigen uitvoert, is het Hallo resultaat een certificaat met de naam 'P2SChildCert'. Als u tooname Hallo onderliggende certificaat iets anders wilt, wijzigt u Hallo CN-waarde. Hallo TextExtension niet wijzigt wanneer u dit voorbeeld uitvoert. Hallo-clientcertificaat dat u genereren wordt automatisch geïnstalleerd in 'Certificaten - Huidige gebruiker\Persoonlijk\Certificaten' op uw computer.

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <a name="clientexport"></a>Een clientcertificaat exporteren   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <a name="install"></a>Een geëxporteerde certificaat installeren

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>Volgende stappen

Ga door met de punt-naar-Site-configuratie. 

* Voor **Resource Manager** model implementatiestappen Zie [configureren van een punt-naar-Site-verbinding tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md). 
* Voor **klassieke** model implementatiestappen Zie [configureren van een punt-naar-Site VPN-verbinding tooa VNet (klassiek)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
