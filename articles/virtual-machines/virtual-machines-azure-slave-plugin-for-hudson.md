---
title: aaaHow toouse hello Azure slave invoegtoepassing met Hudson continue integratie | Microsoft Docs
description: Hierin wordt beschreven hoe toouse hello Azure slave invoegtoepassing met Hudson continue integratie.
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a>Hoe toouse hello Azure slave invoegtoepassing met Hudson continue integratie
Hello Azure slave invoegtoepassing voor Hudson kunt u tooprovision slave knooppunten op Azure bij het uitvoeren van gedistribueerde bouwt.

## <a name="install-hello-azure-slave-plug-in"></a>Hello Azure Slave invoegtoepassing installeren
1. In Hallo Hudson dashboard, klikt u op **Hudson beheren**.
2. In Hallo **beheren Hudson** pagina, klikt u op **invoegtoepassingen beheren**.
3. Klik op Hallo **beschikbaar** tabblad.
4. Klik op **Search** en het type **Azure** toolimit Hallo lijst toorelevant invoegtoepassingen.
   
    Als u ervoor tooscroll door Hallo lijst met beschikbare invoegtoepassingen kiezen, vindt u hello Azure slave invoegtoepassing onder Hallo **Clusterbeheer en gedistribueerd bouwen** sectie in Hallo **anderen** tabblad.
5. Schakel dit selectievakje in Hallo voor **Azure Slave invoegtoepassing**.
6. Klik op **Install**.
7. Opnieuw opstarten Hudson.

Nu die Hallo invoegtoepassing is geïnstalleerd, zou de volgende stappen Hallo tooconfigure Hallo invoegtoepassing met uw Azure-abonnement profiel en een sjabloon die wordt gebruikt bij het maken van Hallo VM voor Hallo slave knooppunt toocreate zijn.

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a>Hello Azure Slave invoegtoepassing configureren met het profiel van uw abonnement
Een profiel abonnement ook waarnaar wordt verwezen tooas publicatie-instellingen, is een XML-bestand met beveiligde referenties en aanvullende informatie moet u toowork met Azure in uw ontwikkelomgeving. tooconfigure hello Azure slave invoegtoepassing, moet u de:

* Uw abonnements-id
* Een beheercertificaat voor uw abonnement

Deze vindt u in uw [abonnement profiel]. Hieronder volgt een voorbeeld van een profiel voor een abonnement.

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

Zodra u het profiel van uw abonnement hebt, volgt u deze stappen tooconfigure hello Azure slave invoegtoepassing.

1. In Hallo Hudson dashboard, klikt u op **Hudson beheren**.
2. Klik op **systeem configureren**.
3. Schuif omlaag Hallo pagina toofind hello **Cloud** sectie.
4. Klik op **toevoegen van nieuwe cloud > Microsoft Azure**.
   
    ![toevoegen van nieuwe cloud][add new cloud]
   
    Hier ziet uw abonnementsgegevens Hallo velden waar u tooenter nodig.
   
    ![profiel configureren][configure profile]
5. Kopiëren Hallo abonnements-id en het beheer van het certificaat uit het profiel van uw abonnement en plak deze in de juiste velden Hallo.
   
    Bij het kopiëren van Hallo abonnement-id en het beheer certificaat **niet** Hallo aanhalingstekens die Hallo-waarden insluiten bevatten.
6. Klik op **controleren configuratie**.
7. Wanneer het Hallo-configuratie is geverifieerd, klikt u op **opslaan**.

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a>Een virtuele machine-sjabloon voor hello Azure Slave invoegtoepassing instellen
Een sjabloon voor virtuele machines Hallo parameters definieert Hallo invoegtoepassing gebruikt toocreate een knooppunt slave op Azure. In de volgende stappen uit Hallo maakt we sjabloon voor een Ubuntu VM.

1. In Hallo Hudson dashboard, klikt u op **Hudson beheren**.
2. Klik op **systeem configureren**.
3. Schuif omlaag Hallo pagina toofind hello **Cloud** sectie.
4. Binnen Hallo **Cloud** sectie, zoeken **Azure virtuele Machine-sjabloon toevoegen** en klik op Hallo **toevoegen** knop.
   
    ![vm-sjabloon toevoegen][add vm template]
5. Geef de naam van een cloudservice in Hallo **naam** veld. Als Hallo-naam die u opgeeft tooan bestaande cloudservice verwijst, worden Hallo VM ingericht in die service. Azure wordt anders maakt u een nieuwe.
6. In Hallo **beschrijving** en voer de tekst die beschrijft Hallo-sjabloon die u maakt. Deze informatie wordt alleen gebruikt voor administratieve doeleinden en wordt niet gebruikt in een VM-inrichting.
7. In Hallo **Labels** veld **linux**. Dit label is gebruikte tooidentify Hallo sjabloon die u maakt en vervolgens gebruikte tooreference Hallo sjabloon bij het maken van een taak Hudson.
8. Selecteer een regio waar Hallo VM wordt gemaakt.
9. Selecteer de relevante VM-grootte Hallo.
10. Geef een opslagaccount waar Hallo VM wordt gemaakt. Zorg ervoor dat deze zich in Hallo dezelfde regio als Hallo cloudservice die u wilt gebruiken. Als u nieuwe opslag toobe gemaakt wilt, kunt u dit veld leeg laten.
11. Bewaartijd geeft het aantal minuten op voordat Hudson wordt verwijderd als een niet-actieve slave Hallo. Dit laat de standaardwaarde Hallo van 60.
12. In **gebruik**, selecteer welke voorwaarde Hallo wanneer dit knooppunt slave wordt gebruikt. Selecteer nu **gebruikmaken van dit knooppunt zo veel mogelijk**.
    
     Op dit moment eruit uw formulier enigszins vergelijkbaar toothis:
    
     ![De sjabloonconfiguratie][template config]
13. In **installatiekopie familie-Id of** hebt toospecify welke installatiekopie wordt geïnstalleerd op de virtuele machine. U kunt selecteren in een lijst van families van de afbeelding of geef een aangepaste installatiekopie.
    
     Als u tooselect uit een lijst met installatiekopie families wilt, Voer Hallo eerste teken (hoofdlettergevoelig) van familienaam Hallo-installatiekopie. Voor het exemplaar typen **U** verschijnt nu een lijst met Ubuntu Server families. Wanneer u in de lijst hello selecteert, Jenkins Hallo meest recente versie van deze installatiekopie van die familie gebruikt bij het inrichten van uw virtuele machine.
    
     ![Lijst met familie van besturingssystemen][OS family list]
    
     Als u een aangepaste installatiekopie dat u wilt dat toouse in plaats daarvan hebt, Voer Hallo-naam van de aangepaste installatiekopie. Afbeelding van aangepaste namen worden niet weergegeven in een lijst zodat u tooensure die Hallo naam correct is ingevoerd.    
    
     Typ voor deze zelfstudie **U** toobring een lijst weergegeven van Ubuntu-installatiekopieën en selecteer **Ubuntu Server 14.04 TNS**.
14. Voor **methode starten**, selecteer **SSH**.
15. Hallo onderstaande script kopiëren en plakken op Hallo **Init script** veld.
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     Hallo **Init script** worden uitgevoerd na Hallo virtuele machine wordt gemaakt. In dit voorbeeld installeert Hallo script Java, git en ant.
16. In Hallo **gebruikersnaam** en **wachtwoord** velden, voert u de gewenste waarden voor Hallo administrator-account dat wordt gemaakt op de virtuele machine.
17. Klik op **sjabloon controleren** toocheck als Hallo-parameters die u hebt opgegeven geldig zijn.
18. Klik op **Opslaan**.

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a>Een taak Hudson die wordt uitgevoerd op een lager niveau bevindende-knooppunt in Azure maken
In deze sectie maakt u een Hudson-taak die wordt uitgevoerd op een knooppunt slave op Azure.

1. In Hallo Hudson dashboard, klikt u op **nieuwe taak**.
2. Voer een naam voor de Hallo-taak die u maakt.
3. Selecteer Hallo taaktype **bouwen van een taak vrije-stijl software**.
4. Klik op **OK**.
5. Selecteer in de taak configuratiepagina Hallo **beperken waar dit project kan worden uitgevoerd**.
6. Selecteer **knooppunt en label menu** en selecteer **linux** (we opgegeven dit label bij het maken van virtuele-machinesjabloon Hallo in de vorige sectie Hallo).
7. In Hallo **bouwen** sectie, klikt u op **toevoegen build stap** en selecteer **shell uitvoeren**.
8. Hallo script volgen en vervangt bewerken **{uw github-accountnaam}**, **{projectnaam van uw}**, en **{uw projectmap}** met waarden nodig en Hallo plakken bewerkt script Hallo tekst in die wordt weergegeven.
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. Klik op **Opslaan**.
10. In Hallo Hudson dashboard, zoek de Hallo-taak die u zojuist hebt gemaakt en klik op Hallo **plannen van een build** pictogram.

Hudson vervolgens maakt u een lager niveau bevindende knooppunt met Hallo-sjabloon is gemaakt in de vorige sectie Hallo en Hallo-script die u hebt opgegeven in Hallo build stap voor deze taak uitvoeren.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[abonnement profiel]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

