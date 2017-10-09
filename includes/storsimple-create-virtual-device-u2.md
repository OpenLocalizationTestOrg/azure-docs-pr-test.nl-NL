#### <a name="toocreate-a-virtual-device"></a>een virtueel apparaat toocreate
1. Ga in de Azure-portal hello, toohello **StorSimple Manager** service.
2. Ga toohello **apparaten** pagina. Klik op **virtueel apparaat maken** onderin Hallo Hallo **apparaten** pagina.
3. In Hallo **dialoogvenster virtueelapparaat maken**, geef Hallo volgende details.
   
    ![Virtueel StorSimple-apparaat maken](./media/storsimple-create-virtual-device-u2/CreatePremiumsva1.png)
   
   1. **Naam**: een unieke naam voor uw virtuele apparaat.
   2. **Model** -model van het virtuele apparaat Hallo Hallo kiezen. Dit veld wordt alleen weergegeven als u Update 2 of hoger uitvoert. Een 8010-apparaatmodel biedt 30 TB Standard-opslag terwijl 8020 64 TB Premium Storage heeft. Geef 8010 op
   3. toodeploy ophaalscenario's op itemniveau vanuit back-ups. Selecteer 8020 toodeploy hoge prestaties, lage latentie werkbelastingen of wordt gebruikt als een tweede apparaat voor herstel na noodgevallen.
   4. **Versie** -versie van het virtuele apparaat Hallo Hallo kiezen. Als een 8020-Apparaatmodel wordt geselecteerd, worden klikt u vervolgens Hallo Versieveld niet weergegeven toohello gebruiker. Deze optie ontbreekt als alle Hallo fysieke apparaten die zijn geregistreerd met deze service worden uitgevoerd met Update 1 (of hoger). Dit veld wordt alleen weergegeven als er een mix van 1 vóór het bijwerken en Update 1 fysieke apparaten dat is geregistreerd bij Hallo dezelfde service. Gegeven Hallo versie van het virtuele apparaat Hallo bepaalt welk fysiek apparaat u kunt failover of klonen vanaf het is belangrijk dat u een juiste versie van het virtuele apparaat Hallo maakt. Selecteer:
      
      * Versie Update 0.3 voor failover of DR vanaf een fysiek apparaat met Update 0.3 of lager. 
      * Versie Update 1 voor failover of klonen vanaf een fysiek apparaat met Update 1 (of lager). 
   5. **Virtueel netwerk** – Geef een virtueel netwerk dat u wilt dat toouse met dit virtuele apparaat. Als u Premium-opslag (Update 2 of hoger), moet u een virtueel netwerk dat wordt ondersteund met Hallo Premium Storage-account selecteren. Hallo niet-ondersteunde virtuele netwerken worden lichter gekleurd weergegeven in de vervolgkeuzelijst Hallo. U wordt gewaarschuwd als u een niet-ondersteund virtueel netwerk selecteert. 
   6. **Opslagaccount voor het maken van virtuele apparaten** – Selecteer een toohold Hallo installatiekopie van het opslagaccount van het virtuele apparaat Hallo tijdens het inrichten. Dit opslagaccount moet Hallo dezelfde regio bevinden als het virtuele apparaat Hallo en virtuele netwerken. Deze mag niet worden gebruikt voor de opslag van gegevens door Hallo fysieke of virtuele Hallo-apparaat. Voor dit doel wordt standaard een nieuw opslagaccount gemaakt. Echter, als u weet dat u al een opslagaccount die geschikt is voor dit gebruik hebt, kunt u deze uit de lijst Hallo. Als een premium virtueel apparaat maakt, worden Hallo vervolgkeuzelijst alleen Premium-opslagaccounts weergegeven. 
      
      > [!NOTE]
      > Hallo virtueel apparaat kunt alleen met hello Azure storage-accounts werken. Andere cloudserviceproviders zoals Amazon, HP en OpenStack (die worden ondersteund voor het fysieke apparaat Hallo) worden niet ondersteund voor Hallo virtuele StorSimple-apparaat.
      > 
      > 
   7. Klik op Hallo vinkje tooindicate die u begrijpen dat Hallo-gegevens die zijn opgeslagen op het virtuele apparaat Hallo zal worden gehost in een Microsoft-datacentrum. Wanneer u alleen een fysiek apparaat gebruikt, wordt de versleutelingssleutel op uw apparaat opgeslagen. Daarom kan Microsoft deze niet ontsleutelen. 
      
       Wanneer u een virtueel apparaat gebruikt, worden zowel de versleutelingssleutel Hallo en Hallo ontsleutelingssleutel opgeslagen in Microsoft Azure. Zie de [beveiligingsoverwegingen voor het gebruik van een virtueel apparaat](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security) voor meer informatie.
   8. Klik op Hallo selectievakje pictogram toocreate Hallo virtueel apparaat. Hallo apparaat duurt ongeveer 30 minuten toobe ingericht.
      
      ![Aanmaakfase voor een virtueel StorSimple-apparaat](./media/storsimple-create-virtual-device-u2/StorSimple_VirtualDeviceCreating1M.png)

