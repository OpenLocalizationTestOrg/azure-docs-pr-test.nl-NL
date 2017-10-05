---
title: Overzicht van Azure Cloud-Shell (Preview) | Microsoft Docs
description: Overzicht van de Azure-Cloud-Shell.
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 7165633cd354eeea2e3619f839338e6af1524e56
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a>Overzicht van Azure-Cloud-Shell (Preview)
Azure Cloud-Shell is een interactieve, browser toegankelijke shell voor het beheren van Azure-resources.

![](media/overview-pic.png)

## <a name="features"></a>Functies
### <a name="browser-based-shell-experience"></a>Browser gebaseerde shell-ervaring
Cloud-Shell kan toegang tot een browser gebaseerde opdrachtregelprogramma ervaring gebouwd met Azure beheertaken in gedachten. Hefboomwerking Cloud Shell voelt van een lokale computer werkt op een manier alleen de cloud kunnen bieden.

### <a name="pre-configured-azure-workstation"></a>Vooraf geconfigureerde Azure werkstation
Cloud-Shell is voorgeïnstalleerd met populaire opdrachtregelprogramma's en talen zodat u sneller kunt werken.

[De lijst volledige tooling voor Azure Cloud Shell hier weergeven.](features.md#tools)

### <a name="automatic-authentication"></a>Automatische verificatie
Cloud-Shell verifieert veilig automatisch op elke sessie voor directe toegang tot uw resources via de Azure CLI 2.0.

### <a name="connect-your-azure-file-storage"></a>Verbinding maken met uw Azure File storage
Cloud-Shell-machines zijn tijdelijk en als gevolg hiervan vereisen een Azure-bestandsshare te koppelen als `clouddrive` voor het persistent maken van uw directory $Home.
Op de eerste keer opstarten die cloud Shell wordt gevraagd om een resource te maken delen groep, storage-account en -bestand namens jou. Dit is een eenmalige stap en wordt automatisch voor alle sessies worden gekoppeld. 

#### <a name="create-new-storage"></a>Maken van nieuwe opslag
![](media/basic-storage.png)

Een lokaal redundant opslagaccount (LRS) kan namens jou worden gemaakt met een Azure-bestandsshare met de installatiekopie van een standaard 5 GB schijf. De bestandsshare koppelt als `clouddrive` delen interactie met de installatiekopie van de schijf die wordt gebruikt om te synchroniseren en uw directory $Home behouden voor het bestand. Reguliere opslagkosten van toepassing.

Drie bronnen worden namens jou gemaakt:
1. De resourcegroep met de naam:`cloud-shell-storage-<region>`
2. Opslagaccount met de naam:`cs<uniqueGuid>`
3. De bestandsshare met de naam:`cs-<user>-<domain>-com-uniqueGuid`

> [!Note]
> Alle bestanden in uw directory $Home zoals SSH-sleutels worden doorgevoerd in de schijfinstallatiekopie van uw gebruiker opgeslagen in de gekoppelde bestandsshare. Aanbevolen procedures van toepassing bij het opslaan van bestanden in uw directory $Home en gekoppelde bestandsshare.

#### <a name="use-existing-resources"></a>Bestaande bronnen gebruiken
![](media/advanced-storage.png)

Een geavanceerde optie is ook beschikbaar waarmee u kunt het koppelen van bestaande resources voor Cloud-Shell. Wanneer de opslag setup prompt krijgt, klikt u op 'Weergeven geavanceerde instellingen' om extra opties te selecteren. Opgegeven waarin DropDowns worden gefilterd voor uw toegewezen Cloud Shell regio en lokaal/globaal-redundant storage-accounts.

[Meer informatie over opslag voor Cloud-Shell, gedeelde bestanden bijwerken en het uploaden/downloaden van bestanden.] (het behouden blijven-shell-storage.md)

## <a name="concepts"></a>Concepten
* Cloud-Shell wordt uitgevoerd op een tijdelijke machine die is opgegeven op een per-sessie per gebruiker
* Time-out opgetreden voor de cloud Shell na 20 minuten zonder interactieve activiteit
* Cloud-Shell zijn alleen toegankelijk met een bestandsshare die is gekoppeld
* Cloud-Shell wordt één machine per gebruikersaccount toegewezen
* Machtigingen zijn ingesteld als een gewone Linux-gebruiker

[Meer informatie over alle functies van de Cloud-Shell.](features.md)

## <a name="examples"></a>Voorbeelden
* Maken of bewerken van scripts voor het automatiseren van Azure management
* Resources via Azure portal en Azure CLI 2.0 tegelijkertijd te beheren
* Azure CLI 2.0 Test-Drive

[Probeer deze voorbeelden op de Cloud Shell Quick Start.](quickstart.md)

## <a name="pricing"></a>Prijzen
De computer die als host fungeert voor Cloud-Shell is gratis, met een vereiste van een gekoppelde Azure-bestandsshare voor het persistent maken van uw directory $Home. Reguliere opslagkosten van toepassing.

## <a name="supported-browsers"></a>Ondersteunde browsers
Cloud-Shell wordt aanbevolen voor Chrome, rand en Safari. Cloud-Shell wordt ondersteund voor Chrome, Firefox Safari, Internet Explorer en Edge, is Cloud Shell onderworpen aan specifieke browserinstellingen.

## <a name="troubleshooting"></a>Problemen oplossen
1. Wanneer u een abonnement op Azure Active Directory gebruikt, kan ik niet maken opslag vanwege fout: 400 DisallowedOperation. Gebruik een Azure-abonnement te maken van de storage-resources op te lossen dit. Er zijn geen AD-abonnementen kunnen maken van Azure-resources.

Voor specifieke bekende beperkingen, gaat u naar [beperkingen van Cloud-Shell](limitations.md).
