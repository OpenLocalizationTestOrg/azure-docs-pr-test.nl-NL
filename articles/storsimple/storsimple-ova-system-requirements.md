---
title: systeemvereisten voor virtuele Azure StorSimple-matrix aaaMicrosoft | Microsoft Docs
description: Meer informatie over de netwerk- en softwarevereisten Hallo voor uw virtuele StorSimple-matrix
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: ea1d3bca-e71b-453d-aa82-440d2638f5e3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.openlocfilehash: 7a124873fdd806d409c7279851456e6347e7ec0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-system-requirements"></a>Systeemvereisten voor StorSimple virtuele array
## <a name="overview"></a>Overzicht
Dit artikel wordt beschreven Hallo belangrijk systeemvereisten voor uw Microsoft Azure StorSimple virtuele matrix en voor Hallo opslag clients toegang tot Hallo matrix. Het is raadzaam dat u Hallo informatie voordat u uw StorSimple-systeem te implementeren en vervolgens tooit zo nodig tijdens de implementatie en de volgende bewerking terugverwijzen zorgvuldig te controleren.

Hallo systeemvereisten zijn onder andere:

* **Softwarevereisten voor opslag clients** -beschrijft Hallo ondersteund virtualisatieplatforms, webbrowsers iSCSI-initiators, SMB-clients, minimale virtueel apparaatvereisten en eventuele bijkomende vereisten voor deze besturingssystemen.
* **Netwerkvereisten voor de StorSimple-apparaat Hallo** -informatie over poorten Hallo dat openen in uw firewall tooallow nodig toobe biedt voor iSCSI-, cloud- of management-verkeer.

systeemvereisten voor Hallo StorSimple informatie gepubliceerd in dit artikel is van toepassing tooStorSimple alleen virtuele matrices.

* 8000-serie, gaat te[systeemvereisten voor uw StorSimple 8000 series apparaat](storsimple-system-requirements.md).
* 7000-serie, gaat te[systeemvereisten voor uw StorSimple 5000 7000-serie apparaat](http://onlinehelp.storsimple.com/1_StorSimple_System_Requirements).

## <a name="software-requirements"></a>Softwarevereisten
Softwarevereisten Hallo Hallo informatie opnemen op Hallo ondersteunde webbrowsers, SMB-versies, virtualisatieplatforms en Hallo virtueel apparaat minimale vereisten.

### <a name="supported-virtualization-platforms"></a>Ondersteunde virtualisatieplatforms
| **Hypervisor** | **Versie** |
| --- | --- |
| Hyper-V |Windows Server 2008 R2 SP1 en hoger |
| VMware ESXi |5.5 en hoger |

### <a name="virtual-device-requirements"></a>Vereisten voor virtuele apparaten
| **Onderdeel** | **Vereiste** |
| --- | --- |
| Minimum aantal virtuele processors (kernen) |4 |
| Minimaal geheugen (RAM) |8 GB <br> Voor een bestandsserver, 8 GB voor minder dan 2 miljoen bestanden en 16 GB voor 2-4 miljoen bestanden|
| Schijfruimte<sup>1</sup> |Besturingssysteemschijf - 80 GB <br></br>Gegevensschijf - 500 GB too8 TB |
| Minimum aantal netwerkinterfaces |1 |
| Minimale bandbreedte met Internet<sup>2</sup> |5 Mbps |

<sup>1</sup> - thin ingericht

<sup>2</sup> -netwerkvereisten afhankelijk van de dagelijkse gegevenswijzigingssnelheid Hallo. Bijvoorbeeld, als een apparaat tooback van 10 GB of meer wijzigingen aanbrengen tijdens een dag moet, kan klikt u vervolgens hello dagelijkse back-up via een verbinding met 5 Mbps duren voordat too4.25 uur (als Hallo gegevens kan niet worden gecomprimeerd of ontdubbeld).

### <a name="supported-web-browsers"></a>Ondersteunde webbrowsers
| **Onderdeel** | **Versie** | **Aanvullende vereisten/opmerkingen** |
| --- | --- | --- |
| Microsoft Edge |meest recente versie | |
| Internet Explorer |meest recente versie |Getest met Internet Explorer 11 |
| Google Chrome |meest recente versie |Getest met Chrome 46 |

### <a name="supported-storage-clients"></a>Opslag van ondersteunde clients
Hallo volgens de softwarevereisten zijn voor Hallo iSCSI-initiators die toegang hebben tot uw virtuele StorSimple-matrix (geconfigureerd als een iSCSI-server).

| **Ondersteunde besturingssystemen** | **Vereiste versie** | **Aanvullende vereisten/opmerkingen** |
| --- | --- | --- |
| Windows Server |2008 R2 SP1, 2012 2012R2 |StorSimple kunt maken voor thin provisioning en volledig ingerichte volumes. Er kan geen gedeeltelijk ingerichte volumes maken. ISCSI-StorSimple-volumes worden alleen ondersteund voor: <ul><li>Eenvoudige volumes op standaardschijven van Windows.</li><li>Windows NTFS voor het formatteren van een volume.</li> |

Hallo volgens de softwarevereisten zijn voor Hallo SMB-clients die toegang krijgen uw virtuele StorSimple-matrix tot (geconfigureerd als een bestandsserver).

| **SMB-versie** |
| --- |
| SMB 2.x |
| SMB 3.0 |
| SMB 3.02 |

> [!IMPORTANT]
> Niet kopiëren of opslaan van bestanden die zijn beveiligd door Windows Encrypting File System (EFS) toohello virtuele StorSimple-matrix file server; Dit leidt tot een niet-ondersteunde configuratie. 
> 

### <a name="supported-storage-format"></a>Opslagindeling ondersteund
Alleen hello Azure blok-blob-opslag wordt ondersteund. Pagina-blobs worden niet ondersteund. Meer informatie [over blok-blobs en pagina-blobs](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs).

## <a name="networking-requirements"></a>Netwerkvereisten
Hallo bevat volgende tabel Hallo-poorten die toobe geopend in uw firewall tooallow voor iSCSI, SMB, cloud of beheer van verkeer moeten. In deze tabel *in* of *inkomende* verwijst toohello richting waaruit binnenkomende aanvragen van clients toegang uw apparaat tot. *Uitgaand* of *uitgaande* toohello richting waarin uw StorSimple-apparaat gegevens extern, afgezien van Hallo implementatie verzendt verwijst: bijvoorbeeld uitgaande toohello Internet.

| **Poort nr.<sup>1</sup>** | **In- of uitzoomen** | **Poort-bereik** | **Vereist** | **Opmerkingen bij de** |
| --- | --- | --- | --- | --- |
| TCP 80 (HTTP) |out |WAN |Nee |Uitgaande poort wordt gebruikt voor toegang tot tooretrieve updates van Internet. <br></br>Hallo uitgaande webproxy is gebruiker worden geconfigureerd. |
| TCP 443 (HTTPS) |out |WAN |Ja |Uitgaande poort wordt gebruikt voor toegang tot gegevens in de cloud Hallo. <br></br>Hallo uitgaande webproxy is gebruiker worden geconfigureerd. |
| UDP 53 (DNS) |out |WAN |In sommige gevallen; Zie de opmerkingen. |Deze poort is alleen vereist als u een Internet-gebaseerd DNS-server gebruikt. <br></br> Houd er rekening mee dat als een bestandsserver implementeert, wordt u aangeraden lokale DNS-server. |
| UDP 123 (NTP) |out |WAN |In sommige gevallen; Zie de opmerkingen. |Deze poort is alleen vereist als u een Internet-gebaseerd NTP-server gebruikt.<br></br> Houd er rekening mee dat als u een bestandsserver implementeert, raden wij aan tijd synchroniseren met uw Active Directory-domeincontrollers. |
| TCP 80 (HTTP) |in |LAN |Ja |Dit is de binnenkomende poort Hallo voor de lokale gebruikersinterface op Hallo StorSimple-apparaat voor lokaal beheer. <br></br> Houd er rekening mee dat openen Hallo lokale UI via HTTP worden automatisch omgeleid tooHTTPS. |
| TCP 443 (HTTPS) |in |LAN |Ja |Dit is de binnenkomende poort Hallo voor de lokale gebruikersinterface op Hallo StorSimple-apparaat voor lokaal beheer. |
| TCP-3260 (iSCSI) |in |LAN |Nee |Deze poort is gebruikte tooaccess gegevens via iSCSI. |

<sup>1</sup> geen poorten voor inkomend verkeer moeten toobe geopend op Hallo van openbare Internet.

> [!IMPORTANT]
> Zorg ervoor dat deze firewall Hallo niet wijzigen of ontsleutelen van een SSL-verkeer tussen Hallo StorSimple-apparaat en Azure.
> 
> 

### <a name="url-patterns-for-firewall-rules"></a>URL-patronen voor firewallregels
Netwerkbeheerders kunnen vaak geavanceerde firewall regels op basis van Hallo URL patronen toofilter Hallo inkomend en uitgaand verkeer Hallo configureren. Uw virtuele matrix en het Hallo-service Manager voor StorSimple-apparaat, is afhankelijk van andere Microsoft-toepassingen zoals Azure Service Bus, Azure Active Directory-toegangsbeheer, storage-accounts en Microsoft Update-servers. Hallo URL-patronen die zijn gekoppeld aan deze toepassingen kunnen worden gebruikt tooconfigure firewallregels. Het is belangrijk toounderstand die Hallo URL-patronen die zijn gekoppeld aan deze toepassingen kunnen wijzigen. Dit wordt op zijn beurt Hallo netwerk beheerder toomonitor vereisen en firewallregels bijwerken voor uw StorSimple als en indien nodig. 

Het is raadzaam dat u de firewallregels voor uitgaand verkeer, op basis van vaste IP-adressen, opneemt in de meeste gevallen StorSimple ingesteld. U kunt echter Hallo informatie onder tooset geavanceerde firewallregels die vereist toocreate beveiligde omgevingen zijn.

> [!NOTE]
> 
> * Hallo-apparaat (bron) IP-adressen moet altijd tooall Hallo ingeschakeld voor de cloud netwerkinterfaces worden ingesteld. 
> * Hallo bestemming IP-adressen te moet worden ingesteld[Azure datacenter IP-adresbereiken](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653).
> 
> 

| URL-patroon | Onderdeel/functionaliteit |
| --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*` |StorSimple-apparaat Manager-service<br>Access Control Service<br>Azure Service Bus |
| `http://*.backup.windowsazure.com` |Apparaatregistratie |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Intrekken van certificaten |
| `https://*.core.windows.net/*`<br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Azure storage-accounts en controle |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Microsoft Update-servers<br> |
| `http://*.deploy.akamaitechnologies.com` |CDN van Akamai |
| `https://*.partners.extranet.microsoft.com/*` |Ondersteuningspakket |
| `http://*.data.microsoft.com ` |Telemetrie-service in Windows hello Zie [update voor klantervaring en diagnostische telemetrie](https://support.microsoft.com/en-us/kb/3068708) |

## <a name="next-step"></a>Volgende stap
* [Hallo portal toodeploy uw virtuele StorSimple-matrix voorbereiden](storsimple-virtual-array-deploy1-portal-prep.md)

