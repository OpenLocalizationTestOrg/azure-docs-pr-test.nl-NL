---
title: aaaCreate een klassieke Azure-VM met MySQL | Microsoft Docs
description: Maken van een virtuele machine van Azure waarop Windows Server 2012 R2 en MySQL-database met het klassieke implementatiemodel Hallo Hallo.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 98fa06d2-9b92-4d05-ac16-3f8e9fd4feaa
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: cynthn
ms.openlocfilehash: 2c9564955c2bab197a8e494e939ce16c0b9bb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-created-with-hello-classic-deployment-model-running-windows-server-2016"></a>MySQL installeren op een virtuele machine gemaakt met het klassieke implementatiemodel Hallo met Windows Server 2016
[MySQL](https://www.mysql.com) is een populaire open-source, SQL-database. Deze zelfstudie leert u hoe tooinstall en Voer Hallo **community-versie van MySQL 5.7.18** als een MySQL-Server op een virtuele machine met **Windows Server 2016**. Uw ervaring mogelijk enigszins verschillen voor andere versies van MySQL of Windows Server.

Zie voor instructies over het installeren van MySQL op Linux: [hoe tooinstall MySQL in Azure](../../linux/mysql-install.md).

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

## <a name="create-a-virtual-machine-running-windows-server-2016"></a>Maak een virtuele machine met Windows Server 2016
Als u een virtuele machine met Windows Server 2016 nog geen hebt, kunt u dit [zelfstudie](./tutorial.md) toocreate Hallo virtuele machine.

## <a name="attach-a-data-disk"></a>Een gegevensschijf koppelen
Nadat Hallo virtuele machine is gemaakt, kunt u eventueel een gegevensschijf koppelen. Toevoegen van dat een gegevensschijf wordt aanbevolen voor productieworkloads en tooavoid bijna geen schijfruimte meer op Hallo OS-schijf (C:), waaronder Hallo-besturingssysteem.

Zie [hoe tooattach data tooa virtuele Windows-machine schijf](../attach-managed-disk-portal.md) en volg de instructies voor het koppelen van een lege schijf Hallo. Stel Hallo cache hostinstelling te**geen** of **alleen-lezen**.

## <a name="log-on-toohello-virtual-machine"></a>Meld u aan toohello virtuele machine
Vervolgens moet u [toohello virtuele machine aanmelden](./connect-logon.md) zodat u MySQL kunt installeren.

## <a name="install-and-run-mysql-community-server-on-hello-virtual-machine"></a>Installeren en uitvoeren van MySQL-Community-Server op Hallo virtuele machine
Volg deze stappen tooinstall, configureren en Hallo Community-versie van MySQL-Server wordt uitgevoerd:

> [!NOTE]
> Bij het downloaden van items die met Internet Explorer kunt u instellen Hallo IE **verbeterde beveiliging** tooOff, en Hallo downloaden proces vereenvoudigen. Vanuit het startmenu hello, hulpprogramma's of de Server Manager/lokale beheerserver Klik IE **verbeterde beveiliging** en stel Hallo configuratie tooOff).
>
>

1. Nadat u verbinding hebt met het toohello virtuele machine via Extern bureaublad, klikt u op **Internet Explorer** vanuit het startscherm Hallo.
2. Selecteer Hallo **extra** knop op Hallo rechterbovenhoek (Hallo cogged wheel pictogram) en klik vervolgens op **Internetopties**. Klik op Hallo **beveiliging** en klik op Hallo **vertrouwde websites** pictogram en klik vervolgens op Hallo **Sites** knop. Http://*.mysql.com toohello lijst met vertrouwde sites toevoegen. Klik op **sluiten**, en klik vervolgens op **OK**.
3. In Hallo adresbalk van Internet Explorer, typ https://dev.mysql.com/downloads/mysql/.
4. Gebruik Hallo MySQL site toolocate en download de nieuwste versie Hallo van MySQL-installatieprogramma voor Windows hello. Bij het kiezen van Hallo MySQL installatieprogramma Hallo-versie waarop Hallo voltooien bestandsset (bijvoorbeeld Hallo mysql-installatieprogramma-community-5.7.18.0.msi met een bestandsgrootte van 352.8 MB) en sla Hallo-installatieprogramma downloaden.
5. Wanneer het Hallo-installatieprogramma downloaden is voltooid, klikt u op **uitvoeren** toolaunch setup.
6. Op Hallo **License Agreement** pagina, Hallo licentieovereenkomst accepteren en klik op **volgende**.
7. Op Hallo **kiezen van een installatietype** pagina, klikt u op Hallo-installatietype dat u wilt en klik vervolgens op **volgende**. Hallo volgende stappen wordt ervan uitgegaan Hallo selectie Hallo **alleen Server** type installatie.
8. Als hello **vereisten controleren** pagina, klikt u op **Execute** toolet Hallo installatieprogramma ontbrekende onderdelen installeren. Volg de instructies die wordt weergegeven, zoals Hallo C++ Redistributable-runtime.
9. Op Hallo **installatie** pagina, klikt u op **Execute**. Wanneer de installatie is voltooid, klikt u op **volgende**.

10. Op Hallo **productconfiguratie** pagina, klikt u op **volgende**.

11. Op Hallo **Type en netwerken** pagina, geeft u de gewenste configuratie type en connectiviteit opties, waaronder Hallo TCP-poort indien nodig. Selecteer **geavanceerde opties weergeven**, en klik vervolgens op **volgende**.
    ![](./media/mysql-2008r2/MySQL_TypeNetworking.png)

12. Op Hallo **Accounts en rollen** pagina, Geef een sterk wachtwoord van de MySQL-hoofdmap. Aanvullende MySQL-gebruikersaccounts toevoegen, indien nodig, en klik vervolgens op **volgende**.

    ![](./media/mysql-2008r2/MySQL_AccountsRoles_Filled.png)
13. Op Hallo **Windows-Service** pagina en klik vervolgens op wijzigingen toohello standaardinstellingen opgeven voor het uitvoeren van Hallo MySQL-Server als een Windows-service naar behoefte **volgende**.

    ![](./media/mysql-2008r2/MySQL_WindowsService.png)
14. Hallo keuzes op Hallo **invoegtoepassingen en -extensies** pagina zijn optioneel. Klik op **volgende** toocontinue.
15. Op Hallo **geavanceerde opties** pagina, geef zo nodig wijzigingen toologging opties en klik vervolgens op **volgende**.

    ![](./media/mysql-2008r2/MySQL_AdvOptions.png)
16. Op Hallo **serverconfiguratie toepassen** pagina, klikt u op **Execute**. Wanneer het Hallo-configuratiestappen zijn voltooid, klikt u op **voltooien**.
17. Op Hallo **productconfiguratie** pagina, klikt u op **volgende**.
18. Op Hallo **Installation Complete** pagina, klikt u op **kopie logboek tooClipboard** als u wilt tooexamine later, en klik vervolgens op **voltooien**.
19. Typ vanuit het startscherm Hallo **mysql**, en klik vervolgens op **MySQL 5.7 Command-Line Client**.
20. Voer Hallo hoofdwachtwoord die u hebt opgegeven in stap 12 en krijgt u een prompt waar kunt u opdrachten tooconfigure MySQL uitgeven. Zie voor meer informatie Hallo van opdrachten en syntaxis [MySQL verwijzing handleidingen](https://dev.mysql.com/doc/refman/5.7/en/server-configuration.html).

    ![](./media/mysql-2008r2/MySQL_CommandPrompt.png)
21. U kunt ook configuratie standaardserverinstellingen, zoals Hallo base gegevensmappen en stations en configureren. Zie voor meer informatie [6.1.2 Server Configuration standaard](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html).

## <a name="configure-endpoints"></a>Eindpunten configureren

Hallo MySQL service toobe beschikbaar tooclient computers op Hallo Internet, moet u een eindpunt configureert voor Hallo TCP-poort en maakt u een Windows Firewall-regel. Hallo poort standaardwaarde op welke Hallo MySQL-Server-service voor clients van MySQL wordt geluisterd is 3306. U kunt een andere poort opgeven, zolang het Hallo-poort is consistent met de Hallo waarde die is opgegeven op Hallo **Type en netwerken** (stap 11 van de vorige procedure Hallo).

> [!NOTE]
> Voor gebruik in productieomgevingen, kunt u Hallo beveiligingsgebied van het service beschikbaar tooall computers maken Hallo MySQL-Server op Hallo Internet. U kunt definiëren Hallo set bron-IP-adressen die toouse Hallo-eindpunt met een lijst met ACL (Access Control) zijn toegestaan. Zie voor meer informatie [hoe tooSet Up eindpunten tooa virtuele Machine](setup-endpoints.md).
>
>

tooconfigure een eindpunt voor Hallo MySQL Server-service:

1. Klik in hello Azure-portal, op **virtuele Machines (klassiek)**Hallo-naam van uw MySQL virtuele machine op en klik vervolgens op **eindpunten**.
2. Klik in de opdrachtbalk Hallo **toevoegen**.
3. Op Hallo **eindpunt toevoegen** pagina, typt u een unieke naam voor **naam**.
4. Selecteer **TCP** als Hallo-protocol.
5. Typ het poortnummer hello, zoals **3306**, in beide **openbare poort** en **particuliere poort**, en klik vervolgens op **OK**.

## <a name="add-a-windows-firewall-rule-tooallow-mysql-traffic"></a>Toevoegen van een Windows Firewall-regel tooallow MySQL-verkeer
een Windows Firewall-regel waarmee verkeer van Hallo Internet, Voer Hallo-opdracht op de volgende MySQL tooadd een _opdrachtprompt van Windows PowerShell_ op Hallo MySQL server virtuele machine.

    New-NetFirewallRule -DisplayName "MySQL57" -Direction Inbound –Protocol TCP –LocalPort 3306 -Action Allow -Profile Public

## <a name="test-your-remote-connection"></a>Test de externe verbinding
tootest uw externe verbinding toohello virtuele machine van Azure actief Hallo MySQL-Server-service, moet u Hallo DNS-naam van de cloudservice Hallo Hallo VN met opgeven.

1. In hello Azure-portal, klikt u op **virtuele Machines (klassiek)**, klikt u op Hallo-naam van de virtuele machine van uw MySQL-server en klik vervolgens op **overzicht**.
2. Uit dashboard van de virtuele machine hello, houd er rekening mee Hallo **DNS-naam** waarde. Hier volgt een voorbeeld:

   ![](media/mysql-2008r2/MySQL_DNSName.png)
3. Uitvoeren van een lokale computer met MySQL of Hallo MySQL-client, Hallo opdracht toolog in als een gebruiker MySQL te volgen.

     MySQL -u <yourMysqlUsername> - p -h<yourDNSname>

   Bijvoorbeeld, met behulp van Hallo MySQL gebruikersnaam _dbadmin3_ en Hallo _testmysql.cloudapp.net_ DNS-naam voor de virtuele machine van hello, MySQL met behulp van de volgende opdracht Hallo kan worden gestart:

     MySQL -u dbadmin3 -p -h testmysql.cloudapp.net

## <a name="next-steps"></a>Volgende stappen
toolearn meer over het uitvoeren van MySQL, Zie Hallo [MySQL documentatie](http://dev.mysql.com/doc/).
