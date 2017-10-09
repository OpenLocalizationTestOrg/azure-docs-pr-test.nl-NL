---
title: Overzicht van Azure-infrastructuur aaaExample | Microsoft Docs
description: Meer informatie over Hallo belangrijke ontwerp- en implementatiestappen richtlijnen voor het implementeren van een voorbeeld van de infrastructuur in Azure.
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7032b586-e4e5-4954-952f-fdfc03fc1980
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd6b6e904404bea0b5be37dfce6d60039daae636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-windows-vms"></a>Voorbeeld van de Azure-infrastructuur overzicht voor het Windows-VM 's

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

In dit artikel wordt uitgelegd opzetten van een voorbeeld van de toepassing-infrastructuur. We beschreven ontwerpen van een infrastructuur voor een eenvoudige online winkel die alle Hallo richtlijnen en beslissingen rond naamconventies, beschikbaarheidssets, virtuele netwerken en taakverdelers samenbrengt en distribueren van uw virtuele machines (VM's).

## <a name="example-workload"></a>Voorbeeld van de werkbelasting
Adventure Works Cycles wil toobuild een online store-toepassing in Azure die bestaat uit:

* Twee IIS-servers met Hallo client front-end in een weblaag
* Twee IIS-servers verwerken van gegevens en bestellingen in de toepassingslaag van een
* Twee exemplaren van Microsoft SQL Server met AlwaysOn availability groups (twee SQL-Servers en een meerderheid knooppunt witness) voor het opslaan van productgegevens- en bestellingen in een databaselaag
* Twee Active Directory-domeincontrollers voor klantaccounts en leveranciers in een verificatie-laag
* Alle Hallo-servers bevinden zich in twee subnetten:
  * een front-end-subnet voor webservers Hallo 
  * een back-end-subnet voor toepassingsservers hello, SQL-cluster en domeincontrollers

![Diagram van verschillende lagen voor de infrastructuur van de toepassing](./media/infrastructure-example/example-tiers.png)

Binnenkomende beveiligde webverkeer moet Netwerktaakverdeling tussen Hallo webservers als klanten Hallo online winkel bladeren. Volgorde Hallo vorm van HTTP-verkeer verwerken van aanvragen van Hallo web servers moeten worden verdeeld tussen Hallo toepassingsservers. Bovendien moet Hallo-infrastructuur zijn ontworpen voor hoge beschikbaarheid.

Hallo resulterende ontwerp moet gebruikmaken van:

* Een Azure-abonnement en -account
* Één resourcegroep
* Azure Managed Disks
* Een virtueel netwerk met twee subnetten
* Beschikbaarheidssets voor Hallo virtuele machines met een vergelijkbare rol
* Virtuele machines

Alle bovenstaande Hallo voldoen aan deze naamgeving:

* Adventure Works Cycles gebruikt **[IT werkbelasting]-[locatie]-[Azure resource]** als voorvoegsel
  * Bijvoorbeeld, "**azos**' (Azure Online Store) is de naam van de IT-werkbelasting Hallo en '**gebruiken**' (VS-Oost 2) is Hallo locatie
* Virtuele netwerken maken gebruik van AZOS-gebruik-VN**[aantal]**
* Beschikbaarheidssets gebruiken azos-gebruiken-als-**[rol]**
* Namen van de virtuele machine gebruiken azos-gebruiken-vm -**[vmname]**

## <a name="azure-subscriptions-and-accounts"></a>Azure-abonnementen en accounts
Adventure Works Cycles maakt gebruik van de Enterprise-abonnement, met de naam Adventure Works Enterprise-abonnement, tooprovide facturering voor deze IT-werkbelasting.

## <a name="storage"></a>Storage
Adventure Works Cycles bepaald dat ze beheerd Azure-schijven moeten gebruiken. Bij het maken van virtuele machines worden beide beschikbare opslag opslaglagen gebruikt:

* **Standard-opslag** voor webservers hello, toepassingsservers, en domeincontrollers en hun gegevensschijven.
* **Premium-opslag** voor Hallo SQL Server-VM's en hun gegevensschijven.

## <a name="virtual-network-and-subnets"></a>Virtueel netwerk en subnetten
Omdat Hallo virtueel netwerk niet nodig heeft voor lopende connectiviteit toohello Adventure werk cycli on-premises netwerk, worden ze besloten op een virtueel netwerk alleen in de cloud.

Ze een virtueel netwerk alleen in de cloud gemaakt met de Hallo-instellingen met hello Azure-portal te volgen:

* Naam: AZOS gebruik VN01
* Locatie: VS-Oost 2
* Adresruimte virtuele netwerk: 10.0.0.0/8
* Eerste subnet:
  * Naam: FrontEnd
  * Adresruimte: 10.0.1.0/24
* Tweede subnet:
  * Naam: back-end
  * Adresruimte: 10.0.2.0/24

## <a name="availability-sets"></a>Beschikbaarheidssets
toomaintain hoge beschikbaarheid van alle vier lagen van de online winkel, Adventure Works Cycles genomen over de vier beschikbaarheidssets:

* **azos gebruik als web** voor webservers Hallo
* **azos gebruik als app** voor toepassingsservers Hallo
* **azos gebruiken als sql** voor Hallo SQL-Servers
* **azos gebruik als dc** voor Hallo-domeincontrollers

## <a name="virtual-machines"></a>Virtuele machines
Adventure Works Cycles besloten op Hallo namen voor hun virtuele Azure-machines te volgen:

* **azos, gebruik, vm, web01** voor de eerste webserver Hallo
* **azos, gebruik, vm, web02** voor de tweede webserver Hallo
* **azos, gebruik, vm, app01** voor de eerste toepassingsserver Hallo
* **azos, gebruik, vm, app02** voor de tweede toepassingsserver Hallo
* **azos, gebruik, vm, sql01** voor Hallo eerste SQL Server-server in het Hallo-cluster
* **azos, gebruik, vm, sql02** voor Hallo tweede SQL Server-server in het Hallo-cluster
* **azos, gebruik, vm, dc01** voor de eerste domeincontroller Hallo
* **azos, gebruik, vm, dc02** op Hallo tweede domeincontroller

Hier wordt de resulterende configuratie Hallo.

![Laatste infrastructuur geïmplementeerd in Azure](./media/infrastructure-example/example-config.png)

Deze configuratie omvat:

* Een virtueel netwerk met twee subnetten (FrontEnd en BackEnd) alleen in de cloud
* Azure-beheerde schijven met standaard- en Premium-schijven
* Vier beschikbaarheidssets, één voor elke laag van de online winkel Hallo
* Hallo virtuele machines voor Hallo vier lagen
* Een externe set met gelijke taakverdeling voor HTTPS-gebaseerde internetverkeer van Hallo Internet toohello webservers
* Een interne set voor niet-versleuteld webverkeer vanaf Hallo servers toohello Webtoepassingsservers met gelijke taakverdeling
* Één resourcegroep