---
title: de Services en management certificaten aaaCloud | Microsoft Docs
description: Meer informatie over hoe toocreate en het gebruik van certificaten met Microsoft Azure
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: fc70d00d-899b-4771-855f-44574dc4bfc6
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 69cb5467ece58a91dae06b4120954aeb2826bde1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="certificates-overview-for-azure-cloud-services"></a>Certificaten voor Azure Cloud Services-overzicht
Certificaten worden gebruikt in Azure voor cloudservices ([service certificaten](#what-are-service-certificates)) en voor de verificatie met Hallo management API ([beheercertificaten](#what-are-management-certificates) wanneer met behulp van Hallo klassieke Azure-portal en niet Hallo klassieke Azure-portal). In dit onderwerp biedt een algemeen overzicht van beide typen certificaten hoe te[maken](#create) en [implementeren](#deploy) ze tooAzure.

Certificaten worden gebruikt in Azure worden x.509 v3-certificaten en kunnen worden ondertekend door een andere vertrouwd certificaat of deze kunnen zelfondertekend zijn. Een zelfondertekend certificaat is ondertekend door de maker van een eigen, dus niet vertrouwd standaard. De meeste browsers kunnen dit probleem negeren. Gebruik alleen zelfondertekende certificaten bij het ontwikkelen en testen van uw cloudservices. 

Certificaten die door Azure kunnen een persoonlijke of een openbare sleutel bevatten. Certificaten hebben een vingerafdruk waarmee een tooidentify betekent dat ze in een niet-ambigue manier. Deze vingerafdruk wordt gebruikt in hello Azure [configuratiebestand](cloud-services-configure-ssl-certificate.md) tooidentify die een cloudservice van het certificaat moet worden gebruikt. 

## <a name="what-are-service-certificates"></a>Wat zijn servicecertificaten?
Service-certificaten zijn aangesloten toocloud services en veilige communicatie tooand van Hallo-service inschakelen. Als u een Webrol hebt geïmplementeerd, kunt u bijvoorbeeld toosupply een certificaat dat een blootgestelde HTTPS-eindpunt kan worden geverifieerd. Service-certificaten, gedefinieerd in de servicedefinitie van de zijn toohello automatisch geïmplementeerde virtuele machine die een exemplaar van uw rol wordt uitgevoerd. 

U kunt uploaden service certificaten tooAzure klassieke portal ofwel met behulp van Azure classic portal of met behulp van het klassieke implementatiemodel Hallo Hallo. Certificaten van de service zijn gekoppeld aan een specifieke cloud-service. Ze zijn tooa implementatie in het servicedefinitiebestand Hallo toegewezen.

Certificaten kunnen afzonderlijk worden beheerd vanaf uw services en kunnen worden beheerd door andere personen. Een ontwikkelaar kan bijvoorbeeld uploaden van een servicepakket dat tooa certificaat die een IT-beheerder eerder heeft geüpload tooAzure verwijst. Een IT-beheerder kan beheren en vernieuwen van dat certificaat (Hallo configuratie van Hallo service gewijzigd) zonder tooupload een nieuw servicepakket. Bijwerken zonder een nieuw servicepakket is mogelijk omdat de logische naam hello, Opslagnaam en locatie van Hallo-certificaat is in het servicedefinitiebestand Hallo en tijdens Hallo de vingerafdruk van certificaat is opgegeven in het serviceconfiguratiebestand Hallo. tooupdate Hallo-certificaat is alleen nodig tooupload een nieuw certificaat en de wijziging Hallo vingerafdruk in het configuratiebestand Hallo-service waarde.

>[!Note]
>Hallo [Cloud Services-Veelgestelde vragen over](cloud-services-faq.md) artikel bevat meer informatie over certificaten.

## <a name="what-are-management-certificates"></a>Wat zijn certificaten?
Van beheercertificaten kunnen u tooauthenticate met het klassieke implementatiemodel Hallo. Veel programma's en hulpprogramma's (zoals Visual Studio of hello Azure SDK) gebruiken deze certificaten tooautomate configuratie en implementatie van verschillende Azure-services. Deze zijn niet echt gerelateerde toocloud services. 

> [!WARNING]
> Wees voorzichtig! Deze typen certificaten dat alle gebruikers worden geverifieerd met hen toomanage Hallo abonnement ze zijn gekoppeld. 
> 
> 

### <a name="limitations"></a>Beperkingen
Er is een limiet van 100 beheercertificaten per abonnement. Er is ook een limiet van 100 beheercertificaten voor alle abonnementen onder een bepaalde service-beheerder gebruikers-ID. Als gebruikers-ID voor de accountbeheerder Hallo Hallo is al gebruikte tooadd 100-beheercertificaten en er een meer certificaten nodig is, kunt u een extra certificaten voor medebeheerder tooadd Hallo kunt toevoegen. 

Zie voordat u meer dan 100 certificaten toe te voegen, als u een bestaand certificaat kunt hergebruiken. Met behulp van CO-beheerders wordt mogelijk onnodige complexiteit tooyour certificaat beheerproces toegevoegd.

<a name="create"></a>
## <a name="create-a-new-self-signed-certificate"></a>Een nieuw zelfondertekend certificaat maken
U kunt elk hulpprogramma beschikbaar toocreate een zelfondertekend certificaat gebruiken mits ze toothese instellingen:

* Een X.509-certificaat.
* Een persoonlijke sleutel bevat.
* Voor sleuteluitwisseling (PFX-bestand) gemaakt.
* Naam van het onderwerp moet overeenkomen met de Hallo domein gebruikt tooaccess Hallo-cloudservice.

    > U kunt een SSL-certificaat voor Hallo cloudapp.net kan geen verkrijgen (of voor een Azure-gerelateerde)-domein. de onderwerpnaam van het Hallo-certificaat moet overeenkomen met Hallo aangepast domein naam die wordt gebruikt tooaccess uw toepassing. Bijvoorbeeld: **contoso.net**, niet **contoso.cloudapp.net**.

* Minimaal 2048-bits versleuteling.
* **Service-certificaat alleen**: Client-side-certificaat moet zich bevinden in Hallo *persoonlijke* certificaatarchief.

Er zijn twee manieren toocreate een certificaat op Windows Hello `makecert.exe` hulpprogramma of IIS.

### <a name="makecertexe"></a>MakeCert.exe
Dit hulpprogramma is afgeschaft en wordt niet meer hier beschreven. Zie voor meer informatie [deze MSDN-artikel](https://msdn.microsoft.com/library/windows/desktop/aa386968).

### <a name="powershell"></a>PowerShell
```powershell
$cert = New-SelfSignedCertificate -DnsName yourdomain.cloudapp.net -CertStoreLocation "cert:\LocalMachine\My"
$password = ConvertTo-SecureString -String "your-password" -Force -AsPlainText
Export-PfxCertificate -Cert $cert -FilePath ".\my-cert-file.pfx" -Password $password
```

> [!NOTE]
> Als u toouse Hallo certificaat met een IP-adres in plaats van een domein wilt, gebruikt u Hallo IP-adres in het Hallo - DnsName parameter.


Als u dat toouse wilt [certificaat met de beheerportal Hallo](../azure-api-management-certs.md), exporteren tooa **.cer** bestand:

```powershell
Export-Certificate -Type CERT -Cert $cert -FilePath .\my-cert-file.cer
```

### <a name="internet-information-services-iis"></a>Internet informatieservices (IIS)
Er zijn meerdere pagina's op Hallo internet die betrekking hebben op hoe toodo dit bij IIS. [Hier](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) is een uitstekende ik heb ik denk dat deze wordt ook uitgelegd. 

### <a name="java"></a>Java
U kunt ook Java gebruiken[maken van een certificaat](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate).

### <a name="linux"></a>Linux
[Dit](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artikel wordt beschreven hoe toocreate met SSH-certificaten.

## <a name="next-steps"></a>Volgende stappen
[Uploaden van uw service-certificaat toohello klassieke Azure-portal](cloud-services-configure-ssl-certificate.md) (of Hallo [Azure-portal](cloud-services-configure-ssl-certificate-portal.md)).

Upload een [beheercertificaat API](../azure-api-management-certs.md) toohello klassieke Azure-portal. Hello Azure-portal maakt geen gebruik van certificaten voor verificatie.

