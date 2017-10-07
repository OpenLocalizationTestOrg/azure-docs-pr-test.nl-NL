---
title: Overwegingen voor SQL Server in Azure aaaSecurity | Microsoft Docs
description: Dit onderwerp bevat algemene richtlijnen voor het beveiligen van SQL Server wordt uitgevoerd in een virtuele Machine van Azure.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: d710c296-e490-43e7-8ca9-8932586b71da
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/02/2017
ms.author: jroth
ms.openlocfilehash: 14c3d828fa87446da67beea6d28886de254afe15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-sql-server-in-azure-virtual-machines"></a>Veiligheidsoverwegingen voor SQL Server in Azure Virtual Machines

Dit onderwerp bevat algemene richtlijnen voor beveiliging die helpt bij het vaststellen van beveiligde toegang tooSQL Server-exemplaren in Azure een virtuele machine (VM).

Azure voldoet aan de verschillende regelgeving vanuit de sector en standaarden waarmee u kunnen een compatibele oplossing toobuild met SQL Server in een virtuele machine wordt uitgevoerd. Zie voor meer informatie over de naleving van regelgeving met Azure [Azure Vertrouwenscentrum](https://azure.microsoft.com/support/trust-center/).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="control-access-toohello-sql-vm"></a>Beheer toegang toohello SQL VM

Wanneer u uw virtuele machine van SQL Server maakt, kunt u overwegen hoe toocarefully bepalen wie toegang toohello machine en tooSQL Server. In het algemeen moet u doen Hallo volgende:

- Beperken van toegang tooSQL tooonly Hallo servertoepassingen en clients die u nodig hebt.
- Volg de aanbevolen procedures voor het beheren van gebruikersaccounts en wachtwoorden.

Hallo volgende secties bieden suggesties over denken via deze punten.

## <a name="secure-connections"></a>Beveiligde verbindingen

Wanneer u een virtuele machine van SQL Server met een afbeelding maakt, Hallo **SQL Server-verbindingen** optie geeft u de keuze van Hallo **lokale (binnen VM)**, **privé (binnen virtueel netwerk)** , of **openbaar (Internet)**.

![SQL Server-verbinding](./media/virtual-machines-windows-sql-security/sql-vm-connectivity-option.png)

Voor de beste beveiliging Hallo optie Hallo meest beperkende voor uw scenario. Bijvoorbeeld, als u een toepassing die toegang heeft tot SQL Server op Hallo dezelfde VM vervolgens **lokale** is de veiligste optie Hallo. Als u werkt met een Azure-toepassing waarvoor toegang toohello SQL Server vervolgens **persoonlijke** communicatie tooSQL Server alleen binnen de opgegeven Hallo beveiligt [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md). Als u nodig hebt **openbare** (internest) toegang toohello SQL Server VM vervolgens Zorg ervoor dat toofollow andere aanbevolen procedures in dit onderwerp tooreduce uw oppervlak aanval.

Hallo geselecteerde opties in de portal hello gebruiken inkomende beveiligingsregels op Hallo VMs [Netwerkbeveiligingsgroep](../../../virtual-network/virtual-networks-nsg.md) tooallow (NSG) of weigeren netwerkverkeer tooyour virtuele machine. U kunt wijzigen of nieuwe inkomende NSG-regels maken tooallow verkeer toohello SQL Server-poort (standaard 1433). U kunt ook bepaalde IP-adressen die toocommunicate via deze poort mogen opgeven.

![Netwerkbeveiligingsgroepen](./media/virtual-machines-windows-sql-security/sql-vm-network-security-group-rules.png)

Bovendien tooNSG toorestrict netwerkverkeer regels, kunt u ook Hallo Windows Firewall op Hallo virtuele machine.

Als u van eindpunten met het klassieke implementatiemodel hello gebruikmaakt, verwijdert u geen eindpunten op Hallo virtuele machine als u deze niet gebruikt. Zie voor instructies over het gebruik van ACL's met eindpunten [beheren Hallo ACL op een eindpunt](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint). Dit is niet nodig is voor virtuele machines die gebruikmaken van Hallo Resource Manager.

Ten slotte kunt u de versleutelde verbindingen voor Hallo exemplaar van SQL Server Database Engine Hallo uw virtuele machine van Azure inschakelen. Configureer SQL server-exemplaar met een ondertekend certificaat. Zie voor meer informatie [versleutelde verbindingen inschakelen toohello Database-Engine](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine) en [syntaxis verbindingsreeks](https://msdn.microsoft.com/library/ms254500.aspx).

## <a name="use-a-non-default-port"></a>Gebruik van een niet-standaard poort

Standaard luistert SQL Server op een bekende poort 1433. Voor een betere beveiliging toolisten van SQL Server op een niet-standaard-poort, zoals 1401 te configureren. Als u een installatiekopie van SQL Server-galerie in hello Azure-portal inricht, kunt u deze poort in Hallo **SQL Server-instellingen** blade.

tooconfigure deze na het inrichten, hebt u twee opties:

- Voor virtuele machines van Resource Manager, kunt u **SQL Server-configuratiebestand** van Hallo VM overzichtsblade. Dit biedt een optie toochange Hallo poort.

  ![TCP-poort wijzigen in portal](./media/virtual-machines-windows-sql-security/sql-vm-change-tcp-port.png)

- Voor klassieke virtuele machines of SQL Server-VM's die niet zijn ingericht met Hallo-portal, kunt u handmatig Hallo poort configureren door verbinding te maken op afstand toohello VM. Zie voor de configuratiestappen hello, [een tooListen Server configureren op een specifieke TCP-poort](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port). Als u deze handmatig techniek gebruikt, moet u ook een Windows Firewall regel tooallow binnenkomend verkeer op TCP-poort tooadd.

> [!IMPORTANT]
> Het opgeven van een niet-standaardpoort is een goed idee als uw SQL Server-poort openen toopublic internet-verbindingen.

Wanneer SQL Server naar een niet-standaardpoort luistert, moet u poort Hallo opgeven wanneer u verbinding maakt. Neem bijvoorbeeld een scenario waarbij Hallo server IP-adres 13.55.255.255 en SQL Server luistert op poort 1401. tooconnect tooSQL Server, geeft u `13.55.255.255,1401` in Hallo-verbindingsreeks.

## <a name="manage-accounts"></a>Accounts beheren

U wilt niet dat aanvallers tooeasily schatting accountnamen of wachtwoorden. Gebruik Hallo toohelp tips te volgen:

- Maak een unieke lokale administrator-account met heeft geen naam **beheerder**.

- Complexe sterke wachtwoorden gebruiken voor alle accounts. Voor meer informatie over het toocreate een sterk wachtwoord, Zie [maken van een sterk wachtwoord](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password) artikel.

- Azure selecteert standaard Windows-verificatie tijdens de installatie van de virtuele Machine van SQL Server. Daarom Hallo **SA** aanmelding is uitgeschakeld en een wachtwoord is toegewezen door setup. We raden aan dat Hallo **SA** aanmelding moet niet worden gebruikt of ingeschakeld. Als u een SQL-aanmelding hebben moet, een van volgende strategieën hello gebruiken:

  - Een SQL-account maken met een unieke naam met **sysadmin** lidmaatschap. U kunt dit doen via de portal Hallo doordat **SQL-verificatie** tijdens het inrichten.

    > [!TIP] 
    > Als u SQL-verificatie niet tijdens het inrichten inschakelt, moet u handmatig wijzigen Hallo verificatiemodus te**SQL Server en Windows-verificatiemodus**. Zie voor meer informatie [wijziging Server-verificatiemodus](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode).

  - Als u Hallo gebruiken moet **SA** aanmelding, enable Hallo aanmelding na inrichting en het toewijzen van een sterk wachtwoord.

## <a name="follow-on-premises-best-practices"></a>Volg de aanbevolen procedures voor lokale

Bovendien toohello procedures wordt beschreven in dit onderwerp wordt aangeraden dat u bekijken en Hallo traditionele on-premises beveiligingsprocedures implementeren, indien van toepassing. Zie voor meer informatie [beveiligingsoverwegingen voor een SQL Server-installatie](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)

## <a name="next-steps"></a>Volgende stappen

Als u ook geïnteresseerd in aanbevolen procedures om de prestaties, Zie [Best Practices prestaties for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).

Voor andere onderwerpen die betrekking toorunning SQL-Server in Azure VM's hebben, Zie [SQL Server op Azure Virtual Machines-overzicht](virtual-machines-windows-sql-server-iaas-overview.md).

