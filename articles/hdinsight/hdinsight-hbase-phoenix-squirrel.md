---
title: aaaUse Apache Phoenix en SQuirreL met op basis van Windows Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Apache Phoenix in HDInsight, en hoe tooinstall en SQuirreL configureren op uw werkstation tooconnect tooan HBase-cluster in HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a>Apache Phoenix en SQuirreL gebruiken met HBase op basis van Windows-clusters in HDInsight
Meer informatie over hoe toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, en hoe tooinstall en SQuirreL configureren op uw werkstation tooconnect tooan HBase-cluster in HDInsight. Zie voor meer informatie over Phoenix [Phoenix in 15 minuten of minder](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html). Zie voor Hallo Phoenix grammatica, [Phoenix grammatica](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Zie voor Hallo Phoenix versie-informatie in HDInsight, [wat is er nieuw in Hallo Hadoop-clusterversies geleverd door HDInsight?](hdinsight-component-versioning.md).
>

> [!IMPORTANT]
> Hallo stappen in dit document alleen werk voor op Windows gebaseerde HDInsight-clusters. HDInsight is alleen beschikbaar in Windows voor versies lager is dan HDInsight 3.4. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie. Zie voor meer informatie over het gebruik van Phoenix op Linux gebaseerde HDInsight [gebruik Apache Phoenix met HBase op basis van Linux-clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).
>



## <a name="use-sqlline"></a>Gebruik SQLLine
[SQLLine](http://sqlline.sourceforge.net/) is een opdrachtregel-hulpprogramma tooexecute SQL.

### <a name="prerequisites"></a>Vereisten
Voordat u SQLLine gebruiken kunt, moet u de volgende Hallo hebben:

* **Een HBase-cluster in HDInsight**. Voor informatie over het inrichten van HBase-cluster, Zie [aan de slag met Apache HBase in HDInsight][hdinsight-hbase-get-started].
* **Verbinding maken met HBase-cluster via remote desktop protocol Hallo toohello**. Zie voor instructies [beheren Hadoop-clusters in HDInsight met behulp van de klassieke Azure-Portal Hallo][hdinsight-manage-portal].

**toofind uit Hallo-hostnaam**

1. Open **Hadoop-opdrachtregel** vanaf Hallo bureaublad.
2. Voer Hallo opdracht tooget Hallo DNS-achtervoegsel te volgen:

        ipconfig

    Noteer **verbindingsspecifieke DNS-achtervoegsel**. Bijvoorbeeld: *myhbasecluster.f5.internal.cloudapp.net*. Als u verbinding tooan HBase-cluster, moet u tooconnect tooone van Hallo Zookeepers met FQDN-naam. Elke HDInsight-cluster heeft 3 Zookeepers. Ze zijn *zookeeper0*, *zookeeper1*, en *zookeeper2*. Hallo FQDN is ongeveer *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.

**toouse SQLLine**

1. Open **Hadoop-opdrachtregel** vanaf Hallo bureaublad.
2. Voer Hallo opdrachten tooopen SQLLine te volgen:

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![Phoenix sqlline van HDInsight hbase][hdinsight-hbase-phoenix-sqlline]

    Hallo-opdrachten in het Hallo-voorbeeld gebruikt:

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

Zie voor meer informatie [SQLLine handmatige](http://sqlline.sourceforge.net/#manual) en [Phoenix grammatica](http://phoenix.apache.org/language/index.html).

## <a name="use-squirrel"></a>SQuirreL gebruiken
[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is een grafische Java-programma dat kunt u tooview Hallo structuur van een JDBC compatibele database, gegevens hello in tabellen bladeren, voert u SQL-opdrachten enzovoort. Het kan gebruikte tooconnect tooApache Phoenix in HDInsight zijn.

Deze sectie leest u hoe tooinstall en SQuirreL configureren op uw werkstation tooconnect tooan HBase-cluster in HDInsight via VPN.

### <a name="prerequisites"></a>Vereisten
Voordat u Hallo procedures uitvoert, moet u Hallo volgende hebben:

* Een HBase-cluster geïmplementeerd tooan virtuele Azure-netwerk met een DNS-virtuele machine.  Zie voor instructies [maken HBase-clusters op Azure Virtual Network][hdinsight-hbase-provision-vnet].

* Hallo HBase-cluster cluster verbindingsspecifiek DNS-achtervoegsel worden opgehaald. tooget het RDP in Hallo-cluster, en voer vervolgens IPConfig.  Hallo DNS-achtervoegsel is vergelijkbaar met:

        myhbase.b7.internal.cloudapp.net
* Download en installeer [Microsoft Visual Studio Express voor Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) op uw werkstation. U moet makecert van Hallo pakket toocreate uw certificaat.  
* Download en installeer [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) op uw werkstation.  SQuirreL SQL clientversie 3.0 en hoger vereist JRE 1.6 of hoger.  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a>Een punt-naar-Site VPN-verbinding toohello virtuele Azure-netwerk configureren
Er zijn 3 stappen voor het configureren van een punt-naar-site VPN-verbinding:

1. [Een virtueel netwerk en een gateway voor dynamische routering configureren](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [Uw certificaten maken](#Create-your-certificates)
3. [Uw VPN-client configureren](#Configure-your-VPN-client)

Zie [configureren van een punt-naar-Site VPN-verbinding tooan Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) voor meer informatie.

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a>Een virtueel netwerk en een gateway voor dynamische routering configureren
U hebt een HBase-cluster in virtueel netwerk van Azure ingericht zorgen (Zie Hallo-vereisten voor deze sectie). de volgende stap Hallo is tooconfigure een punt-naar-site-verbinding.

**tooconfigure hello punt-naar-site-connectiviteit**

1. Meld u aan toohello [klassieke Azure-Portal][azure-portal].
2. Klik aan de linkerkant Hallo op **netwerken**.
3. Klik op Hallo virtuele netwerk dat u hebt gemaakt (Zie [inrichten HBase-clusters op Azure Virtual Network][hdinsight-hbase-provision-vnet]).
4. Klik op **configureren** van Hallo boven.
5. In Hallo **punt-naar-site-connectiviteit** sectie **punt-naar-site-connectiviteit configureren**.
6. Configureer **IP-BEGINADRES** en **CIDR** toospecify Hallo IP-adresbereik waarvan uw VPN-clients een IP-adres ontvangen wanneer verbonden adres. Hallo bereik kan niet overlappen met Hallo bereiken in uw on-premises netwerk en Hallo u verbinding met virtuele Azure-netwerk. Bijvoorbeeld. Als u 10.0.0.0/20 voor Hallo virtueel netwerk hebt geselecteerd, kunt u 10.1.0.0/24 voor Hallo client-adresruimte. Zie Hallo [punt-naar-Site-connectiviteit] [ vnet-point-to-site-connectivity] pagina voor meer informatie.
7. Klik in Hallo virtueel netwerk adres spaties sectie op **gatewaysubnet toevoegen**.
8. Klik op **opslaan** op Hallo onder aan Hallo pagina.
9. Klik op **Ja** tooconfirm Hallo wijzigen. Wacht totdat het Hallo-systeem Hallo wijzigen voordat u doorgaat met de volgende procedure toohello heeft aangebracht.

**toocreate een gateway voor dynamische routering**

1. Hallo klassieke Azure-Portal, klik op **DASHBOARD** van Hallo Hallo pagina bovenaan.
2. Klik op **GATEWAY maken** van Hallo onder Hallo.
3. Klik op **Ja** tooconfirm. Wacht totdat het Hallo-gateway is gemaakt.
4. Klik op **DASHBOARD** van Hallo boven.  Hier ziet u een diagram van het virtuele netwerk Hallo:

    ![Virtuele Azure-netwerk punt-naar-site-diagram][img-vnet-diagram]

    Hallo diagram toont 0 clientverbindingen. Nadat u een verbinding toohello virtueel netwerk, wordt Hallo aantal bijgewerkte tooone zijn.

#### <a name="create-your-certificates"></a>Uw certificaten maken
Eenzijdige toocreate een X.509-certificaat is via Hallo certificaat hulpprogramma voor het maken (makecert.exe) die wordt geleverd met [Microsoft Visual Studio Express voor Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).

**een zelfondertekend basiscertificaat toocreate**

1. Open een opdrachtpromptvenster vanuit uw werkstation.
2. Navigeer map toohello Visual Studio-hulpprogramma's.
3. Hallo volgende opdracht in Hallo in het volgende voorbeeld maakt en installeer een basiscertificaat in Hallo persoonlijke certificaatarchief op uw werkstation en ook maken een cer-bestand dat u later toohello klassieke Azure-Portal gaat uploaden.

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    Toohello map die u Hallo .cer-bestand toobe bevinden zich wilt in, waarbij HBaseVnetVPNRootCertificate Hallo naam dat u toouse voor Hallo certificaat wilt wijzigen.

    Sluit de opdrachtprompt Hallo niet.  U moet deze in de volgende procedure Hallo.

   > [!NOTE]
   > Omdat u een basiscertificaat op basis waarvan clientcertificaten worden gegenereerd hebt gemaakt, kunt u tooexport wilt dat dit certificaat samen met de persoonlijke sleutel en sla het tooa veilige locatie waar deze kunnen worden hersteld.
   >
   >

**een clientcertificaat toocreate**

* Van Hallo dezelfde opdrachtprompt (toobe op Hallo heeft dezelfde computer waarop u Hallo basiscertificaat hebt gemaakt. Hallo-clientcertificaat moet worden gegenereerd vanuit Hallo basiscertificaat), voer hello volgende opdracht:

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    HBaseVnetVPNRootCertificate is certificaatnaam Hallo-hoofdmap.  Toomatch hello hoofdnaam certificaat heeft.  

    Zowel Hallo-basiscertificaat en clientcertificaat Hallo worden opgeslagen in uw persoonlijke certificaatarchief op uw computer. Gebruik certmgr.msc tooverify.

    ![Virtuele Azure-netwerk punt-naar-site VPN-certificaat][img-certificate]

    Een clientcertificaat moet worden geïnstalleerd op elke computer die u wilt dat tooconnect toohello virtueel netwerk. U wordt aangeraden dat u unieke client certificaten voor elke computer maken die u wilt dat tooconnect toohello virtueel netwerk. Hallo clientcertificaten tooexport certmgr.msc gebruiken.

**tooupload hello root certificate toohello klassieke Azure-Portal**

1. Hallo klassieke Azure-Portal, klik op **netwerk** op Hallo links.
2. Klik op Hallo virtueel netwerk waar uw HBase-cluster wordt geïmplementeerd op.
3. Klik op **certificaten** van Hallo boven.
4. Klik op **uploaden** van Hallo onderzijde en u hebt gemaakt in procedure vóór laatste Hallo Hallo basiscertificaatbestand opgeven. Wacht totdat het Hallo-certificaat hebt geïmporteerd.
5. Klik op **DASHBOARD** Hallo bovenaan.  Hallo virtuele diagram toont Hallo status.

#### <a name="configure-your-vpn-client"></a>Uw VPN-client configureren
**toodownload en installeer Hallo VPN-clientpakket**

1. Klik op een van de dashboardpagina Hallo Hallo virtueel netwerk in Hallo snelle weergave sectie **downloaden Hallo 64-bits VPN-clientpakket** of **downloaden Hallo 32-bits VPN-clientpakket** op basis van uw werkstation OS-versie.
2. Klik op **uitvoeren** tooinstall Hallo-pakket.
3. Hallo wordt weergegeven, klikt u op **meer info**, en klik vervolgens op **toch uitvoeren**.
4. Klik op **Ja** twee keer.

**tooconnect tooVPN**

1. Klik op Hallo netwerken pictogram op de taakbalk Hallo op Hallo-bureaublad van uw werkstation. U ziet een VPN-verbinding met de naam van uw virtuele netwerk.
2. Klik op de naam van Hallo VPN-verbinding.
3. Klik op **Verbinden**.

**tootest hello naamomzetting van VPN-verbinding en het domein**

* Open een opdrachtprompt op Hallo-werkstation en ping Hallo na namen Hallo HBase-cluster van DNS-achtervoegsel is myhbase.b7.internal.cloudapp.net:

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a>Installeren en configureren van SQuirreL op uw werkstation
**tooinstall SQuirreL**

1. Hallo SQuirreL SQL client jar bestand downloaden via [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).
2. Hallo openen/uitvoeren jar-bestand. Hiervoor Hallo [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).
3. Klik op **volgende** twee keer.
4. Geef een pad op waar u Hallo schrijftoegang en klik vervolgens op hebt **volgende**.

  > [!NOTE]
  > Hallo standaardinstallatiemap is Hallo C:\Program Files\squirrel-sql-3.6 map.  In de volgorde toowrite toothis pad moet Hallo installatieprogramma Hallo administrator-bevoegdheden worden toegekend. U kunt open een opdrachtprompt als beheerder, navigeer tooJava de bin-map en voer vervolgens:
  >
  >     Java.exe-jar [pad Hallo van Hallo SQuirreL jar-bestand]
5. Klik op **OK** tooconfirm Hallo doelmap maken.
6. de standaardinstelling Hallo is tooinstall Hallo basis en standaard pakketten.  Klik op **Volgende**.
7. Klik op **volgende** tweemaal, en klik vervolgens op **gedaan**.

**tooinstall hello Phoenix stuurprogramma**

Hallo phoenix stuurprogramma jar-bestand bevindt zich op Hallo HBase-cluster. Hallo-pad is vergelijkbaar toohello volgende op basis van Hallo-versies:

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
U moet toocopy het werkstation tooyour onder Hallo [SQuirreL-installatiemap] / lib pad.  Hallo gemakkelijkst tooRDP in Hallo-cluster en gebruik bestand kopiëren en plakken (CTRL + C en CTRL + V) toocopy het tooyour werkstation.

**een stuurprogramma Phoenix tooSQuirreL tooadd**

1. Open SQuirreL SQL-Client op uw werkstation.
2. Klik op Hallo **stuurprogramma** tabblad op Hallo links.
3. Van Hallo **stuurprogramma's** menu, klikt u op **nieuw stuurprogramma**.
4. Voer Hallo volgende informatie:

   * **Naam**: Phoenix
   * **Voorbeeld-URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net
   * **Klassenaam**: org.apache.phoenix.jdbc.PhoenixDriver

     > [!WARNING]
     > Gebruiker alle kleine letters in Hallo voorbeeld-URL. U kunt gebruiken ze volledig zookeeper quorum als een ervan is niet beschikbaar.  Hallo hostnamen zijn zookeeper0, zookeeper1 en zookeeper2.
     >
     >

     ![HDInsight HBase Phoenix SQuirreL stuurprogramma][img-squirrel-driver]
5. Klik op **OK**.

**toocreate een alias toohello HBase-cluster**

1. Klik op Hallo van SQuirreL, **aliassen** tabblad op Hallo links.
2. Van Hallo **aliassen** menu, klikt u op **Alias voor nieuwe**.
3. Voer Hallo volgende informatie:

   * **Naam**: Hallo-naam van Hallo HBase-cluster of een willekeurige naam die u liever.
   * **Stuurprogramma**: Phoenix.  Dit moet overeenkomen met de naam stuurprogramma Hallo die u hebt gemaakt in de laatste procedure Hallo.
   * **URL**: Hallo-URL is gekopieerd uit uw stuurprogrammaconfiguratie van het. Zorg ervoor dat toouser alle kleine letters.
   * **Gebruikersnaam**: deze tekst kan worden.  Omdat u hier VPN-verbinding gebruiken, wordt helemaal Hallo gebruikersnaam niet gebruikt.
   * **Wachtwoord**: deze tekst kan worden.

     ![HDInsight HBase Phoenix SQuirreL stuurprogramma][img-squirrel-alias]
4. Klik op **Test**.
5. Klik op **Verbinden**. Wanneer het Hallo-verbinding maakt, wordt de SQuirreL ziet:

    ![HBase Phoenix SQuirreL][img-squirrel]

**een test toorun**

1. Klik op Hallo **SQL** tabblad rechts volgende toohello **objecten** tabblad.
2. Kopieer en plak de volgende code Hallo:

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. Klik op Hallo uitvoeren.

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. Overschakelen back toohello **objecten** tabblad.
5. Vouw de aliasnaam Hallo uit en vouw vervolgens **tabel**.  U ziet de nieuwe tabel Hallo vermeld in.

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe toouse Apache Phoenix in HDInsight.  toolearn meer, Zie

* [Overzicht van HDInsight HBase][hdinsight-hbase-overview]: HBase is een Apache, open-source NoSQL-database op basis van Hadoop. HBase biedt willekeurige toegang en een sterke consistentie voor grote hoeveelheden ongestructureerde en semigestructureerde gegevens.
* [HBase-clusters op Azure Virtual Network inrichten][hdinsight-hbase-provision-vnet]: aan de integratie van virtueel netwerk, HBase-clusters geïmplementeerde toohello virtuele netwerk als uw toepassingen zodat kunnen worden dat toepassingen met communiceren kunnen Rechtstreeks HBase.
* [Configureren van replicatie van HBase in HDInsight](hdinsight-hbase-replication.md): meer informatie over hoe tooconfigure HBase-replicatie tussen twee Azure-datacenters.
* [Twitter-gevoel met HBase in HDInsight analyseren][hbase-twitter-sentiment]: meer informatie over hoe toodo realtime [gevoel analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) van big data met behulp van HBase in een Hadoop-cluster in HDInsight.

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
