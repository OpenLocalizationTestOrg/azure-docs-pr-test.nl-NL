---
title: aaaConfigure AlwaysOn-beschikbaarheidsgroep in Azure Virtual Machines (klassiek) | Microsoft Docs
description: Maken van een AlwaysOn-beschikbaarheidsgroep met Azure Virtual Machines. Deze zelfstudie wordt voornamelijk Hallo-gebruikersinterface en hulpprogramma's in plaats van scripts.
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 8d48a3d2-79f8-4ab0-9327-2f30ee0b2ff1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: f428ad994a55378c281c959f4696fdcaf50632b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-virtual-machines-classic"></a>AlwaysOn-beschikbaarheidsgroep configureren in Azure Virtual Machines (klassiek)
> [!div class="op_single_selector"]
> * [Klassieke: UI](../classic/portal-sql-alwayson-availability-groups.md)
> * [Klassieke: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

Voordat u begint, kunt u overwegen of u kunt deze taak in Azure Resource Manager-model voltooien. U wordt aangeraden Azure Resource Manager-model voor nieuwe implementaties. Zie [op virtuele machines in Azure SQL Server altijd op beschikbaarheidsgroepen](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

> [!IMPORTANT] 
> Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Azure heeft twee verschillende implementatie modellen toocreate en werken met resources: [Resource Manager en classic](../../../azure-resource-manager/resource-manager-deployment-model.md). Dit artikel wordt uitgelegd hoe toouse Hallo klassieke implementatiemodel. 

toocomplete deze taak met hello Azure Resource Manager-model, Zie [op virtuele machines in Azure SQL Server altijd op beschikbaarheidsgroepen](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

Deze end-to-end zelfstudie ziet u hoe tooimplement-beschikbaarheidsgroepen met behulp van SQL Server Always On uitgevoerd op Azure Virtual Machines.

Uw oplossing SQL Server Always On in Azure wordt aan het einde van de Hallo Hallo zelfstudie bestaan uit Hallo volgende elementen:

* Een virtueel netwerk dat meerdere subnetten bevat en een front-end- en een back-end-subnet
* Een domeincontroller met een Active Directory (Azure AD)-domein
* Twee virtuele machines waarop SQL Server wordt uitgevoerd en zijn geïmplementeerde toohello back-end-subnet en gekoppelde toohello Azure AD-domein
* Een drie-knooppunt van een failovercluster met Hallo Knooppuntmeerderheid quorummodel
* Een beschikbaarheidsgroep met twee synchrone doorvoer replica's van een beschikbaarheidsdatabase

Hallo volgende afbeelding is een grafische voorstelling van Hallo-oplossing.

![Testlab-architectuur voor beschikbaarheidsgroepen in Azure](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC791912.png)

Houd er rekening mee dat dit een mogelijke configuratie is. Bijvoorbeeld, kunt u het aantal virtuele machines voor een beschikbaarheidsgroep van twee replica Hallo minimaliseren. Deze configuratie wordt opgeslagen op rekenuren in Azure met behulp van de domeincontroller Hallo als Hallo bestandssharewitness van quorum in een cluster met twee knooppunten. Deze methode beperkt het aantal virtuele machine Hallo door een van de configuratie Hallo geïllustreerd.

Deze zelfstudie wordt ervan uitgegaan dat de volgende Hallo:

* U hebt al een Azure-account.
* Weet u al hoe toouse Hallo GUI in Hallo virtuele machine galerie tooprovision een klassieke virtuele machine waarop SQL Server wordt uitgevoerd.
* U hebt al een goed begrip van AlwaysOn-beschikbaarheidsgroepen. Zie voor meer informatie [altijd op beschikbaarheidsgroepen (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).

> [!NOTE]
> Als u geïnteresseerd bent in het gebruik van AlwaysOn-beschikbaarheidsgroepen met SharePoint, zien ook de [configureren SQL Server 2012 Always On Availability Groups voor SharePoint 2013](https://technet.microsoft.com/library/jj715261.aspx).
> 
> 

## <a name="create-hello-virtual-network-and-domain-controller-server"></a>Hallo virtueel netwerk en domeincontrollerserver maken
U begint met een nieuwe Azure proefaccount. Nadat u uw account hebt ingesteld, moet u een van de startscherm Hallo Hallo klassieke Azure-portal.

1. Klik op Hallo **nieuw** op Hallo linkerhoek van Hallo onder aan Hallo pagina, zoals wordt weergegeven in de volgende schermafbeelding Hallo knop.
   
    ![Klik op Nieuw in Hallo-portal](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665511.gif)
2. Klik op **netwerkservices** > **virtueel netwerk** > **aangepast maken**, zoals weergegeven in de volgende schermafbeelding Hallo.
   
    ![Virtueel netwerk maken](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665512.gif)
3. In Hallo **VIRTUEEL netwerk maken** dialoogvenster vak, maakt u een nieuw virtueel netwerk door te doorlopen Hallo pagina's en instellingen Hallo Hallo volgende tabel. 
   
   | Pagina | Instellingen |
   | --- | --- |
   | Details van virtueel netwerk |**NAAM ContosoNET =**<br/>**De regio VS-West =** |
   | DNS-Servers en VPN-verbinding |Geen |
   | Adresruimten voor virtueel netwerk |Instellingen worden weergegeven in de volgende schermafbeelding Hallo: ![Virtueel netwerk maken](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784620.png) |
4. Maak Hallo virtuele machine die u als Hallo-domeincontroller (DC gebruiken wilt). Klik op **nieuw** > **Compute** > **virtuele Machine** > **uit galerie**, zoals weergegeven in Hallo volgende schermopname.
   
    ![Een virtuele machine maken](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784621.png)
5. In Hallo **een virtuele MACHINE maken** dialoogvenster een nieuwe virtuele machine configureren door te doorlopen Hallo pagina's en instellingen Hallo Hallo volgende tabel. 
   
   | Pagina | Instellingen |
   | --- | --- |
   | Selecteer het besturingssysteem van de virtuele machine Hallo |Windows Server 2012 R2 Datacenter |
   | Configuratie van virtuele machine |**VERSIE RELEASEDATUM** = (laatste)<br/>**NAAM van virtuele MACHINE** ContosoDC =<br/>**LAAG** = STANDARD<br/>**De grootte van** = A2 (2 kernen)<br/>**NIEUWE gebruikersnaam** AzureAdmin =<br/>**Nieuw wachtwoord** = Contoso! 000<br/>**Bevestig** = Contoso! 000 |
   | Configuratie van virtuele machine |**CLOUDSERVICE** = Maak een nieuwe cloudservice<br/>**DNS-naam van CLOUDSERVICE** = de naam van een unieke cloudservice<br/>**DNS-naam** een unieke naam = (ex: ContosoDC123)<br/>**REGIO/AFFINITEITSGROEP/VIRTUEEL netwerk** ContosoNET =<br/>**VIRTUEEL NETWERKSUBNETTEN** Back(10.10.2.0/24) =<br/>**STORAGE-ACCOUNT** = gebruik een automatisch gegenereerde storage-account<br/>**BESCHIKBAARHEIDSSET** = (geen) |
   | Opties voor de virtuele machine |Standaardinstellingen gebruiken |

Nadat u de nieuwe virtuele machine Hallo configureert, wacht u totdat Hallo virtuele machine toobe provsioned. Dit proces neemt enige tijd toofinish. Als u klikt op Hallo **virtuele Machine** tabblad in Hallo klassieke Azure portal, ziet u ContosoDC waarbij statussen van **starten (inrichten)** te**gestopt**, **Starten**, **uitgevoerd (inrichten)**, en tot slot **met**.

Hallo DC-server is nu is ingericht. Vervolgens configureert u Hallo Active Directory-domein op deze DC-server.

## <a name="configure-hello-domain-controller"></a>Hallo-domeincontroller configureren
Hallo stappen te volgen, configureert u Hallo ContosoDC machine als een domeincontroller voor corp.contoso.com.

1. Selecteer in de portal Hallo Hallo **ContosoDC** machine. Op Hallo **Dashboard** tabblad **Connect** tooopen een extern bureaublad (RDP)-bestand voor toegang tot extern bureaublad.
   
    ![Verbinding maken met tooVritual Machine](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784622.png)
2. Meld u aan met uw geconfigureerde beheerdersaccount (**\AzureAdmin**) en het wachtwoord (**Contoso! 000**).
3. Standaard Hallo **Serverbeheer** dashboard moet worden weergegeven.
4. Klik op Hallo **functies en onderdelen toevoegen** koppeling op Hallo-dashboard.
   
    ![Server Explorer functies toevoegen](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784623.png)
5. Klik op **volgende** totdat u toohello **serverfuncties** sectie.
6. Selecteer Hallo **Active Directory Domain Services** en **DNS-Server** rollen. Wanneer u wordt gevraagd, meer onderdelen toevoegen die deze rollen is vereist.
   
   > [!NOTE]
   > U ontvangt een waarschuwing dat er geen statische IP-adres is validatie. Als u Hallo configuratie testen wilt, klikt u op **doorgaan**. Voor productiescenario's [PowerShell tooset Hallo statische IP-adres van Hallo domain controller machine](../../../virtual-network/virtual-networks-reserved-private-ip.md).
   > 
   > 
   
    ![Dialoogvenster rollen toevoegen](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784624.png)
7. Klik op **volgende** totdat u Hallo **bevestiging** sectie. Selecteer Hallo **Hallo doelserver opnieuw opstarten automatisch indien nodig** selectievakje.
8. Klik op **Install**.
9. Nadat het Hallo-functies zijn geïnstalleerd, keert u terug toohello **Serverbeheer** dashboard.
10. Selecteer nieuwe Hallo **AD DS** optie in het linkerdeelvenster Hallo.
11. Klik op Hallo **meer** koppeling op de gele Hallo waarschuwing balk.
    
     ![Dialoogvenster van AD DS op virtuele machine van DNS-server](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784625.png)
12. In Hallo **actie** kolom Hallo **alle Server-taakdetails** in het dialoogvenster, klikt u op **deze server tooa-domeincontroller promoveert**.
13. In Hallo **Wizard Active Directory Domain Services configureren**, Hallo volgende waarden gebruiken:
    
    | Pagina | Instelling |
    | --- | --- |
    | Implementatieconfiguratie |**Een nieuw forest toevoegen** geselecteerde =<br/>**Naam van hoofddomein** corp.contoso.com = |
    | Opties voor domeincontroller |**Wachtwoord** = Contoso! 000<br/>**Bevestig het wachtwoord** = Contoso! 000 |
14. Klik op **volgende** toogo via andere pagina's in de wizard Hallo Hallo. Op Hallo **controle van vereisten** pagina, controleert u of er Hallo volgende bericht: **alle controles op vereisten zijn geslaagd**. Houd er rekening mee dat u wordt aangeraden alle toepasselijke waarschuwingsberichten, maar het is mogelijk toocontinue Hallo-installatie.
15. Klik op **Install**. Hallo **ContosoDC** virtuele machine wordt automatisch opnieuw opgestart.

## <a name="configure-domain-accounts"></a>Domeinaccounts configureren
de volgende stappen Hallo configureren Hallo Active Directory-accounts voor later gebruik.

1. Meld u weer aan toohello **ContosoDC** machine.
2. In **Serverbeheer**, klikt u op **extra** > **Active Directory Administrative Center**.
   
    ![Active Directory-beheercentrum](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784626.png)
3. In Hallo **Active Directory Administrative Center**, selecteer **corp (lokaal)** in het linkerdeelvenster Hallo.
4. Op de juiste Hallo **taken** deelvenster, klikt u op **nieuw** > **gebruiker**. Gebruik Hallo volgende instellingen:
   
   | Instelling | Waarde |
   | --- | --- |
   | **Voornaam** |Installeren |
   | **SamAccountName van gebruiker** |Installeren |
   | **Wachtwoord** |Contoso! 000 |
   | **Wachtwoord bevestigen** |Contoso! 000 |
   | **Andere opties voor wachtwoord** |Geselecteerd |
   | **Wachtwoord verloopt nooit** |Geselecteerd |
5. Klik op **OK** toocreate hello **installeren** gebruiker. Deze account wordt gebruikt tooconfigure Hallo failover-cluster en Hallo beschikbaarheidsgroep zijn.
6. Maak twee extra gebruikers, **CORP\SQLSvc1** en **CORP\SQLSvc2**, hello dezelfde stappen. Deze accounts wordt gebruikt voor Hallo SQL Server-exemplaren. Vervolgens moet u toogive **CORP\Install** Hallo noodzakelijke machtigingen tooconfigure Windows Failoverclustering.
7. In Hallo **Active Directory Administrative Center**, klikt u op **corp (lokaal)** in het linkerdeelvenster Hallo. In Hallo **taken** deelvenster, klikt u op **eigenschappen**.
   
    ![Gebruikerseigenschappen CORP](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784627.png)
8. Selecteer **extensies**, en klik vervolgens op Hallo **Geavanceerd** knop op Hallo **beveiliging** tabblad.
9. In Hallo **geavanceerde beveiligingsinstellingen voor de corp** in het dialoogvenster, klikt u op **toevoegen**.
10. Klik op **een principal selecteren**, zoeken naar **CORP\Install**, en klik vervolgens op **OK**.
11. Selecteer Hallo **alle eigenschappen lezen** en **Computerobjecten maken** machtigingen.
    
     ![Gebruikersmachtigingen Corp](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784628.png)
12. Klik op **OK**, en klik vervolgens op **OK** opnieuw. Sluit Hallo corp eigenschappenvenster.

Nu dat u Active Directory en gebruikersobjecten Hallo hebt geconfigureerd, wordt u drie virtuele machines van de SQL Server maken en toothis domein kan toevoegen.

## <a name="create-hello-sql-server-virtual-machines"></a>Hallo SQL Server virtuele machines maken
Maak drie virtuele machines. Een voor een clusterknooppunt is en twee zijn voor SQL Server. toocreate van Hallo virtuele machines, gaat u een back-toohello klassieke Azure portal maken, klikt u op **nieuw** > **Compute** > **virtuele Machine**  >  **Vanuit galerie**. Gebruik vervolgens Hallo sjablonen in Hallo na tabel toohelp u Hallo virtuele machines maken.

| Pagina | VM1 | VM2 | VM3 |
| --- | --- | --- | --- |
| Selecteer het besturingssysteem van de virtuele machine Hallo |**Windows Server 2012 R2 Datacenter** |**SQL Server 2014 RTM Enterprise** |**SQL Server 2014 RTM Enterprise** |
| Configuratie van virtuele machine |**VERSIE RELEASEDATUM** = (laatste)<br/>**NAAM van virtuele MACHINE** ContosoWSFCNode =<br/>**LAAG** = STANDARD<br/>**De grootte van** = A2 (2 kernen)<br/>**NIEUWE gebruikersnaam** AzureAdmin =<br/>**Nieuw wachtwoord** = Contoso! 000<br/>**Bevestig** = Contoso! 000 |**VERSIE RELEASEDATUM** = (laatste)<br/>**NAAM van virtuele MACHINE** ContosoSQL1 =<br/>**LAAG** = STANDARD<br/>**De grootte van** = A3 (4 kernen)<br/>**NIEUWE gebruikersnaam** AzureAdmin =<br/>**Nieuw wachtwoord** = Contoso! 000<br/>**Bevestig** = Contoso! 000 |**VERSIE RELEASEDATUM** = (laatste)<br/>**NAAM van virtuele MACHINE** ContosoSQL2 =<br/>**LAAG** = STANDARD<br/>**De grootte van** = A3 (4 kernen)<br/>**NIEUWE gebruikersnaam** AzureAdmin =<br/>**Nieuw wachtwoord** = Contoso! 000<br/>**Bevestig** = Contoso! 000 |
| Configuratie van virtuele machine |**CLOUDSERVICE** = eerder gemaakte unieke Cloud Service DNS-naam (ex: ContosoDC123)<br/>**REGIO/AFFINITEITSGROEP/VIRTUEEL netwerk** ContosoNET =<br/>**VIRTUEEL NETWERKSUBNETTEN** Back(10.10.2.0/24) =<br/>**STORAGE-ACCOUNT** = gebruik een automatisch gegenereerde storage-account<br/>**BESCHIKBAARHEIDSSET** = Maak een beschikbaarheidsset instellen<br/>**NAAM VAN DE BESCHIKBAARHEIDSSET** SQLHADR = |**CLOUDSERVICE** = eerder gemaakte unieke Cloud Service DNS-naam (ex: ContosoDC123)<br/>**REGIO/AFFINITEITSGROEP/VIRTUEEL netwerk** ContosoNET =<br/>**VIRTUEEL NETWERKSUBNETTEN** Back(10.10.2.0/24) =<br/>**STORAGE-ACCOUNT** = gebruik een automatisch gegenereerde storage-account<br/>**BESCHIKBAARHEIDSSET** = SQLHADR (u kunt ook configureren Hallo beschikbaarheidsset nadat Hallo machine is gemaakt. Alle drie de machines moeten worden toegewezen toohello SQLHADR beschikbaarheidsset.) |**CLOUDSERVICE** = eerder gemaakte unieke Cloud Service DNS-naam (ex: ContosoDC123)<br/>**REGIO/AFFINITEITSGROEP/VIRTUEEL netwerk** ContosoNET =<br/>**VIRTUEEL NETWERKSUBNETTEN** Back(10.10.2.0/24) =<br/>**STORAGE-ACCOUNT** = gebruik een automatisch gegenereerde storage-account<br/>**BESCHIKBAARHEIDSSET** = SQLHADR (u kunt ook configureren Hallo beschikbaarheidsset nadat Hallo machine is gemaakt. Alle drie de machines moeten worden toegewezen toohello SQLHADR beschikbaarheidsset.) |
| Opties voor de virtuele machine |Standaardinstellingen gebruiken |Standaardinstellingen gebruiken |Standaardinstellingen gebruiken |

<br/>

> [!NOTE]
> de vorige configuratie Hallo stelt standaardcategorie virtuele machines, omdat BASIC laagmachines eindpunten taakverdeling niet ondersteunen. Moet u Netwerktaakverdeling eindpunten hoger toocreate een beschikbaarheidsgroep-listener. Hallo machine grootten die hier worden voorgesteld zijn ook bedoeld voor het testen van beschikbaarheidsgroepen in Azure Virtual Machines. Zie voor de beste prestaties op productieworkloads Hallo Hallo aanbevelingen voor de grootte van de SQL Server-machines en configuratie in [best practices prestaties for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-performance.md).
> 
> 

Nadat het Hallo drie virtuele machines zijn volledig is ingericht, moet u toojoin ze toohello **corp.contoso.com** domein en verleen CORP\Install beheerdersrechten toohello machines. toodo deze, gebruik Hallo volgende stappen uit voor elk Hallo drie virtuele machines.

1. Hiermee wijzigt u eerst, Hallo voorkeurs-DNS-serveradres. Lokale map voor elke virtuele machine RDP-bestand tooyour downloaden door te klikken op Hallo te Hallo virtuele machine selecteren in lijst Hallo **Connect** knop. tooselect een virtuele machine, klik ergens maar Hallo eerste cel in rij hello, zoals wordt weergegeven in de volgende schermafbeelding Hallo.
   
    ![Hallo RDP-bestand downloaden](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC664953.jpg)
2. Open hello RDP-bestand dat u gedownload en toohello virtuele machine aanmelden met uw geconfigureerde beheerdersaccount (**BUILTIN\AzureAdmin**) en het wachtwoord (**Contoso! 000**).
3. Nadat u zich aanmeldt, ziet u Hallo **Serverbeheer** dashboard. Klik op **lokale Server** in het linkerdeelvenster Hallo.
4. Klik op Hallo **IPv4-adres toegewezen door DHCP, IPv6 ingeschakeld** koppeling.
5. In Hallo **netwerkverbindingen** dialoogvenster vak, klikt u op het netwerkpictogram Hallo.
   
    ![Wijziging Hallo virtuele machine voorkeurs-DNS-server](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784629.png)
6. Klik op de opdrachtbalk Hallo **Hallo-instellingen van deze verbinding wijzigen**. (Afhankelijk van de grootte van de Hallo van het venster, u wellicht tooclick Hallo dubbele pijl naar rechts toosee met deze opdracht).
7. Selecteer **Internet Protocol versie 4 (TCP/IPv4)**, en klik vervolgens op **eigenschappen**.
8. Selecteer **gebruik Hallo volgende DNS-serveradressen** en geef vervolgens **10.10.2.4** in **voorkeurs-DNS-server**.
9. Hallo **10.10.2.4** is Hallo-adres dat is toegewezen tooa virtuele machine in Hallo 10.10.2.0/24 subnet in een Azure-netwerk. Dat de virtuele machine is **ContosoDC**. tooverify **ContosoDC**van IP-adres, gebruik **nslookup contosodc** in Hallo opdrachtpromptvenster, zoals wordt weergegeven in de volgende schermafbeelding Hallo.
   
    ![Gebruik NSLOOKUP toofind IP-adres voor de domeincontroller](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC664954.jpg)
10. Klik op **OK** > **sluiten** toocommit Hallo wijzigingen. U kunt nu Hallo virtuele machine te koppelen**corp.contoso.com**.
11. Terug in Hallo **lokale Server** venster, klikt u op Hallo **werkgroep** koppeling.
12. In Hallo **computernaam** sectie, klikt u op **wijziging**.
13. Selecteer Hallo **domein** selectievakje, type **corp.contoso.com** in Hallo in het tekstvak en klik vervolgens op **OK**.
14. In Hallo **Windows-beveiliging** dialoogvenster geeft u de Hallo referenties voor Hallo standaard domeinbeheerdersaccount (**CORP\AzureAdmin**) en het Hallo-wachtwoord (**Contoso! 000**).
15. Wanneer u het 'Welkom toohello domein corp.contoso.com' Hallo-bericht ziet, klikt u op **OK**.
16. Klik op **sluiten** > **nu opnieuw opstarten** in het dialoogvenster Hallo.

### <a name="add-hello-corpinstall-user-as-an-administrator-on-each-virtual-machine"></a>Hallo Corp\Install gebruiker toevoegen als beheerder op elke virtuele machine
1. Wacht totdat de Hallo virtuele machine opnieuw is opgestart, en open vervolgens Hallo RDP-bestand opnieuw toosign in toohello virtuele machine met behulp van Hallo **BUILTIN\AzureAdmin** account.
2. In **Serverbeheer** klikt u op **extra** > **Computerbeheer**.
   
    ![Computerbeheer](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784630.png)
3. In Hallo **Computerbeheer** dialoogvenster Vouw **lokale gebruikers en groepen**, en klik vervolgens op **groepen**.
4. Dubbelklik op Hallo **beheerders** groep.
5. In Hallo **beheerders eigenschappen** dialoogvenster vak, klikt u op Hallo **toevoegen** knop.
6. Voer Hallo gebruiker **CORP\Install**, en klik vervolgens op **OK**. Wanneer u wordt gevraagd om referenties, gebruiken Hallo **AzureAdmin** account Hello **Contoso! 000** wachtwoord.
7. Klik op **OK** tooclose hello **beheerder eigenschappen** in het dialoogvenster.

### <a name="add-hello-failover-clustering-feature-tooeach-virtual-machine"></a>Hallo Failoverclustering functie tooeach virtuele machine toevoegen
1. In Hallo **Serverbeheer** dashboard, klikt u op **functies en onderdelen toevoegen**.
2. In Hallo **Wizard Functies toevoegen en onderdelen**, klikt u op **volgende** totdat u toohello **functies** pagina.
3. Selecteer **Failoverclustering**. Wanneer u wordt gevraagd, andere afhankelijke onderdelen toevoegen.
   
    ![Functie Failover Clustering toovirtual machine toevoegen](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784631.png)
4. Klik op **volgende**, en klik vervolgens op **installeren** op Hallo **bevestiging** pagina.
5. Wanneer Hallo **Failoverclustering** functie-installatie is voltooid, klikt u op **sluiten**.
6. Afmelden bij Hallo virtuele machine.
7. Herhaal Hallo stappen in deze sectie voor alle drie de servers: **ContosoWSFCNode**, **ContosoSQL1**, en **ContosoSQL2**.

Hallo van SQL Server is nu door virtuele machines zijn ingericht en wordt uitgevoerd, maar elk Hallo standaardopties voor SQL Server heeft.

## <a name="create-hello-failover-cluster"></a>Hallo failover-cluster maken
In deze sectie maakt u Hallo failover-cluster die als host fungeert Hallo beschikbaarheidsgroep die u later gaat maken. Nu moet u na tooeach van Hallo drie virtuele machines die u in het failovercluster Hallo gebruiken wilt Hallo hebben gedaan:

* Hallo volledig ingerichte virtuele machine in Azure
* Is toegevoegd aan Hallo virtuele machine toohello domein
* Toegevoegd **CORP\Install** toohello lokale groep Administrators
* Toegevoegde Hallo functie Failoverclustering

Al deze zijn vereisten op elke virtuele machine voordat u kunt deelnemen aan het toohello failover-cluster.

Bovendien Let op Hallo van virtuele Azure-netwerk niet meer werkt in Hallo dezelfde manier als een on-premises netwerk. U moet toocreate Hallo cluster in Hallo volgorde:

1. Maken van een cluster met één knooppunt op één knooppunt (**ContosoSQL1**).
2. Hallo cluster IP-adres tooan wijzigen ongebruikt IP-adres (**10.10.2.101**).
3. Hallo clusternaam online brengen.
4. Voeg Hallo van andere knooppunten (**ContosoSQL2** en **ContosoWSFCNode**).

Gebruik Hallo volgende stappen toocomplete Hallo taken die volledig Hallo-cluster te configureren.

1. Open Hallo RDP-bestand voor **ContosoSQL1**, en meld u aan met het domeinaccount Hallo **CORP\Install**.
2. In Hallo **Serverbeheer** dashboard, klikt u op **extra** > **Failoverclusterbeheer**.
3. Klik in het linkerdeelvenster Hallo met de rechtermuisknop op **Failoverclusterbeheer**, en klik vervolgens op **maken van een Cluster**, zoals weergegeven in de volgende schermafbeelding Hallo.
   
    ![Cluster maken](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784632.png)
4. Hallo in de Wizard Cluster maken, moet u een cluster met één knooppunt maken door te doorlopen Hallo pagina's en Hallo-instellingen in de volgende tabel Hallo:
   
   | Pagina | Instellingen |
   | --- | --- |
   | Voordat u begint |Standaardinstellingen gebruiken |
   | Servers selecteren |Type **ContosoSQL1** in **Enter servernaam** en klik op **toevoegen** |
   | Van validatiewaarschuwing |Selecteer **nr. ik geen ondersteuning van Microsoft nodig hebt voor dit cluster, en daarom niet wilt dat toorun Hallo validatie wordt getest. Als ik op Volgende klikt, doorgaan met het Hallo-cluster maken**. |
   | Toegangspunt voor beheer Hallo Cluster |Type **Cluster1** in **clusternaam** |
   | Bevestiging |Gebruik de standaardwaarden tenzij u van opslagruimten gebruikmaakt. Zie Hallo waarschuwing onder deze tabel. |
   
   > [!WARNING]
   > Als u [opslagruimten](https://technet.microsoft.com/library/hh831739), die meerdere schijven in opslaggroepen hebt gegroepeerd, moet u Hallo wissen **Voeg alle in aanmerking komende opslag toohello cluster** selectievakje op Hallo **bevestiging** pagina. Als u deze optie niet uitschakelt, wordt virtuele schijven Hallo losgekoppeld tijdens Hallo clustering proces. Als gevolg hiervan weergegeven deze ook niet in Schijfbeheer of Verkenner totdat Hallo opslagruimten zijn verwijderd uit de cluster Hallo en opnieuw worden gekoppeld met behulp van PowerShell.
   > 
   > 
5. Vouw in het linkerdeelvenster hello, **Failoverclusterbeheer**, en klik vervolgens op **Cluster1.corp.contoso.com**.
6. In het middelste deelvenster hello, schuif naar beneden toohello **Clusterkernresources** uit en vouw Hallo **naam: Clutser1** details. Ziet u beide Hallo **naam** en Hallo **IP-adres** bronnen in Hallo **mislukt** status. Hallo bron van het IP-adres kan niet online worden gebracht omdat Hallo-cluster is toegewezen Hallo hetzelfde IP-adres als Hallo machine zelf, dit is een dubbel adres.
7. Klik met de rechtermuisknop Hallo mislukt **IP-adres** bron en klik vervolgens op **eigenschappen**.
   
    ![Eigenschappen van cluster](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784633.png)
8. Selecteer **statisch IP-adres**, geef **10.10.2.101** in Hallo **adres** in het tekstvak en klik vervolgens op **OK**.
9. In Hallo **Clusterkernresources** sectie, met de rechtermuisknop op **naam: Cluster1**, en klik vervolgens op **Online brengen**. Wacht totdat beide bronnen online zijn. Wanneer de naam clusterbron Hallo online wordt gezet, worden Hallo DC-server wordt bijgewerkt met een nieuw Active Directory-computeraccount. Deze Active Directory-account wordt gebruikt toorun Hallo van de beschikbaarheidsgroep geclusterde service later.
10. Hallo resterende knooppunten toohello cluster toevoegen. Hallo-browser-consolestructuur met de rechtermuisknop op **Cluster1.corp.contoso.com**, en klik vervolgens op **knooppunt toevoegen**, zoals weergegeven in de volgende schermafbeelding Hallo.
    
     ![Knooppunt toohello cluster toevoegen](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784634.png)
11. In Hallo **Wizard knooppunt toevoegen**, klikt u op **volgende** op Hallo **Servers selecteren** pagina, het toevoegen van **ContosoSQL2** en **ContosoWSFCNode**  toohello lijst door te typen Hallo-servernaam in **Enter servernaam** en vervolgens te klikken op **toevoegen**. Wanneer u klaar bent, klikt u op **volgende**.
12. Op Hallo **Validation Warning** pagina, klikt u op **Nee**, maar in een productiescenario, moet u Hallo validatietests uitvoeren. Klik op **Volgende**.
13. Op Hallo **bevestiging** pagina, klikt u op **volgende** tooadd Hallo knooppunten.
    
    > [!WARNING]
    > Als u [opslagruimten](https://technet.microsoft.com/library/hh831739), die meerdere schijven in opslaggroepen hebt gegroepeerd, moet u Hallo wissen **Voeg alle in aanmerking komende opslag toohello cluster** selectievakje. Als u deze optie niet uitschakelt, wordt virtuele schijven Hallo losgekoppeld tijdens Hallo clustering proces. Als gevolg hiervan worden ook niet weergegeven in Schijfbeheer of Explorer totdat Hallo opslagruimten worden verwijderd uit het cluster en opnieuw gekoppeld met behulp van PowerShell.
    > 
    > 
14. Nadat het Hallo-knooppunten kan toohello cluster worden toegevoegd, klikt u op **voltooien**. Failover-clusterbeheer worden nu weergegeven dat het cluster heeft drie knooppunten en aanmelden Hallo **knooppunten** container.
15. Afmelden bij de extern-bureaubladsessie Hallo.

## <a name="prepare-hello-sql-server-instances-for-availability-groups"></a>Hallo SQL Server-exemplaren voor beschikbaarheidsgroepen voorbereiden
In deze sectie, doet u Hallo op beide **ContosoSQL1** en **contosoSQL2**:

* Toevoegen van een aanmelding voor **NT AUTHORITY\System** ingesteld toohello standaard SQL Server-exemplaar met de vereiste machtigingen beschikt.
* Voeg **CORP\Install** als een sysadmin-rol toohello standaard SQL Server-exemplaar.
* Hallo firewall voor externe toegang van SQL Server openen.
* Hallo Always On availability groepsfunctie inschakelen.
* Hallo SQL Server-serviceaccount ook wijzigen**CORP\SQLSvc1** en **CORP\SQLSvc2**respectievelijk.

Deze acties kunnen worden uitgevoerd in een willekeurige volgorde. Niettemin doorlopen Hallo stappen die ze in volgorde. Hallo voor beide stappen **ContosoSQL1** en **ContosoSQL2**:

1. Als u bent niet afgemeld bij Hallo extern bureaublad-sessiehost voor Hallo virtuele machine, moet u dit nu doen.
2. Open Hallo RDP-bestanden voor **ContosoSQL1** en **ContosoSQL2**, en meld u aan als **BUILTIN\AzureAdmin**.
3. Voeg **NT AUTHORITY\System** toohello SQL Server-aanmeldingen met vereiste machtigingen. Open **SQL Server Management Studio**.
4. Klik op **Connect** tooconnect toohello standaard SQL Server-exemplaar.
5. In **Objectverkenner**, vouw **beveiliging**, en vouw vervolgens **aanmeldingen**.
6. Klik met de rechtermuisknop Hallo **NT AUTHORITY\System** aanmelding en klik vervolgens op **eigenschappen**.
7. Op Hallo **Securables** pagina voor Hallo lokale server, selecteer **Grant** voor Hallo volgende machtigingen en klik vervolgens op **OK**.
   
   * Wijzigen van een beschikbaarheidsgroep
   * Verbinding maken met SQL
   * Status van de server weergeven
8. Voeg **CORP\Install** als een **sysadmin** rol toohello standaard SQL Server-exemplaar. In **Objectverkenner**, met de rechtermuisknop op **aanmeldingen**, en klik vervolgens op **New Login**.
9. Type **CORP\Install** in **aanmeldingsnaam**.
10. Op Hallo **serverfuncties** pagina **sysadmin**, en klik vervolgens op **OK**. Nadat u Hallo aanmelding hebt gemaakt, kunt u deze bekijken door het uitbreiden van **aanmeldingen** in **Objectverkenner**.
11. een firewallregel voor SQL Server op Hallo toocreate **Start** scherm open **Windows Firewall met geavanceerde beveiliging**.
12. Selecteer in het linkerdeelvenster Hallo **regels voor binnenkomende verbindingen**. Klik in het rechterdeelvenster hello, **nieuwe regel**.
13. Op Hallo **regeltype** pagina, klikt u op **programma** > **volgende**.
14. Op Hallo **programma** pagina **dit programmapad**, type **%ProgramFiles%\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\Binn\sqlservr.exe** in Hallo in het tekstvak en klik vervolgens op **volgende**. Als u deze aanwijzingen maar met behulp van SQL Server 2012, SQL Server-directory Hallo is **MSSQL11. MSSQLSERVER**.
15. Op Hallo **actie** pagina, houden **Hallo verbinding toestaan** geselecteerd en klik vervolgens op **volgende**.
16. Op Hallo **profiel** pagina, Hallo standaardinstellingen accepteren en klik vervolgens op **volgende**.
17. Op Hallo **naam** pagina, geef de regelnaam van een, zoals **SQL Server (programmaregel)**, in Hallo **naam** tekst vak en klik vervolgens op **voltooien**.
18. Hallo tooenable **altijd op beschikbaarheidsgroepen** functie op Hallo **Start** scherm open **SQL Server Configuration Manager**.
19. In de structuur van de browser hello, klikt u op **SQL Server-Services**, klik met de rechtermuisknop Hallo **SQL Server (MSSQLSERVER)** service en klik vervolgens op **eigenschappen**.
20. Klik op Hallo **altijd op hoge beschikbaarheid** tabblad **inschakelen altijd op beschikbaarheidsgroepen**, zoals weergegeven in Hallo volgende schermafbeelding en klik vervolgens op **toepassen**. Klik op **OK** in in het dialoogvenster Hallo en Hallo niet sluiten **eigenschappen** nog in het dialoogvenster. U kunt het Hallo SQL Server-service wordt opnieuw opgestart nadat u Hallo-serviceaccount wijzigen.
    
     ![Schakel altijd op beschikbaarheidsgroepen](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665520.gif)
21. toochange hello SQL Server-serviceaccount, klik op Hallo **aanmelden** tabblad, typt u **CORP\SQLSvc1** (voor **ContosoSQL1**) of **CORP\SQLSvc2** () voor **ContosoSQL2**) in **accountnaam**, vul Hallo wachtwoord bevestigen en klik vervolgens op **OK**.
22. In het dialoogvenster Hallo dat wordt geopend, klikt u op **Ja** toorestart Hallo SQL Server-service. Nadat het Hallo SQL Server-service opnieuw is opgestart, wijzigt u dat u hebt aangebracht in Hallo **eigenschappen** in het dialoogvenster geldig zijn.
23. Afmelden bij Hallo virtuele machines.

## <a name="create-hello-availability-group"></a>Hallo-beschikbaarheidsgroep maken
U bent nu klaar tooconfigure een beschikbaarheidsgroep. Hieronder vindt u een overzicht van wat u doet:

* Een nieuwe database maken (**MyDB1**) op **ContosoSQL1**.
* Neem een volledige back-up en de een transactielogboek van Hallo-database.
* Hallo volledige herstellen en logboekback-ups te**ContosoSQL2** Hello **NORECOVERY** optie.
* Hallo-beschikbaarheidsgroep maken (**AG1**) met synchrone doorvoer en automatische failover leesbare secundaire replica's.

### <a name="create-hello-mydb1-database-on-contososql1"></a>Hallo MyDB1 database maken op ContosoSQL1
1. Als u niet bent al geabonneerd buiten Hallo extern bureaublad-sessies voor **ContosoSQL1** en **ContosoSQL2**, doet u dat nu.
2. Open Hallo RDP-bestand voor **ContosoSQL1**, en meld u aan als **CORP\Install**.
3. In **Verkenner**onder **C:\\**, maak een map met de naam **back-**. U gebruikt deze directory tooback en uw database terugzetten.
4. Met de rechtermuisknop op de nieuwe map hello, wijst u te**delen met**, en klik vervolgens op **specifieke personen**, zoals weergegeven in de volgende schermafbeelding Hallo.
   
    ![Maak een back-map](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665521.gif)
5. Voeg **CORP\SQLSvc1**, en wijs hieraan Hallo **lezen/schrijven** machtiging. Toevoegen **CORP\SQLSvc2**, en wijs hieraan Hallo **lezen** toestemming hebben, zoals wordt weergegeven in volgende screenshot Hallo en klik vervolgens op **Share**. Nadat het delen van bestanden Hallo-proces is voltooid, klikt u op **gedaan**.
   
    ![Machtigingen voor back-upmap](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665522.gif)
6. toocreate Hallo-database, van Hallo **Start** menu openen **SQL Server Management Studio**, en klik vervolgens op **Connect** tooconnect toohello standaard SQL Server-exemplaar.
7. In **Objectverkenner**, met de rechtermuisknop op **Databases**, en klik vervolgens op **nieuwe Database**.
8. In **databasenaam**, type **MyDB1**, en klik vervolgens op **OK**.

### <a name="make-a-full-backup-of-mydb1-and-restore-it-on-contososql2"></a>Maak een volledige back-up van MyDB1 en terugzetten op ContosoSQL2
1. database een volledige back-up van Hallo toomake **Objectverkenner**, vouw **Databases**, met de rechtermuisknop op **MyDB1**, wijst u te**taken**, en Klik vervolgens op **Back-Up**.
2. In Hallo **bron** sectie, houden **back-uptype** instellen te**volledige**. In Hallo **bestemming** sectie, klikt u op **verwijderen** tooremove Hallo standaardpad voor back-upbestand Hallo.
3. In Hallo **bestemming** sectie, klikt u op **toevoegen**.
4. In Hallo **bestandsnaam** in het tekstvak  **\\ContosoSQL1\backup\MyDB1.bak**, klikt u op **OK**, en klik vervolgens op **OK** opnieuw tooback up Hallo-database. Wanneer de back-upbewerking Hallo is voltooid, klikt u op **OK** opnieuw tooclose Hallo in het dialoogvenster.
5. toomake een transactie aanmelden back-up van database hello, **Objectverkenner**, vouw **Databases**, met de rechtermuisknop op **MyDB1**, wijst u te**taken**, en klik vervolgens op **Back-Up**.
6. In **back-uptype**, selecteer **transactielogboek**. Hallo houden **bestemming** pad set toohello u eerder opgegeven bestand en klik vervolgens op **OK**. Nadat de back-upbewerking Hallo is voltooid, klikt u op **OK** opnieuw.
7. toorestore hello volledige- en transactie logboekback-ups op **ContosoSQL2**Open Hallo RDP-bestand voor **ContosoSQL2**, en meld u aan als **CORP\Install**. Hallo extern bureaublad-sessiehost voor laat **ContosoSQL1** openen.
8. Van Hallo **Start** menu openen **SQL Server Management Studio**, en klik vervolgens op **Connect** tooconnect toohello standaard SQL Server-exemplaar.
9. In **Objectverkenner**, met de rechtermuisknop op **Databases**, en klik vervolgens op **Restore Database**.
10. In Hallo **bron** sectie **apparaat**, en klik op Hallo weglatingsteken **...** te klikken.
11. In **Selecteer back-upapparaten**, klikt u op **toevoegen**.
12. In **back-up bestandslocatie**, type  **\\ContosoSQL1\backup**, klikt u op **vernieuwen**, selecteer **MyDB1.bak**, klikt u op **OK**, en klik vervolgens op **OK** opnieuw. U ziet nu hello volledige back-up- en Hallo logboekback-up in Hallo **back-upsets toorestore** deelvenster.
13. Ga toohello **opties** pagina **RESTORE WITH NORECOVERY** in **herstelstatus**, en klik vervolgens op **OK** toorestore Hallo-database. Herstellen na Hallo bewerking is voltooid, klikt u op **OK**.

### <a name="create-hello-availability-group"></a>Hallo-beschikbaarheidsgroep maken
1. Ga back-toohello extern bureaublad-sessiehost voor **ContosoSQL1**. In **Objectverkenner** in SQL Server Management Studio, met de rechtermuisknop op **altijd op hoge beschikbaarheid**, en klik vervolgens op **nieuwe Wizard beschikbaarheidsgroep**, zoals weergegeven in Hallo volgende schermopname.
   
    ![Start de Wizard Nieuwe beschikbaarheidsgroep](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665523.gif)
2. Op Hallo **inleiding** pagina, klikt u op **volgende**. Op Hallo **naam van de beschikbaarheidsgroep opgeven** typt **AG1** in **naam van de beschikbaarheidsgroep**, klikt u vervolgens op **volgende** opnieuw.
   
    ![Wizard Nieuwe beschikbaarheidsgroep, geef de naam van beschikbaarheidsgroep](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665524.gif)
3. Op Hallo **Databases selecteren** pagina **MyDB1**, en klik vervolgens op **volgende**. Hallo database voldoet Hallo-vereisten voor een beschikbaarheidsgroep aan omdat u ten minste één volledige back-up hebt uitgevoerd op Hallo beoogde primaire replica.
   
    ![Wizard Nieuwe Availabilty groep, selecteer databases](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665525.gif)
4. op Hallo **replica's opgeven** pagina, klikt u op **Replica toevoegen**.
   
    ![Wizard Nieuwe Availabilty groep, replica's opgeven](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665526.gif)
5. In Hallo **verbinding tooServer** in het dialoogvenster, type **ContosoSQL2** in **servernaam**, en klik vervolgens op **Connect**.
   
    ![Wizard Nieuwe Availabilty groepen Connect tooserver](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665527.gif)
6. Terug op Hallo **replica's opgeven** pagina u ziet nu **ContosoSQL2** die worden vermeld in **beschikbare replica's**. Hallo-replica's configureren zoals wordt weergegeven in de volgende schermafbeelding Hallo. Wanneer u klaar bent, klikt u op **volgende**.
   
    ![Wizard Nieuwe Availabilty groep, geef replica's (voltooien)](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665528.gif)
7. Op Hallo **eerste gegevenssynchronisatie selecteren** pagina **alleen deelnemen**, en klik vervolgens op **volgende**. U al gegevenssynchronisatie handmatig uitgevoerd wanneer u Hallo volledige transactie back-ups en aangebracht op **ContosoSQL1** en deze teruggezet op **ContosoSQL2**. U kunt kiezen niet tooperform Hallo back-up en herstel bewerkingen op de database en selecteert u in plaats daarvan **volledige** toolet Hallo nieuwe Wizard beschikbaarheidsgroep gegevenssynchronisatie voor u uitvoeren. Echter raadzaam niet deze optie voor zeer grote databases die zijn gevonden in sommige bedrijven.
   
    ![De Wizard Nieuwe Availabilty groep, eerste gegevenssynchronisatie selecteren](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665529.gif)
8. Op Hallo **validatie** pagina, klikt u op **volgende**. Deze pagina ziet vergelijkbare toohello volgende schermopname. Er is een waarschuwing voor de configuratie van de listener Hallo omdat u een beschikbaarheidsgroep-listener niet hebt geconfigureerd. Omdat een listener niet is geconfigureerd met deze zelfstudie, kunt u deze waarschuwing negeren. tooconfigure hello listener na het voltooien van deze zelfstudie, Zie [een ILB-listener voor AlwaysOn-beschikbaarheidsgroepen configureren in Azure](../classic/ps-sql-int-listener.md).
   
    ![Availabilty Wizard nieuwe validatie](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665530.gif)
9. Op Hallo **samenvatting** pagina, klikt u op **voltooien**, en wacht tot Hallo wizard configureert u de nieuwe beschikbaarheidsgroep Hallo. Op Hallo **voortgang** pagina, klikt u op **meer details** tooview Hallo gedetailleerde uitgevoerd. Nadat de wizard Hallo is voltooid, controleert u Hallo **resultaten** pagina tooverify die Hallo-beschikbaarheidsgroep is gemaakt, zoals wordt weergegeven in de volgende schermafbeelding Hallo en klik vervolgens op **sluiten** tooexit Hallo de wizard.
   
    ![Wizard Nieuwe groep Availabilty, resultaten](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665531.gif)
10. In **Objectverkenner**, vouw **altijd op hoge beschikbaarheid**, en vouw vervolgens **beschikbaarheidsgroepen**. U ziet nu de nieuwe beschikbaarheidsgroep Hallo in deze container. Met de rechtermuisknop op **AG1 (primaire)**, en klik vervolgens op **Dashboard weergeven**.
    
     ![Dashboard van de beschikbaarheidsgroep weergeven](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665532.gif)
11. Uw **altijd op Dashboard** moet uiterlijk vergelijkbare toohello een in Hallo volgende schermopname. U kunt zien Hallo replica's, Hallo failover-modus van elke replica en het Hallo-synchronisatiestatus.
    
     ![Beschikbaarheidsgroep-Dashboard](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665533.gif)
12. Te retourneren**Serverbeheer**, klikt u op **extra**, en open vervolgens **Failoverclusterbeheer**.
13. Vouw **Cluster1.corp.contoso.com**, en vouw vervolgens **Services en toepassingen**. Selecteer **rollen** en houd er rekening mee dat Hallo **AG1** rol beschikbaarheid-groep is gemaakt. Houd er rekening mee dat AG1 geen IP-adres door welke database clients verbinding toohello beschikbaarheidsgroep maken kunnen, omdat u niet een listener hebt geconfigureerd. U kunt rechtstreeks verbinden toohello primaire voor lees-/ schrijfbewerkingen en Hallo secundaire knooppunten voor query's voor alleen-lezen.
    
     ![AG in Failoverclusterbeheer](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665534.gif)

> [!WARNING]
> Probeer niet toofail via beschikbaarheidsgroep Hallo van Hallo Failover Cluster Manager. Alle failover-bewerkingen moeten worden uitgevoerd vanuit **altijd op Dashboard** in SQL Server Management Studio. Zie voor meer informatie [beperkingen op met Failover Cluster Manager met beschikbaarheidsgroepen Hallo](https://msdn.microsoft.com/library/ff929171.aspx).
> 
> 

## <a name="next-steps"></a>Volgende stappen
U hebt nu geïmplementeerd SQL Server Always On door het maken van een beschikbaarheidsgroep in Azure. Zie een listener voor deze beschikbaarheidsgroep tooconfigure [een ILB-listener voor AlwaysOn-beschikbaarheidsgroepen configureren in Azure](../classic/ps-sql-int-listener.md).

Zie voor meer informatie over het gebruik van SQL Server in Azure, [SQL Server op Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

