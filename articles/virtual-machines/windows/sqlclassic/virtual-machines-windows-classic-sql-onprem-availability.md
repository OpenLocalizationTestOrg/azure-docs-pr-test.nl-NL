---
title: aaaExtend lokale altijd op beschikbaarheidsgroepen tooAzure | Microsoft Docs
description: Deze zelfstudie maakt gebruik van resources die zijn gemaakt met het klassieke implementatiemodel Hallo en beschrijft hoe toouse Hallo Replica toevoegen-wizard in SQL Server Management Studio (SSMS) tooadd de replica van een AlwaysOn-beschikbaarheidsgroep in Azure.
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 7ca7c423-8342-4175-a70b-d5101dfb7f23
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: 51fe117b40d69706b35f30101538a7a36116e128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="extend-on-premises-always-on-availability-groups-tooazure"></a>Lokale altijd op beschikbaarheidsgroepen tooAzure uitbreiden
Altijd op beschikbaarheidsgroepen bieden hoge beschikbaarheid voor groepen van database door secundaire replica's toe te voegen. Deze replica's staan failover wordt uitgevoerd de databases bij een fout. Daarnaast kunnen ze gebruikte toooffload werkbelastingen of back-uptaken lezen zijn.

U kunt lokale Availability Groups tooMicrosoft Azure uitbreiden door een of meer virtuele Azure-machines met SQL Server-inrichting en vervolgens toe te voegen als tooyour replica's op lokale Availability Groups.

Deze zelfstudie wordt ervan uitgegaan dat u de volgende Hallo hebt:

* Een actief Azure-abonnement. U kunt [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).
* Een bestaande altijd op beschikbaarheidsgroep on-premises bevinden. Zie voor meer informatie over beschikbaarheidsgroepen [altijd op beschikbaarheidsgroepen](https://msdn.microsoft.com/library/hh510230.aspx).
* Connectiviteit tussen Hallo on-premises netwerk en uw virtuele Azure-netwerk. Zie voor meer informatie over het maken van dit virtuele netwerk [Azure-portal (klassiek) maken een Site-naar-Site-verbinding gebruikt Hallo](../../../vpn-gateway/vpn-gateway-howto-site-to-site-classic-portal.md).

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

## <a name="add-azure-replica-wizard"></a>Wizard Azure Replica toevoegen
Deze sectie leest u hoe toouse hello **Azure Replica Wizard toevoegen** tooextend uw AlwaysOn-beschikbaarheidsgroep oplossing tooinclude Azure replica's.

> [!IMPORTANT]
> Hallo **Azure Replica Wizard toevoegen** biedt alleen ondersteuning voor virtuele machines die zijn gemaakt met de Hallo klassieke implementatiemodel. Nieuwe VM-implementaties moeten Hallo nieuwere Resource Manager-model gebruiken. Als u virtuele machines met Resource Manager, moet u handmatig Hallo secundaire Azure replica met behulp van Transact-SQL-commmands (hier niet weergegeven) toevoegen. Deze wizard werken niet in Hallo Resource Manager-scenario.

1. Uit binnen SQL Server Management Studio, vouw **altijd op hoge beschikbaarheid** > **beschikbaarheidsgroepen** > **[naam van de beschikbaarheidsgroep]**.
2. Met de rechtermuisknop op **Beschikbaarheidsreplica**, klikt u vervolgens op **Replica toevoegen**.
3. Standaard Hallo **Replica toevoegen tooAvailability Wizard groep** wordt weergegeven. Klik op **Volgende**.  Als u hebt geselecteerd Hallo **deze pagina niet meer weergeven** optie onderaan Hallo Hallo pagina tijdens het starten van een vorige van deze wizard, in dit scherm wordt niet weergegeven.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742861.png)
4. U zult vereist tooconnect tooall bestaande secundaire replica's. U kunt klikken op **verbinden...** naast elke replica of u kunt klikken op **verbinding maken met alle...** aan de onderkant van de Hallo van welkomstscherm. Nadat de verificatie, klikt u op **volgende** tooadvance toohello volgende scherm.
5. Op Hallo **replica's opgeven** pagina meerdere tabbladen worden weergegeven aan de bovenkant Hallo: **replica's**, **eindpunten**, **back-up voorkeuren**, en **Listener**. Van Hallo **replica's** tabblad **Azure Replica toevoegen...** toolaunch hello Azure Replica Wizard toevoegen.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742863.png)
6. Selecteer een bestaand Azure-Beheercertificaat in lokale Windows-certificaatarchief Hallo als u een voordat hebt geïnstalleerd. Selecteer of Voer Hallo-id van een Azure-abonnement als u een voordat hebt gebruikt. U kunt op toodownload downloaden en installeren van een Azure-Beheercertificaat en downloaden van Hallo lijst met abonnementen op basis van een Azure-account.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742864.png)
7. U kunt elk veld op de pagina Hallo met waarden die worden gebruikt toocreate hello Azure virtuele Machine (VM) die als host Hallo replica fungeert wordt gevuld.
   
   | Instelling | Beschrijving |
   | --- | --- |
   | **Afbeelding** |Hallo gewenst combinatie van het besturingssysteem en SQL Server selecteren |
   | **VM-grootte** |Selecteer Hallo grootte van virtuele machine die het beste past bij uw bedrijfsbehoeften |
   | **VM-naam** |Geef een unieke naam voor Hallo nieuwe virtuele machine. Hallo naam moet tussen 3 en 15 tekens bevatten, kunnen alleen letters, cijfers en afbreekstreepjes bevatten en moet beginnen met een letter en eindigen met een letter of een cijfer. |
   | **VM-gebruikersnaam** |Geef een gebruikersnaam die Hallo-beheerdersaccount op Hallo VM fungeren zal |
   | **Beheerderswachtwoord voor VM** |Geef een wachtwoord voor het nieuwe account Hallo |
   | **Wachtwoord bevestigen** |Bevestig het wachtwoord van de nieuwe account Hallo Hallo |
   | **Virtueel netwerk** |Geef hello Azure virtual network die Hallo nieuwe virtuele machine moet worden gebruikt. Zie voor meer informatie over virtuele netwerken [Virtual Network-overzicht](../../../virtual-network/virtual-networks-overview.md). |
   | **Virtueel netwerksubnet** |Geef Hallo virtueel netwerksubnet die Hallo die nieuwe virtuele machine moet gebruiken |
   | **Domein** |Controleer vooraf ingestelde waarde voor domein Hallo Hallo juist |
   | **Domein-gebruikersnaam** |Geef een account dat in de lokale beheerdersgroep op de lokale clusterknooppunten Hallo Hallo |
   | **Wachtwoord** |Hallo-wachtwoord voor Hallo domeingebruikersnaam opgeven |
8. Klik op **OK** toovalidate Hallo implementatie-instellingen.
9. Juridische voorwaarden worden vervolgens weergegeven. Lees en klik op **OK** als u akkoord toothese gaat voorwaarden.
10. Hallo **replica's opgeven** pagina opnieuw wordt weergegeven. Controleer de instellingen voor nieuwe hello Azure replica op Hallo Hallo **replica's**, **eindpunten**, en **back-up voorkeuren** tabbladen. Wijzig instellingen toomeet uw zakelijke vereisten.  Zie voor meer informatie over Hallo-parameters die zijn opgenomen op deze tabbladen [pagina opgeven voor replica's (nieuwe Wizard/Add Replica Wizard beschikbaarheidsgroep)](https://msdn.microsoft.com/library/hh213088.aspx). Houd er rekening mee dat listeners kunnen niet worden gemaakt met behulp van Hallo Listener tabblad voor beschikbaarheidsgroepen die Azure replica's bevatten. Bovendien, als al een listener voorafgaande toolaunching Hallo Wizard gemaakt is, ontvangt u een bericht weergegeven dat aangeeft dat deze niet wordt ondersteund in Azure. Laten we zien hoe u toocreate luisteraars in Hallo **maken van een beschikbaarheidsgroep-Listener** sectie.
    
     ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742865.png)
11. Klik op **Volgende**.
12. Hallo synchronisatiemethode gewenste toouse op Hallo selecteren **eerste gegevenssynchronisatie selecteren** pagina en klik op **volgende**. Selecteer voor de meeste scenario **volledige gegevenssynchronisatie**. Zie voor meer informatie over synchronisatiemethoden gegevens [Selecteer initiële synchronisatie gegevenspagina (altijd op beschikbaarheid van groep Wizards)](https://msdn.microsoft.com/library/hh231021.aspx).
13. Bekijkt hello resultaten op Hallo **validatie** pagina. Corrigeer de problemen en start opnieuw Hallo validatie indien nodig. Klik op **Volgende**.
    
     ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742866.png)
14. Controleer de instellingen Hallo op Hallo **samenvatting** pagina en klik vervolgens op **voltooien**.
15. Hallo inrichtingsproces begint. Wanneer het Hallo-wizard is voltooid, klikt u op **sluiten** tooexit buiten het Hallo-wizard.

> [!NOTE]
> Hallo toevoegen Azure Replica Wizard maakt een logbestand in Users\User Name\AppData\Local\SQL Server\AddReplicaWizard. Dit logboekbestand mag implementaties van Azure replica gebruikte tootroubleshoot is mislukt. Als Hallo Wizard uitvoering actie is mislukt, alle vorige bewerkingen worden teruggedraaid, met inbegrip van het verwijderen van Hallo VM ingericht.
> 
> 

## <a name="create-an-availability-group-listener"></a>Maken van een beschikbaarheidsgroep-listener
Nadat het Hallo-beschikbaarheidsgroep is gemaakt, moet u een listener voor clients tooconnect toohello replica's maken. Primaire tooeither Hallo binnenkomende verbindingen of een secundaire replica alleen-lezen-listeners doorgestuurd. Zie voor meer informatie over listeners [een ILB-listener voor AlwaysOn-beschikbaarheidsgroepen configureren in Azure](../classic/ps-sql-int-listener.md).

## <a name="next-steps"></a>Volgende stappen
In aanvulling toousing hello **Azure Replica Wizard toevoegen** tooextend uw tooAzure AlwaysOn-beschikbaarheidsgroep u mogelijk ook sommige SQL Server-werkbelastingen verplaatsen volledig tooAzure. tooget gestart, Zie [inrichten van een virtuele Machine van SQL Server op Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).

Voor andere onderwerpen die betrekking toorunning SQL-Server in Azure VM's hebben, Zie [SQL Server op Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

