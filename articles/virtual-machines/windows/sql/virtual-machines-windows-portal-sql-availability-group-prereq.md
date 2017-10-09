---
title: aaaSQL serverbeschikbaarheid groepen - virtuele machines in Azure - vereisten | Microsoft Docs
description: Deze zelfstudie laat zien hoe tooconfigure Hallo vereisten voor het maken van een SQL Server Always On availability groeperen op Azure Virtual machines.
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: c492db4c-3faa-4645-849f-5a1a663be55a
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: eed0729ead25c7793bb17a04cd7fd996c7dc8c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="complete-hello-prerequisites-for-creating-always-on-availability-groups-on-azure-virtual-machines"></a>Hallo-vereisten voor het maken van AlwaysOn-beschikbaarheidsgroepen op Azure virtuele machines te voltooien

Deze zelfstudie laat zien hoe toocomplete Hallo vereisten voor het maken van een [SQL Server Always On beschikbaarheidsgroep op Azure virtuele machines (VM's)](virtual-machines-windows-portal-sql-availability-group-tutorial.md). Wanneer u klaar bent met het Hallo-vereisten, hebt u een domeincontroller, twee SQL Server-VM's en een witness-server in één resourcegroep.

**Tijd schatting**: het duurt een paar uur toocomplete Hallo vereisten. Veel van deze tijd wordt besteed aan het maken van virtuele machines.

Hallo volgende diagram ziet u wat u in de zelfstudie Hallo bouwen.

![Beschikbaarheidsgroep](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="review-availability-group-documentation"></a>Documentatie voor beschikbaarheid van groep lezen

Deze zelfstudie wordt ervan uitgegaan dat u basiskennis van SQL Server Always On availability groups. Als u niet bekend met deze technologie bent, Zie [overzicht van AlwaysOn-beschikbaarheidsgroepen (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).


## <a name="create-an-azure-account"></a>Maak een Azure-account
U hebt een Azure-account nodig. U kunt [gratis Azure-account openen](/pricing/free-trial/?WT.mc_id=A261C142F) of [voordelen als Visual Studio-abonnee activeren](/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

## <a name="create-a-resource-group"></a>Een resourcegroep maken
1. Meld u aan toohello [Azure-portal](http://portal.azure.com).
2. Klik op  **+**  toocreate een nieuw object in Hallo-portal.

   ![Nieuw object](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-portalplus.png)

3. Type **resourcegroep** in Hallo **Marketplace** zoekvenster.

   ![Resourcegroep](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-resourcegroupsymbol.png)
4. Klik op **resourcegroep**.
5. Klik op **Create**.
6. Op Hallo **resourcegroep** blade onder **Resourcegroepnaam**, typ een naam voor de resourcegroep Hallo. Typ bijvoorbeeld **sql-ha-rg**.
7. Als u meerdere Azure-abonnementen hebt, controleert u of Hallo abonnement hello Azure-abonnement dat u wilt toocreate Hallo-beschikbaarheidsgroep in.
8. Selecteer een locatie. Hallo-locatie is hello Azure-regio waar u toocreate Hallo-beschikbaarheidsgroep. Voor deze zelfstudie gaan we toobuild alle resources in een Azure-locatie.
9. Controleer **pincode toodashboard** is ingeschakeld. Deze instelling optioneel wordt een snelkoppeling voor resourcegroep Hallo op Hallo Azure-portaldashboard.

   ![Resourcegroep](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-resourcegroup.png)

10. Klik op **maken** toocreate Hallo resourcegroep.

Azure maakt Hallo resourcegroep en pincodes een snelkoppeling toohello-resourcegroep in Hallo-portal.

## <a name="create-hello-network-and-subnets"></a>Hallo-netwerk en subnetten maken
de volgende stap Hallo is toocreate Hallo netwerken en subnetten in hello Azure-resourcegroep.

Hallo-oplossing maakt gebruik van een virtueel netwerk met twee subnetten. Hallo [Virtual network-overzicht](../../../virtual-network/virtual-networks-overview.md) vindt u meer informatie over netwerken in Azure.

toocreate hello virtueel netwerk:

1. Klik in hello Azure-portal in de resourcegroep op **+ toevoegen**. Azure wordt geopend Hallo **Alles** blade.

   ![Nieuw item](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/02-newiteminrg.png)
2. Zoeken naar **virtueel netwerk**.

     ![Het virtuele netwerk zoeken](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/04-findvirtualnetwork.png)
3. Klik op **virtueel netwerk**.
4. Op Hallo **virtueel netwerk** blade, klikt u op Hallo **Resource Manager** implementatiemodel en klik vervolgens op **maken**.

    Hallo bevat volgende tabel instellingen voor het virtuele netwerk Hallo Hallo:

   | **Veld** | Waarde |
   | --- | --- |
   | **Naam** |autoHAVNET |
   | **Adresruimte** |10.33.0.0/24 |
   | **Subnetnaam** |Beheerder |
   | **Subnetadresbereik** |10.33.0.0/29 |
   | **Abonnement** |Hallo-abonnement dat u van plan toouse bent opgeven. **Abonnement** is leeg als u slechts één abonnement hebt. |
   | **Resourcegroep** |Kies **gebruik bestaande** en Hallo-naam van de resourcegroep hello te kiezen. |
   | **Locatie** |Geef hello Azure-locatie. |

   Uw adres en het subnet-adresbereik kan afwijken van Hallo-tabel. Afhankelijk van uw abonnement voorgesteld Hallo portal een beschikbare adresruimte en de bijbehorende subnet-adresbereik. Als er geen voldoende adresruimte beschikbaar is, gebruikt u een ander abonnement.

   Hallo-voorbeeld gebruikt Hallo subnetnaam **Admin**. Dit subnet is voor Hallo-domeincontrollers.

5. Klik op **Create**.

   ![Hallo virtueel netwerk configureren](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/06-configurevirtualnetwork.png)

Azure retourneert u toohello portaldashboard en waarschuwt u als nieuwe Hallo-netwerk wordt gemaakt.

### <a name="create-a-second-subnet"></a>Maak een tweede subnet
Hallo nieuw virtueel netwerk heeft een subnet, met de naam **Admin**. Hallo domeincontrollers gebruiken dit subnet. Hallo VM's van SQL Server gebruikt een tweede subnet met de naam **SQL**. tooconfigure dit subnet:

1. Klik op het dashboard op Hallo resourcegroep die u hebt gemaakt, **SQL-HA-RG**. Hallo-netwerk niet vinden in de resourcegroep Hallo onder **Resources**.

    Als **SQL-HA-RG** niet wordt weergegeven, vinden door te klikken op **resourcegroepen** en door de naam van resourcegroep hello te filteren.
2. Klik op **autoHAVNET** op Hallo lijst met resources. Azure Hallo netwerk configuratie blade geopend.
3. Op Hallo **autoHAVNET** blade virtueel netwerk onder **instellingen** , klikt u op **subnetten**.

    Houd er rekening mee Hallo-subnet dat u al hebt gemaakt.

   ![Hallo virtueel netwerk configureren](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/07-addsubnet.png)
5. Maak een tweede subnet. Klik op **+ Subnet**.
6. Op Hallo **subnet toevoegen** blade Hallo subnet configureren door te typen **sqlsubnet** onder **naam**. Azure automatisch een geldige geeft **-adresbereik**. Controleer of dit adresbereik ten minste 10 adressen erin. In een productieomgeving mogelijk meer adressen.
7. Klik op **OK**.

    ![Hallo virtueel netwerk configureren](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/08-configuresubnet.png)

Hallo volgende tabel geeft een overzicht van Hallo netwerkconfiguratie-instellingen:

| **Veld** | Waarde |
| --- | --- |
| **Naam** |**autoHAVNET** |
| **Adresruimte** |Deze waarde is afhankelijk van Hallo beschikbaar adresruimten in uw abonnement. Een typische waarde is 10.0.0.0/16. |
| **Subnetnaam** |**beheerder** |
| **Subnetadresbereik** |Deze waarde is afhankelijk van Hallo beschikbaar-adresbereiken in uw abonnement. Een typische waarde is 10.0.0.0/24. |
| **Subnetnaam** |**sqlsubnet** |
| **Subnetadresbereik** |Deze waarde is afhankelijk van Hallo beschikbaar-adresbereiken in uw abonnement. Een typische waarde is 10.0.1.0/24. |
| **Abonnement** |Hallo-abonnement dat u van plan toouse bent opgeven. |
| **Resourcegroep** |**SQL-HA-RG** |
| **Locatie** |Geef dezelfde locatie die u hebt gekozen voor de resourcegroep Hallo Hallo. |

## <a name="create-availability-sets"></a>Beschikbaarheidssets maken

Voordat u virtuele machines maken, moet u toocreate beschikbaarheidssets. Beschikbaarheidssets verminderen Hallo uitvaltijd van gebeurtenissen voor gepland of ongepland onderhoud. Een Azure beschikbaarheidsset is een logische groep resources die door Azure wordt geplaatst op fysieke domeinen met fouten en domeinen van de update. Een foutdomein zorgt ervoor dat leden van de beschikbaarheidsset Hallo Hallo afzonderlijke energie- en netwerkbronnen. Een updatedomein zorgt ervoor dat leden van de beschikbaarheidsset Hallo zijn niet voor onderhoud op Hallo dezelfde verbroken tijd. Zie voor meer informatie [Hallo beschikbaarheid van virtuele machines beheren](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

U moet twee beschikbaarheidssets. Een is voor Hallo-domeincontrollers. Hallo is het tweede voor virtuele machines Hallo SQL Server.

toocreate een beschikbaarheid instellen Ga toohello resourcegroep en klik **toevoegen**. Hallo resultaten filteren door te typen **beschikbaarheidsset**. Klik op **Beschikbaarheidsset** in Hallo resultaten en klik vervolgens op **maken**.

Twee beschikbaarheidssets volgens toohello parameters in de volgende tabel Hallo configureren:

| **Veld** | Beschikbaarheidsset domain-controller | Beschikbaarheidsset voor SQL Server |
| --- | --- | --- |
| **Naam** |adavailabilityset |sqlavailabilityset |
| **Resourcegroep** |SQL-HA-RG |SQL-HA-RG |
| **Domeinen met fouten** |3 |3 |
| **Domeinen bijwerken** |5 |3 |

Nadat u beschikbaarheidssets Hallo hebt gemaakt, retourneert u de resourcegroep toohello in hello Azure-portal.

## <a name="create-domain-controllers"></a>Maken van domeincontrollers
Wanneer u Hallo netwerk, subnetten, beschikbaarheidssets en een Internet gerichte load balancer hebt gemaakt, bent u klaar toocreate Hallo virtuele machines voor Hallo-domeincontrollers.

### <a name="create-virtual-machines-for-hello-domain-controllers"></a>Maken van virtuele machines voor Hallo domeincontrollers
toocreate en Hallo domeincontrollers configureren, retourneren toohello **SQL-HA-RG** resourcegroep.

1. Klik op **Add**. Hallo **Alles** blade wordt geopend.
2. Type **Windows Server 2016 Datacenter**.
3. Klik op **Windows Server 2016 Datacenter**. In Hallo **Windows Server 2016 Datacenter** blade controleren die implementatiemodel Hallo **Resource Manager**, en klik vervolgens op **maken**. Azure wordt geopend Hallo **virtuele machine maken** blade.

Herhaal de voorgaande stappen toocreate twee virtuele machines Hallo. Naam Hallo twee virtuele machines:

* AD-primaire-dc
* AD-secundaire-dc

  > [!NOTE]
  > Hallo **ad-secundaire-dc** virtuele machine is optioneel, tooprovide hoge beschikbaarheid voor Active Directory Domain Services.
  >
  >

Hallo bevat volgende tabel instellingen voor deze twee machines Hallo:

| **Veld** | Waarde |
| --- | --- |
| **Naam** |Eerste domeincontroller: *ad-primaire-dc*.</br>Tweede domeincontroller *ad-secundaire-dc*. |
| **Type VM-schijf** |SSD |
| **Gebruikersnaam** |DomainAdmin |
| **Wachtwoord** |Contoso! 0000 |
| **Abonnement** |*Uw abonnement* |
| **Resourcegroep** |SQL-HA-RG |
| **Locatie** |*Uw locatie* |
| **Grootte** |DS1_V2 |
| **Storage** | **Gebruik de schijven van de beheerde** - **Ja** |
| **Virtueel netwerk** |autoHAVNET |
| **Subnet** |Beheerder |
| **Openbaar IP-adres** |*Dezelfde naam als Hallo VM* |
| **Netwerkbeveiligingsgroep** |*Dezelfde naam als Hallo VM* |
| **Beschikbaarheidsset** |adavailabilityset </br>**Fault-domeinen**: 2</br>**Bijwerken van domeinen**: 2|
| **Diagnostics** |Ingeschakeld |
| **Opslagaccount voor diagnostische gegevens** |*Automatisch gemaakt* |

   >[!IMPORTANT]
   >U kunt alleen een virtuele machine in een beschikbaarheidsset wanneer u deze maakt plaatsen. U kunt Hallo beschikbaarheid instellen nadat een virtuele machine is gemaakt niet wijzigen. Zie [Hallo beschikbaarheid van virtuele machines beheren](../manage-availability.md).

Azure maakt Hallo virtuele machines.

Nadat het Hallo virtuele machines worden gemaakt, configureert u Hallo-domeincontroller.

### <a name="configure-hello-domain-controller"></a>Hallo-domeincontroller configureren
In Hallo configureert de volgende stappen Hallo **ad-primaire-dc** machines als een domeincontroller voor corp.contoso.com.

1. Open in Hallo portal Hallo **SQL-HA-RG** resourcegroep en selecteer Hallo **ad-primaire-dc** machine. Op Hallo **ad-primaire-dc** blade, klikt u op **Connect** tooopen een RDP-bestand voor toegang tot extern bureaublad.

    ![Verbinding maken met tooa virtuele machine](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/20-connectrdp.png)
2. Meld u aan met uw geconfigureerde beheerdersaccount (**\DomainAdmin**) en het wachtwoord (**Contoso! 0000**).
3. Standaard Hallo **Serverbeheer** dashboard moet worden weergegeven.
4. Klik op Hallo **functies en onderdelen toevoegen** koppeling op Hallo-dashboard.

    ![Server Manager - functies toevoegen](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
5. Selecteer **volgende** totdat u toohello **serverfuncties** sectie.
6. Selecteer Hallo **Active Directory Domain Services** en **DNS-Server** rollen. Wanneer u wordt gevraagd, voeg eventuele aanvullende functies die voor deze rollen vereist zijn.

   > [!NOTE]
   > Windows waarschuwt u dat er geen statische IP-adres is. Als u Hallo configuration test, klikt u op **doorgaan**. Instellen voor productiescenario's Hallo IP-adres toostatic in hello Azure-portal of [PowerShell tooset Hallo statische IP-adres van Hallo domain controller machine](../../../virtual-network/virtual-networks-reserved-private-ip.md).
   >
   >

    ![Dialoogvenster rollen toevoegen](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/23-addroles.png)
7. Klik op **volgende** totdat u Hallo **bevestiging** sectie. Selecteer Hallo **Hallo doelserver opnieuw opstarten automatisch indien nodig** selectievakje.
8. Klik op **Install**.
9. Nadat Hallo-functies installeren, return toohello **Serverbeheer** dashboard.
10. Selecteer nieuwe Hallo **AD DS** optie op Hallo linkerdeelvenster.
11. Klik op Hallo **meer** koppeling op de gele Hallo waarschuwing balk.

    ![Dialoogvenster van de AD DS op Hallo DNS-Server-VM](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/24-addsmore.png)
12. In Hallo **actie** kolom Hallo **alle Server-taakdetails** dialoogvenster, klikt u op **deze server tooa-domeincontroller promoveert**.
13. In Hallo **Wizard Active Directory Domain Services configureren**, Hallo volgende waarden gebruiken:

    | **Pagina** | Instelling |
    | --- | --- |
    | **Implementatieconfiguratie** |**Een nieuw forest toevoegen**<br/> **Naam van hoofddomein** corp.contoso.com = |
    | **Opties voor domeincontroller** |**DSRM-wachtwoord** = Contoso! 0000<br/>**Bevestig het wachtwoord** = Contoso! 0000 |
14. Klik op **volgende** toogo via andere pagina's in de wizard Hallo Hallo. Op Hallo **controle van vereisten** pagina, controleert u of er Hallo volgende bericht: **alle controles op vereisten zijn geslaagd**. U kunt toepasselijke waarschuwingsberichten bekijken, maar het is mogelijk toocontinue Hallo-installatie.
15. Klik op **Install**. Hallo **ad-primaire-dc** virtuele machine automatisch opnieuw wordt opgestart.

### <a name="note-hello-ip-address-of-hello-primary-domain-controller"></a>Houd er rekening mee Hallo IP-adres van de primaire domeincontroller Hallo

De primaire domeincontroller Hallo gebruiken voor DNS. Houd er rekening mee Hallo primaire domain controller IP-adres.

Eenzijdige tooget Hallo primaire domain controller IP-adres is via hello Azure-portal.

1. Open op Hallo Azure-portal, Hallo resourcegroep.

2. Klik op de primaire domeincontroller Hallo.

3. Klik op Hallo primaire domain controller blade **netwerkinterfaces**.

![Netwerkinterfaces](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/25-primarydcip.png)

Houd er rekening mee Hallo privé IP-adres voor deze server.

### <a name="configure-hello-virtual-network-dns"></a>Hallo virtueel netwerk DNS configureren
Nadat u de eerste domeincontroller Hallo maken en DNS op de eerste server hello inschakelen, Hallo virtueel netwerk toouse deze server configureren voor DNS.

1. Hallo Azure-portal, klik op Hallo virtueel netwerk.

2. Onder **instellingen**, klikt u op **DNS-Server**.

3. Klik op **aangepaste**, en typt u privé IP-adres van de primaire domeincontroller Hallo Hallo.

4. Klik op **Opslaan**.

### <a name="configure-hello-second-domain-controller"></a>Hallo tweede domeincontroller configureren
Nadat de primaire domeincontroller Hallo opnieuw is opgestart, kunt u de tweede domeincontroller Hallo kunt configureren. Deze stap optioneel is voor hoge beschikbaarheid. Volg deze stappen tooconfigure Hallo tweede-domeincontroller:

1. Open in Hallo portal Hallo **SQL-HA-RG** resourcegroep en selecteer Hallo **ad-secundaire-dc** machine. Op Hallo **ad-secundaire-dc** blade, klikt u op **Connect** tooopen een RDP-bestand voor toegang tot extern bureaublad.
2. Toohello VM aanmelden met uw geconfigureerde beheerdersaccount (**BUILTIN\DomainAdmin**) en het wachtwoord (**Contoso! 0000**).
3. Wijziging Hallo voorkeur toohello adres van DNS-server-adres van de domeincontroller Hallo.
4. In **Netwerkcentrum**, klikt u op Hallo-netwerkinterface.
   ![Netwerkinterface](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/26-networkinterface.png)

5. Klik op **Eigenschappen**.
6. Selecteer **Internet Protocol versie 4 (TCP/IPv4)** en klik op **eigenschappen**.
7. Selecteer **gebruik Hallo volgende DNS-serveradressen** en geef Hallo-adres van de primaire domeincontroller Hallo in **voorkeurs-DNS-server**.
8. Klik op **OK**, en vervolgens **sluiten** toocommit Hallo wijzigingen. U bent nu kunnen toojoin Hallo VM te**corp.contoso.com**.

   >[!IMPORTANT]
   >Als u Hallo verbinding tooyour extern bureaublad verliest na Hallo DNS-instelling te wijzigen, gaat u toohello Azure portal en opnieuw opstarten Hallo virtuele machine.

9. Open in Hallo extern bureaublad toohello secundaire domeincontroller, **Dashboard voor Serverbeheer**.
10. Klik op Hallo **functies en onderdelen toevoegen** koppeling op Hallo-dashboard.

    ![Server Manager - functies toevoegen](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
11. Selecteer **volgende** totdat u toohello **serverfuncties** sectie.
12. Selecteer Hallo **Active Directory Domain Services** en **DNS-Server** rollen. Wanneer u wordt gevraagd, voeg eventuele aanvullende functies die voor deze rollen vereist zijn.
13. Nadat Hallo-functies installeren, return toohello **Serverbeheer** dashboard.
14. Selecteer nieuwe Hallo **AD DS** optie op Hallo linkerdeelvenster.
15. Klik op Hallo **meer** koppeling op de gele Hallo waarschuwing balk.
16. In Hallo **actie** kolom Hallo **alle Server-taakdetails** dialoogvenster, klikt u op **deze server tooa-domeincontroller promoveert**.
17. Onder **implementatieconfiguratie**, selecteer **toevoegen van een domeincontroller tooan bestaande domein**.
   ![Implementatieconfiguratie](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/28-deploymentconfig.png)
18. Klik op **Selecteren**.
19. Verbinding maken met behulp van Hallo administrator-account (**CORP. Contoso.COM\domainadmin**) en het wachtwoord (**Contoso! 0000**).
20. In **Selecteer een domein in het forest Hallo**, klikt u op uw domein en klik vervolgens op **OK**.
21. In **opties voor domeincontroller**, gebruikt u de standaardwaarden Hallo en een DSRM-wachtwoord instellen.

   >[!NOTE]
   >Hallo **DNS-opties** pagina worden gewaarschuwd dat een overdracht voor deze DNS-server kan niet worden gemaakt. U kunt deze waarschuwing in niet-productieve omgevingen negeren.
22. Klik op **volgende** totdat Hallo dialoogvenster Hallo bereikt **vereisten** controleren. Klik vervolgens op **Installeren**.

Hallo-server opnieuw opstarten als Hallo server Hallo configuratiewijzigingen is voltooid.

### <a name="add-hello-private-ip-address-toohello-second-domain-controller-toohello-vpn-dns-server"></a>Hallo particulier IP-adres toohello tweede domain controller toohello VPN-DNS-Server toevoegen

Wijzig Hallo DNS-Server tooinclude Hallo IP-adres van de secundaire domeincontroller Hallo in hello Azure-portal onder virtuele netwerk. Hierdoor Hallo DNS-service redundantie.

### <a name=DomainAccounts></a>Hallo-domeinaccounts configureren

In de volgende stappen hello configureert u Hallo Active Directory-accounts. Hallo ziet volgende tabel u Hallo accounts:

| |Installatie-account<br/> |SQL Server-0 <br/>SQL Server en SQL Agent-Service-account |SQL Server-1<br/>SQL Server en SQL Agent-Service-account
| --- | --- | --- | ---
|**Voornaam** |Installeren |SQLSvc1 | SQLSvc2
|**SamAccountName van gebruiker** |Installeren |SQLSvc1 | SQLSvc2

Volgende stappen toocreate Hallo elk account gebruiken.

1. Meld u aan toohello **ad-primaire-dc** machine.
2. In **Serverbeheer**, selecteer **extra**, en klik vervolgens op **Active Directory Administrative Center**.   
3. Selecteer **corp (lokaal)** in het linkerdeelvenster Hallo.
4. Op de juiste Hallo **taken** deelvenster **nieuw**, en klik vervolgens op **gebruiker**.
   ![Active Directory-beheercentrum](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/29-addcnewuser.png)

   >[!TIP]
   >Stel een complex wachtwoord voor elke account.<br/> Niet-productieve omgevingen, set Hallo gebruiker account toonever verloopt.

5. Klik op **OK** toocreate Hallo gebruiker.
6. Herhaal de vorige stappen voor elk van de drie accounts Hallo Hallo.

### <a name="grant-hello-required-permissions-toohello-installation-account"></a>Hallo vereist machtigingen verlenen toohello installatie-account
1. In Hallo **Active Directory Administrative Center**, selecteer **corp (lokaal)** in het linkerdeelvenster Hallo. Klik in het rechterdeelvenster Hallo **taken** deelvenster, klikt u op **eigenschappen**.

    ![Gebruikerseigenschappen CORP](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/31-addcproperties.png)
2. Selecteer **extensies**, en klik vervolgens op Hallo **Geavanceerd** knop op Hallo **beveiliging** tabblad.
3. In Hallo **geavanceerde beveiligingsinstellingen voor de corp** dialoogvenster, klikt u op **toevoegen**.
4. Klik op **een principal selecteren**, zoeken naar **CORP\Install**, en klik vervolgens op **OK**.
5. Selecteer Hallo **alle eigenschappen lezen** selectievakje.

6. Selecteer Hallo **Computerobjecten maken** selectievakje.

     ![Gebruikersmachtigingen Corp](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/33-addpermissions.png)
7. Klik op **OK**, en klik vervolgens op **OK** opnieuw. Sluit Hallo **corp** eigenschappenvenster.

Nu dat u klaar bent met het configureren van Active Directory en gebruikersobjecten hello, twee SQL Server-VM's en een witness-server VM maken. Meldt u zich alle drie toohello-domein.

## <a name="create-sql-server-vms"></a>SQL Server-VM's maken

Drie extra virtuele machines maken. Hallo oplossing vereist twee virtuele machines met SQL Server-exemplaren. Een derde virtuele machine fungeert als een witness. Windows Server 2016 kunt gebruiken een [cloud witness](http://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness), maar voor consistentie met eerdere besturingssystemen in dit document maakt gebruik van een virtuele machine voor een witness.  

Overweeg Hallo deisign beslissingen te volgen voordat u doorgaat.

* **Opslag - Azure schijven die worden beheerd**

   Voor de opslag van de virtuele machine hello, Azure beheerd schijven te gebruiken. Microsoft raadt beheerd schijven voor virtuele machines van SQL Server. Schijven ingangen opslag achter de schermen Hallo beheerd. Bovendien wanneer virtuele machines met beheerd schijven zich in Hallo dezelfde beschikbaarheidsset, Azure distribueert Hallo opslag resources tooprovide juiste redundantie. Zie [Azure Managed Disks overview](../managed-disks-overview.md) (Overzicht van Azure Managed Disks) voor meer informatie. Zie voor meer details over beheerde schijven in een beschikbaarheidsset [beheerd schijven gebruiken voor virtuele machines in een beschikbaarheidsset](../manage-availability.md#use-managed-disks-for-vms-in-an-availability-set).

* **Netwerk - particuliere IP-adressen in productie**

   Deze zelfstudie wordt voor Hallo virtuele machines, openbare IP-adressen. Hierdoor kan externe verbinding rechtstreeks toohello virtuele machine via internet Hallo - het configuratiestappen eenvoudiger maakt. In een productieomgeving, wordt aangeraden alleen persoonlijke IP-adressen in volgorde tooreduce hello kwetsbaarheidfootprint van SQL Server-exemplaar Hallo VM-resource.

### <a name="create-and-configure-hello-sql-server-vms"></a>Maak en configureer Hallo SQL Server-VM 's
Maak vervolgens drie virtuele machines--twee SQL Server-VM's en een VM voor een extra clusterknooppunt. toocreate van virtuele machines hello, gaat u terug toohello **SQL-HA-RG** resourcegroep, klikt u op **toevoegen**, zoeken naar Hallo juiste galerij-item, klikt u op **virtuele Machine**, en vervolgens Klik op **uit galerie**. Gebruik Hallo informatie in Hallo tabel toohelp maken van virtuele machines hello te volgen:


| Pagina | VM1 | VM2 | VM3 |
| --- | --- | --- | --- |
| Hallo juiste galerij-item selecteren |**Windows Server 2016 Datacenter** |**SQL Server 2016 SP1 Enterprise op WindowsServer 2016** |**SQL Server 2016 SP1 Enterprise op WindowsServer 2016** |
| Virtuele-machineconfiguratie **basisbeginselen** |**Naam** cluster fsw =<br/>**Gebruikersnaam** DomainAdmin =<br/>**Wachtwoord** = Contoso! 0000<br/>**Abonnement** = van uw abonnement<br/>**Resourcegroep** SQL-HA-RG =<br/>**Locatie** = van uw azure-locatie |**Naam** sqlserver-0 =<br/>**Gebruikersnaam** DomainAdmin =<br/>**Wachtwoord** = Contoso! 0000<br/>**Abonnement** = van uw abonnement<br/>**Resourcegroep** SQL-HA-RG =<br/>**Locatie** = van uw azure-locatie |**Naam** sqlserver-1 =<br/>**Gebruikersnaam** DomainAdmin =<br/>**Wachtwoord** = Contoso! 0000<br/>**Abonnement** = van uw abonnement<br/>**Resourcegroep** SQL-HA-RG =<br/>**Locatie** = van uw azure-locatie |
| Virtuele-machineconfiguratie **grootte** |**De grootte van** = DS1\_V2 (1 kerngeheugen, 3.5 GB) |**De grootte van** DS2 =\_V2 (2 kernen, 7 GB)</br>Hallo grootte moet ondersteuning bieden voor SSD-opslag (ondersteuning van Premium-schijven. )) |**De grootte van** DS2 =\_V2 (2 kernen, 7 GB) |
| Virtuele-machineconfiguratie **instellingen** |**Opslag**: gebruik schijven die worden beheerd.<br/>**Virtueel netwerk** autoHAVNET =<br/>**Subnet** sqlsubnet(10.1.1.0/24) =<br/>**Openbaar IP-adres** automatisch is gegenereerd.<br/>**Netwerkbeveiligingsgroep** = geen<br/>**Bewaking van diagnostische gegevens** = ingeschakeld<br/>**Opslagaccount voor diagnostische gegevens** = gebruik een automatisch gegenereerde storage-account<br/>**Beschikbaarheidsset** sqlAvailabilitySet =<br/> |**Opslag**: gebruik schijven die worden beheerd.<br/>**Virtueel netwerk** autoHAVNET =<br/>**Subnet** sqlsubnet(10.1.1.0/24) =<br/>**Openbaar IP-adres** automatisch is gegenereerd.<br/>**Netwerkbeveiligingsgroep** = geen<br/>**Bewaking van diagnostische gegevens** = ingeschakeld<br/>**Opslagaccount voor diagnostische gegevens** = gebruik een automatisch gegenereerde storage-account<br/>**Beschikbaarheidsset** sqlAvailabilitySet =<br/> |**Opslag**: gebruik schijven die worden beheerd.<br/>**Virtueel netwerk** autoHAVNET =<br/>**Subnet** sqlsubnet(10.1.1.0/24) =<br/>**Openbaar IP-adres** automatisch is gegenereerd.<br/>**Netwerkbeveiligingsgroep** = geen<br/>**Bewaking van diagnostische gegevens** = ingeschakeld<br/>**Opslagaccount voor diagnostische gegevens** = gebruik een automatisch gegenereerde storage-account<br/>**Beschikbaarheidsset** sqlAvailabilitySet =<br/> |
| Virtuele-machineconfiguratie **SQL Server-instellingen** |Niet van toepassing |**SQL-connectiviteit** = privé (binnen virtueel netwerk)<br/>**Poort** 1433 =<br/>**SQL-verificatie** = uitschakelen<br/>**Opslagconfiguratie** algemene =<br/>**Automatisch patchen** = zondag om 2:00 uur<br/>**Automatische back-up** = uitgeschakeld</br>**Integratie van Azure Sleutelkluis** = uitgeschakeld |**SQL-connectiviteit** = privé (binnen virtueel netwerk)<br/>**Poort** 1433 =<br/>**SQL-verificatie** = uitschakelen<br/>**Opslagconfiguratie** algemene =<br/>**Automatisch patchen** = zondag om 2:00 uur<br/>**Automatische back-up** = uitgeschakeld</br>**Integratie van Azure Sleutelkluis** = uitgeschakeld |

<br/>

> [!NOTE]
> de grootte van de machines Hallo hier voorgesteld zijn bedoeld voor het testen van beschikbaarheidsgroepen in Azure Virtual machines. Zie voor de beste prestaties op productieworkloads Hallo Hallo aanbevelingen voor de grootte van de SQL Server-machines en configuratie in [best practices prestaties for SQL Server op Azure virtual machines](virtual-machines-windows-sql-performance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
>
>

Nadat het Hallo drie virtuele machines zijn volledig is ingericht, moet u toojoin ze toohello **corp.contoso.com** domein en verleen CORP\Install beheerdersrechten toohello machines.

### <a name="joinDomain"></a>Lid worden van Hallo servers toohello domein

U bent nu kunnen toojoin Hallo virtuele machines te**corp.contoso.com**. Hallo volgende voor zowel Hallo SQL Server-VM's en Hallo-bestand delen witness-server:

1. Extern verbinding toohello virtuele machine met **BUILTIN\DomainAdmin**.
2. In **Serverbeheer**, klikt u op **lokale Server**.
3. Klik op Hallo **werkgroep** koppeling.
4. In Hallo **computernaam** sectie, klikt u op **wijziging**.
5. Selecteer Hallo **domein** selectievakje in en typ **corp.contoso.com** in het tekstvak Hallo. Klik op **OK**.
6. In Hallo **Windows-beveiliging** dialoogvenster pop, geef referenties op Hallo voor Hallo standaard domeinbeheerdersaccount (**CORP\DomainAdmin**) en het Hallo-wachtwoord (**Contoso! 0000**).
7. Wanneer u het 'Welkom toohello domein corp.contoso.com' Hallo-bericht ziet, klikt u op **OK**.
8. Klik op **sluiten**, en klik vervolgens op **nu opnieuw opstarten** in Hallo pop-up dialoogvenster.

### <a name="add-hello-corpinstall-user-as-an-administrator-on-each-cluster-vm"></a>Hallo Corp\Install gebruiker toevoegen als een beheerder zijn op elk cluster VM

Nadat u elke virtuele machine opnieuw wordt opgestart als lid van domein hello, toevoegen **CORP\Install** als lid van de lokale beheerdersgroep Hallo.

1. Wacht totdat het Hallo VM opnieuw wordt gestart en vervolgens Hallo RDP-bestand van Hallo primaire domain controller toosign in opnieuw te starten**sqlserver 0** met behulp van Hallo **CORP\DomainAdmin** account.
   >[!TIP]
   >Zorg ervoor dat u zich met een domeinbeheerdersaccount Hallo aanmeldt. In de vorige stappen hello gebruikten Hallo IN van de ingebouwde administrator-account. Nu hello server zich in Hallo domein gebruiken Hallo domeinaccount. Geef in uw RDP-sessie *domein*\\*gebruikersnaam*.

2. In **Serverbeheer**, selecteer **extra**, en klik vervolgens op **Computerbeheer**.
3. In Hallo **Computerbeheer** venster Vouw **lokale gebruikers en groepen**, en selecteer vervolgens **groepen**.
4. Dubbelklik op Hallo **beheerders** groep.
5. In Hallo **beheerders eigenschappen** dialoogvenster, klikt u op Hallo **toevoegen** knop.
6. Voer Hallo gebruiker **CORP\Install**, en klik vervolgens op **OK**.
7. Klik op **OK** tooclose hello **beheerder eigenschappen** dialoogvenster.
8. Herhaal de vorige stappen Hallo **sqlserver 1** en **cluster fsw**.

### <a name="setServiceAccount"></a>Hallo SQL Server-serviceaccounts instellen

Stel Hallo SQL Server-serviceaccount op elke virtuele machine van SQL Server. Gebruik Hallo-accounts die u hebt gemaakt wanneer u [geconfigureerd Hallo domeinaccounts](#DomainAccounts).

1. Open **SQL Server Configuration Manager**.
2. Met de rechtermuisknop op Hallo SQL Server-service en klik vervolgens op **eigenschappen**.
3. Hallo-account en wachtwoord instellen.
4. Herhaal deze stappen op Hallo van andere virtuele machine van SQL Server.  

Voor SQL Server-beschikbaarheidsgroepen moet elke SQL Server-VM toorun als een domeinaccount.

### <a name="create-a-sign-in-on-each-sql-server-vm-for-hello-installation-account"></a>Een aanmeldingspagina op elke SQL Server-VM voor Hallo installatie-account maken

Hallo-installatie-account (CORP\install) tooconfigure Hallo beschikbaarheidsgroep gebruiken. Dit account moet lid zijn van Hallo toobe **sysadmin** vaste serverrol op elke virtuele machine van SQL Server. Hallo volgende stappen maakt u een aanmeldingspagina voor Hallo installatie-account:

1. Toohello server via Hallo Remote Desktop Protocol (RDP) verbinding maken met behulp van Hallo  *\<MachineName\>\DomainAdmin* account.

1. Open SQL Server Management Studio en maak verbinding toohello lokale exemplaar van SQL Server.

1. In **Objectverkenner**, klikt u op **beveiliging**.

1. Met de rechtermuisknop op **aanmeldingen**. Klik op **New Login**.

1. In **Login - nieuwe**, klikt u op **Search**.

1. Klik op **locaties**.

1. Voer Hallo netwerk domeinbeheerdersreferenties.

1. Hallo-installatie-account gebruiken.

1. Hallo aanmelden toobe lid zijn van Hallo ingesteld **sysadmin** vaste serverrol.

1. Klik op **OK**.

Herhaal Hallo vorige stappen op Hallo van andere virtuele machine van SQL Server.

## <a name="add-failover-clustering-features-tooboth-sql-server-vms"></a>Toevoegen van functies tooboth VM's van SQL Server Failover Clustering

functies voor failoverclustering tooadd Hallo op beide VM's van SQL Server:

1. Toohello SQL Server-virtuele machine via Hallo Remote Desktop Protocol (RDP) verbinding maken met behulp van Hallo *CORP\install* account. Open **Dashboard voor Serverbeheer**.
2. Klik op Hallo **functies en onderdelen toevoegen** koppeling op Hallo-dashboard.

    ![Server Manager - functies toevoegen](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
3. Selecteer **volgende** totdat u toohello **serverfuncties** sectie.
4. In **functies**, selecteer **Failoverclustering**.
5. Voeg eventuele aanvullende vereiste functies.
6. Klik op **installeren** tooadd Hallo functies.

Herhaal stappen op Hallo Hallo andere SQL Server-VM.

## <a name="a-nameendpoint-firewall-configure-hello-firewall-on-each-sql-server-vm"></a><a name="endpoint-firewall">Hallo-firewall op elke virtuele machine van SQL Server configureren

Hallo oplossing vereist Hallo toobe openen in Hallo firewall TCP-poorten te volgen:

- **SQL Server-machine**:<br/>
   Poort 1433 voor een standaardexemplaar van SQL Server.
- **Azure load balancer-test:**<br/>
   Een beschikbare poort. De voorbeelden gebruiken vaak 59999.
- **Eindpunt voor databasespiegeling:** <br/>
   Een beschikbare poort. De voorbeelden gebruiken vaak 5022.

Hallo firewall-poorten moeten toobe geopend zijn op beide VM's van SQL Server.

Hallo-methode Hallo poorten te openen, is afhankelijk van Hallo firewalloplossing die u gebruikt. Hallo volgende sectie wordt uitgelegd hoe tooopen Hallo in Windows Firewall-poorten. Hallo vereist poorten openen op elk van uw SQL Server-VM.

### <a name="open-a-tcp-port-in-hello-firewall"></a>Een TCP-poort in de Hallo firewall openen

1. Hallo eerste SQL-Server op **Start** scherm, starten **Windows Firewall met geavanceerde beveiliging**.
2. Selecteer in het linkerdeelvenster Hallo **regels voor binnenkomende verbindingen**. Klik in het rechterdeelvenster Hallo **nieuwe regel**.
3. Voor **regeltype**, kies **poort**.
4. Geef voor het Hallo-poort, **TCP** en type Hallo poortnummers nodig. Zie Hallo voorbeeld te volgen:

   ![SQL-firewall](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/35-tcpports.png)

5. Klik op **Volgende**.
6. Op Hallo **actie** pagina, houden **Hallo verbinding toestaan** geselecteerd en klik vervolgens op **volgende**.
7. Op Hallo **profiel** pagina, Hallo standaardinstellingen accepteren en klik vervolgens op **volgende**.
8. Op Hallo **naam** pagina, geeft u de regelnaam van een (zoals **Azure LB Probe**) in Hallo **naam** in het tekstvak en klik vervolgens op **voltooien**.

Herhaal deze stappen uit op Hallo tweede SQL Server-VM.

## <a name="next-steps"></a>Volgende stappen

* [Een SQL Server Always On-beschikbaarheidsgroep maken op virtuele machines in Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md)
