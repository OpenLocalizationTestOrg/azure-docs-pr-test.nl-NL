---
title: een virtuele Machine van Azure aaaEncrypt | Microsoft Docs
description: Dit document helpt u een virtuele Machine van Azure tooencrypt na de ontvangst van een waarschuwing van Azure Security Center.
services: security, security-center
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: 
ms.assetid: f6c28bc4-1f79-4352-89d0-03659b2fa2f5
ms.service: security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/15/2017
ms.author: tomsh
ms.openlocfilehash: 7c7c6eed39d16bde8a0dfaffe3a3331c58101634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-an-azure-virtual-machine"></a>Een virtuele machine van Azure versleutelen
Het Azure Beveiligingscentrum stuurt u een waarschuwingsbericht wanneer u virtuele machines hebt die niet versleuteld zijn. Deze waarschuwingen wordt weergegeven als hoog Dreigingsniveau en Hallo aanbeveling is tooencrypt deze virtuele machines.

![Aanbevelingen voor schijfversleuteling](./media/security-center-disk-encryption/security-center-disk-encryption-fig1.png)

> [!NOTE]
> Hallo-informatie in dit document is van toepassing tooencrypting virtuele machines zonder gebruik van een coderingssleutel Key (dit is vereist voor back-ups van virtuele machines maken met Azure Backup). Zie artikel Hallo [Azure Disk Encryption for Windows en Linux Azure Virtual Machines](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) voor meer informatie over toouse een coderingssleutel Key toosupport Azure Backup voor versleutelde Azure Virtual Machines.
>
>

Azure Virtual Machines die zijn geïdentificeerd door Azure Security Center welke tooencrypt, raden we Hallo stappen te volgen:

* Installeer en configureer Azure PowerShell. Hierdoor kunt u toorun Hallo PowerShell-opdrachten vereist tooset up Hallo vereisten vereist tooencrypt Azure Virtual Machines.
* Verkrijgen en hello Azure schijf versleuteling vereisten Azure PowerShell-script uitvoeren
* Versleutel uw virtuele machines

Hallo-doel van dit document is tooenable tooencrypt u uw virtuele machines, zelfs als er weinig tot geen kennis in Azure PowerShell.
Dit document wordt ervan uitgegaan dat u gebruikmaakt van Windows 10 als clientmachine Hallo waarin u Azure Disk Encryption configureren.

Er zijn veel manieren die gebruikt toosetup Hallo vereisten en tooconfigure versleuteling voor Azure Virtual Machines worden kunnen. Als u al goed bekend bent met Azure PowerShell of Azure CLI, kunt u alternatieve methoden toouse mogelijk liever.

> [!NOTE]
> Zie toolearn meer informatie over andere manieren tooconfiguring versleuteling voor Azure virtual machines [Azure Disk Encryption for Windows en Linux Azure Virtual Machines](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).
>
>

## <a name="install-and-configure-azure-powershell"></a>Azure PowerShell installeren en configureren
Azure PowerShell-versie 1.2.1 of hoger moet op uw computer geïnstalleerd zijn. Hallo artikel [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) bevat alle Hallo stappen u moet tooprovision van uw computer toowork met Azure PowerShell. de eenvoudigste manier Hallo is toouse Hallo Web PI installatie benadering die in dit artikel worden vermeld. Zelfs als u al hebt Azure PowerShell geïnstalleerd, installeert u opnieuw met Hallo Web PI benadering, zodat u de meest recente versie van Azure PowerShell Hallo hebt.

## <a name="obtain-and-run-hello-azure-disk-encryption-prerequisites-configuration-script"></a>Verkrijgen en vereisten voor Azure disk encryption Hallo configuratiescript uitvoeren
Hallo configuratiescript met Azure schijf versleuteling vereisten stelt alle Hallo vereisten voor het versleutelen van uw Azure Virtual Machines.

1. Ga toohello GitHub-pagina met Hallo [Azure schijf versleuteling installatiescript voor vereisten](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
2. Klik op de Github-pagina Hallo Hallo **Raw** knop.
3. Gebruik **CTRL-A** tooselect alle tekst op de pagina Hallo Hallo en gebruik vervolgens **CTRL-C** toocopy alle tekst op Hallo pagina toohello Klembord Hallo.
4. Open **Kladblok** en plak de tekst hello gekopieerd in Kladblok.
5. Maak een nieuwe map op uw C:-schijf met de naam **AzureADEScript**.
6. Sla het Kladblok-bestand Hallo: klik op **bestand**, klikt u vervolgens op **OpslaanAls**. Voer in Hallo tekstvak Bestandsnaam de naam **"ADEPrereqScript.ps1"** en klik op **opslaan**. (Zorg ervoor dat u plaats Hallo aanhalingstekens rond Hallo-naam, anders wordt het Hallo-bestand opgeslagen met een bestandsextensie .txt).

Nu dat Hallo script inhoud is opgeslagen, opent u Hallo script in Hallo PowerShell ISE:

1. Klik in het Menu Start hello, **Cortana**. Vraag **Cortana** "PowerShell" door te typen **PowerShell** in het zoekvak Hallo.
2. Klik met de rechtermuisknop op **Windows PowerShell ISE** en klik op **Als administrator uitvoeren**.
3. In Hallo **Administrator: Windows PowerShell ISE** venster, klikt u op **weergave** en klik vervolgens op **scriptvenster weergeven**.
4. Als u Hallo ziet **opdrachten** deelvenster aan de rechterkant Hallo van Hallo-venster, klikt u op Hallo **'x'** in Hallo rechtsboven Hallo deelvenster tooclose deze. Als de tekst hello te klein voor u toosee is, gebruikt u **CTRL + het plus** ('Add' hello is ' + ' melden). Als de tekst hello te groot is, gebruikt u **CTRL + het min** (aftrekken is Hallo '-' aanmelding).
5. Klik op **Bestand** en vervolgens op **Openen**. Navigeer toohello **C:\AzureADEScript** map en Hallo Dubbelklik op Hallo **ADEPrereqScript**.
6. Hallo **ADEPrereqScript** inhoud wordt nu weergegeven in de PowerShell ISE Hallo en gekleurde toohelp u verschillende onderdelen, zoals opdrachten, parameters en variabelen makkelijker te zien is.

U ziet nu ongeveer Hallo afbeelding hieronder.

![PowerShell ISE-venster](./media/security-center-disk-encryption/security-center-disk-encryption-fig2.png)

het bovenste deelvenster Hallo is waarnaar wordt verwezen tooas Hallo 'scriptvenster' en Hallo onderste deelvenster is waarnaar wordt verwezen tooas Hallo 'console'. Deze termen zullen we verderop in dit artikel gebruiken.

## <a name="run-hello-azure-disk-encryption-prerequisites-powershell-command"></a>Hello Azure disk encryption vereisten PowerShell-opdracht uitvoeren
Vereisten voor Azure Disk Encryption script Hello wordt u gevraagd voor Hallo informatie te volgen nadat u bent Hallo script begonnen:

* **De Resourcegroepnaam** - naam van de resourcegroep die u wilt dat tooput Hallo Hallo Sleutelkluis in.  Een nieuwe resourcegroep met de Hallo-naam die u invoert wordt gemaakt als er niet al een met die naam gemaakt. Als u al een resourcegroep die u wilt dat toouse in dit abonnement hebt, voert u Hallo-naam van die resourcegroep.
* **Naam Sleutelkluis** -naam van Hallo Sleutelkluis waar versleutelingssleutels in sleutels toobe geplaatst worden. Als u nog geen Key Vault hebt met de door u ingevulde naam bestaat, wordt deze aangemaakt. Als u al een Sleutelkluis die u toouse wilt, Voer Hallo-naam van bestaande Sleutelkluis Hallo.
* **Locatie** -locatie van Hallo Sleutelkluis. Zorg ervoor dat Hallo Sleutelkluis en de virtuele machines toobe versleuteld in Hallo dezelfde locatie. Als u niet Hallo locatie weet, er zijn stappen verderop in dit artikel waarin wordt uitgelegd hoe u toofind uit.
* **Azure Active Directory-toepassingsnaam** -naam van hello Azure Active Directory-toepassing die wordt gebruikt toowrite geheimen toohello Sleutelkluis. Als er nog geen toepassing met deze naam bestaat, wordt deze aangemaakt. Als u al een Azure Active Directory-toepassing die u toouse wilt hebt, Voer Hallo-naam van die Azure Active Directory-toepassing.

> [!NOTE]
> Als u dit als toowhy interessant moet u een Azure Active Directory-toepassing, toocreate Zie *een toepassing registreren met Azure Active Directory* in Hallo artikel [aan de slag met Azure Key Vault](../key-vault/key-vault-get-started.md).
>
>

Voer Hallo stappen tooencrypt een virtuele Machine van Azure te volgen:

1. Als u Hallo PowerShell ISE hebt gesloten, opent u Hallo PowerShell ISE dan met verhoogde bevoegdheid. Volg Hallo-instructies eerder in dit artikel als Hallo die PowerShell ISE nog niet is geopend. Als u Hallo script hebt gesloten, open vervolgens Hallo **ADEPrereqScript.ps1** te klikken op **bestand**, klikt u vervolgens **openen** en Hallo script selecteren in Hallo **c:\ AzureADEScript** map. Als u dit artikel hebt gevolgd van Hallo begin, ga dan verder op de volgende stap toohello.
2. Wijzigen in de console Hallo Hallo PowerShell ISE (onderste deelvenster Hallo Hallo PowerShell ISE) Hallo focus toohello lokale van Hallo script door te typen **cd c:\AzureADEScript** en druk op **ENTER**.
3. Hallo-uitvoeringsbeleid op uw computer zo instellen dat u kunt Hallo-script uitvoeren. Type **Set-ExecutionPolicy Unrestricted** in de console Hallo en druk op ENTER. Als u een dialoogvenster om te informeren over Hallo gevolgen van het beleid voor Hallo wijziging tooexecution ziet, klik op **Ja tooall** of **Ja** (als u ziet **Ja tooall**, selecteert u die optie – als u ziet geen **Ja tooall**, klikt u vervolgens op **Ja**).
4. Meld u aan bij uw Azure-account. Typ in het Hallo-console **Login-AzureRmAccount** en druk op **ENTER**. Een dialoogvenster weergegeven waarin u uw referenties invoeren (Zorg ervoor dat u hebt rechten toochange Hallo virtuele machines-als u geen rechten hebt, u zich niet kunnen tooencrypt ze. Als u niet weet of u bevoegd bent, neem dan contact op met de eigenaar van uw abonnement of uw beheerder). U ziet nu informatie over uw **omgeving**, **account**, **tenant-ID**, **abonnements-ID** en **huidige opslagaccount**. Kopiëren Hallo **SubscriptionId** tooNotepad. U moet toouse dit in stap &#6;.
5. Welk abonnement uw virtuele machine vinden tooand behoort de locatie. Ga te[https://portal.azure.com](ttps://portal.azure.com) en zich aanmelden.  Klik op Hallo linkerkant van de pagina hello, **virtuele Machines**. U ziet een lijst van de virtuele machines en het Hallo-abonnementen waartoe ze behoren.

   ![Virtuele machines](./media/security-center-disk-encryption/security-center-disk-encryption-fig3.png)
6. PowerShell ISE toohello retourneren. Stel Hallo abonnementscontext waarin Hallo script wordt uitgevoerd. Typ in het Hallo-console **Select-AzureRmSubscription – SubscriptionId < your_subscription_Id >** (Vervang **< your_subscription_Id >** met uw abonnements-ID) en druk op  **Voer**. Ziet u informatie over het Hallo-omgeving, **Account**, **TenantId**, **SubscriptionId** en **huidige Opslagaccount**.
7. U bent nu klaar toorun Hallo script. Klik op Hallo **-Script uitvoeren** of drukt u op **F5** op Hallo toetsenbord.

   ![Het PowerShell-script uitvoeren](./media/security-center-disk-encryption/security-center-disk-encryption-fig4.png)
8. Hallo script vraagt om **resourceGroupName:** -Geef de naam Hallo van *resourcegroep* gewenste toouse, drukt u vervolgens op **ENTER**. Als u nog geen hebt, voer een naam die u voor een nieuwe toouse wilt instellen. Als u al een *resourcegroep* die u toouse (zoals Hallo een uw virtuele machine), voer de naam Hallo Hallo bestaande resourcegroep.
9. Hallo script vraagt om **keyVaultName:** -Voer de naam Hallo Hallo *Sleutelkluis* u wilt dat toouse en druk op ENTER. Als u nog geen hebt, voer een naam die u voor een nieuwe toouse wilt instellen. Als u al een Sleutelkluis die u toouse wilt hebt, Voer Hallo-naam van bestaande Hallo *Sleutelkluis*.
10. Hallo script vraagt om **locatie:** : Voer de naam Hallo Hallo locatie in welke Hallo gewenste tooencrypt VM zich bevindt en druk op **ENTER**. Als u niet meer Hallo locatie weet, gaat u terug toostep #5.
11. Hallo script vraagt om **aadAppName:** -Voer de naam Hallo Hallo *Azure Active Directory* toepassing die u wilt dat toouse, drukt u vervolgens op **ENTER**. Als u nog geen hebt, voer een naam die u voor een nieuwe toouse wilt instellen. Als u al een *Azure Active Directory-toepassing* u wilt dat toouse, Voer Hallo-naam van bestaande Hallo *Azure Active Directory-toepassing*.
12. Een aanmeldvenster wordt weergegeven. Geef uw referenties (Ja, u zich eenmaal hebt aangemeld, maar u moet nu toodo nogmaals).
13. Hallo-script wordt uitgevoerd en als voltooid, wordt u gevraagt toocopy Hallo waarden Hallo **aadClientID**, **aadClientSecret**, **diskEncryptionKeyVaultUrl**, en **keyVaultResourceId**. Elk van deze waarden toohello Klembord Kopieer en plak deze in Kladblok.
14. Toohello PowerShell ISE terug en plaatst u Hallo cursor aan einde van de laatste regel Hallo en druk op Hallo **ENTER**.

Hallo-uitvoer van Hallo script ziet er ongeveer als welkomstscherm hieronder:

![PowerShell-resultaat](./media/security-center-disk-encryption/security-center-disk-encryption-fig5.png)

## <a name="encrypt-hello-azure-virtual-machine"></a>Hallo virtuele machine van Azure versleutelen
U bent nu klaar tooencrypt uw virtuele machine. Als uw virtuele machine zich bevindt in Hallo dezelfde resourcegroep als uw Sleutelkluis, kunt u toohello versleuteling stappen sectie gaan. Als uw virtuele machine zich niet in hello dezelfde resourcegroep als uw Sleutelkluis, moet u tooenter Hallo volgende in Hallo-console in Hallo PowerShell ISE:

**$resourceGroupName = <’Virtual_Machine_RG’>**

Vervang **< Virtual_Machine_RG >** met Hallo-naam van resourcegroep Hallo waarin uw virtuele machines zijn opgenomen, tussen enkele aanhalingstekens. Druk vervolgens op **ENTER**.
tooconfirm die Hallo juiste naam van de resourcegroep hebt ingevoerd, typt u Hallo volgende Hallo PowerShell ISE-console:

**$resourceGroupName**

Druk op **ENTER**. U ziet Hallo-naam van resourcegroep die uw virtuele machines zich bevinden in. Bijvoorbeeld:

![PowerShell-resultaat](./media/security-center-disk-encryption/security-center-disk-encryption-fig6.png)

### <a name="encryption-steps"></a>Stappen voor het versleutelen
Eerst moet u de naam van de Hallo PowerShell tootell van Hallo virtuele machine die u wilt tooencrypt. Typ in het Hallo-console:

**$vmName = <’your_vm_name’>**

Vervang **<'your_vm_name ' >** met de naam van uw VM hello (Zorg ervoor dat Hallo naam tussen enkele aanhalingstekens) en druk vervolgens op **ENTER**.

tooconfirm die Hallo juiste naam van de VM hebt ingevoerd, typt:

**$vmName**

Druk op **ENTER**. U ziet Hallo-naam van Hallo virtuele machine die u wilt tooencrypt. Bijvoorbeeld:

![PowerShell-resultaat](./media/security-center-disk-encryption/security-center-disk-encryption-fig7.png)

Er zijn twee methoden toorun Hallo versleuteling opdracht tooencrypt alle stations op Hallo virtuele machine. de eerste methode Hallo is tootype Hallo volgende opdracht in Hallo PowerShell ISE-console:

~~~
Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $resourceGroupName -VMName $vmName -AadClientID $aadClientID -AadClientSecret $aadClientSecret -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl -DiskEncryptionKeyVaultId $keyVaultResourceId -VolumeType All
~~~

Na deze opdracht drukt u op **ENTER**.

de tweede methode Hallo is tooclick in Hallo scriptvenster (Hallo het bovenste deelvenster Hallo PowerShell ISE) en schuif omlaag toohello onderaan Hallo script. Markeer Hallo bovenstaande Opdrachtlijst, en klik vervolgens op de rechtermuisknop en klik vervolgens op **selectie uitvoeren** of druk op **F8** op Hallo toetsenbord.

![PowerShell ISE](./media/security-center-disk-encryption/security-center-disk-encryption-fig8.png)

Ongeacht Hallo methode u gebruikt, verschijnt een dialoogvenster waarin wordt gemeld dat het Hallo bewerking toocomplete 10-15 minuten duurt. Klik op **Ja**.

Tijdens het Hallo-versleutelingsproces plaatsvindt, kunt u retourneren toohello Azure-Portal en ziet Hallo status van Hallo virtuele machine. Op Hallo linkerkant van Hallo pagina, klikt u op **virtuele Machines**, klik dan in Hallo **virtuele Machines** blade, klikt u op de naam Hallo van Hallo virtuele machine versleutelen bent. Hallo-blade die wordt weergegeven, zult u merken dat Hallo **Status** gesteld dat het **Updating**. Dit toont aan dat versleuteling wordt uitgevoerd.

![Meer informatie over Hallo VM](./media/security-center-disk-encryption/security-center-disk-encryption-fig9.png)

PowerShell ISE toohello retourneren. Wanneer het Hallo-script is voltooid, ziet u wat wordt weergegeven in onderstaande afbeelding ziet Hallo.

![PowerShell-resultaat](./media/security-center-disk-encryption/security-center-disk-encryption-fig10.png)

toodemonstrate die Hallo van virtuele machine nu versleuteld terug toohello Azure-Portal en klikt u op **virtuele Machines** op Hallo linkerkant van Hallo pagina. Klik op de naam Hallo van Hallo virtuele machine die u versleuteld. In Hallo **instellingen** blade, klikt u op **schijven**.

![Opties voor instellingen](./media/security-center-disk-encryption/security-center-disk-encryption-fig11.png)

Op Hallo **schijven** blade ziet u dat **versleuteling** is **ingeschakeld**.

![Schijfeigenschappen](./media/security-center-disk-encryption/security-center-disk-encryption-fig12.png)

## <a name="next-steps"></a>Volgende stappen
In dit document, u leert hoe tooencrypt een virtuele Machine van Azure. toolearn meer informatie over Azure Security Center Hallo ziet:

* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) : meer informatie over hoe toomonitor Hallo status van uw Azure-resources
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) -informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) : Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service
* [Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/) (Azure-beveiligingsblog): lees blogberichten over de beveiliging en naleving van Azure
