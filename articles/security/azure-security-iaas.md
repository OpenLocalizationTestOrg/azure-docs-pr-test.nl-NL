---
title: aaaSecurity best practices voor IaaS werkbelastingen in Azure | Microsoft Docs
description: " Hallo-migratie van werkbelastingen tooAzure IaaS brengt verkoopkansen tooreevaluate onze ontwerpen "
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 02c5b7d2-a77f-4e7f-9a1e-40247c57e7e2
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: barclayn
ms.openlocfilehash: 9cee1ca6effe9561e51dc8b945e7388ffea169b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-best-practices-for-iaas-workloads-in-azure"></a>Aanbevolen beveiligingsprocedures voor IaaS-workloads in Azure

Als u nadenken over zwevend werkbelastingen tooAzure infrastructuur gestart als een service (IaaS), gerealiseerde u waarschijnlijk dat er enkele overwegingen bekend bent. U hebt mogelijk al ervaring voor het beveiligen van virtuele omgevingen. Wanneer u tooAzure IaaS verplaatst, kunt u uw kennis in het beveiligen van virtuele omgevingen van toepassing en uw assets voor een nieuwe reeks opties toohelp beveiligde gebruiken.

Laten we beginnen door te zeggen dat we geen toobring lokale bronnen als een-op-een tooAzure verwachten. Hallo nieuwe uitdagingen en nieuwe opties Hallo brengt een kans tooreevaluate bestaande deigns, hulpprogramma's voor databaseontwikkeling en verwerkt.

Uw verantwoordelijkheid voor beveiliging is gebaseerd op Hallo-type van de cloudservice. Hallo volgende diagram geeft een overzicht van Hallo verdelen van de verantwoordelijkheid voor zowel Microsoft als u:


![Verantwoordelijkheidsgebieden](./media/azure-security-iaas/sec-cloudstack-new.png)


Gaan we enkele van Hallo-opties die beschikbaar zijn in Azure kunt u voldoen aan de beveiligingsvereisten van uw organisatie. Houd er rekening mee dat de beveiligingsvereisten voor verschillende typen werkbelastingen kunnen verschillen. Niet een van deze best practices kan zelfstandig Beveilig uw systemen. Net als iets anders in de beveiliging, u hebt toochoose Hallo juiste opties en Zie hoe Hallo-oplossingen kunnen elkaar aanvullen door hiaten.

## <a name="use-privileged-access-workstations"></a>Privileged Access Workstations gebruiken

Organisaties misbruik vaak vallen toocyberattacks omdat beheerders acties uitvoeren tijdens het gebruik van accounts met verhoogde rechten. Meestal dit met kwaadaardige bedoelingen wordt niet uitgevoerd, maar omdat de bestaande configuratie en processen toe te staan. De meeste van deze gebruikers Hallo risico van de volgende acties uit conceptueel oogpunt begrijpt, maar nog steeds kiezen toodo ze.

Opdrachten, zoals het controleren van e-mail en surfen op Internet Hallo onschuldige genoeg lijken uit te voeren. Maar ze kunnen openbaren verhoogde accounts toocompromise door schadelijke actoren die Browse activiteiten, speciaal e-mailberichten of andere technieken toogain toegang tooyour onderneming kunnen gebruiken. We raden Hallo gebruik van beveiligde Beheerwerkstations voor de uitvoering van alle Azure beheerderstaken als een manier om blootstelling tooaccidental inbreuk te verminderen.

Privileged Access Workstations (poten) bieden een toegewijde besturingssysteem voor gevoelige taken--één die is beveiligd tegen aanvallen via Internet en bedreigingen met zich mee. Deze gevoelige taken en de accounts van elkaar te scheiden Hallo dagelijks gebruik werkstations en apparaten sterke bescherming bieden tegen phishingaanvallen, toepassing en OS beveiligingsproblemen, verschillende imitatie aanvallen en credential theft aanvallen, zoals toetsaanslag logboekregistratie, Pass-the-Hash en Pass-the-Ticket.

Hallo PAW aanpak is een uitbreiding van Hallo gevestigd en aanbevolen praktijken toouse een afzonderlijk toegewezen Administrator-account dat is gescheiden van een standaardgebruikersaccount. Een PAW biedt een betrouwbare werkstation voor die gevoelige accounts.

Zie voor meer informatie en de implementatie-instructies, [Privileged Access Workstations](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/privileged-access-workstations).

## <a name="use-multi-factor-authentication"></a>Meervoudige verificatie gebruiken

In de afgelopen hello is uw netwerkverbinding gebruikte toocontrol access toocorporate-gegevens. In een wereld cloud eerste, mobile eerste identiteit is Hallo besturingselement vlak: U deze toocontrol toegang tooIaaS services vanaf elk apparaat gebruiken. U deze ook gebruiken tooget zichtbaarheid en inzicht in hoe en waar uw gegevens wordt gebruikt. Beveiligen van de digitale identiteit Hallo van uw Azure gebruikers is Hallo basis van het beveiligen van uw abonnementen van identiteitsdiefstal en andere cybercrimes.

Een van de meeste zin stappen Hallo dat u toosecure een account ondernemen kunt is tooenable tweeledige verificatie. Tweeledige verificatie is een manier te verifiëren met behulp van iets in toevoeging tooa wachtwoord. Het helpt Hallo risico van toegang door iemand die u tooget beheert wachtwoord van iemand anders.

[Azure multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) u beveiligt toegang toodata en toepassingen en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden. Sterke verificatie met een bereik van eenvoudige verificatie-opties--telefoongesprek, tekstbericht of mobiele-appmelding levert. Hallo-methode dat ze desgewenst kunnen gebruikers kiezen.

Hallo gemakkelijkste manier toouse multi-factor Authentication is Hallo Microsoft Authenticator mobiele app, die kan worden gebruikt voor mobiele apparaten met Windows, iOS en Android. Met de meest recente versie van Windows 10 en Hallo integratie van lokale Active Directory met Azure Active Directory (Azure AD), Hallo [Windows Hello voor bedrijven](../active-directory/active-directory-azureadjoin-passport-deployment.md) voor naadloze eenmalige aanmelding tooAzure resources kunnen worden gebruikt. In dit geval wordt Hallo Windows 10-apparaat gebruikt als tweede factor Hallo voor verificatie.

Voor accounts die uw Azure-abonnement beheren en voor accounts die de machines toovirtual kunnen aanmelden hebt met multi-factor Authentication u een veel hoger niveau van beveiliging dan het gebruik van alleen een wachtwoord. Andere vormen van tweeledige verificatie werken net zo goed mogelijk, maar deze kunnen mogelijk ingewikkeld als ze nog niet in de productieomgeving.

Hallo volgende schermafbeelding ziet u enkele van Hallo-opties die beschikbaar zijn voor Azure multi-factor Authentication:

![Opties voor meervoudige verificatie](./media/azure-security-iaas/mfa-options.png)

## <a name="limit-and-constrain-administrative-access"></a>Beperk de beheerderstoegang te beperken

Het is zeer belangrijk voor het beveiligen van Hallo-accounts die uw Azure-abonnement kunnen beheren. Hallo inbreuk op een van deze accounts genegeerd Hallo-waarde van alle Hallo andere stappen die u tooensure Hallo vertrouwelijkheid en integriteit van uw gegevens kunt uitvoeren. Als onlangs geïllustreerd door Hallo [Edward Snowden](https://en.wikipedia.org/wiki/Edward_Snowden) geheugenlek van geclassificeerde gegevens interne aanvallen vormen een enorme threat toohello algehele beveiliging van elke organisatie.

Personen voor beheerdersrechten evalueren door de volgende criteria vergelijkbare toothese:

- Presteren ze taken die u hebt u beheerdersbevoegdheden nodig?
- Hoe vaak worden Hallo taken uitgevoerd?
- Is er een specifieke reden waarom Hallo taken kunnen niet worden uitgevoerd door een andere beheerder namens hen?

Documenteer alle andere bekende alternatieve benaderingen toogranting Hallo bevoegdheden en waarom elk kan niet worden geaccepteerd.

Hallo-gebruik van just in time-beheer wordt voorkomen dat onnodige bestaan Hallo van accounts met verhoogde rechten tijdens perioden wanneer deze rechten niet nodig zijn. Accounts wel verhoogde bevoegdheden hebben voor een beperkte tijd zodat beheerders kunnen hun werk. Deze rechten worden vervolgens verwijderd aan Hallo einde van een verschuiving of wanneer een taak is voltooid.

U kunt [Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-configure.md) toomanage, bewaking en beheer openen in uw organisatie. U kunt blijven op de hoogte van het Hallo-acties die personen in uw organisatie worden uitgevoerd. Brengt dit ook zich just in time-beheer tooAzure AD door de introductie van Hallo concept van in aanmerking komende beheerders. Dit zijn personen die hebben accounts met mogelijke toobe Hallo beheerdersrechten verleend. Deze typen van gebruikers kunnen doorlopen die een proces voor het activeren en beheerdersrechten worden verleend voor een beperkte periode.


## <a name="use-devtest-labs"></a>Gebruik DevTest Labs

Met Azure voor labs en ontwikkelomgevingen kunnen organisaties toogain flexibiliteit bij testen en ontwikkeling door duurt opslag Hallo vertragingen die hardware inkoop introduceert. Helaas een gebrek aan bekend bent met Azure of een toohelp desire de ingebruikname versnellen Hallo beheerder toobe te soepele kan opleveren met de toewijzing van gebruiksrecht. Dit risico kan Hallo organisatie toointernal aanvallen onbedoeld worden blootgesteld. Sommige gebruikers mogelijk veel meer toegang dan ze moeten worden verleend.

Hallo [Azure DevTest Labs](../devtest-lab/devtest-lab-overview.md) service gebruikt [rollen gebaseerd toegangsbeheer](../active-directory/role-based-access-control-what-is.md) (RBAC). Met behulp van RBAC kunt u taken scheiden binnen uw team in functies die alleen Hallo niveau van toegang nodig is voor gebruikers toodo hun werk verlenen. RBAC wordt geleverd met vooraf gedefinieerde functies (eigenaar, lab-gebruiker en Inzender). U kunt zelfs gebruiken deze functies tooassign rechten tooexternal partners en samenwerking aanzienlijk te vereenvoudigen.

Omdat DevTest Labs RBAC gebruikt, is het mogelijk extra, toocreate [aangepaste rollen](../devtest-lab/devtest-lab-grant-user-permissions-to-specific-lab-policies.md). DevTest Labs vereenvoudigt niet alleen Hallo beheer van machtigingen, het Hallo-proces van het ophalen van omgevingen ingericht vereenvoudigt. Hiermee kunt u ook andere typische uitdagingen van teams die op een ontwikkel- en testomgevingen werkt behandelt. Voorbereiding is vereist, maar de lange termijn hello, deze wordt gemakkelijker voor uw team.

Azure DevTest Labs functies:

- Hallo opties beschikbaar toousers worden beheerd. Hallo beheerder kunt dingen zoals toegestane VM-grootten, het maximum aantal virtuele machines, en wanneer virtuele machines worden gestart en afsluiten centraal beheren.
- Automatisering van lab maken.
- Kosten bijhouden.
- Vereenvoudigde verdeling van virtuele machines tijdelijke samenwerkingsmogelijkheden.
- Selfservice waarmee gebruikers tooprovision hun labs met behulp van sjablonen.
- Beheren en beperken van verbruik.

![Met behulp van DevTest Labs toocreate een lab](./media/azure-security-iaas/devtestlabs.png)

Kan zonder extra kosten is gekoppeld aan Hallo gebruik van DevTest Labs. Hallo maken van labs, beleid, sjablonen en artefacten is gratis. U betaalt voor alleen hello Azure-resources in uw labs, zoals virtuele machines, opslagaccounts en virtuele netwerken gebruikt.



## <a name="control-and-limit-endpoint-access"></a>Controle- en limit endpoint-toegang

Het hosten van labs of productiesystemen van Azure betekent dat uw systemen toobe toegankelijk is vanaf Internet Hallo moeten. Standaard een nieuwe virtuele machine voor Windows hello RDP-poort die toegankelijk is vanaf Internet Hallo heeft en een virtuele Linux-machine heeft Hallo SSH-poort openen. Stappen toolimit blootgesteld eindpunten is noodzakelijk toominimize Hallo risico op onbevoegde toegang.

Technologieën in Azure kunt u Hallo toegang toothose beheerdersrechten eindpunten te beperken. In Azure, kunt u [netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md) (nsg's). Wanneer u Azure Resource Manager voor implementatie gebruikt, beperkt nsg's Hallo toegang vanaf alle netwerken toojust Hallo eindpunten voor beheer (RDP of SSH). Als u nsg's nadenkt, beschouw router ACL's. U kunt deze gebruiken tootightly besturingselement Hallo netwerkcommunicatie tussen verschillende segmenten van uw Azure-netwerken. Dit is vergelijkbaar toocreating netwerken in het perimeternetwerk of andere geïsoleerde netwerken. Ze doen Hallo-verkeer niet controleren, maar ze helpen bij netwerksegmentering.


In Azure, configureert u een [site-naar-site VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) van uw on-premises netwerk. Een site-naar-site VPN breidt uw on-premises netwerk toohello cloud. Hiermee krijgt u een andere mogelijkheid toouse nsg's, omdat u kunt ook wijzigen Hallo nsg's toonot toegang toestaan via ergens anders dan het lokale netwerk Hallo. Vervolgens kunt u vereisen dat het beheer wordt uitgevoerd door de eerste verbinding toohello Azure-netwerk via VPN.

Hallo site-naar-site VPN-optie mogelijk meest aantrekkelijk in gevallen waarin u productiesystemen die nauw worden geïntegreerd met uw lokale resources in Azure worden gehost.

U kunt ook hello gebruiken [punt-naar-site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md) optie in situaties waar u toomanage systemen die geen moet toegang tot tooon-premises resources. Deze systemen kunnen worden geïsoleerd in hun eigen virtuele Azure-netwerk. Beheerders kunnen VPN in hello Azure gehoste omgeving van hun werkstation voor beheer.

>[!NOTE]
>U kunt een VPN-optie tooreconfigure Hallo-ACL's op Hallo nsg's toonot toegang toomanagement eindpunten van Hallo Internet kunnen gebruiken.

Een andere optie waard is een [extern bureaublad-Gateway](../multi-factor-authentication/multi-factor-authentication-get-started-server-rdg.md) implementatie. U kunt deze implementatie toosecurely tooRemote bureaublad servers verbinden via HTTPS, als deze toepassing meer gedetailleerde toothose verbindingen wordt geregeld.

Functies die u hebt toegang tot tooinclude:

- De beheerder opties toolimit verbindingen toorequests van specifieke systemen.
- Smart card-verificatie of Azure multi-factor Authentication.
- Bepalen via welke systemen iemand toovia Hallo gateway verbinding kan maken.
- De controle over apparaten en schijf-omleiding.

## <a name="use-a-key-management-solution"></a>Gebruik een oplossing voor sleutelbeheer

Beveiligd Sleutelbeheer is essentieel tooprotecting gegevens in Hallo cloud. Met [Azure Key Vault](../key-vault/key-vault-whatis.md), kunt u veilig versleutelingssleutels opslaan en klein geheimen zoals wachtwoorden in hardware security modules (HSM's). Voor extra zekerheid kunt u de sleutels importeren of genereren in HSM's.

De processen Microsoft uw sleutels in FIPS 140-2 Level 2 gevalideerde HSM (hardware en firmware). Monitor en audit sleutelgebruik met logboekregistratie van Azure: pipe-Logboeken in Azure of uw Security Information en Event Management (SIEM) systeem voor extra analyse en detectie van bedreigingen.

Iedereen met een Azure-abonnement kunt maken en gebruiken van sleutelkluizen. Hoewel Sleutelkluis voordelen biedt voor ontwikkelaars en beveiligingsadministrators, kan deze worden geïmplementeerd en beheerd door een beheerder die verantwoordelijk is voor het beheren van Azure-services in een organisatie.


## <a name="encrypt-virtual-disks-and-disk-storage"></a>Virtuele schijven en schijfopslag versleutelen

[Azure Disk Encryption](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0) adressen Hallo bedreigingen van gegevensdiefstal of blootstelling tegen onbevoegde toegang, die wordt bereikt door het verplaatsen van een schijf. Hallo-schijf kan worden aangesloten tooanother systeem als een manier om andere beveiligingsmechanismen omzeilen. Schijf wordt gebruikt voor versleuteling [BitLocker](https://technet.microsoft.com/library/hh831713) in Windows en DM-Crypt in Linux tooencrypt-besturingssysteem en de schijven. Azure Disk Encryption kan worden geïntegreerd met Sleutelkluis toocontrol en beheren van versleutelingssleutels Hallo. Is beschikbaar voor de standaard virtuele machines en virtuele machines met premium-opslag.

Zie voor meer informatie [Azure Disk Encryption in Windows en Linux IaaS VM's](azure-security-disk-encryption.md).

[Azure Storage-Service: versleuteling](../storage/common/storage-service-encryption.md) beschermt uw gegevens in rust. Het niveau Hallo storage-account ingeschakeld. Gegevens worden gecodeerd als ze de datacenters worden geschreven en wordt dit automatisch ontsleuteld wanneer u toegang hebt. Hallo volgen scenario's ondersteund:

- Versleuteling van blok-blobs, toevoeg-blobs en pagina-blobs
- Versleuteling van gearchiveerde VHD's en sjablonen tooAzure gebracht van on-premises
- Versleuteling van het onderliggende besturingssysteem en gegevensschijven voor IaaS VM's die u hebt gemaakt met behulp van uw VHD 's

Voordat u met Azure Storage Encryption doorgaat, worden op de hoogte van twee beperkingen:

- Het is niet beschikbaar op klassieke opslagaccounts.
- Alleen de gegevens die zijn geschreven nadat de codering is ingeschakeld, worden versleuteld.

## <a name="use-a-centralized-security-management-system"></a>Gebruik een beheersysteem voor gecentraliseerde beveiliging

Uw servers moeten toobe gecontroleerd op patchen, configuratie, gebeurtenissen en activiteiten die als beveiligingsproblemen worden beschouwd. tooaddress die betrekking heeft, kunt u [Security Center](https://azure.microsoft.com/services/security-center/) en [Operations Management Suite-beveiliging en naleving](https://azure.microsoft.com/services/security-center/). Beide opties verder dan Hallo-configuratie in het Hallo-besturingssysteem. Ze bieden ook bewaking van de configuratie Hallo Hallo onderliggende infrastructuur, zoals configuratie en het gebruik van virtueel apparaat.

## <a name="manage-operating-systems"></a>Besturingssystemen beheren

In een IaaS-implementatie bent u nog steeds verantwoordelijk voor het beheer van Hallo Hallo-systemen die u, net als een andere server of werkstation in uw omgeving implementeert. Patchen, beperken, toegewezen rechten en andere activiteiten met betrekking tot toohello onderhoud van uw systeem zijn nog steeds zelf verantwoordelijk. Voor systemen die zijn geïntegreerd met uw lokale bronnen, kunt u toouse Hallo dezelfde hulpprogramma's en procedures die u hebt lokale gebruikt voor items zoals antivirus, anti-malware, patchen en back-up.

### <a name="harden-systems"></a>Systemen beperken
Alle virtuele machines in Azure IaaS moet worden gehard zodat ze openbaren alleen service-eindpunten die vereist zijn voor het Hallo-toepassingen die zijn geïnstalleerd. Volg voor virtuele machines van Windows hello aanbevelingen die Microsoft als basislijnen voor Hallo publiceert [Security Compliance Manager](https://technet.microsoft.com/solutionaccelerators/cc835245.aspx) oplossing.

Security Compliance Manager is een gratis hulpprogramma. U kunt deze tooquickly configureren en beheren van uw bureaubladen, traditionele datacenter en private en openbare cloud met behulp van Groepsbeleid en System Center Configuration Manager.

Security Compliance Manager biedt gereed te implementeren beleid en Desired Configuration Management-configuratiepakketten die zijn getest. Deze basislijnen zijn gebaseerd op [Microsoft-beveiligingsrichtlijnen](https://technet.microsoft.com/en-us/library/cc184906.aspx) aanbevelingen en andere aanbevolen procedures. Ze helpen u configuratie afwijking, adres nalevingsvereisten, beheren en beveiligingsrisico's verkleinen.

U kunt Security Compliance Manager tooimport Hallo huidige configuratie van uw computers met behulp van twee verschillende methoden gebruiken. Ten eerste kunt u Groepsbeleid op basis van Active Directory importeren. Ten tweede kunt u configuratie van de 'gouden master' hello importeren referentiecomputer met behulp van Hallo [LocalGPO hulpprogramma](https://blogs.technet.microsoft.com/secguide/2016/01/21/lgpo-exe-local-group-policy-object-utility-v1-0/) tooback Hallo lokale Groepsbeleid. U kunt het lokale Groepsbeleid Hallo vervolgens importeren in Security Compliance Manager.

Aanbevolen procedures voor standaarden tooindustry vergelijken, aanpassen en nieuw beleid en Desired Configuration Management-configuratiepakketten maken. Basislijnen zijn gepubliceerd voor alle ondersteunde besturingssystemen, met inbegrip van Windows 10 Verjaardag en Update voor Windows Server 2016.


### <a name="install-and-manage-antimalware"></a>Installeren en beheren van antimalware

In omgevingen die afzonderlijk van uw productieomgeving worden gehost, kunt u een anti-malware-extensie toohelp beveiligen van uw virtuele machines en cloudservices. Het is geïntegreerd met [Azure Security Center](../security-center/security-center-intro.md).


[Microsoft Antimalware](azure-security-antimalware.md) bevat functies zoals realtime-beveiliging, geplande scan, oplossen van malware, handtekening updates, engine-updates en rapportage, uitsluiting gebeurtenissen verzamelen, voorbeelden en [PowerShell-ondersteuning](https://msdn.microsoft.com/library/dn771715.aspx).

![Azure Antimalware](./media/azure-security-iaas/azantimalware.png)

### <a name="install-hello-latest-security-updates"></a>Installeer de meest recente beveiligingsupdates Hallo
Sommige van de eerste werkbelastingen Hallo dat klanten tooAzure verplaatsen zijn labs en externe systemen. Als uw Azure gehoste virtuele machines host toepassingen of services die toobe toegankelijk toohello Internet nodig, worden bedacht patchen. Patch dan Hallo-besturingssysteem. Niet-gepatchte beveiligingsproblemen op toepassingen van derden kunnen ook leiden tooproblems die kunnen worden voorkomen als goed patch management aanwezig is.

### <a name="deploy-and-test-a-backup-solution"></a>Implementeren en testen van een back-upoplossing

Net als beveiligingsupdates, moet een back-up toobe verwerkt Hallo dezelfde manier waarop u een andere bewerking worden verwerkt. Dit geldt voor systemen die deel uitmaken van uw productieomgeving toohello cloud uitbreiden. Test-en Developer moeten volgen op back-strategieën die mogelijkheden voor terugzetten die vergelijkbaar toowhat gebruikers zijn gewend zijn bieden, op basis van hun ervaringen met on-premises omgevingen.

Productieworkloads verplaatst tooAzure moet integreren met bestaande back-upoplossingen indien mogelijk. Of u kunt [Azure Backup](../backup/backup-azure-arm-vms.md) toohelp houden met de vereisten van uw back-up.


## <a name="monitor"></a>Bewaken

[Security Center](../security-center/security-center-intro.md) biedt continue evaluatie van Hallo beveiligingsstatus van uw Azure-resources tooidentify mogelijke beveiligingsproblemen. Een lijst met aanbevelingen begeleidt u bij het Hallo-proces voor het configureren van benodigde besturingselementen.

Voorbeelden zijn:

- Inrichting van antimalware toohelp identificeren en verwijderen van schadelijke software.
- Configureren van beveiliging groepen en regels toocontrol verkeer toovirtual machines in het netwerk.
- Web application firewalls toohelp beschermen tegen aanvallen die zijn gericht op uw webtoepassingen inrichten.
- Ontbrekende systeemupdates implementeren.
- Aanpassing van besturingssysteemconfiguraties die niet overeenkomen met de Hallo aanbevolen basislijnen.

Hallo volgende afbeelding ziet u enkele van Hallo-opties die u in Security Center inschakelen kunt.

![Azure Security Center-beleid](./media/azure-security-iaas/security-center-policies.png)

[Operations Management Suite](../operations-management-suite/operations-management-suite-overview.md) is een Microsoft cloud-gebaseerde IT beheeroplossing waarmee u beheren kunt en beveiligen van uw on-premises en cloud-infrastructuur. Omdat de Operations Management Suite is geïmplementeerd als een cloudservice, kan worden geïmplementeerd snel en met minimale investeringen in infrastructuurresources.

Nieuwe functies worden automatisch geleverd zodat u van voortdurend onderhoud en kosten upgrade. Operations Management Suite is ook worden geïntegreerd met System Center Operations Manager. Heeft verschillende onderdelen toohelp beter beheer van uw Azure-werkbelastingen, waaronder een [beveiliging en naleving](../operations-management-suite/oms-security-getting-started.md) module.

U kunt Hallo beveiliging en naleving functies gebruiken in Operations Management Suite tooview informatie over uw resources. Hallo-informatie is onderverdeeld in vier hoofdcategorieën:

- **Beveiligingsdomeinen**: verder verkennen beveiligingsrecord gedurende een bepaalde periode. Toegang tot de evaluatie van schadelijke software, beoordeling, netwerkgegevens voor beveiliging, informatie over identiteit en toegang en computers met beveiligingsgebeurtenissen bijwerken. Profiteren van snelle toegang toohello Azure Security Center-dashboard.
- **Problemen die aandacht vereisen**: snel Hallo aantal actieve problemen identificeren en Hallo ernst van deze problemen.
- **Detecties (preview)**: aanval worden geïdentificeerd patronen door beveiligingswaarschuwingen visualiseren meteen op basis van uw resources.
- **Dreiging intelligence**: aanval worden geïdentificeerd patronen door het totaal aantal servers met uitgaand schadelijk IP-verkeer Hallo visualiseren Hallo schadelijke threat type en een toewijzing die laat zien waar deze IP-adressen afkomstig zijn uit.
- **Algemene query's voor beveiliging**: Zie een lijst met de meest voorkomende beveiliging Hallo query's waarmee u toomonitor uw omgeving kunt. Wanneer u op een van de query's, Hallo **Search** blade wordt geopend en toont Hallo resultaten voor deze query.

Hallo toont volgende schermafbeelding een voorbeeld van Hallo-informatie die Operations Management Suite kunt weergeven.

![Operations Management Suite-beveiligingsbasislijnen](./media/azure-security-iaas/oms-security-baseline.png)



## <a name="next-steps"></a>Volgende stappen


* [Blog van het Azure-beveiligingsteam](https://blogs.msdn.microsoft.com/azuresecurity/)
* [Microsoft Security Response Center](https://technet.microsoft.com/library/dn440717.aspx)
* [Azure-beveiliging aanbevolen procedures en patronen](security-best-practices-and-patterns.md)
