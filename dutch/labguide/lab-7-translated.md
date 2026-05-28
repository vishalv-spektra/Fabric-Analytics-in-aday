# Microsoft Fabric - Fabric Analyst in a Day - Lab 7

![](../media/Lab-1/main7.jpg)

# Inhoudsopgave

- Inleiding

- Power BI

    - Taak 1: Rapport automatisch aanmaken

    - Taak 2: Achtergrond configureren voor een nieuw rapport

    - Taak 3: Koptekst toevoegen aan het rapport

    - Taak 4: KPI's toevoegen aan het rapport

    - Taak 5: Line chart toevoegen aan het rapport

    - Taak 6: Het rapport opslaan

    - Taak 7: Kolom Year configureren in de tabel Date

    - Taak 8: Kolom Month Name configureren in de tabel Date

    - Taak 9: Line chart opmaken

    - Taak 10: Power BI Desktop verbinden met het Semantic model

    - Taak 11: Nieuwe gegevens toevoegen om Direct Lake Mode te simuleren

- Labomgeving opruimen

- Referenties

# Inleiding

In deze cursus hebt u kennisgemaakt met de Lakehouse, hebt u gegevens vanuit verschillende databronnen in de Lakehouse geladen, een vernieuwingsschema voor de databronnen ingesteld en een datamodel aangemaakt. Nu gaat u een rapport maken.

Aan het einde van dit lab hebt u geleerd:

- Hoe u automatisch een rapport aanmaakt

- Hoe u een rapport opbouwt vanaf een leeg canvas

- Hoe u een rapport opbouwt met Power BI Desktop

- Hoe u Direct Lake mode ervaart, waarbij gegevens automatisch worden vernieuwd

# Power BI

## Taak 1: Rapport automatisch aanmaken

Laten we beginnen met de optie om het rapport automatisch aan te maken. Later in het lab maken we het rapport opnieuw dat we hebben in Power BI.

1. Navigeer terug naar de **Fabric-workspace** die u heeft aangemaakt in Lab 2, met de naam **FAIAD_<inject key="Deployment ID" enableCopy="false"/>**.

2. Selecteer onderin het linkerdeelvenster het pictogram **Fabric-ervaringskiezer**.

    ![](../media/Lab-7/image6.png)

3. Het dialoogvenster Fabric-ervaring wordt geopend. Selecteer **Power BI**. U wordt doorgestuurd naar de **Power BI-startpagina**.

    ![](../media/Lab-7/image7.png)

4. Selecteer **+ Nieuw rapport** in het bovenste menu.

    ![](../media/Lab-7/image8.png)

5. U wordt doorgestuurd naar het scherm **Uw eerste rapport bouwen**. Er zijn opties om een rapport te bouwen met Excel, CSV, gegevens handmatig in te voeren of een gepubliceerd semantisch model te kiezen. We hebben in de vorige labs een semantisch model aangemaakt, dus laten we dat gebruiken. Selecteer **Een gepubliceerd semantisch model kiezen**.

    ![](../media/Lab-7/image9.png)

6. Wanneer de pagina wordt geopend, kiest u een dataset om in uw rapport te gebruiken. U ziet dat we meerdere opties hebben. **Selecteer sm_FAIAD**.

    1. **sm_FAIAD:** Dit is het semantische model dat we hebben aangemaakt en dat we willen gebruiken om het rapport te bouwen.

    2. **lh_FAIAD:** Dit is de Lakehouse waar we alle gegevens in hebben geladen.

    3. **Units by Supplier:** Dit is de dataset die we hebben aangemaakt met T-SQL.

7. Klik op de **pijl naast de knop Rapport automatisch aanmaken**. U ziet dat er twee opties zijn: Rapport automatisch aanmaken en Een leeg rapport maken. Laten we het automatisch aanmaken uitproberen; selecteer **Automatisch rapport aanmaken**.

    ![](../media/Lab-7/image10.png)

8. Power BI begint het rapport automatisch aan te maken. Wanneer het rapport klaar is, verschijnt er rechtsboven in het scherm een dialoogvenster. Selecteer **Rapport nu weergeven**, of het wordt automatisch geladen over enkele seconden.

    ![](../media/Lab-7/image11.png)

    >**Controlepunt:** U beschikt nu over een rapport dat eruitziet zoals de onderstaande schermafbeelding. Er zijn een aantal KPI's en enkele trendvisuals. Dit is een goed startpunt als u een nieuw model analyseert en snel aan de slag wilt.

    >**Opmerking:** U ziet dat u in het bovenste menu de mogelijkheid heeft om het rapport te bewerken of sommige gegevens als tabellen te bekijken. U kunt deze opties vrijelijk verkennen.

9. Laten we dit rapport opslaan. Selecteer in het bovenste menu **Opslaan**.

10. Het dialoogvenster voor het opslaan van uw rapport wordt geopend. Geef het rapport de naam **rpt_Sales_Auto_Report**.

    >**Opmerking:** we voegen het voorvoegsel rpt toe aan de rapportnaam, wat een afkorting is van rapport.

11. Zorg ervoor dat het rapport wordt opgeslagen in uw workspace, **FAIAD_<inject key="Deployment ID" enableCopy="false"/>**.

12. Selecteer **Opslaan**.

    ![](../media/Lab-7/image12.png)
    
    >**Opmerking:** Het automatisch aangemaakt rapport kan er bij u anders uitzien, omdat het "automatisch aangemaakt" is. Dit is ook afhankelijk van de relaties en measures die u in het vorige lab (Lab 6) heeft aangemaakt.

    De bovenstaande schermafbeelding toont hoe het automatisch aangemaakt rapport er **mogelijk** uitziet als u alle relaties en measures heeft aangemaakt, inclusief de optionele relaties (Lab 6).

    De onderstaande schermafbeelding toont hoe het automatisch aangemaakt rapport er **mogelijk** uitziet als u het aanmaken van de optionele relaties en measures heeft overgeslagen (Lab 6).

    ![](../media/Lab-7/image13.png)

## Taak 2: Achtergrond configureren voor een nieuw rapport

Laten we een nieuw rapport maken met een leeg canvas.

1. Selecteer in het **linkerdeelvenster** de naam van uw workspace, **FAIAD_<inject key="Deployment ID" enableCopy="false"/>**, om naar de workspace te navigeren.

2. Selecteer in het bovenste menu **Nieuw item -> Rapport**. U wordt doorgestuurd naar de pagina voor het bouwen van uw eerste rapport.

    ![](../media/Lab-7/image14.png)

3. Selecteer **Een gepubliceerd semantisch model kiezen**, zodat we het model kunnen kiezen dat we hebben aangemaakt.

    ![](../media/Lab-7/image9.png)

4. Wanneer het dialoogvenster "Een semantisch model kiezen om in uw rapport te gebruiken" wordt geopend, selecteert u **sm_FAIAD**.

5. Klik op de **pijl naast de knop Rapport automatisch aanmaken**. Selecteer **Een leeg rapport maken**. U wordt doorgestuurd naar een rapportpagina die lijkt op de rapportpagina van Power BI Desktop.

    ![](../media/Lab-7/image15.png)

6. Als u dit nog niet heeft gedaan, open dan het bestand **FAIAD.pbix** in de map **Reports** op het **bureaublad** van uw labomgeving.

    We gaan dit rapport als referentie gebruiken. We beginnen met het toevoegen van de canvasachtergrond. We maken de rapportkoptekst aan, voegen een paar KPI's toe en maken de line chart Sales over time. In het belang van de tijd en met het begrip dat u ervaring heeft met het bouwen van visuals in Power BI Desktop, zullen we niet alle visuals aanmaken.

    ![](../media/Lab-7/image16.png)

7. Navigeer terug naar het **Power BI-canvas** in uw browser.

8. Selecteer het pictogram **Pagina opmaken** in het deelvenster **Visualisatie**.

9. Vouw de sectie **Canvasachtergrond** uit.

10. Selecteer **Bladeren** bij de optie **Afbeelding**. Het dialoogvenster Bestandsverkenner wordt geopend.

11. Navigeer naar de map **Reports** op het **bureaublad** van uw labomgeving.

12. Selecteer **Summary Background.png**.

13. Stel de vervolgkeuzelijst **Afbeeldingsaanpassing** in op **Passend maken**.

14. Stel de **Transparantie** in op **0%**.

    ![](../media/Lab-7/image17.png)

## Taak 3: Koptekst toevoegen aan het rapport

1. Laten we de koptekst toevoegen in de bovenste marge. Selecteer in het **menu** de optie **Tekstvak**.

2. Voer **Fabrikam Company** in als de eerste regel in het tekstvak.

3. Voer **Sales Report** in als de tweede regel in het tekstvak.

4. Markeer **Fabrikam Company** en stel **Lettertype** in op **Segoe UI** en **tekengrootte** op **18, vet**.

5. Markeer **Sales Report** en stel **Lettertype** in op **Segoe UI** en **tekengrootte** op **14**.

6. Met het **tekstvak geselecteerd**, vouwt u in het deelvenster **Tekstvak opmaken** aan de rechterkant **Effecten** uit.

7. Gebruik de schuifregelaar **Achtergrond** om deze in te stellen op **Uit**.

8. Pas de grootte van het **tekstvak aan zodat het in de bovenste marge past**.

    ![](../media/Lab-7/image18.png)

## Taak 4: KPI's toevoegen aan het rapport

1. Laten we de KPI Sales toevoegen. Selecteer de **lege ruimte** op het canvas om de focus van het tekstvak weg te halen.

2. Selecteer in de sectie **Visualisaties** de visual **Kaart**.

3. Vouw in de sectie **Gegevens** de tabel **Sales** uit.

4. Selecteer de measure **Sales**.

    ![](../media/Lab-7/image19.png)

5. Met de **Kaart-visual geselecteerd**, selecteert u het pictogram **Visual opmaken** in de sectie **Visualisaties**.

6. Vouw de sectie **Callout** uit.

7. Selecteer de vervolgkeuzelijst **Waarde**. Wijzig de tekengrootte naar **12**.

    ![](../media/Lab-7/image20.png)

8. Met de sectie **Callout** nog steeds geselecteerd, vouwt u de sectie **Label** uit.

9. Verklein de **tekengrootte** naar **10**.

10. Selecteer de vervolgkeuzelijst **Kleur**. Het dialoogvenster met het kleurenpalet wordt geopend.

11. Selecteer **Meer kleuren**.

12. Stel de hexadecimale waarde in op **#004753**.

    ![](../media/Lab-7/image21.png)

13. Vouw de sectie **Kaarten** uit.

14. Gebruik de schuifregelaar **Accentbalk** om deze in te stellen op **Uit**.

    ![](../media/Lab-7/image22.png)

15. Selecteer **Algemeen** in het deelvenster Visualisaties.

16. Vouw de sectie **Effecten** uit.

17. Gebruik de schuifregelaar **Achtergrond** om deze in te stellen op **Uit**.

18. Pas de grootte van de **visual** aan en verplaats deze naar **het linker vak zoals weergegeven in de schermafbeelding**.

    ![](../media/Lab-7/image23.png)

19. Laten we nog een kaart toevoegen. Selecteer de **Sales-kaart** die we zojuist hebben aangemaakt. **Kopieer** de visual door **Ctrl+C** op uw toetsenbord te selecteren.

20. **Plak** de visual door **Ctrl+V** op uw toetsenbord te selecteren. U ziet dat de visual op het canvas wordt geplakt.

21. Met de **nieuwe visual geselecteerd**, verwijdert u in de sectie **Visualisatiepaneel -> Visual bouwen -> Velden** de measure **Sales**.

22. Vouw vanuit de sectie **Gegevens** de tabel **Sales** uit en selecteer de measure **Units**.

23. Pas de grootte van de **visual** aan en **plaats deze in het vak onder de Sales-visual**.

    ![](../media/Lab-7/image24.png)

## Taak 5: Line chart toevoegen aan het rapport

Laten we een line chart maken om Sales over tijd per Reseller Company te visualiseren.


1. Selecteer de **lege ruimte** op het canvas om de focus van de multi-row card visual weg te halen.


2. Selecteer in de sectie **Visualizations** de **Line chart**.


3. Vouw in de sectie **Data** de tabel **Date** uit.


4. Selecteer het veld **Year**. U ziet dat Year standaard wordt opgeteld en aan de Y-axis wordt toegevoegd. Laten we dit corrigeren.

    ![](../media/Lab-7/image25.png)

## Taak 6: Het rapport opslaan

Laten we het rapport opslaan voordat we het rapport verlaten om wijzigingen in het model aan te brengen.


1. Selecteer in het menu **File -> Save**.


2. Het dialoogvenster voor het opslaan van uw rapport wordt geopend. Geef het rapport de naam **rpt_Sales_Report**.

    >**Opmerking:** We voegen het voorvoegsel rpt toe aan de rapportnaam, wat een afkorting is van rapport.

3. Zorg ervoor dat het rapport wordt opgeslagen in de workspace **FAIAD_<inject key="Deployment ID" enableCopy="false"/>**.


4. Selecteer **Save**. U ziet dat het rapport is opgeslagen en dat u zich in de weergavemodus bevindt.

    ![](../media/Lab-7/image26.png)

## Taak 7: Kolom Year configureren in de tabel Date


1. Selecteer in het **bovenste menu** de optie **Edit** om terug te gaan naar de bewerkingsmodus.

    ![](../media/Lab-7/image27.png)


2. Selecteer in het **bovenste menu** de optie **Open semantic model**. U ziet dat het semantic model wordt geopend in een nieuw browservenster of -tabblad.

    ![](../media/Lab-7/image28.png)


3. Schakel in de rechterbovenhoek naar de modus **Editing**.


4. Selecteer vanuit het **deelvenster Data aan de rechterkant** de optie Tables.


5. Vouw de tabel **Date** uit.


6. Selecteer de kolom **Year**.


7. Vouw in het deelvenster **Properties** aan de linkerkant de sectie **Advanced** uit.


8. Selecteer in de vervolgkeuzelijst **Summarize by** de optie **None**.

    ![](../media/Lab-7/image29.png)


9. Navigeer terug naar het **rapportvenster of -tabblad** van de browser.


10. Vouw in het **deelvenster Data** aan de rechterkant de tabel **Date** uit. U ziet dat Year geen sommatieveld meer is.


11. Met de **Line chart visual geselecteerd**, verwijdert u **Sum of Year** van de Y-axis.


12. Selecteer het veld **Year** en het wordt aan de **X-axis** toegevoegd.


13. Vouw de tabel **Sales** uit en selecteer de measure **Sales**.

    ![](../media/Lab-7/image30.png)

## Taak 8: Kolom Month Name configureren in de tabel Date


1. Laten we Month aan dit diagram toevoegen. Sleep vanuit de tabel Date het veld **MonthNameShort** onder **Year** in de **X-axis**. U ziet dat de visual is gesorteerd op Sales. Laten we het sorteren op **MonthNameShort**.


2. Selecteer het **beletselteken (…)** in de rechterbovenhoek van de visual.


3. Selecteer **Sort by -> Year Short_Month_Name**.


4. Selecteer het **beletselteken (…)** in de rechterbovenhoek van de visual.


5. Selecteer **Sort by -> Sort ascending**.

    ![](../media/Lab-7/L8T5P3.png)

    >**Opmerking:** De maanden zijn alfabetisch gesorteerd. Laten we dit oplossen.

    ![](../media/Lab-7/image32.png)


6. Navigeer terug naar het **browservenster of -tabblad** waar u het semantic model geopend heeft.


7. Vouw in het deelvenster **Data** de tabel **Date** uit.


8. Selecteer de kolom **MonthNameShort**.


9. Vouw in het deelvenster **Properties** aan de linkerkant de sectie **Advanced** uit.


10. Selecteer in de vervolgkeuzelijst **Sort by column** de optie **Month**.

    ![](../media/Lab-7/image33.png)


11. Navigeer terug naar het **rapportvenster of -tabblad** van de browser. U ziet dat de maanden nu correct zijn gesorteerd.

    ![](../media/Lab-7/image34.png)

## Taak 9: Line chart opmaken

U ziet hoe eenvoudig het is om het semantic model bij te werken terwijl u rapporten bouwt. Dit geeft een naadloze interactie zoals in Power BI Desktop.

1. Met de **Line chart visual geselecteerd**, vouwt u in de sectie **Data** de tabel **Reseller** uit.

1. Sleep het veld **Reseller -> Reseller Company** naar de sectie **Legend**.

    ![](../media/Lab-7/image35.png)

1. Met de **Line chart visual geselecteerd**, selecteert u vanuit de sectie **Visualization** het pictogram **Format visual icon -> General**.

1. Vouw de sectie **Title** uit.

1. Stel de tekst **Title** in op **Sales over time**.

1. Vouw de sectie **Effects** uit.

1. Gebruik de schuifregelaar **Background** om deze in te stellen op **Off**.

    ![](../media/Lab-7/image36.png)

1. Selecteer vanuit de sectie **Visualization** het pictogram **Format visual icon -> Visual**.

1. Vouw de sectie **Lines** uit.

1. Selecteer in de vervolgkeuzelijst **Apply settings to -> Series** de optie **Tailspin Toys**.

1. Vouw de sectie **Colors** uit.

1. Stel de **color** in op **#F17925**.

1. Selecteer in de vervolgkeuzelijst **Apply settings to -> Series** de optie **Wingtip Toys**.

1. Stel de **color** in op **#004753**.

1. Pas de grootte van de **visual** aan en verplaats deze naar **het vak rechtsboven zoals weergegeven in de schermafbeelding**.

1. Scroll naar rechts in de visual en **merk op dat we gegevens hebben tot en met april 2024**.

    ![](../media/Lab-7/image37.png)

1. Laten we het rapport opslaan; selecteer in het menu **File -> Save**.

    Zoals eerder vermeld, zullen we in dit lab niet alle visuals bouwen. In uw eigen tijd kunt u gerust meer visuals bouwen.

## Taak 10: Power BI Desktop verbinden met het Semantic model

Laten we nu zien hoe eenvoudig het is om Power BI Desktop te verbinden met het semantic model en visuals te bouwen.


1. Open het bestand **FAIADTemplate.pbix** in de map **Reports** op het **bureaublad** van uw labomgeving.


2. Selecteer in het lint **Home -> OneLake Catalog -> Power BI semantic models**.

    ![](../media/Lab-7/image38.png)


3. Het dialoogvenster OneLake data hub wordt geopend. Selecteer **sm_FAIAD**, het semantic model dat we hebben aangemaakt.


4. Selecteer **Connect**. U ziet dat het deelvenster Data de tabellen uit het semantic model bevat.

    ![](../media/Lab-7/image39.png)


5. Selecteer in het **linkerdeelvenster** de **Model view**. U ziet dat we de relaties tussen tabellen kunnen bekijken.

    ![](../media/Lab-7/image40.png)


6. Selecteer in het **linkerdeelvenster** de **Report view** om terug te navigeren naar de rapportweergave.


7. Als u dit nog niet heeft gedaan, open dan het bestand **FAIAD.pbix** in de map **Reports** op het **bureaublad** van uw labomgeving.


8. Selecteer de **rapporttitel visual**.


9. Selecteer in het lint **Home -> Copy**.

    ![](../media/Lab-7/image41.png)


10. Navigeer naar **FAIADTemplate.pbix** en selecteer het rapportcanvas.


11. Selecteer in het lint **Home -> Paste**.

    ![](../media/Lab-7/image42.png)


12. Kopieer en plak op dezelfde manier de **KPI's Sales en Units**. Ter informatie – meerdere visuals kunnen tegelijk worden gekopieerd en geplakt.

    ![](../media/Lab-7/image43.png)

    U ziet dat het eenvoudig is om visuals uit een bestaand rapport te kopiëren en te plakken in een rapport dat verbinding maakt met een semantic model. Houd er rekening mee dat de tabelnamen, kolomnamen en measurenamen identiek moeten zijn om kopiëren en plakken te laten werken. Als ze niet identiek zijn, kan er een fout optreden, maar dit is gemakkelijk op te lossen.


13. Navigeer naar **FAIAD.pbix** en selecteer de line chart Sales over time.


14. Selecteer in het lint **Home -> Copy**.


15. Navigeer naar **FAIADTemplate.pbix** en selecteer het rapportcanvas.


16. Selecteer in het lint **Home -> Paste**. U ziet dat de visual niet wordt weergegeven. Dit komt doordat het semantic model momenteel geen hiërarchie maakt op basis van het datumveld.


17. Laten we dit oplossen. Verwijder in het deelvenster **Visualization**, onder **X-axis**, het veld **StartOfMonth**.

    ![](../media/Lab-7/image44.png)


18. Vouw vanuit het **deelvenster Data** de tabel **Date** uit.


19. Sleep het veld **StartOfMonth** naar de **X-axis**. Hiermee wordt de visual hersteld. Mogelijk moet u de visual nog opmaken.

    ![](../media/Lab-7/image45.png)


20. Laten we het rapport opslaan; selecteer in het lint **File -> Save**.

## Taak 11: Nieuwe gegevens toevoegen om Direct Lake Mode te simuleren

Normaal gesproken moeten we bij Import mode, zodra de gegevens in de bron zijn vernieuwd, het Power BI model vernieuwen, waarna de gegevens in het rapport worden bijgewerkt. Bij Direct query mode zijn de gegevens direct beschikbaar in het Power BI rapport zodra ze in de bron zijn vernieuwd. Direct query mode is echter doorgaans traag. Om dit probleem op te lossen, heeft Microsoft Fabric Direct Lake mode geïntroduceerd. Direct Lake is een snelle manier om gegevens rechtstreeks vanuit de lake in de Power BI engine te laden, klaar voor analyse.

Laten we het scenario verkennen waarbij gegevens worden bijgewerkt in ADLS Gen2 en de wijzigingen onmiddellijk worden weergegeven in het Power BI rapport zonder dat er vernieuwingen hoeven te worden uitgevoerd.

In een werkelijk scenario worden gegevens bijgewerkt bij de bron. Omdat we ons in een trainingsomgeving bevinden, simuleren we dit. We hebben verkoopgegevens tot en met april 2024. Laten we verkoopgegevens voor mei 2024 toevoegen door een shortcut te maken naar het bestand van mei 2024 in ADLS Gen2 en de Sales view bij te werken.

1. Navigeer terug naar de **browser**.

2. Klik in de rechterbenedenhoek op het **Fabric logo** en schakel over naar de **Fabric view**.

3. Selecteer **FAIAD_<inject key="Deployment ID" enableCopy="false"/>** in de linker menubalk om naar de workspace home te navigeren.

4. Selecteer **lh_FAIAD** om naar de Lakehouse te navigeren.

    ![](../media/Lab-7/image46.png)

5. Selecteer in het **deelvenster Explorer** aan de linkerkant het **beletselteken** naast **Tables**.


6. Selecteer **New shortcut**.

    ![](../media/Lab-7/image47.png)


7. Het dialoogvenster New shortcut wordt geopend. Selecteer onder **External sources** de optie **Azure Data Lake Storage Gen2**.

    ![](../media/Lab-7/image48.png)


8. Omdat u eerder in de labs al een verbinding heeft aangemaakt, hoeft u geen nieuwe verbinding aan te maken en ziet u uw ADLS verbinding onder de bestaande verbindingen.


9. Als u deze verbinding eerder in de cursus niet heeft aangemaakt, klikt u op **Create New connection** en voert u de volgende stappen uit:


10. Voer onder **Connection Settings -> URL** de volgende link in: **https://stvnextblobstorage.dfs.core.windows.net/fabrikam-sales**


11. Selecteer **Next**.

    ![](../media/Lab-7/image49.png)


12. U maakt verbinding met ADLS Gen2 waarbij de mappenstructuur wordt weergegeven in het linkerdeelvenster. Vouw **Delta-Parquet-Format-FY25** uit.


13. Selecteer **Sales.Invoices_May**.


14. Selecteer **Next**.

    ![](../media/Lab-7/image50.png)


15. U wordt doorgestuurd naar het volgende dialoogvenster waar u de namen kunt bewerken. Selecteer het **bewerkingspictogram** onder Actions voor **Sales.Invoices_May**.


16. Hernoem **Sales.Invoices_May** naar **InvoicesMay**.


17. Selecteer het **vinkje** naast de naam om de wijziging op te slaan.


18. Selecteer **Create**.

    ![](../media/Lab-7/image51.png)

    U ziet in het **deelvenster Explorer** aan de linkerkant dat we nu de tabel InvoicesMay hebben. Nu moeten we de Sales view bijwerken.

19. Selecteer rechtsboven in het scherm **Lakehouse -> SQL analytics endpoint**.

    ![](../media/Lab-7/image52.png)

20. Selecteer in het bovenste menu **Home -> New SQL query**. Er wordt een nieuw SQL query-deelvenster geopend.

21. **Kopieer** de onderstaande code en **plak** deze in het **SQL query-deelvenster**.

    ```
    ALTER VIEW [dbo].[Sales] AS (
    select [$Outer].[InvoiceLineID] as [InvoiceLineID],
        [$Outer].[InvoiceID] as [InvoiceID],
        [$Outer].[StockItemID] as [StockItemID],
        [$Outer].[Quantity] as [Quantity],
        [$Outer].[UnitPrice] as [UnitPrice],
        [$Outer].[TaxRate] as [TaxRate],
        [$Outer].[TaxAmount] as [TaxAmount],
        [$Outer].[LineProfit] as [LineProfit],
        [$Outer].[ExtendedPrice] as [ExtendedPrice],
        [$Outer].[CustomerID] as [ResellerID],
        [$Outer].[SalespersonPersonID] as [SalespersonPersonID],
        [$Outer].[InvoiceDate] as [InvoiceDate],
        [$Outer].[t0_0] as [Sales Amount]
    from 
    (
        select [_].[InvoiceLineID] as [InvoiceLineID],
            [_].[InvoiceID] as [InvoiceID],
            [_].[StockItemID] as [StockItemID],
            [_].[Quantity] as [Quantity],
            [_].[UnitPrice] as [UnitPrice],
            [_].[TaxRate] as [TaxRate],
            [_].[TaxAmount] as [TaxAmount],
            [_].[LineProfit] as [LineProfit],
            [_].[ExtendedPrice] as [ExtendedPrice],
            [_].[CustomerID] as [CustomerID],
            [_].[SalespersonPersonID] as [SalespersonPersonID],
            [_].[InvoiceDate] as [InvoiceDate],
            [_].[ExtendedPrice] - [_].[TaxAmount] as [t0_0]
        from 
        (
            select [$Outer].[InvoiceLineID],
                [$Outer].[InvoiceID],
                [$Outer].[StockItemID],
                [$Outer].[Quantity],
                [$Outer].[UnitPrice],
                [$Outer].[TaxRate],
                [$Outer].[TaxAmount],
                [$Outer].[LineProfit],
                [$Outer].[ExtendedPrice],
                [$Inner].[CustomerID],
                [$Inner].[SalespersonPersonID],
                [$Inner].[InvoiceDate]
            from [lh_FAIAD].[dbo].[InvoiceLineItems] as [$Outer]
            inner join 
            (
                select [_].[InvoiceID] as [InvoiceID2],
                    [_].[CustomerID] as [CustomerID],
                    [_].[BillToResellerID] as [BillToResellerID],
                    [_].[OrderID] as [OrderID],
                    [_].[DeliveryMethodID] as [DeliveryMethodID],
                    [_].[ContactPersonID] as [ContactPersonID],
                    [_].[AccountsPersonID] as [AccountsPersonID],
                    [_].[SalespersonPersonID] as [SalespersonPersonID],
                    [_].[PackedByPersonID] as [PackedByPersonID],
                    [_].[InvoiceDate] as [InvoiceDate],
                    [_].[CustomerPurchaseOrderNumber] as [CustomerPurchaseOrderNumber],
                    [_].[IsCreditNote] as [IsCreditNote],
                    [_].[CreditNoteReason] as [CreditNoteReason],
                    [_].[Comments] as [Comments],
                    [_].[DeliveryInstructions] as [DeliveryInstructions],
                    [_].[InternalComments] as [InternalComments],
                    [_].[TotalDryItems] as [TotalDryItems],
                    [_].[TotalChillerItems] as [TotalChillerItems],
                    [_].[DeliveryRun] as [DeliveryRun],
                    [_].[RunPosition] as [RunPosition],
                    [_].[ReturnedDeliveryData] as [ReturnedDeliveryData],
                    [_].[ConfirmedDeliveryTime] as [ConfirmedDeliveryTime],
                    [_].[ConfirmedReceivedBy] as [ConfirmedReceivedBy],
                    [_].[LastEditedBy] as [LastEditedBy2],
                    [_].[LastEditedWhen] as [LastEditedWhen2]
                from 
                (
                    select [$Table].[InvoiceID] as [InvoiceID],
                        [$Table].[CustomerID] as [CustomerID],
                        [$Table].[BillToResellerID] as [BillToResellerID],
                        [$Table].[OrderID] as [OrderID],
                        [$Table].[DeliveryMethodID] as [DeliveryMethodID],
                        [$Table].[ContactPersonID] as [ContactPersonID],
                        [$Table].[AccountsPersonID] as [AccountsPersonID],
                        [$Table].[SalespersonPersonID] as [SalespersonPersonID],
                        [$Table].[PackedByPersonID] as [PackedByPersonID],
                        [$Table].[InvoiceDate] as [InvoiceDate],
                        [$Table].[CustomerPurchaseOrderNumber] as [CustomerPurchaseOrderNumber],
                        [$Table].[IsCreditNote] as [IsCreditNote],
                        [$Table].[CreditNoteReason] as [CreditNoteReason],
                        [$Table].[Comments] as [Comments],
                        [$Table].[DeliveryInstructions] as [DeliveryInstructions],
                        [$Table].[InternalComments] as [InternalComments],
                        [$Table].[TotalDryItems] as [TotalDryItems],
                        [$Table].[TotalChillerItems] as [TotalChillerItems],
                        [$Table].[DeliveryRun] as [DeliveryRun],
                        [$Table].[RunPosition] as [RunPosition],
                        [$Table].[ReturnedDeliveryData] as [ReturnedDeliveryData],
                        [$Table].[ConfirmedDeliveryTime] as [ConfirmedDeliveryTime],
                        [$Table].[ConfirmedReceivedBy] as [ConfirmedReceivedBy],
                        [$Table].[LastEditedBy] as [LastEditedBy],
                        [$Table].[LastEditedWhen] as [LastEditedWhen]
                    from [lh_FAIAD].[dbo].[Invoices] as [$Table]
                    union all select [$Table].[InvoiceID] as [InvoiceID],
                        [$Table].[CustomerID] as [CustomerID],
                        [$Table].[BillToResellerID] as [BillToResellerID],
                        [$Table].[OrderID] as [OrderID],
                        [$Table].[DeliveryMethodID] as [DeliveryMethodID],
                        [$Table].[ContactPersonID] as [ContactPersonID],
                        [$Table].[AccountsPersonID] as [AccountsPersonID],
                        [$Table].[SalespersonPersonID] as [SalespersonPersonID],
                        [$Table].[PackedByPersonID] as [PackedByPersonID],
                        [$Table].[InvoiceDate] as [InvoiceDate],
                        [$Table].[CustomerPurchaseOrderNumber] as [CustomerPurchaseOrderNumber],
                        [$Table].[IsCreditNote] as [IsCreditNote],
                        [$Table].[CreditNoteReason] as [CreditNoteReason],
                        [$Table].[Comments] as [Comments],
                        [$Table].[DeliveryInstructions] as [DeliveryInstructions],
                        [$Table].[InternalComments] as [InternalComments],
                        [$Table].[TotalDryItems] as [TotalDryItems],
                        [$Table].[TotalChillerItems] as [TotalChillerItems],
                        [$Table].[DeliveryRun] as [DeliveryRun],
                        [$Table].[RunPosition] as [RunPosition],
                        [$Table].[ReturnedDeliveryData] as [ReturnedDeliveryData],
                        [$Table].[ConfirmedDeliveryTime] as [ConfirmedDeliveryTime],
                        [$Table].[ConfirmedReceivedBy] as [ConfirmedReceivedBy],
                        [$Table].[LastEditedBy] as [LastEditedBy],
                        [$Table].[LastEditedWhen] as [LastEditedWhen]
                    from [lh_FAIAD].[dbo].[InvoicesMay] as [$Table]
                ) as [_]
            ) as [$Inner] on ([$Outer].[InvoiceID] = [$Inner].[InvoiceID2] or [$Outer].[InvoiceID] is null and [$Inner].[InvoiceID2] is null)
        ) as [_]
    ) as [$Outer]
    where exists 
    (
        select 1
        from 
        (
            select [ResellerID]
            from [lh_FAIAD].[dbo].[Reseller] as [$Table]
        ) as [$Inner]
        where [$Outer].[CustomerID] = [$Inner].[ResellerID] or [$Outer].[CustomerID] is null and [$Inner].[ResellerID] is null
    )
    )
    ```

22. Selecteer in het menu van de visuele query de optie **Run** om de code uit te voeren.

    Zodra de code is uitgevoerd, hebben we de tabel Sales bijgewerkt met de gegevens van mei 2024.

    ![](../media/Lab-7/image53.png)

23. Selecteer **rpt_Sales_Report** in de linker menubalk om terug te navigeren naar het rapport.


24. Selecteer in het bovenste menu het **pictogram Vernieuwen**. U ziet nu in de Line chart gegevens voor mei 2024. U ziet ook dat het verkoopbedrag is toegenomen.

    ![](../media/Lab-7/image54.png)

    We hoeven het datamodel en het rapport niet te vernieuwen wanneer de gegevens worden gewijzigd. Dit is het voordeel van Direct Lake en Direct query.

    Laten we de uitdagingen opnieuw bekijken die zijn opgesomd in de probleemstelling:

    - **U moet uw dataset minimaal drie keer per dag vernieuwen om rekening te houden met de verschillende bijwerktijden voor de verschillende databronnen**.

        Dit hebben we opgelost met behulp van Direct Lake. Elke afzonderlijke Dataflow wordt vernieuwd volgens zijn eigen schema. Datasets en rapporten hoeven niet te worden vernieuwd.

    - **Uw vernieuwingsbewerkingen duren lang omdat u telkens een volledige vernieuwing moet uitvoeren om alle updates die in de bronsystemen zijn doorgevoerd vast te leggen**.

        Dit hebben we eveneens opgelost met behulp van Direct Lake. Elke afzonderlijke Dataflow wordt vernieuwd volgens zijn eigen schema. Datasets en rapporten hoeven niet te worden vernieuwd, dus we hoeven ons geen zorgen te maken over een volledige vernieuwing.

    - **Eventuele fouten in een van de databronnen waaruit u gegevens haalt, zorgen ervoor dat de vernieuwing van uw dataset mislukt. Het bestand met medewerkers wordt vaak niet op tijd geüpload, waardoor de vernieuwing van uw dataset mislukt**.

        Pipelines helpen dit probleem op te lossen door de mogelijkheid te bieden om de vernieuwing bij mislukking opnieuw te proberen en op verschillende intervallen.

    - **Het kost erg veel tijd om wijzigingen in uw datamodel aan te brengen, omdat Power Query er lang over doet om de voorbeelden te vernieuwen vanwege de grote gegevensomvang en complexe transformaties**.

        We hebben gemerkt dat Dataflows en Lakehouses efficiënt zijn en dat wijzigingen eenvoudig door te voeren zijn. Doorgaans duurt het laden van voorbeelden in Dataflows en Lakehouses niet lang.

    - **U heeft een Windows-pc nodig om Power BI Desktop te gebruiken, terwijl de bedrijfsstandaard Mac is**.

    Microsoft Fabric is een SaaS aanbieding. Het enige dat u nodig heeft, is een browser om toegang te krijgen tot de service. Er hoeft geen software op onze desktops te worden geïnstalleerd.

# Labomgeving opruimen

Zodra u klaar bent om de labomgeving op te ruimen, volgt u de onderstaande stappen.

1. Selecteer de workspace **FAIAD_<inject key="Deployment ID" enableCopy="false"/>** in het linkerdeelvenster om naar de workspace home te navigeren.

2. Selecteer in het bovenste menu **Workspace settings**.

    ![](../media/Lab-7/image55.png)

3. Het dialoogvenster Workspace settings wordt geopend. Scroll omlaag in de sectie **General**.

4. Selecteer **Remove this workspace**.

5. Het dialoogvenster voor het verwijderen van de workspace wordt geopend. Selecteer **Delete**.

    Hiermee worden de workspace en alle items die in de workspace waren opgeslagen, verwijderd.

    ![](../media/Lab-7/image56.jpeg)

# Referenties

Fabric Analyst in a Day (FAIAD) introduceert u in een aantal van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service bevat de sectie Help (?) koppelingen naar uitstekende bronnen.

![](../media/Lab-1/image29.png)

Hier zijn nog enkele bronnen die u kunnen helpen bij uw volgende stappen met Microsoft Fabric.

- Lees de blogpost voor de volledige [aankondiging van Microsoft Fabric GA](https://aka.ms/Fabric-Hero-Blog-Ignite23)

- Verken Fabric via de [Guided Tour](https://aka.ms/Fabric-GuidedTour)

- Meld u aan voor de [gratis proefversie van Microsoft Fabric](https://aka.ms/try-fabric)

- Bezoek de [Microsoft Fabric website](https://aka.ms/microsoft-fabric)

- Leer nieuwe vaardigheden door de [Fabric Learning modules](https://aka.ms/learn-fabric) te verkennen

- Verken de [technische documentatie van Fabric](https://aka.ms/fabric-docs)

- Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook)

- Word lid van de [Fabric community](https://aka.ms/fabric-community) om uw vragen te stellen, feedback te delen en van anderen te leren

Lees de meer gedetailleerde aankondigingsblogs over de Fabric experiences:

- [Data Factory experience in Fabric blog](https://aka.ms/Fabric-Data-Factory-Blog)

- [Synapse Data Engineering experience in Fabric blog](https://aka.ms/Fabric-DE-Blog)

- [Synapse Data Science experience in Fabric blog](https://aka.ms/Fabric-DS-Blog)

- [Synapse Data Warehousing experience in Fabric blog](https://aka.ms/Fabric-DW-Blog)

- [Synapse Real-Time Analytics experience in Fabric blog](https://aka.ms/Fabric-RTA-Blog)

- [Power BI announcement blog](https://aka.ms/Fabric-PBI-Blog)

- [Data Activator experience in Fabric blog](https://aka.ms/Fabric-DA-Blog)

- [Administration and governance in Fabric blog](https://aka.ms/Fabric-Admin-Gov-Blog)

- [OneLake in Fabric blog](https://aka.ms/Fabric-OneLake-Blog)

- [Dataverse and Microsoft Fabric integration blog](https://aka.ms/Dataverse-Fabric-Blog)

© 2026 Microsoft Corporation. Alle rechten voorbehouden.

Door gebruik te maken van deze demo/dit lab, gaat u akkoord met de volgende voorwaarden:

De technologie/functionaliteit die in deze demo/dit lab wordt beschreven, wordt door Microsoft Corporation aangeboden met als doel uw feedback te verkrijgen en u een leerervaring te bieden. U mag de demo/het lab uitsluitend gebruiken om dergelijke technologiefuncties en -functionaliteiten te evalueren en feedback aan Microsoft te geven. U mag deze niet voor enig ander doel gebruiken. U mag deze demo/dit lab of een gedeelte daarvan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, licentiëren, er afgeleide werken van maken, overdragen of verkopen.

HET KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF EEN GEDEELTE DAARVAN) NAAR ENIGE ANDERE SERVER OF LOCATIE TEN BEHOEVE VAN VERDERE REPRODUCTIE OF HERDISTRIBUTIE IS UITDRUKKELIJK VERBODEN.

DEZE DEMO/DIT LAB BIEDT BEPAALDE SOFTWARETECHNOLOGIE-/PRODUCTFUNCTIES EN -FUNCTIONALITEITEN, INCLUSIEF MOGELIJKE NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF CONFIGURATIE VOOR HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN DIE IN DEZE DEMO/DIT LAB WORDEN GEPRESENTEERD, VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIEFUNCTIONALITEIT EN WERKEN MOGELIJK NIET OP DEZELFDE MANIER ALS EEN DEFINITIEVE VERSIE. WIJ BRENGEN MOGELIJK OOK GEEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN UIT. UW ERVARING MET HET GEBRUIK VAN DERGELIJKE FUNCTIES EN FUNCTIONALITEITEN IN EEN FYSIEKE OMGEVING KAN OOK ANDERS ZIJN.

**FEEDBACK**. Als u Microsoft feedback geeft over de technologiefuncties, functionaliteiten en/of concepten die in deze demo/dit lab worden beschreven, verleent u Microsoft kosteloos het recht om uw feedback op welke manier en voor welk doel dan ook te gebruiken, te delen en te commercialiseren. U verleent derden tevens kosteloos alle octrooirechten die nodig zijn voor hun producten, technologieën en diensten om specifieke onderdelen van een Microsoft-software of -service te gebruiken of te koppelen die de feedback bevatten. U geeft geen feedback die onderworpen is aan een licentie die vereist dat Microsoft zijn software of documentatie in licentie geeft aan derden omdat wij uw feedback daarin opnemen. Deze rechten blijven van kracht na afloop van deze overeenkomst.

MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN MET BETREKKING TOT DE DEMO/HET LAB AF, MET INBEGRIP VAN ALLE GARANTIES EN VOORWAARDEN VAN VERKOOPBAARHEID, HETZIJ UITDRUKKELIJK, IMPLICIET OF WETTELIJK, GESCHIKTHEID VOOR EEN BEPAALD DOEL, EIGENDOMSRECHT EN NIET-INBREUK. MICROSOFT GEEFT GEEN VERKLARINGEN OF GARANTIES MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, DE UITVOER DIE VOORTVLOEIT UIT HET GEBRUIK VAN DE DEMO/HET LAB, OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR EEN BEPAALD DOEL.

**VRIJWARING**

Deze demo/dit lab bevat slechts een gedeelte van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen worden gewijzigd in toekomstige versies van het product. In deze demo/dit lab leert u over een aantal, maar niet alle, nieuwe functies.
