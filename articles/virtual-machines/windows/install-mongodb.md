---
title: aaaInstall MongoDB op een Windows-virtuele machine in Azure | Microsoft Docs
description: Meer informatie over hoe tooinstall MongoDB op een Azure-virtuele machine met Windows Server 2012 R2 is gemaakt met Hallo Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a>Installeren en configureren van MongoDB op een Windows-VM in Azure
[MongoDB](http://www.mongodb.org) is een populaire open-source, hoogwaardige NoSQL-database. In dit artikel begeleidt u bij het installeren en configureren van MongoDB op een Windows Server 2012 R2 virtual machine (VM) in Azure. U kunt ook [MongoDB installeren op een Linux VM in Azure](../linux/install-mongodb.md).

## <a name="prerequisites"></a>Vereisten
Voordat u installeren en configureren van MongoDB, u moet toocreate een virtuele machine en, in het ideale geval een schijf gegevens tooit toevoegen. Zie Hallo artikelen toocreate een virtuele machine te volgen en een gegevensschijf toevoegen:

* Maak een Windows Server-VM met [hello Azure-portal](quick-create-portal.md) of [Azure PowerShell](quick-create-powershell.md).
* Koppel een gegevens schijf tooa Windows Server-VM met [hello Azure-portal](attach-managed-disk-portal.md) of [Azure PowerShell](attach-disk-ps.md).

toobegin installeren en configureren van MongoDB, [tooyour VM van Windows Server aanmelden](connect-logon.md) met behulp van extern bureaublad.

## <a name="install-mongodb"></a>MongoDB installeren
> [!IMPORTANT]
> Beveiligingsfuncties van MongoDB, zoals verificatie en IP-adresbinding zijn niet standaard ingeschakeld. Beveiligingsfuncties moeten worden ingeschakeld voordat u MongoDB tooa productieomgeving implementeert. Zie voor meer informatie [MongoDB-beveiliging en verificatie](http://www.mongodb.org/display/DOCS/Security+and+Authentication).


1. Nadat u verbinding hebt met het tooyour VM maken met extern bureaublad, Internet Explorer openen vanuit Hallo **Start** menu op Hallo VM.
2. Selecteer **aanbevolen instellingen voor beveiliging, privacy en compatibiliteit gebruiken** wanneer Internet Explorer eerst wordt geopend en klik op **OK**.
3. Verbeterde beveiliging van Internet Explorer is standaard ingeschakeld. Hallo MongoDB website toohello lijst met toegestane websites toevoegen:
   
   * Selecteer Hallo **extra** pictogram in de rechterbovenhoek Hallo.
   * In **Internetopties**, selecteer Hallo **beveiliging** tabblad en selecteer vervolgens Hallo **vertrouwde websites** pictogram.
   * Klik op Hallo **Sites** knop. Voeg *https://\*. mongodb.org* toohello lijst met vertrouwde sites en het dialoogvenster sluit Hallo.
     
     ![Instellingen van Internet Explorer configureren](./media/install-mongodb/configure-internet-explorer-security.png)
4. Blader toohello [MongoDB - Downloads](http://www.mongodb.org/downloads) pagina (http://www.mongodb.org/downloads).
5. Selecteer, indien nodig Hallo **Community Server** edition en selecteer vervolgens Hallo nieuwste huidige stabiele release voor Windows Server 2008 R2 64-bits of hoger. toodownload Hallo installatieprogramma, klikt u op **downloaden (msi)**.
   
    ![MongoDB-installatieprogramma downloaden](./media/install-mongodb/download-mongodb.png)
   
    Voer Hallo installatieprogramma als Hallo downloaden voltooid is.
6. Lees en accepteer de gebruiksrechtovereenkomst Hallo. Wanneer u wordt gevraagd, selecteert u **Complete** installeren.
7. Klik op het laatste scherm hello, **installeren**.

## <a name="configure-hello-vm-and-mongodb"></a>Hallo VM en MongoDB configureren
1. Hallo-padvariabelen worden niet bijgewerkt door Hallo MongoDB installer. Zonder Hallo MongoDB `bin` locatie in de variabele path, moet u toospecify Hallo volledig pad telkens wanneer u een uitvoerbaar bestand van MongoDB gebruiken. tooadd hello locatie tooyour padvariabele:
   
   * Klik met de rechtermuisknop Hallo **Start** menu en selecteer **System**.
   * Klik op **Geavanceerde systeeminstellingen**, en klik vervolgens op **omgevingsvariabelen**.
   * Onder **systeemvariabelen**, selecteer **pad**, en klik vervolgens op **bewerken**.
     
     ![Padvariabelen configureren](./media/install-mongodb/configure-path-variables.png)
     
     Toevoegen van Hallo pad tooyour MongoDB `bin` map. MongoDB wordt doorgaans geïnstalleerd in *C:\Program Files\MongoDB*. Controleer of Hallo-installatiepad op de virtuele machine. Hallo volgende voorbeeld wordt toegevoegd Hallo standaard MongoDB installeren locatie toohello `PATH` variabele:
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > Ervoor tooadd Hallo toonaangevende puntkomma worden (`;`) toe te voegen een locatie tooyour tooindicate `PATH` variabele.

2. MongoDB-gegevens en logboekbestanden mappen op de gegevensschijf van uw maken. Van Hallo **Start** selecteert u **opdrachtprompt**. Hallo volgen voorbeelden maken Hallo mappen op station F:
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. Start een MongoDB-exemplaar met Hallo de volgende opdracht, Hallo pad tooyour gegevens aanpassen en meld u mappen dienovereenkomstig:
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    Het kan enkele minuten duren voordat MongoDB tooallocate Hallo journaal bestanden en beginnen met luisteren voor verbindingen. Alle berichten in het logboek zijn gerichte toohello *F:\MongoLogs\mongolog.log* opslaan als `mongod.exe` server wordt gestart en wijst journaal-bestanden.
   
   > [!NOTE]
   > Hallo-opdrachtprompt blijft gericht zijn op deze taak terwijl het MongoDB-exemplaar wordt uitgevoerd. Laat Hallo opdrachtprompt venster open toocontinue met MongoDB. Of MongoDB installeren als service, zoals beschreven in de volgende stap Hallo.

4. Installeer voor een meer robuuste MongoDB-ervaring Hallo `mongod.exe` als een service. Een service maakt, dat u hoeft niet tooleave een opdrachtprompt uitgevoerd elke keer dat u wilt dat toouse MongoDB. Hallo service maken als volgt Hallo pad tooyour gegevens en logboekbestanden mappen dienovereenkomstig aanpassen:
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    Hallo voorgaande opdracht maakt u een service met de naam MongoDB, met een beschrijving van "DB met Mongo". volgende parameters Hallo worden ook opgegeven:
   
   * Hallo `--dbpath` optie geeft u op Hallo-locatie van map Hallo-gegevens.
   * Hallo `--logpath` optie moet gebruikte toospecify een logboekbestand, omdat de actieve service Hallo geen toodisplay uitvoer van een venster.
   * Hallo `--logappend` optie geeft u uitvoer tooappend toohello bestaande logboekbestand zorgt ervoor dat Hallo-service opnieuw wordt opgestart.
   
   toostart hello MongoDB-service, Hallo volgende opdracht uitvoeren:
   
    ```
    net start MongoDB
    ```
   
    Zie voor meer informatie over het maken van Hallo MongoDB service [configureren van een Windows-Service voor MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).

## <a name="test-hello-mongodb-instance"></a>Test Hallo MongoDB-exemplaar
Met MongoDB uitgevoerd als één exemplaar of als een service is geïnstalleerd, kunt u nu starten maken en gebruiken van uw databases. toostart hello beheerdersrechten MongoDB-shell, een ander opdrachtpromptvenster openen vanuit Hallo **Start** menu en voer de volgende opdracht Hallo:

```
mongo  
```

Hallo-databases met Hallo aanbieden `db` opdracht. Voeg enkele gegeven als volgt:

```
db.foo.insert( { a : 1 } )
```

Zoek naar gegevens als volgt:

```
db.foo.find()
```

Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

Exit Hallo `mongo` console als volgt:

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a>Netwerkbeveiligingsgroep regels en firewall configureren
Nu dat MongoDB geïnstalleerd en wordt uitgevoerd is, opent u een poort in Windows Firewall zodat u tooMongoDB op afstand verbinding kan maken. toocreate een nieuwe regel voor binnenkomende verbindingen tooallow TCP-poort 27017, open een administratieve PowerShell-prompt en voert u Hallo volgende opdracht:

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

U kunt ook Hallo regel maken met behulp van Hallo **Windows Firewall met geavanceerde beveiliging** grafisch beheerprogramma. Maak een nieuwe regel voor binnenkomende verbindingen tooallow TCP-poort 27017.

Maak een Netwerkbeveiligingsgroep regel tooallow toegang tooMongoDB van buiten een bestaand virtueel netwerk van Azure-subnet Hallo indien nodig. U kunt Hallo Netwerkbeveiligingsgroep regels maken met behulp van Hallo [Azure-portal](nsg-quickstart-portal.md) of [Azure PowerShell](nsg-quickstart-powershell.md). Net als bij Hallo Windows Firewall-regels, kunt u TCP-poort 27017 toohello virtuele netwerkinterface van de MongoDB-VM.

> [!NOTE]
> TCP-poort 27017 is Hallo standaardpoort die wordt gebruikt door MongoDB. U kunt deze poort wijzigen met behulp van Hallo `--port` parameter bij het starten van `mongod.exe` handmatig of via een service. Als u poort Hallo wijzigt, moet u ervoor dat tooupdate Hallo Windows Firewall- en Netwerkbeveiligingsgroep regels in de vorige stappen Hallo.


## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd hoe tooinstall en MongoDB configureren op uw Windows-VM. U kunt nu toegang tot MongoDB op uw Windows-VM door na Hallo geavanceerde onderwerpen in Hallo [MongoDB-documentatie](https://docs.mongodb.com/manual/).

