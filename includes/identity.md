Het beheren van identiteit is net zo belangrijk in de openbare cloud als on-premises. Om dit te, ondersteunt Azure verschillende andere cloud identity-technologieën. Ze omvatten deze:

* U kunt Windows Server Active Directory (alleen AD opstartbestande wordt genoemd) in de cloud met behulp van virtuele machines die zijn gemaakt met Azure virtuele machines uitvoeren. Deze aanpak is wel zinvol wanneer u uw on-premises datacentrum in de cloud uitbreiden via Azure.
* U kunt Azure Active Directory geeft uw gebruikers eenmalige aanmelding voor [Software als een Service (SaaS)](https://azure.microsoft.com/overview/what-is-saas/) toepassingen. Van Microsoft Office 365 maakt gebruik van deze technologie bijvoorbeeld en toepassingen die worden uitgevoerd op Azure of andere cloudplatforms kunnen ook worden gebruikt.
* Toepassingen die worden uitgevoerd in de cloud of on-premises kunt toegangsbeheer van Azure Active Directory kunnen gebruikers zich aanmelden bij het gebruik van identiteiten van Facebook, Google, Microsoft en andere id-providers.

In dit artikel beschrijft alle drie deze opties.

## <a name="table-of-contents"></a>Inhoudsopgave
* [Windows Server Active Directory uitgevoerd op virtuele machines](#adinvm)
* [Met behulp van Azure Active Directory](#ad)
* [Met behulp van Azure Active Directory-toegangsbeheer](#ac)

## <a name="adinvm"></a>Windows Server Active Directory uitgevoerd op virtuele machines
Windows Server AD uitvoeren in virtuele machines in Azure, is vergelijkbaar met het lokale uitvoert. [Afbeelding 1](#fig1) toont een typisch voorbeeld van hoe dit eruitziet.

![Azure Active Directory in de virtuele Machine](./media/identity/identity_01_ADinVM.png)

<a name="Fig1"></a>Afbeelding 1: Windows Server Active Directory kunt uitvoeren in Azure virtuele machines die zijn verbonden met een organisatie on-premises datacentrum met behulp van Azure Virtual Network.

In het voorbeeld wordt Windows Server AD in virtuele machines die zijn gemaakt met behulp van Azure Virtual Machines, IaaS-technologie voor het platform worden uitgevoerd. Deze virtuele machines en enkele andere zijn gegroepeerd in een virtueel netwerk is verbonden met een on-premises datacentrum met behulp van Azure Virtual Network. Het virtuele netwerk carves uit een groep van cloud virtuele machines die met de on-premises netwerk via een virtueel particulier netwerk (VPN)-verbinding communiceren. Deze kunt doen deze Azure virtuele machines zien eruit als een ander subnet voor de on-premises datacentrum. Zoals u in de afbeelding ziet, worden twee van deze VMs domeincontrollers Windows Server AD uitgevoerd. De andere virtuele machines in het virtuele netwerk kan worden uitgevoerd als toepassingen, zoals SharePoint of worden gebruikt in een andere manier zoals voor het ontwikkelen en testen. De on-premises datacentrum twee Windows Server AD-domeincontrollers ook wordt uitgevoerd.

Er zijn verschillende opties voor het verbinden van de domeincontrollers in de cloud met de on-premises uitgevoerd:

* Controleer alle ze deel uitmaken van één Active Directory-domein.
* Maken van afzonderlijke AD-domeinen on-premises en in de cloud die deel uitmaken van hetzelfde forest bevinden.
* Maken van afzonderlijke AD-forests in de cloud en on-premises en verbind de forests met behulp van vertrouwensrelaties tussen forests of Windows Server Active Directory Federation Services (AD FS), die u ook in virtuele machines in Azure uitvoeren kunt.

Ongeacht de keuze is gemaakt, een beheerder moet ervoor zorgen dat verificatieaanvragen van on-premises gebruikers gaat u naar de cloud-domeincontrollers alleen indien nodig, omdat de koppeling naar de cloud is waarschijnlijk langzamer dan on-premises netwerken. Een andere afweging bij verbindende cloud en lokale domeincontrollers wordt verkeer dat wordt gegenereerd door middel van replicatie. Domeincontrollers in de cloud zijn meestal in hun eigen AD-site, die kan een beheerder om te plannen hoe vaak replicatie wordt uitgevoerd. Azure kosten voor verkeer dat buiten een Azure-datacenter wordt verzonden, maar niet voor bytes verzonden in die van invloed kunnen zijn op de replicatie-opties van de beheerder. Het is ook waard wijzen dat terwijl Azure een eigen Domain Name System (DNS)-ondersteuning biedt, deze service die vereist zijn voor Active Directory (zoals ondersteuning voor dynamische DNS- en SRV-records ontbreekt). Daarom vereist Windows Server AD uitgevoerd op Azure instellen van uw eigen DNS-servers in de cloud.

Windows Server AD uitgevoerd in Azure VM's kunt zinvol in diverse verschillende situaties. Hier volgen enkele voorbeelden:

* Als u Azure Virtual Machines gebruikt als een uitbreiding van uw eigen datacenter, kunt u toepassingen kunt uitvoeren in de cloud die lokale domeincontrollers voor het afhandelen van dingen zoals geïntegreerde Windows-verificatie aanvragen of LDAP-query's nodig. SharePoint, bijvoorbeeld communiceert regelmatig met Active Directory en dus het is mogelijk uit te voeren van een SharePoint-farm op Azure met behulp van een on-premises adreslijst, instellen van domeincontrollers in de cloud wordt prestaties aanzienlijk verbeteren. (Dit is er rekening mee dat dit is niet noodzakelijkerwijs vereist, maar; veel toepassingen kunnen probleemloos worden uitgevoerd in de cloud met alleen lokale domeincontrollers).
* Stel dat een veel filiaal beschikt niet over de resources voor uitvoering van een eigen domeincontrollers. Vandaag de dag haar gebruikers moeten worden geverifieerd met domeincontrollers op de andere kant van de hele wereld - aanmeldingen langzaam worden uitgevoerd. Active Directory worden uitgevoerd op Azure in een Microsoft-datacentrum dichter kunt versnellen dit zonder meer servers in het filiaal.
* Een organisatie die gebruikmaakt van Azure voor noodherstel mogelijk een kleine set van actieve virtuele machines in de cloud, met inbegrip van een domeincontroller onderhouden. Deze kan vervolgens worden voorbereid voor deze site, indien nodig over te nemen voor mislukte elders uitbreiden.

Er zijn ook andere mogelijkheden. Bijvoorbeeld, bent u niet vereist voor Windows Server AD in de cloud verbinden met een on-premises datacenter. Als u wilt uitvoeren van een SharePoint-farm die een bepaalde reeks gebruikers behandeld, voor het exemplaar van wie uitsluitend met cloud-gebaseerde identiteiten wilt aanmelden, u kunt een zelfstandige forest maken in Azure. Hoe u deze technologie gebruiken, is afhankelijk van wat de doelstellingen van uw zijn. (Voor meer richtlijnen gedetailleerde over het gebruik van Windows Server AD met Azure, [Hier ziet](http://msdn.microsoft.com/library/windowsazure/jj156090.aspx).)

## <a name="ad"></a>Met behulp van Azure Active Directory
SaaS-toepassingen komen meer algemene, ze een voor de hand liggende vraag verhogen: wat voor soort adreslijstservice moeten deze cloud-gebaseerde toepassingen gebruiken? Antwoord op die vraag van Microsoft is Azure Active Directory.

Er zijn twee manieren voor het gebruik van deze directoryservice in de cloud:

* Personen en organisaties die gebruikmaken van SaaS-toepassingen kunnen gebruikgemaakt van Azure Active Directory als de enige directoryservice.
* Organisaties met Windows Server Active Directory kunnen verbinding maken met hun on-premises directory naar Azure Active Directory en vervolgens gebruiken om aan te geven hun gebruikers eenmalige aanmelding tot SaaS-toepassingen.

[Afbeelding 2](#fig2) ziet u de eerste dag van deze twee opties, waarbij Azure Active Directory alle die vereist zijn.

![Azure Active Directory in de virtuele Machine](./media/identity/identity_02_AD.png)

<a name="fig2"></a>Afbeelding 2: Azure Active Directory biedt een organisatie gebruikers eenmalige aanmelding voor SaaS-toepassingen, waaronder Office 365.

Zoals u in de afbeelding ziet, is Azure AD een multitenant-service. Dit betekent dat veel verschillende organisaties opslaan van informatie over gebruikers op elk van deze directory gelijktijdig kan worden ondersteund. In dit voorbeeld wordt een gebruiker op de organisatie A probeert te openen van een SaaS-toepassing. Deze toepassing kan onderdeel zijn van Office 365, zoals SharePoint Online of mogelijk iets anders - niet-Microsoft-toepassingen kunnen ook gebruikmaken van deze technologie. Omdat Azure AD het SAML 2.0-protocol ondersteunt, is alle die vereist zijn van een toepassing de mogelijkheid om te communiceren met behulp van deze industrie-initiatief. (In feite toepassingen die gebruikmaken van Azure AD kunnen worden uitgevoerd in een datacenter, niet alleen een Azure-datacenter.)

Het wordt gestart wanneer de gebruiker een SaaS-toepassing (stap 1 opent). Voor het gebruik van deze toepassing, moet de gebruiker een token dat is uitgegeven door Azure AD aanwezig.

Dit token bevat informatie waarmee de gebruiker en het digitaal is ondertekend door Azure AD. Als u het token, de gebruiker wordt geverifieerd zelf naar Azure AD door te geven van een gebruikersnaam en wachtwoord (stap 2). Azure AD vervolgens het token retourneert hij moet (stap 3).

Dit token wordt verzonden naar de SaaS-toepassing (stap 4) en die valideert de handtekening van het token en die gebruikmaakt van de inhoud (stap 5). De toepassing wordt normaal gesproken de identiteitsgegevens die het token bevat om te bepalen welke informatie die de gebruiker is toegestaan voor toegang en mogelijk op andere manieren gebruiken.

Als de toepassing moet meer informatie over de gebruiker dan wat in het token opgenomen, kan deze dit aanvragen rechtstreeks vanuit Azure AD met behulp van de Azure AD Graph-API (stap 6). In de eerste versie van Azure AD het directory-schema is heel eenvoudig: het bevat alleen gebruikers en groepen en relaties tussen deze. Toepassingen kunnen gebruikmaken van deze informatie voor meer informatie over verbindingen tussen gebruikers. Stel bijvoorbeeld dat een toepassing moet weten wie de manager van deze gebruiker is om te bepalen of hij toegang tot sommige chunk van gegevens is toegestaan. Het kan informatie over dit door het uitvoeren van query's Azure AD via de Graph API.

De Graph-API maakt gebruik van een normale RESTful-protocol, waardoor het eenvoudig om het gebruik van de meeste clients, met inbegrip van mobiele apparaten. De API ondersteunt ook de uitbreidingen die zijn gedefinieerd door OData, dingen zoals een querytaal waarmee clients toegang tot gegevens in nuttiger manieren toe te voegen. (Zie voor meer informatie over OData [Introducing OData](http://download.microsoft.com/download/E/5/A/E5A59052-EE48-4D64-897B-5F7C608165B8/IntroducingOData.pdf).) Omdat de Graph API kunnen worden gebruikt voor meer informatie over de relaties tussen gebruikers, kan deze toepassingen inzicht in de sociale grafiek die ingesloten in het Azure AD-schema voor een bepaalde organisatie (dat is waarom heeft de Graph API aangeroepen). En om zichzelf te verifiëren met Azure AD Graph API-aanvragen, een toepassing maakt gebruik van OAuth 2.0.

Als een organisatie geen gebruik maakt van Windows Server Active Directory - het heeft geen lokale servers of domeinen - en uitsluitend gebruikmaakt van cloudtoepassingen die gebruikmaken van Azure AD, zou met alleen de clouddirectory van deze geven van de onderneming gebruikers eenmalige aanmelding tot ze allemaal. Nog terwijl dit scenario vaker elke dag wordt, nog steeds gebruik van de meeste organisaties on-premises domeinen gemaakt met Windows Server Active Directory. Azure AD heeft een nuttig rol spelen hier ook als [afbeelding 3](#fig3) bevat.

![Azure Active Directory in de virtuele Machine](./media/identity/identity_03_AD.png)
<a id="fig3"></a>afbeelding 3: een organisatie kan worden gefedereerd als u Windows Server Active Directory met Azure Active Directory zodat de gebruikers eenmalige aanmelding tot de SaaS-toepassingen.

In dit scenario wordt een gebruiker op de organisatie B wenst voor toegang tot een SaaS-toepassing. Voordat ze dit doet, moeten de directory-beheerders van de organisatie een federatieve relatie maken met Azure AD dat gebruikmaakt van AD FS, zoals in de afbeelding wordt weergegeven. Deze beheerders moet ook configureren voor gegevenssynchronisatie tussen de organisatie lokale Windows Server AD en Azure AD. Dit automatisch gekopieerd gebruiker en groepsinformatie uit de on-premises directory naar Azure AD. U ziet wat dit is toegestaan: de organisatie is In feite de on-premises adreslijst breiden naar de cloud. Combineren van Windows Server AD en Azure AD op deze manier biedt de organisatie een directoryservice die kan worden beheerd als één entiteit en toch een footprint hebben zowel on-premises en in de cloud.

Voor het gebruik van Azure AD, de gebruiker meldt zich eerst haar lokale Active Directory-domein gewoon (stap 1). Wanneer ze probeert te krijgen tot de SaaS-toepassing (stap 2), resulteert het federatieproces in Azure AD uitgeven haar een token voor deze toepassing (stap 3). (Zie voor meer informatie over de werking van federatieve [op Claims gebaseerde identiteit voor Windows: scenario's en technologieën](http://www.davidchappell.com/writing/white_papers/Claims-Based_Identity_for_Windows_v3.0--Chappell.docx).) Voordat u, bevat dit token informatie waarmee de gebruiker en het digitaal is ondertekend door Azure AD. Dit token wordt verzonden naar de SaaS-toepassing (stap 4) en die valideert de handtekening van het token en die gebruikmaakt van de inhoud (stap 5). En is in het vorige scenario, de toepassing de Graph API gebruiken kan om meer te weten over deze gebruiker als SaaS nodig (stap 6).

Vandaag de dag is een complete wijziging voor lokale Windows Server AD niet door Azure AD. Zoals al is vermeld, de clouddirectory heeft een veel eenvoudiger schema en ontbreekt ook dingen zoals Groepsbeleid, de mogelijkheid voor het opslaan van informatie over virtuele machines en ondersteuning voor LDAP. (In feite een Windows-machine kan niet worden geconfigureerd zodat gebruikers zich kunnen aanmelden met de niets anders dan Azure AD - dit wordt niet ondersteund scenario.) In plaats daarvan de oorspronkelijke doelstellingen van Azure AD zijn zodat gebruikers toegang tot bedrijfstoepassingen in de cloud zonder het onderhouden van een afzonderlijke aanmelding en vrijmaken on-premises directory-beheerders handmatig synchroniseren van hun on-premises directory met elke SaaS-toepassing die maakt gebruik van hun organisatie. Na verloop van tijd echter verwacht dat deze cloudservice directory voor het oplossen van een breed scala aan scenario's.

## <a name="ac"></a>Met behulp van Azure Active Directory-toegangsbeheer
Cloud-gebaseerde identiteit technologieën kunnen worden gebruikt voor het oplossen van tal van problemen. Azure Active Directory kunt geven van een organisatie gebruikers eenmalige aanmelding tot meerdere SaaS-toepassingen, bijvoorbeeld. Maar identiteit technologieën in de cloud kunnen ook op andere manieren worden gebruikt.

Stel bijvoorbeeld dat een toepassing om de gebruikers te laten wenst Meld u bij het gebruik van tokens die zijn uitgegeven door meerdere *id-providers (IdPs)*. Veel andere identiteitsproviders bestaan vandaag, met inbegrip van anderen, Facebook, Google en Microsoft en toepassingen kunt vaak gebruikers zich kunnen aanmelden met een van deze identiteiten. Waarom moet een toepassing lastig hoeft te vallen behoudt een eigen lijst met gebruikers en wachtwoorden wanneer deze identiteiten die al bestaan in plaats daarvan kunt vertrouwen? Bestaande identiteiten accepteren maakt leven eenvoudiger voor gebruikers met een minder gebruikersnaam en wachtwoord te onthouden, en om de mensen die de toepassing maken die niet langer hoeft te onderhouden van hun eigen lijst met gebruikersnamen en wachtwoorden.

Maar terwijl elke id-provider een soort token uitgeeft, wordt deze tokens worden standaard niet - elke IdP een eigen indeling heeft. Bovendien de informatie in deze tokens ook is niet standaard. Een toepassing die u wenst te accepteren van tokens die zijn uitgegeven door, spreken, Facebook, Google en Microsoft te maken met de uitdaging van de unieke code schrijven voor het afhandelen van elk van deze indelingen.

Maar waarom dit doen? Waarom niet maken in plaats daarvan intermediaire die één token indeling met een algemene representatie van gegevens van identiteit kan genereren? Deze aanpak zouden leven eenvoudiger voor de ontwikkelaars die toepassingen maken omdat ze nu nodig voor het afhandelen van slechts één type token. Azure Active Directory-toegangsbeheer wordt precies dit intermediaire in de cloud te bieden voor het werken met diverse tokens. [Afbeelding 4](#fig4) ziet u hoe het werkt

![Azure Active Directory in de virtuele Machine](./media/identity/identity_04_IdentityProviders.png)
<a id="fig4"></a>afbeelding 4: Azure Active Directory-toegangsbeheer maakt het eenvoudiger om toepassingen te accepteren identiteitstokens die door andere identiteitsproviders zijn uitgegeven.

Het wordt gestart wanneer een gebruiker probeert toegang tot de toepassing vanuit een browser. De toepassing leidt tot een IdP van haar keuze (en de toepassing ook vertrouwensrelaties). Ze worden zichzelf aan deze IdP zoals door in te voeren van een gebruikersnaam en wachtwoord (stap 1) en de IdP retourneert een token dat informatie bevat over haar (stap 2).

Als de afbeelding ziet, Access Control biedt ondersteuning voor tal van verschillende cloud-gebaseerde IdPs, met inbegrip van accounts die zijn gemaakt door Google, Yahoo, Facebook, Microsoft (voorheen Windows Live ID) en elke provider OpenID. Het ondersteunt ook identiteiten die zijn gemaakt met behulp van Azure Active Directory en via federatie met AD FS, Windows Server Active Directory. Het doel is vandaag de dag voor de meest gebruikte identiteiten of ze zijn uitgegeven door IdPs in de cloud of on-premises.

Als een browser van de gebruiker heeft een IdP-token van haar gekozen IdP, stuurt dit token aan toegangsbeheer (stap 3). Toegangsbeheer valideert het token, om ervoor te zorgen dat het echt is uitgegeven door deze IdP, en vervolgens maakt u een nieuw token volgens de regels die zijn gedefinieerd voor deze toepassing. Zoals Azure Active Directory, Access Control is een multitenant-service, maar de tenants worden toepassingen in plaats van de klant organisaties. Elke toepassing krijgt een eigen naamruimte, zoals in de afbeelding wordt weergegeven en verschillende regels over autorisatie en nog veel meer kunt definiëren.

Deze regels kunt definiëren hoe tokens van verschillende IdPs moeten worden omgezet in een Access Control-token van de toepassing-beheerder. Bijvoorbeeld, als verschillende IdPs verschillende typen gebruikt voor de vertegenwoordiging van gebruikersnamen, kunnen Access Control-regels transformeren al deze waarden in een algemeen type van de gebruikersnaam. Toegangsbeheer verzendt vervolgens dit nieuwe token terug naar de browser (stap 4), die aan de toepassing (stap 5) worden verzonden. Als dat zo het token voor toegangsbeheer is, controleert de toepassing of dat dit token echt is uitgegeven door de Access Control en gebruikt de informatie bevat (stap 6).

Tijdens dit proces een beetje ingewikkeld lijkt, daadwerkelijk maakt levensduur aanzienlijk eenvoudiger voor de maker van de toepassing. In plaats van uiteenlopende tokens met andere gegevens verwerken, kan de toepassing identiteiten die worden uitgegeven door meerdere id-providers tijdens het ontvangen van nog steeds alleen een één-token met bekende informatie accepteren. In plaats van elke toepassing zodanig worden geconfigureerd voor verschillende IdPs vertrouwen is vereist, ook deze vertrouwensrelaties in plaats daarvan worden beheerd door Access Control - een toepassing moet alleen vertrouwen.

Wordt het bewerken van af te wijzen dat niets over toegangsbeheer is gekoppeld aan Windows - kan net zo goed worden gebruikt door een Linux-toepassing die alleen Google en Facebook identiteiten geaccepteerd. En hoewel toegangsbeheer deel van de Azure Active Directory-familie uitmaakt, u kunt zien er als een geheel afzonderlijk service uit wat in de vorige sectie is beschreven. Hoewel beide technologieën met de identiteit werken, aanpakken ze heel anders problemen (Hoewel Microsoft heeft gemeld dat het integreren van de twee op een bepaald moment verwacht).

Werken met de identiteit is belangrijk in vrijwel elke toepassing. Het doel van toegangsbeheer is gemakkelijker voor ontwikkelaars die toepassingen te maken die de identiteiten van diverse identiteitsproviders accepteren. De toevoeging van deze service in de cloud, heeft Microsoft deze beschikbaar gemaakt voor elke toepassing die wordt uitgevoerd op elk platform.

## <a name="about-the-author"></a>Over de auteur
David Chappell wordt Principal van Chappell & gekoppeld [www.davidchappell.com](http://www.davidchappell.com) in San Francisco, Californië.

