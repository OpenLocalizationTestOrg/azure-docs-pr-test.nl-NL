#### <a name="toocreate-a-cloud-appliance"></a>toocreate een cloud-apparaat

1. Ga in de Azure-portal hello, toohello **StorSimple Apparaatbeheer** service.
2. Ga toohello **apparaten** blade. Hallo opdrachtbalk in de blade overzicht Hallo-service, klik op **maken cloud toestel**.
    ![StorSimple- cloudapparaat maken](./media/storsimple-8000-create-cloud-appliance-u2/sca-create1.png)
3. In Hallo **maken cloud toestel** blade Hallo volgende details opgeven.
   
    ![StorSimple- cloudapparaat maken](./media/storsimple-8000-create-cloud-appliance-u2/sca-create2m.png)
   
   1. **Naam**: een unieke naam voor uw cloudapparaat.
   2. **Model** -model van Hallo cloud toestel Hallo kiezen. Een 8010-apparaat biedt 30 TB Standard-opslag terwijl 8020 64 TB Premium Storage heeft. Geef 8010 toodeploy ophaalscenario's op itemniveau vanuit back-ups. Selecteer 8020 toodeploy hoge prestaties, lage latentie werkbelastingen, of gebruik als een tweede apparaat voor herstel na noodgevallen.
   3. **Versie** -Hallo-versie van Hallo cloud toestel kiezen. Hallo-versie komt overeen toohello versie van de installatiekopie van de virtuele schijf Hallo die gebruikte toocreate Hallo cloud toestel is. De opgegeven versie van cloud Hallo Hallo toestel bepaalt welke fysieke apparaat u een failover of klonen vanaf, is het belangrijk dat u een juiste versie van Hallo cloud toestel maakt.
   4. **Virtueel netwerk** – Geef een virtueel netwerk dat u wilt dat toouse met dit toestel cloud. Als u Premium-opslag gebruikt, moet u een virtueel netwerk dat wordt ondersteund met Hallo Premium Storage-account selecteren. Hallo niet-ondersteunde virtuele netwerken worden lichter gekleurd weergegeven in de vervolgkeuzelijst Hallo. U wordt gewaarschuwd als u een niet-ondersteund virtueel netwerk selecteert.
   5. **Subnet** -Hallo vervolgkeuzelijst weergegeven op basis van Hallo virtueel netwerk hebt geselecteerd, subnetten Hallo die zijn gekoppeld. Een subnet tooyour cloud toestel toewijzen.
   6. **Storage-account** – Selecteer een toohold Hallo installatiekopie van het opslagaccount van Hallo cloud toestel tijdens het inrichten. Dit opslagaccount moet Hallo dezelfde regio bevinden als Hallo cloud toestel en virtuele netwerken. Deze mag niet worden gebruikt voor de opslag van gegevens door fysieke Hallo of Hallo cloud toestel. Voor dit doel wordt standaard een nieuw opslagaccount gemaakt. Echter, als u weet dat u al een opslagaccount die geschikt is voor dit gebruik hebt, kunt u deze uit de lijst Hallo. Als een apparaat van de cloud premium maakt, wordt Hallo vervolgkeuzelijst alleen Premium-opslagaccounts weergegeven.
      
      > [!NOTE]
      > Hallo cloud toestel kunt alleen met hello Azure storage-accounts werken.
    
   7. Selecteer Hallo selectievakje tooindicate die u begrijpen dat Hallo-gegevens die zijn opgeslagen op Hallo cloud toestel wordt gehost in een Microsoft-datacentrum.
       * Wanneer u alleen een fysiek apparaat gebruikt, wordt de versleutelingssleutel op uw apparaat opgeslagen. Daarom kan Microsoft deze niet ontsleutelen.

       * Wanneer u een cloud-apparaat gebruikt, worden zowel de versleutelingssleutel Hallo en Hallo ontsleutelingssleutel opgeslagen in Microsoft Azure. Zie de [beveiligingsoverwegingen voor het gebruik van een cloudapparaat](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security) voor meer informatie.
   8. Klik op **maken** tooprovision Hallo cloud toestel. Hallo apparaat duurt ongeveer 30 minuten toobe ingericht. U wordt gewaarschuwd wanneer Hallo cloud toestel is gemaakt. Ga tooDevices blade en Hallo lijst met apparaten vernieuwen toodisplay Hallo cloud toestel. Hallo-status van Hallo toestel is **tooset gereed**.
      
      ![StorSimple Cloud toestel gereed tooset up](./media/storsimple-8000-create-cloud-appliance-u2/sca-create3.png)

