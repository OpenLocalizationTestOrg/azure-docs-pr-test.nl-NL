---
title: aaaIsolation in Hallo openbare Azure-Cloud | Microsoft Docs
description: Meer informatie over cloud-gebaseerde computers onder meer services als een groot aantal compute-exemplaren en services die kunnen worden geschaald omhoog en omlaag automatisch toomeet Hallo behoeften van uw toepassing of enterprise.
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 271e5f0d00abcfd404ce6c50cfb7d1ac26360c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="isolation-in-hello-azure-public-cloud"></a>Isolatie in Hallo openbare Azure-Cloud
##  <a name="introduction"></a>Inleiding
### <a name="overview"></a>Overzicht
tooassist huidige en toekomstige Azure-klanten begrijpen en te gebruiken Hallo verschillende beveiligingsgerelateerde-mogelijkheden beschikbaar in en omringende Hallo Azure-platform, er is een reeks whitepapers, overzichten van de beveiliging, Best Practices, ontwikkeld en Controlelijsten.
bereik van de onderwerpen in termen van breedte en diepte Hallo en regelmatig worden bijgewerkt. Dit document is onderdeel van de reeks zoals samengevat in Hallo abstracte sectie volgen.

### <a name="azure-platform"></a>Azure-Platform
Azure is een open en flexibele cloud service-platform dat ondersteuning Hallo breedste selectie van besturingssystemen biedt, programmeertalen, frameworks, hulpprogramma's, databases, en apparaten. U kunt bijvoorbeeld:
- Linux-containers worden uitgevoerd met Docker-integratie;
- Bouwen van apps met JavaScript, Python, .NET, PHP, Java en Node.js; en
- Build back-ends voor iOS, Android en Windows apparaten.

Microsoft Azure ondersteunt Hallo van dezelfde technologieën miljoenen van ontwikkelaars en IT-professionals al zijn afhankelijk van en vertrouwen.

Wanneer u bouwen op of IT-middelen migreren naar een openbare cloud serviceprovider, u zijn afhankelijk van die organisatie mogelijkheden tooprotect uw toepassingen en gegevens met services en Hallo besturingselementen Hallo opgeven deze toomanage Hallo beveiliging van uw cloud-gebaseerde activa.

Azure infrastructuur is speciaal ontworpen van Hallo faciliteit tooapplications voor het hosten van miljoenen klanten tegelijkertijd en biedt een betrouwbare basis waarop bedrijven hun beveiliging behoeften kunnen. Bovendien Azure biedt u een breed scala aan configureerbare beveiliging opties en Hallo mogelijkheid toocontrol ze zodat u beveiliging toomeet Hallo unieke vereisten van uw implementaties kunt aanpassen. Dit document helpt u aan deze vereisten voldoet.

### <a name="abstract"></a>Abstracte

Microsoft Azure kunt u toorun toepassingen en virtuele machines (VM's) op gedeelde fysieke infrastructuur. Een van de Hallo voornaamste economische motivaties toorunning toepassingen in een cloudomgeving is Hallo mogelijkheid toodistribute Hallo kosten van gedeelde resources tussen meerdere klanten. Deze oefening van multi-tenancymodus verbetert de efficiëntie door multiplexing resources onder de verschillende klanten tegen lage kosten. Helaas kleven er ook Hallo risico van het delen van fysieke servers en andere bronnen infrastructuur toorun uw gevoelige toepassingen en virtuele machines die deel van willekeurige tooan en mogelijk schadelijke gebruiker uitmaken mogelijk.

In dit artikel bevat een overzicht van hoe Microsoft Azure biedt isolatie tegen schadelijke en niet kwaadwillende gebruikers en fungeert als een handleiding voor cloudoplossingen door het aanbieden van verschillende isolatie keuzes tooarchitects worden veranderd. Dit document is gericht op het Hallo-technologie van Azure-platform en klantgerichte beveiligingsmechanismen en probeert niet tooaddress Sla's, prijzen modellen en DevOps practice overwegingen.

## <a name="tenant-level-isolation"></a>Niveau isolatie van tenants
Een van de primaire voordelen Hallo van cloud computing concept van een gedeelde gemeenschappelijke infrastructuur tegelijk is over meerdere klanten, voorloopspaties tooeconomies van de schaal. Dit concept wordt multi-tenancymodus genoemd. Microsoft werkt continu tooensure hello multitenant architectuur van Microsoft Cloud Azure biedt ondersteuning voor beveiliging, vertrouwelijkheid, privacy, integriteit en beschikbaarheid standaarden.

Op Hallo ingeschakeld voor de cloud werkplek kan een tenant worden gedefinieerd als een client of organisatie die eigenaar is van en een specifiek exemplaar van die cloudservice beheert. Met Hallo identiteitsplatform geleverd door Microsoft Azure, is een tenant het eigen exemplaar van Azure Active Directory (Azure AD) die uw organisatie ontvangt en de eigenaar is wanneer deze zich voor een Microsoft-cloudservice aanmeldt.

Elke Azure AD-directory is uniek en werkt afzonderlijk van andere Azure AD-directory’s. Net zoals een kantoorgebouw is een specifieke tooonly beveiligd bedrijfsmiddel is van uw organisatie, er is ook een Azure AD-directory ontworpen toobe een beveiligd bedrijfsmiddel alleen door uw organisatie. Hello Azure AD-architectuur isoleert klant- en identiteitsgegevens informatie door elkaar worden gehaald. Dit betekent dat gebruikers en beheerders van een Azure AD-directory niet per ongeluk of opzettelijk gegevens in een andere directory kunnen openen.

### <a name="azure-tenancy"></a>Azure-Tenancymodus
Azure-tenancymodus (Azure-abonnement) verwijst tooa "klant/billing" relatie en een unieke [tenant](https://docs.microsoft.com/azure/active-directory/develop/active-directory-howto-tenant) in [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis). Niveau isolatie van tenants in Microsoft Azure wordt bereikt met Azure Active Directory en [besturingselementen op basis van rollen](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) die worden aangeboden door het. Elk Azure-abonnement is gekoppeld aan één map op Azure Active Directory (AD).

Gebruikers, groepen en toepassingen van die directory kunnen resources in hello Azure-abonnement te beheren. U kunt deze toegangsrechten met hello Azure-portal, Azure-opdrachtregelprogramma's en Azure Management-API's. Een Azure AD-tenant is logisch is geïsoleerd met behulp van beveiligingsgrenzen zodat klanten geen toegang hebt of mede-tenants, met kwaadaardige bedoelingen of per ongeluk in gevaar brengen. Azure AD wordt uitgevoerd op bare-metalcomputer'-servers die zijn geïsoleerd in een netwerksegment gescheiden, waarbij hostniveau pakketfilters en Windows Firewall blokkeren ongewenste verbindingen en verkeer.

- Toodata in Azure AD Access vereist verificatie van de gebruiker via een [beveiligingstokenservice (STS)](https://docs.microsoft.com/azure/app-service-web/web-sites-authentication-authorization). Informatie over de bestaan, de ingeschakelde status en de rol van Hallo gebruiker wordt gebruikt door Hallo autorisatie system toodetermine of Hallo aangevraagde toegang toohello doel tenant voor deze gebruiker is gemachtigd in deze sessie.

![Azure-Tenancymodus](./media/azure-isolation/azure-isolation-fig1.png)


- Tenants discrete containers zijn en er is geen relatie tussen deze.

- Geen toegang via tenants tenzij tenantbeheerder verleend via federatie of het inrichten van gebruikersaccounts van andere tenants.

- Fysieke toegang tooservers waaruit hello Azure AD-service en directe toegang tooAzure AD van back-end-systemen is beperkt.

- Azure AD-gebruikers hebben geen toegang tot toophysical bedrijfsmiddelen of locaties en daarom is het niet mogelijk ze toobypass Hallo logische RBAC beleid controles vermeld te volgen.

Een operationeel model die gebruikmaakt van een systeem van de uitbreiding van bevoegdheden just-in-time-bevoegdheden is vereist en gebruikt voor diagnostische gegevens en onderhoudsbehoeften. Azure AD Privileged Identity Management (PIM) introduceert Hallo concept van een in aanmerking komende-beheerder. [In aanmerking komende beheerders](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure) moeten gebruikers die de juiste rechten moeten toegang af en toe, maar niet elke dag. Hallo-rol is niet actief totdat Hallo gebruiker toegang, moet vervolgens zij een activering te voltooien en een actieve beheerder voor een vooraf bepaalde hoeveelheid tijd zijn geworden.

![Azure AD Privileged Identity Management](./media/azure-isolation/azure-isolation-fig2.png)

Azure Active Directory als host fungeert voor elke tenant in de eigen beveiligde container, met beleidsregels en machtigingen tooand binnen Hallo container uitsluitend eigendom van en beheerd door Hallo-tenant.

Hallo-concept van tenant containers is diep ingrained in de adreslijstservice Hallo voor alle lagen, van portals Hallo alle manier toopersistent opslag.

Zelfs als de metagegevens van meerdere tenants van Azure Active Directory wordt opgeslagen op Hallo dezelfde fysieke schijf, er is geen relatie tussen Hallo containers dan wat door Hallo directoryservice, die op zijn beurt wordt bepaald door de tenantbeheerder Hallo is gedefinieerd.

### <a name="azure-role-based-access-control-rbac"></a>Azure op rollen gebaseerde toegangsbeheer (RBAC)
[Azure op rollen gebaseerde toegangsbeheer (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) helpt u tooshare verschillende onderdelen die beschikbaar zijn in een Azure-abonnement dankzij Geavanceerd toegangsbeheer voor Azure. Azure RBAC kunt u de rechten toosegregate binnen uw organisatie en toegang verlenen op basis van welke gebruikers tooperform moeten hun werk. In plaats van iedereen geven onbeperkte machtigingen in Azure-abonnement of bronnen, kunt u alleen bepaalde acties toestaan.

Azure RBAC heeft drie basic rollen die tooall brontypen die van toepassing:

- **Eigenaar** heeft volledige toegang tooall bronnen, met inbegrip van Hallo rechts toodelegate toegang tooothers.

- **Inzender** kunt maken en beheren van alle soorten Azure-resources, maar kan geen tooothers toegang verlenen.

- **Lezer** bestaande Azure-resources kunt weergeven.

![Op rollen gebaseerde toegangsbeheer van Azure](./media/azure-isolation/azure-isolation-fig3.png)

Hallo rest van Hallo RBAC-rollen in Azure toestaan van beheer van specifieke Azure-resources. Bijvoorbeeld, Hallo rol van inzender van de virtuele Machine kunt Hallo gebruiker toocreate en beheren van virtuele machines. Deze geeft geen ze toegang toohello Azure Virtual Network of Hallo-subnet dat Hallo van virtuele machine verbinding maakt.

[Ingebouwde RBAC-rollen](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) lijst Hallo-functies die beschikbaar zijn in Azure. Deze geeft Hallo bewerkingen en het bereik dat elke ingebouwde rol toousers verleent. Als u op zoek bent toodefine uw eigen rollen voor nog meer controle, Zie hoe toobuild [aangepaste rollen in Azure RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles).

Bepaalde andere functies voor Azure Active Directory zijn onder andere:
- Azure AD kan eenmalige aanmelding tooSaaS toepassingen, ongeacht waar ze worden gehost. Voor sommige toepassingen kan federatieve aanmelding worden gebruikt via Azure AD en voor andere toepassingen kan eenmalige aanmelding (SSO) met een wachtwoord worden gebruikt. Federatieve toepassingen kunnen bieden ook ondersteuning voor gebruikers inrichten en [wachtwoordkluizen](https://www.techopedia.com/definition/31415/password-vault).

- Toegang toodata in [Azure Storage](https://azure.microsoft.com/services/storage/) wordt beheerd via verificatie. Elk opslagaccount is een primaire sleutel ([opslagaccountsleutel](https://docs.microsoft.com/azure/storage/storage-create-storage-account), of SAK) en een secundaire geheime sleutel (shared access signature voor Hallo of SAS).

- Azure AD levert de identiteit als via de federation Service met behulp van [Active Directory Federation Services](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-azure-adfs), synchronisatie en replicatie met on-premises adreslijsten.

- [Azure multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) hello multi-factor authentication-service waarvoor gebruikers tooverify aanmeldingen met een mobiele app, telefonische oproep of SMS-bericht is. Worden kan gebruikt met Azure AD-toohelp veilige on-premises resources met hello Azure multi-factor Authentication-server en aangepaste toepassingen en mappen met Hallo SDK.

- [Azure AD Domain Services](https://azure.microsoft.com/services/active-directory-ds/) kunt u virtuele machines in Azure tooan Active Directory-domein toevoegen zonder het implementeren van domeincontrollers. U kunt toothese virtuele machines zich aanmelden met uw bedrijfsreferenties in Active Directory en domein virtuele machines beheren met behulp van Groepsbeleid tooenforce beveiligingsbasislijnen op uw Azure virtuele machines.

- [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) biedt een maximaal beschikbare globale-identity management-service voor consumententoepassingen die schaalbaar toohundreds miljoenen identiteiten. De service kan worden geïntegreerd in zowel mobiele als webplatforms. Uw consumenten kunnen aanmelden tooall uw toepassingen via aanpasbare ervaringen met behulp van hun bestaande sociale accounts of referenties maken.

### <a name="isolation-from-microsoft-administrators--data-deletion"></a>Isolatie van Microsoft-beheerders & gegevens verwijderen
Microsoft hecht sterk metingen tooprotect uw gegevens uit ongeoorloofde toegang of het gebruik door onbevoegden. Deze operationele processen en -besturingselementen worden ondersteund door Hallo [Online Services-voorwaarden](http://aka.ms/Online-Services-Terms), welke aanbieding contractueel verbintenissen die toegang tot tooyour gegevens bepalen.

-   Microsoft engineers hoeft geen standaard toegang tot tooyour gegevens in de cloud Hallo. In plaats daarvan ze toegang, onder beheer toezicht, alleen indien nodig. Dat toegang is zorgvuldig beheerd en geregistreerd en ingetrokken wanneer het niet langer nodig is.

-   Microsoft kan andere bedrijven tooprovide beperkte services namens de dienst. Onderaannemers mogelijk toegang tot gegevens alleen toodeliver Hallo klantenservice waarvoor, we hebben ingehuurd ze tooprovide, en ze mogen niet voor andere doeleinden te gebruiken. Bovendien zijn ze contractueel gebonden toomaintain Hallo vertrouwelijkheid van gegevens voor onze klanten.

Zakelijke services met gecontroleerde certificeringen zoals ISO/IEC 27001 worden regelmatig gecontroleerd door Microsoft en erkende bedrijven, die voorbeeld audits tooattest uitvoeren die toegang tot controleren, alleen voor legitieme zakelijke doeleinden. U kunt altijd toegang hebt tot uw eigen gegevens van de klant op elk gewenst moment en voor welke reden dan ook.

Als u geen gegevens verwijdert, verwijdert Microsoft Azure Hallo-gegevens, inclusief alle kopieën in de cache of back-up. Voor services-scope gebeurt dat verwijdering binnen 90 dagen na het einde van de bewaarperiode Hallo Hallo. (In de scope-services worden gedefinieerd in Hallo gegevensverwerking voorwaarden sectie van onze [Online Services-voorwaarden](http://aka.ms/Online-Services-Terms).)

Als een schijf die wordt gebruikt voor de opslag van een hardware storing, is het veilig [verwijderd of vernietigd](https://www.microsoft.com/trustcenter/Privacy/You-own-your-data) voordat Microsoft toohello fabrikant voor vervanging of reparatie wordt het geretourneerd. Hallo gegevens op schijf hallo overschreven tooensure die Hallo gegevens kan niet worden hersteld door middel van.

## <a name="compute-isolation"></a>COMPUTE isolatie
Microsoft Azure biedt verschillende cloud-gebaseerde computers onder meer services als een groot aantal compute-exemplaren en services die kunnen worden geschaald omhoog en omlaag automatisch toomeet Hallo behoeften van uw toepassing of enterprise. Deze compute-exemplaar en de service bieden isolatie op meerdere niveaus toosecure gegevens zonder verlies van Hallo flexibiliteit in de configuratie die vraag van klanten.

### <a name="hyper-v--root-os-isolation-between-root-vm--guest-vms"></a>Hyper-V & hoofdmap OS-isolatie tussen & hoofdmap VM-Gast-VM 's
Azure rekenplatform is gebaseerd op de machine virtualisatie: wil zeggen dat alle code van de klant in een Hyper-V virtuele machine wordt uitgevoerd. Voor elke Azure-knooppunt (of netwerkeindpunt) is er een Hypervisor die rechtstreeks via Hallo hardware uitgevoerd en verdeelt van een knooppunt in het nummer van een variabele van de gast (virtuele Machines).


![Hyper-V & hoofdmap OS-isolatie tussen & hoofdmap VM-Gast-VM 's](./media/azure-isolation/azure-isolation-fig4.jpg)


Elk knooppunt heeft ook een speciale hoofdmap VM, die Hallo Host-OS wordt uitgevoerd. De grens van een kritieke is Hallo isolatie van Hallo basiscertificaten VM van Hallo Gast-VM's en Hallo Gast-VM's van elkaar, beheerd door de hypervisor Hallo en Hallo hoofdmap OS. Hallo hypervisor/root OS-koppeling maakt gebruik van Microsoft tientallen jaren besturingssysteem beveiliging ervaring, en meer recente leren van Microsoft Hyper-V, tooprovide sterke isolatie van Gast-VM's.

Hello Azure-platform maakt gebruik van een gevirtualiseerde omgeving. Gebruikersexemplaren werken als zelfstandige virtuele machines die geen toegang tot tooa fysieke host-server en deze isolatie wordt afgedwongen met behulp van de fysieke processor (ring-0-en ring 3) bevoegdheidsniveaus.

Ring 0 is Hallo meest privileged en 3 Hallo minste. Hallo gastbesturingssysteem wordt uitgevoerd in een minder bevoegdheden Ring 1 en toepassingen worden uitgevoerd Hallo laagst Ring 3. Deze virtualisatie van fysieke resources leidt tooa duidelijke scheiding tussen het gastbesturingssysteem en hypervisor, wat leidt tot extra beveiliging scheiding tussen twee Hallo.

Hello Azure hypervisor fungeert als een micro-kernel en worden alle hardware toegangsaanvragen van de Gast virtuele machines toohello host voor de verwerking met behulp van een gedeeld geheugen interface VMBus aangeroepen. Dit voorkomt dat gebruikers het verkrijgen van toegang voor onbewerkte lezen, schrijven/uitvoeren toohello system en verkleint Hallo risico van het delen van systeembronnen.

### <a name="advanced-vm-placement-algorithm--protection-from-side-channel-attacks"></a>Geavanceerde VM plaatsing algoritme & bescherming tegen kanaal aan clientzijde
Een aanval cross-VM bestaat uit twee stappen: plaatsen van een VM adversary beheerd op dezelfde als een Hallo slachtoffer VMs host Hallo en vervolgens schendingen veroorzaken Hallo isolatie grens tooeither slachtoffer gevoelige gegevens worden gestolen of de prestaties voor greed of vandalisme beïnvloeden. Microsoft Azure biedt bescherming op beide stappen met behulp van een geavanceerde VM plaatsing algoritme en beveiliging van alle bekende side kanaal aanvallen, met inbegrip van virtuele machines daarop.

### <a name="hello-azure-fabric-controller"></a>Hello Azure-Infrastructuurcontroller
Hello Azure-Infrastructuurcontroller is verantwoordelijk voor het toewijzen van infrastructuurresources tootenant werkbelastingen en het Unidirectioneel communicatie van Hallo toovirtual hostmachines beheert. Hallo VM brengen algoritme van hello Azure-infrastructuurcontroller is zeer geavanceerde en nagenoeg onmogelijk toopredict als fysieke hostniveau.

![Hello Azure-Infrastructuurcontroller](./media/azure-isolation/azure-isolation-fig5.png)

Hello Azure hypervisor afgedwongen geheugen en proces scheiding tussen virtuele machines en netwerkverkeer tooguest OS tenants veilig van routes. Dit voorkomt kans en aan clientzijde kanaal aanval op het niveau van de virtuele machine.

In Azure, Hallo hoofdmap VM is speciaal: een beperkte besturingssysteem Hallo hoofdmap OS aangeroepen dat als host fungeert voor een fabric-agent (VA) wordt uitgevoerd. VA worden gebruikt in Schakel toomanage Gast agents (GA) binnen gastbesturingssystemen van de klant virtuele machines. Door ook beheren opslagknooppunten.

Hallo verzameling van Azure hypervisor root OS/VA, en virtuele machines/GAs klant bestaat uit een rekenknooppunt. VA worden beheerd door een fabric-controller (FC), die buiten de berekenings- en knooppunten (berekenings- en -clusters worden beheerd door afzonderlijke FCs) bestaat. Als een klant updates hun toepassingsconfiguratiebestand terwijl deze wordt uitgevoerd, communiceert Hallo FC Hallo VA, die vervolgens GAs contact, die toepassing hello van Hallo configuratiewijziging melden. In geval van een hardwarefout Hallo Hallo FC automatisch beschikbare hardware vinden en er Hallo VM starten.

![Azure-Infrastructuurcontroller](./media/azure-isolation/azure-isolation-fig6.jpg)

Communicatie van de agent van een Infrastructuurcontroller tooan is Unidirectioneel. Hallo agent implementeert een service met SSL beveiligde die alleen toorequests van Hallo-controller reageert. Deze kan niet verbindingen toohello controller of andere bevoorrechte interne knooppunten starten. Hallo FC beschouwt alle antwoorden op dezelfde manier als niet-vertrouwd.


![Fabric-Controller](./media/azure-isolation/azure-isolation-fig7.png)

Isolatie breidt van Hallo VM van de hoofdmap van de Gast-VM's en Hallo Gast-VM's van elkaar. COMPUTE knooppunten zijn ook geïsoleerd van de configuratie voor opslagknooppunten voor een betere bescherming.


Hallo-hypervisor en Hallo hostbesturingssysteem bieden netwerkpakket - filters toohelp zorgen dat de niet-vertrouwde virtuele machines kan geen vervalste netwerkverkeer genereren of ontvangen toothem verkeer niet wordt besproken, direct verkeer tooprotected infrastructuur eindpunten of verzenden/ontvangen ongeschikte broadcast-verkeer.


### <a name="additional-rules-configured-by-fabric-controller-agent-tooisolate-vm"></a>Extra regels geconfigureerd door de Fabric-Controller Agent tooIsolate VM
Standaard worden al het verkeer wordt geblokkeerd als een virtuele machine wordt gemaakt en vervolgens Hallo fabric controller agent Hallo filter tooadd regels en uitzonderingen tooallow geautoriseerd pakketverkeer configureert.

Er zijn twee categorieën van regels die zijn geprogrammeerd:

-   **Configuratie of infrastructuur regels machine:** standaard alle communicatie is geblokkeerd. Er zijn uitzonderingen tooallow een virtuele machine toosend en DHCP en DNS-verkeer ontvangen. Virtuele machines kunnen ook verkeer toohello 'openbare' internet en verzenden verkeer tooother virtuele machines binnen hetzelfde virtuele Azure-netwerk Hallo en OS activeringsserver Hallo verzenden. Hallo virtuele machines lijst met toegestane uitgaande bestemmingen omvat geen Azure-router subnetten, Azure management en andere Microsoft-eigenschappen.

-   **Configuratiebestand van de rol:** Hiermee definieert u Hallo inkomende toegangsbeheerlijsten (ACL's) op basis van het servicemodel Hallo-tenant.

### <a name="vlan-isolation"></a>VLAN-isolatie
Er zijn drie VLAN's in elke cluster:

![VLAN-isolatie](./media/azure-isolation/azure-isolation-fig8.jpg)


-   Hallo verbindingen belangrijkste VLAN-niet-vertrouwde klant knooppunten

-   Hallo bevat FC VLAN – vertrouwde FCs- en ondersteunende systemen

-   Hallo apparaat VLAN-vertrouwd netwerk en andere infrastructuurapparaten bevat

Communicatie wordt toegestaan vanaf Hallo FC VLAN toohello belangrijkste VLAN te gebruiken, maar kan niet worden gestart vanaf Hallo belangrijkste VLAN toohello FC VLAN. Hallo belangrijkste VLAN toohello apparaat VLAN is ook communicatie geblokkeerd. Dit zorgt ervoor dat deze knooppunten op Hallo FC of apparaat VLAN's kan niet zelfs als een knooppunt met de klantcode ermee is geknoeid aanvallen.

## <a name="storage-isolation"></a>Isolatie van opslag
### <a name="logical-isolation-between-compute-and-storage"></a>Logische isolatie tussen berekeningen en opslag
Als onderdeel van het ontwerp van de fundamentele scheidt u Microsoft Azure berekeningen uit de opslag op basis van VM. Deze scheiding kunt berekening en opslag tooscale onafhankelijk, waardoor het gemakkelijker tooprovide multi-tenancymodus en isolatie.

Daarom berekent Azure Storage wordt uitgevoerd op afzonderlijke hardware met geen network connectivity tooAzure u behalve logisch. [Dit](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf) betekent dat wanneer een virtuele schijf wordt gemaakt, niet voor de volledige capaciteit schijfruimte. In plaats daarvan een tabel die is toegewezen adressen op Hallo virtuele schijf tooareas op Hallo fysieke schijf wordt gemaakt en die tabel in eerste instantie leeg is. **Hallo eerst die een klant gegevens op de virtuele schijf hello, schrijft ruimte op de fysieke schijf hello wordt toegewezen en een wijzer tooit wordt geplaatst in Hallo tabel.**
### <a name="isolation-using-storage-access-control"></a>Isolatie met behulp van Storage toegangsbeheer
**Toegangsbeheer in Azure Storage** een eenvoudige model voor toegangsbeheer heeft. Elk Azure-abonnement kunt maken van een of meer Accounts voor opslag. Elk Opslagaccount heeft een geheim dat is gebruikt toocontrol access tooall-gegevens in dit Opslagaccount.

![Isolatie met behulp van Storage toegangsbeheer](./media/azure-isolation/azure-isolation-fig9.png)

**Toegang tot tooAzure Storage-gegevens (inclusief tabellen)** kan worden beheerd via een [SAS (Shared Access Signature)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) token, welke verleent toegang binnen het bereik. Hallo is SAS gemaakt via een querysjabloon (URL) zijn ondertekend met Hallo [SAK (Opslagaccountsleutel)](https://msdn.microsoft.com/library/azure/ee460785.aspx). Die [ondertekend URL](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) tooanother proces (dat is gedelegeerd), die u kunt vervolgens Vul Hallo details van Hallo query en Hallo indienen van Hallo storage-service kan worden opgegeven. Een SAS kunt u toogrant toegang op basis van tijd tooclients zonder de geheime sleutel Hallo storage account weer te geven.

Hallo SAS betekent dat er een client beperkte machtigingen, tooobjects in onze storage-account gedurende een bepaalde tijd en met een opgegeven set machtigingen kunt verlenen. We kunnen deze beperkte rechten verlenen zonder tooshare de toegangssleutels van uw account.

### <a name="ip-level-storage-isolation"></a>IP-opslagniveau isolatie
U kunt tot stand brengen van firewalls en een IP-adresbereik opgeven voor uw vertrouwde clients. Met een IP-adresbereik alleen clients met een IP-adres binnen het bereik van Hallo gedefinieerd verbinding kunnen maken te[Azure Storage](https://docs.microsoft.com/azure/storage/storage-security-guide).

IP-storage-gegevens kunnen worden beveiligd tegen onbevoegde gebruikers via een VPN-mechanisme gebruikte tooallocate een tunnel toegewezen of speciale van verkeer tooIP opslag is.

### <a name="encryption"></a>Versleuteling
Azure biedt volgende typen versleuteling tooprotect gegevens:
-   Codering in transit

-   Versleuteling 'at rest'

#### <a name="encryption-in-transit"></a>Codering in Transit
Versleuteling onderweg is een mechanisme om gegevens te beveiligen wanneer deze worden verzonden via netwerken. U kunt beveiligen met behulp van gegevens met Azure Storage:

-   [Versleuteling transportniveau](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit), zoals HTTPS wanneer u gegevens van of naar Azure Storage overbrengen.

-   [Versleuteling Wire](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), zoals versleuteling door SMB 3.0 voor Azure-bestandsshares.

-   [Versleuteling aan clientzijde](https://docs.microsoft.com/azure/storage/storage-security-guide#using-client-side-encryption-to-secure-data-that-you-send-to-storage), tooencrypt Hallo gegevens voordat deze in opslag en toodecrypt Hallo gegevens overgedragen wordt nadat deze zijn overgebracht buiten een opslag.

#### <a name="encryption-at-rest"></a>Codering in rust
Voor veel organisaties [gegevensversleuteling in rust](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) is een verplichte stap naar privacy, naleving en gegevens onafhankelijkheid van gegevens. Er zijn drie Azure-functies waarmee de codering van gegevens die zich 'in rust':

-   [Versleuteling van de opslagruimte](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-at-rest) kunt u toorequest dat Hallo storage-service automatisch coderen van gegevens bij het schrijven van tooAzure opslag.

-   [Versleuteling aan clientzijde](https://docs.microsoft.com/azure/storage/storage-security-guide#client-side-encryption) biedt ook de functie Hallo van versleuteling in rust.

-   [Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) kunt u tooencrypt Hallo OS schijven en gegevensschijven die wordt gebruikt door een virtuele machine voor IaaS.

#### <a name="azure-disk-encryption"></a>Azure Disk Encryption
[Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) voor virtuele machines (VM's) kunt u bedrijfsbeveiligingsbeleid adres- en nalevingsvereisten door uw VM-schijven (inclusief opstart- en gegevensschijven) te versleutelen met sleutels en beleidsregels die u beheert in [Azure-sleutel Kluis](https://azure.microsoft.com/services/key-vault/).

Hallo schijfversleuteling oplossing voor Windows is gebaseerd op [Microsoft BitLocker-stationsversleuteling](https://technet.microsoft.com/library/cc732774.aspx), en Hallo Linux-oplossing is gebaseerd op [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt).

Hallo-oplossing ondersteunt Hallo volgen scenario's voor IaaS VM's wanneer ze zijn ingeschakeld in Microsoft Azure:
-   Integratie met Azure Sleutelkluis

-   Standard-laag VMs: A, D, DS, G, GS, enzovoort, reeks IaaS VM's

-   Codering voor Windows en Linux IaaS VM's inschakelen

-   Het uitschakelen van versleuteling op besturingssysteem en schijven voor Windows IaaS VM 's

-   Codering op gegevensstations voor Linux IaaS VM's uitschakelen

-   IaaS VM's waarop Windows client-OS-codering inschakelen

-   Versleuteling voor volumes met koppelpunten paden inschakelen

-   Inschakelen van versleuteling op Linux-virtuele machines die zijn geconfigureerd met de schijf (RAID) te verwijderen met behulp van [mdadm](https://en.wikipedia.org/wiki/Mdadm)

-   Inschakelen van versleuteling op Linux VM's met behulp van [LVM (beheer van logische volumes)](https://msdn.microsoft.com/library/windows/desktop/bb540532) voor gegevensschijven

-   Op Windows-virtuele machines die zijn geconfigureerd met behulp van opslagruimten-codering inschakelen

-   Alle openbare Azure-regio worden ondersteund

Hallo-oplossing biedt geen ondersteuning voor Hallo volgen scenario's, functies en -technologie in Hallo release:

-   Basisstaffel IaaS VM 's

-   Het uitschakelen van Linux IaaS VM's op een station OS versleuteling

-   IaaS VM's die zijn gemaakt met behulp van Hallo-methode voor het maken van klassieke VM

-   Integratie met uw on-premises Key Management Service

-   Azure Files (gedeelde bestandssysteem), Network File System (NFS), dynamische volumes en virtuele machines van Windows die zijn geconfigureerd met software gebaseerde RAID-systemen

## <a name="sql-azure-database-isolation"></a>SQL Azure Database isolatie
SQL-Database is een relationele database-service in Hallo Microsoft cloud op basis van Hallo toonaangevende Microsoft SQL Server-engine en kan afhandelen bedrijfskritieke werkbelastingen. SQL-Database biedt voorspelbare gegevensisolatie op niveau van de account, Geografie / regio op basis van en in het netwerk, met praktisch zonder beheer.

### <a name="sql-azure-application-model"></a>SQL Azure-toepassing-Model

[Microsoft SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-get-started) Database is een relationele database cloud-gebaseerde service gebouwd op de SQL Server-technologieën. Er is een maximaal beschikbare, schaalbare, multitenant databaseservice gehost door Microsoft in de cloud.

Vanuit het perspectief van een toepassing SQL Azure Hallo hiërarchie volgende biedt: elk niveau heeft een-op-veel containment van onderliggende niveaus.

![SQL Azure-toepassing-Model](./media/azure-isolation/azure-isolation-fig10.png)

Hallo-account en abonnement zijn Microsoft Azure-platform concepten tooassociate facturering en beheer.

Logische servers en databases SQL Azure-specifieke concepten en worden beheerd met behulp van SQL Azure opgegeven OData en TSQL-interfaces of via SQL Azure-portal geïntegreerd in de Azure-portal.

Azure SQL-servers zijn niet fysiek of VM-instanties, in plaats daarvan zijn verzamelingen van databases, beheer- en beveiligingsbeleid van die zijn opgeslagen in een zogenaamde 'logische master'-delen database.

![SQL Azure](./media/azure-isolation/azure-isolation-fig11.png)

Logische-hoofddatabases zijn onder andere:

-   SQL-aanmeldingen gebruikt tooconnect toohello server

-   Firewall-regels

Facturering en gebruik-gerelateerde informatie voor Azure SQL-databases van Hallo dezelfde logische server zijn niet gegarandeerd toobe op Hallo dezelfde fysiek exemplaar in Azure SQL-cluster, in plaats daarvan toepassingen moeten Hallo doel databasenaam opgeven om verbinding te maken.

Vanuit het oogpunt van de klant van een logische server gemaakt in een geografisch grafische regio, terwijl de werkelijke maken van de Hallo van server Hallo gebeurt in een Hallo-clusters in Hallo regio.

### <a name="isolation-through-network-topology"></a>Isolatie door middel van de netwerktopologie

Wanneer een logische server is gemaakt en de DNS-naam is geregistreerd, wijst Hallo DNS-naam toohello zogenaamde 'Gateway VIP'-adres in Hallo specifieke Datacenter waar Hallo-server is geplaatst.

Achter Hallo VIP (virtuele IP-adres) hebben we een verzameling stateless gatewayservices. Gateways ophalen in het algemeen betrokken wanneer er coördinatie nodig tussen meerdere gegevensbronnen (hoofddatabase, gebruikersdatabase, enzovoort). Gatewayservices implementeren Hallo volgende:
-   **TDS-verbinding via een proxy.** Dit omvat gebruikersdatabase in Hallo back-end-cluster te vinden, Hallo aanmeldingssequentie implementeren en vervolgens doorsturen Hallo TDS pakketten toohello back-end en terug.

-   **Database-beheer.** Dit omvat een verzameling van werkstromen toodo CREATE/ALTER/DROP databasebewerkingen implementeren. Hallo databasebewerkingen kunnen worden aangeroepen door sniffing TDS-pakketten of expliciete OData APIs.

-   CREATE/ALTER/DROP aanmeldingsgebruiker bewerkingen

-   Beheerbewerkingen logische server via de OData-API

![Isolatie door middel van de netwerktopologie](./media/azure-isolation/azure-isolation-fig12.png)

Hallo laag achter Hallo gateways wordt 'back-end' genoemd. Dit is waar alle Hallo gegevens wordt opgeslagen in een maximaal beschikbare manier. Elk gegevensitem is genoemde toobelong tooa 'partitie' of 'failover-eenheid', elk met ten minste drie replica's. Replica's worden opgeslagen en gerepliceerd door de engine van SQL Server en beheerd door een failover-systeem vaak tooas 'infrastructuur'.

In het algemeen communiceert Hallo back-end-systeem niet uitgaande tooother systemen veiligheidsoverwegingen. Dit is gereserveerde toohello systemen in Hallo front-end (gateway) laag. Hallo gateway laagmachines beperkt als een mechanisme defense-in-depth-bevoegdheden op Hallo back-end-machines toominimize Hallo kwetsbaarheid voor aanvallen.

### <a name="isolation-by-machine-function-and-access"></a>Isolatie per Machine functie en toegang
SQL Azure (is samengesteld uit de services worden uitgevoerd op andere machine functies. SQL Azure is onderverdeeld in back-end' Cloud-Database en de 'front-end' (Gateway/Management)-omgevingen, met Hallo algemene principe van verkeer alleen gaat naar de back-end en niet uit. Hallo front-omgeving kan communiceren toohello buiten de wereld van andere services en in het algemeen heeft slechts beperkte machtigingen in Hallo back-end (voldoende toocall Hallo ingangspunten deze behoeften tooinvoke).

## <a name="networking-isolation"></a>Isolatie van netwerken
Azure-implementatie bestaat uit meerdere lagen van netwerkisolatie. Hallo toont volgende diagram verschillende lagen van Azure toocustomers biedt netwerkisolatie. Deze lagen zijn zowel systeemeigen in hello Azure-platform zelf en de klant gedefinieerde functies. Inkomende van Hallo Internet, biedt Azure DDoS isolatie tegen grootschalige aanvallen op Azure. Hallo volgende beveiligingslaag isolatie is door de klant gedefinieerde openbare IP-adressen (eindpunten) die zijn gebruikt toodetermine welk verkeer Hallo cloud service toohello virtueel netwerk kunt doorgeven. Systeemeigen Azure virtuele netwerkisolatie garandeert volledige isolatie van alle andere netwerken, en dat alleen verkeersstromen via paden van de gebruiker die is geconfigureerd en methoden. Deze paden en methoden zijn de volgende laag hello, waar nsg's, UDR en virtuele netwerkapparaten gebruikte toocreate isolatie grenzen tooprotect Hallo implementaties van toepassingen in Hallo beveiligd netwerk kunnen worden.

![Isolatie van netwerken](./media/azure-isolation/azure-isolation-fig13.png)

**Isolatie van verkeer:** A [virtueel netwerk](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) Hallo verkeer isolatiegrens op Hallo Azure-platform is. Virtuele machines (VM's) in één virtueel netwerk kan niet communiceren rechtstreeks tooVMs in een ander virtueel netwerk, zelfs als beide virtuele netwerken worden gemaakt door Hallo dezelfde klant. Isolatie is een kritieke eigenschap die ervoor zorgt dat de klant VM's en communicatie blijft persoonlijke binnen een virtueel netwerk.

[Subnet](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#subnets) biedt een extra laag voor isolatie met in het virtuele netwerk op basis van IP-bereik. IP-adressen in het virtuele netwerk hello, kunt u een virtueel netwerk verdelen over meerdere subnetten voor organisatie en beveiliging. Virtuele machines en PaaS-rol instanties zijn geïmplementeerd toosubnets (dezelfde of verschillende) binnen een VNet kunnen met elkaar communiceren zonder extra configuratie. U kunt ook configureren [netwerkbeveiligingsgroep (nsg's)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#network-security-groups-nsg) tooallow of netwerkverkeer tooa VM-instantie op basis van regels die zijn geconfigureerd in de toegangsbeheerlijst (ACL) van het NSG weigeren. NSG's kunnen worden gekoppeld aan subnetten of afzonderlijke VM-exemplaren in dat subnet. Wanneer een NSG gekoppeld aan een subnet is, toepassing hello ACL-regels tooall Hallo VM-exemplaren in dat subnet.

## <a name="next-steps"></a>Volgende stappen

- [Opties voor netwerkisolatie voor Machines in Windows Azure virtuele netwerken](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/)

Dit omvat Hallo klassieke front-end en back-end scenario waar machines in een bepaalde back-endnetwerk of subnetwerk kunnen alleen toestaan dat bepaalde clients of andere computers tooconnect tooa bepaalde eindpunt op basis van een lijst met geaccepteerde IP-adressen.

- [COMPUTE isolatie](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

Microsoft Azure biedt een verschillende cloud-gebaseerde computers onder meer services als een groot aantal compute-exemplaren en services die kunnen worden geschaald omhoog en omlaag automatisch toomeet Hallo behoeften van uw toepassing of enterprise.

- [Isolatie van opslag](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

Microsoft Azure scheidt klant op basis van VM berekeningen uit de opslag. Deze scheiding kunt berekening en opslag tooscale onafhankelijk, waardoor het gemakkelijker tooprovide multi-tenancymodus en isolatie. Daarom berekent Azure Storage wordt uitgevoerd op afzonderlijke hardware met geen network connectivity tooAzure u behalve logisch. Alle aanvragen uitgevoerd via HTTP of HTTPS op basis van de keuze van de klant.

