<!--author=alkohli last changed: 01/12/17-->

### <a name="tootake-a-backup"></a>tootake een back-up

1. Ga tooyour Apparaatbeheer StorSimple-service. Uit Hallo in tabelvorm aanbieding van apparaten, selecteren en klik op het apparaat en klik vervolgens op **alle instellingen**. In Hallo **instellingen** blade te gaan**instellingen > beheren > back-up maken van beleid**.

    ![Back-upbeleid-toevoegen](./media/storsimple-8000-take-backup/step8takebu1.png)

2. In Hallo **back-up maken van beleid** blade, klikt u op **+ beleid toevoegen**.

    ![Back-upbeleid-toevoegen](./media/storsimple-8000-take-backup/step8takebu2.png)

3. In Hallo **back-upbeleid maken** blade, Geef een naam die tussen 3 en 150 tekens voor uw back-upbeleid bevat.

4. Selecteer Hallo volumes toobe back-up gemaakt. Als u meer dan één volume selecteert, zijn deze volumes gegroepeerde samen toocreate een crashconsistente back-up.

    ![Back-upbeleid-toevoegen](./media/storsimple-8000-take-backup/step8takebu4.png)

5. Op de blade **Eerste schema toevoegen**:

    1. Selecteer Hallo type back-up. Selecteer **Lokale momentopname** voor sneller herstellen. Selecteer **Cloudmomentopname** voor gegevenstolerantie.
    2. Geef de back-upfrequentie Hallo in minuten, uren, dagen of weken.
    3. Selecteer een bewaartijd. Hallo bewaren keuzen, is afhankelijk van de back-upfrequentie Hallo. Bijvoorbeeld: voor een dagelijkse beleid Hallo bewaren kan worden opgegeven in weken, terwijl de bewaarperiode voor een maandelijkse beleid in maanden.
    4. Selecteer Hallo datum en tijd van de back-upbeleid hello wordt gestart.
    5. Klik op **OK** toocreate Hallo back-upbeleid.

        ![Back-upbeleid-toevoegen](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. Klik op **maken** toostart Hallo back-upbeleid maken. U wordt gewaarschuwd wanneer de back-upbeleid Hallo is gemaakt. Hallo-lijst met back-upbeleid is tevens bijgewerkt.
      
      ![Back-upbeleid-toevoegen](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      U hebt nu een back-upbeleid voor geplande back-ups van uw volumegegevens.




