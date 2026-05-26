# Microsoft Fabric - Fabric Analyst in een Dag - Lab 3

![](../media/Lab-1/main3.jpg)

# Inhoud

- Introductie

- Snelkoppeling naar ADLS Gen2

    - Taak 1: Snelkoppeling maken

- Gegevens transformeren met Visual Query

    - Taak 2: Geo-weergave maken met Visual Query

    - Taak 3: Reseller-weergave maken met Visual Query

    - Taak 4: Verkoopweergave maken met Visual Query

    - Taak 5: Productweergave maken met Visual Query

- Referenties

# Introductie

In ons scenario komen verkoopgegevens uit het ERP-systeem en worden deze opgeslagen in een ADLS Gen2. Deze gegevens worden elke dag om 12:00 uur 's middags bijgewerkt. We moeten deze gegevens transformeren en opnemen in een Lakehouse om ze vervolgens in ons model te gebruiken.

Er zijn meerdere manieren om deze gegevens op te nemen.

- **Shortcuts:** Hiermee wordt een koppeling naar de gegevens gemaakt en kunnen we Visual Query-weergaven gebruiken om de gegevens te transformeren. In dit lab gaan we Shortcuts gebruiken.

- **Notebooks:** Hiervoor moeten we code schrijven. Dit is een ontwikkelaarsvriendelijke aanpak.

- **Dataflow Gen2:** U bent waarschijnlijk al bekend met Power Query of Dataflow Gen1. Dataflow Gen2 is, zoals de naam aangeeft, de nieuwere versie van Dataflow. Het biedt alle mogelijkheden van Power Query / Dataflow Gen1, met daarnaast de extra mogelijkheid om gegevens te transformeren en op te nemen in meerdere gegevensbronnen. We zullen dit introduceren in de volgende labs.

- **Pipeline:** Dit is een orkestratietool. Activiteiten kunnen worden georkestreerd om gegevens te extraheren, transformeren en op te nemen. We zullen een Pipeline gebruiken om een Dataflow Gen2-activiteit uit te voeren, die op zijn beurt de extractie, transformatie en opname van gegevens zal uitvoeren.

We beginnen met het maken van een Shortcut om gegevens vanuit een ADLS Gen2-gegevensbron in een Lakehouse op te nemen. Nadat de gegevens zijn opgenomen, zullen we Visual Query-weergaven gebruiken om deze te transformeren.

Aan het einde van dit lab heeft u geleerd:

- Hoe u Shortcuts in uw Lakehouse maakt

- Hoe u gegevens transformeert met behulp van de Visual Query-functie

# Snelkoppeling naar ADLS Gen2

## Taak 1: Snelkoppeling maken

Shortcuts worden gebruikt om een koppeling naar de doellocatie te maken. Shortcuts bieden toegang tot gegevens zonder dat de gegevens fysiek naar het Lakehouse hoeven te worden verplaatst. Dit is vergelijkbaar met het maken van snelkoppelingen op het Windows-bureaublad.

1. Selecteer bovenaan uw scherm het tabblad **lh_FAIAD** om naar het Lakehouse te gaan.

1. Als u geen tabblad hebt, kunt u teruggaan naar uw Workspace en het Lakehouse daar openen.

1. Selecteer in het paneel **Explorer** de **drie puntjes (ellipsis)** naast **Tables**.

1. Selecteer **Nieuwe snelkoppeling**.

    ![](../media/Lab-3/image6.png)

1. Het venster **Nieuwe snelkoppeling** wordt geopend. Selecteer onder **Externe bronnen** de optie **Azure Data Lake Storage Gen2**.

    ![](../media/Lab-3/image7.png)

1. Selecteer **Nieuwe verbinding (1)**.

1. Voer de volgende koppeling in bij de eigenschap **URL**: https://stvnextblobstorage.dfs.core.windows.net/fabrikam-sales **(2):**

1. Klik op **Nieuwe verbinding maken (3)** onder de sectie Connection.

1. Selecteer **Shared Access Signature (SAS) (4)** in de vervolgkeuzelijst Authentication kind.

1. Kopieer het SAS-token en plak het in het veld **SAS token (5)**.

    - **SAS-token:** <inject key="Sas token"></inject>

1. Selecteer **Volgende (6)** rechtsonder in het scherm.

    ![](../media/Lab-3/image8.png)

1. U wordt verbonden met ADLS Gen2 waarbij de mappenstructuur in het linkerpaneel wordt weergegeven. Vouw **Delta-Parquet-Format-FY25 (1)** uit.

1. **Selecteer** de volgende mappen **(2)** en klik vervolgens op **Volgende (3):**

    1. Application.Cities

    2. Application.Countries

    3. Application.StateProvinces

    4. DateDim

    5. Sales.BuyingGroups

    6. Sales.Customers

    7. Sales.InvoiceLines

    8. Sales.Invoices

    9. Warehouse.StockGroups

    10. Warehouse.StockItemStockGroups

    11. Warehouse.StockItems

    >**Opmerking:** Sales.Invoices_May is de enige map die **niet** wordt geselecteerd.

    ![](../media/Lab-3/image9.png)

1. U wordt doorgestuurd naar het volgende venster waar we de namen kunnen aanpassen. Selecteer het **Bewerkingspictogram (1)** onder Actions voor **Application.Cities**.

1. Wijzig de naam van **Application.Cities naar Cities (2)**.

1. Selecteer het vinkje naast de naam om de wijziging op te slaan **(3)**.

    ![](../media/Lab-3/image10.png)

1. Wijzig op dezelfde manier de namen van de Shortcuts zoals hieronder aangegeven:

    1. Application.Countries naar **Countries**

    2. Application.StateProvinces naar **States**

    3. DateDim naar **Date**

    4. Sales.BuyingGroups naar **BuyingGroups**

    5. Sales.Customers naar **Customers**

    6. Sales.InvoiceLines naar **InvoiceLineItems**

    7. Sales.Invoices naar **Invoices**

    8. Warehouse.StockGroups naar **ProductGroups**

    9. Warehouse.StockItemStockGroups naar **ProductItemGroup**

    10. Warehouse.StockItems naar **ProductItem**

    > **Opmerking:** Controleer de namen zorgvuldig. Een typefout kan fouten veroorzaken tijdens het lab.

1. Selecteer **Maken** om de Shortcut aan te maken.

    ![](../media/Lab-3/image11.png)

1. Merk op dat alle Shortcuts als tabellen zijn aangemaakt. Selecteer de tabel **BuyingGroups** en merk op dat we een voorbeeld van de gegevens kunnen zien in het gegevenspaneel.

    ![](../media/Lab-3/image12.png)

    De volgende stap is het transformeren van de gegevens, zodat we een semantisch model kunnen maken. We gaan weergaven maken om de gegevens te transformeren.

# Gegevens transformeren met Visual Query

## Taak 2: Geo-weergave maken met Visual Query

1. We kunnen toegang krijgen tot het Lakehouse via een SQL-endpoint. Dit biedt de mogelijkheid om gegevens op te vragen en weergaven te maken. Selecteer **rechtsboven** in het scherm **Gegevens analyseren met (1) -> SQL analytics endpoint (2)**.

    ![](../media/Lab-3/image13.png)

    U wordt doorgestuurd naar het SQL analytics-endpoint. U hebt nu een nieuw item in uw bovenste navigatiemenu en kunt teruggaan naar het Lakehouse door dat tabblad te selecteren. Merk op dat het Explorer-paneel is gewijzigd. U kunt nu weergaven, opgeslagen procedures, query’s en meer maken. We gaan een visuele query maken, omdat deze een low-code interface biedt, vergelijkbaar met Power Query. We zullen het resultaat opslaan als een weergave.

    We beginnen met het maken van een Geo-weergave. We moeten gegevens uit de tabellen Cities, States en Countries samenvoegen om de Geo-weergave te maken.

2. Klik in het bovenste menu op de vervolgkeuzelijst naast **Nieuwe SQL query (1)** en selecteer vervolgens **Nieuwe visuele query (2)**.
    
    ![](../media/Lab-3/image14.png)

3. Om een query te bouwen, moeten we tabellen toevoegen aan het Visual Query-paneel. Klik in het Explorer-paneel op **Schemas (1)**, vouw **dbo (2)** uit, open **Tables (3)**, klik op de drie puntjes naast **Cities (4)** en selecteer **lhvoegen in canvas (5)**.

    ![](../media/Lab-3/image15.png)

4. Herhaal dezelfde stappen voor de tabellen **States** en **Countries**.

    Vervolgens moeten we deze query’s samenvoegen. De Visual Query-editor bevat een optie om de Power Query-editor te gebruiken. Laten we deze gebruiken, omdat we hiermee al vertrouwd zijn vanuit Power BI.

5. Selecteer **in het menu van de Visual Query-editor** het pictogram **Openen in pop-upvenster** (aan de rechterkant). U wordt doorgestuurd naar de Power Query-editor.
         
    >**Opmerking:** Mogelijk moet u naar rechts scrollen of uw Visual Query-tabblad opnieuw openen als u dit pictogram niet direct ziet.

    ![](../media/Lab-3/image16.png)

6. Terwijl de query **Cities (1)** is geselecteerd, selecteert u in het lint van de Power Query-editor **Start (2) -> Combineren (3) -> vervolgkeuzelijst Query's samenvoege (4) -> Query's samenvoegen als nieuw (5)**. Het venster Merge queries wordt geopend.

    ![](../media/Lab-3/image17.png)

7. Selecteer bij **Linkertabel voor samenvoegen** de tabel **Cities**.

8. Selecteer bij **Rechtertabel voor samenvoegen** de tabel **States**.

9. Selecteer de kolommen **StateProvinceID** uit beide tabellen. We gaan deze kolom gebruiken voor de koppeling.

10. Selecteer **Binnen** als **Type Join**.

11. Selecteer **OK**.

    ![](../media/Lab-3/image18.png)

    Merk op dat een nieuwe query met de naam **Merge** is aangemaakt. We hebben enkele kolommen uit States nodig.

12. Klik in de **Data view** (onderste paneel) op de **dubbele pijl** naast de kolom **States** (de laatste kolom aan de rechterkant).

13. Er wordt een paneel geopend. Zorg ervoor dat alleen de volgende kolommen zijn geselecteerd:

    1. StateProvinceCode

    2. StateProvinceName

    3. CountryID

    4. SalesTerritory

14. Selecteer **OK**.

    ![](../media/Lab-3/image19.png)

    We moeten nu de query Countries samenvoegen.

15. Terwijl de query **Merge (1)** geselecteerd is, selecteert u **Start (2) -> Combineren (3) -> vervolgkeuzelijst Query's samenvoegen (4) -> Query's samenvoegen (5)**.

    ![](../media/Lab-3/image20.png)

16. Het venster **Query's samenvoegen** wordt geopend. Selecteer bij **Rechtertabel voor samenvoegen** de tabel **Countries**.

17. Selecteer de kolommen **CountryID** uit beide tabellen. We gaan deze kolom gebruiken voor de koppeling.

18. Selecteer **Binnen (Inner)** als **Type Join**.

19. Selecteer **OK**.

    ![](../media/Lab-3/image21.png)

    We hebben enkele kolommen uit Countries nodig.

20. Klik in de **Data view** (onderste paneel) op de **dubbele pijl** naast de kolom **Countries**.

21. Er wordt een paneel geopend. Zorg ervoor dat alleen de volgende kolommen zijn geselecteerd:

    1. CountryName

    2. FormalName

    3. IsoAlpha3Code

    4. IsoNumericCode

    5. CountryType

    6. Continent

    7. Region

    8. Subregion

22. Selecteer **OK**.

    **Belangrijk:** Zorg ervoor dat u naar beneden scrollt en alle acht kolommen selecteert die in stap 21 zijn vermeld. De onderstaande schermafbeelding toont alleen de eerste vijf kolommen vanwege een beperking van de gebruikersinterface.

    ![](../media/Lab-3/image22.png)

    We hebben niet alle kolommen in de tabel **Merge** nodig. Zorg ervoor dat alleen de benodigde kolommen geselecteerd blijven.

23. Terwijl de query **Samenvoegen (1)** geselecteerd is, selecteert u in het lint **Start (2) -> Kolommen kiezen (3) -> Kolommen kiezen (4)**.

    > **Opmerking:** Als de optie **Kolommen kiezen** niet zichtbaar is, kunt u deze vinden onder **Kolommen beheren**.

    ![](../media/Lab-3/image23.png)

24. Het venster **Kolommen kiezen** wordt geopend. **Schakel de selectie uit** voor de volgende kolommen:

    1. StateProvinceID

    2. Location

    3. LastEditedBy

    4. ValidFrom

    5. ValidTo

    6. CountryID

25. Selecteer **OK**.

    ![](../media/Lab-3/image24.png)

    Merk op dat het proces vergelijkbaar is met Power Query; alle stappen worden vastgelegd in zowel het paneel **Applied Steps** aan de rechterkant als in de visuele weergave. Laten we nu de query Merge hernoemen en **Enable Load** inschakelen, zodat de gegevens vanuit deze query worden geladen.

26. **Klik met de rechtermuisknop** op de query **Samenvoegen** in het paneel **Query's** (links). Selecteer **Naam wijzigen** en wijzig de naam van de query naar **Geo**.

27. **Klik met de rechtermuisknop** op de query **Geo** in het paneel **Query's** (links). Selecteer **Laden inschakelen** om deze query in te schakelen.

28. Zorg ervoor dat de query's **Cities**, **States** en **Countries** zijn **uitgeschakeld**.

29. Selecteer **Opslaan**, rechtsonder in de **Power Query-editor**.

    ![](../media/Lab-3/image25.png)

    U wordt doorgestuurd naar de Visual Query-editor. Laten we deze query nu opslaan als een weergave.

    >**Opmerking:** Alle stappen die we met de Power Query-editor hebben uitgevoerd, kunnen ook in de Visual Query-editor worden uitgevoerd.

30. Selecteer in het menu van de Visual Query-editor **Opslaan als weergave**.

    ![](../media/Lab-3/image26.png)

    Het venster **Opslaan als weergave** wordt geopend. Merk op dat de SQL-query beschikbaar is. U kunt deze bekijken als u de SQL-code wilt controleren.

31. Voer **Geo** in als **Naam van de weergave**.

32. Selecteer **OK** om de weergave op te slaan.

    ![](../media/Lab-3/image27.png)

    U ontvangt een melding zodra de weergave is opgeslagen.

33. Vouw in het paneel **Verkenner** (links) **Weergaven** uit. U ziet nu de nieuw aangemaakte **Geo-weergave**.

    ![](../media/Lab-3/image28.png)

## Taak 3: Reseller-weergave maken met Visual Query

Laten we de Reseller-weergave maken, die wordt gecreëerd door de tabellen Customers en BuyingGroups samen te voegen. Deze keer maken we de weergave met Visual Query zonder de Power Query-optie te openen.

1. Klik in het bovenste menu op de vervolgkeuzelijst naast **Nieuwe SQL-query (1)** en selecteer vervolgens **Nieuwe visuele query (2)**.

    ![](../media/Lab-3/image54.png)

2. Om een query op te bouwen, moeten we tabellen toevoegen aan het **Visual Query-paneel**. Klik op de drie puntjes naast de tabel **BuyingGroups (1)** en selecteer **Invoegen in canvas (2)**.

    ![](../media/Lab-3/image29.png)

3. Herhaal dezelfde stappen voor de tabel **Customers**.

4. **Selecteer de query Customers**. Wanneer deze geselecteerd is, krijgt Customers een **“+”**-teken achter Table (dit geeft aan dat we een stap toevoegen na Table. Als u het **“+”**-teken niet ziet, heeft u mogelijk een andere stap geselecteerd. Selecteer opnieuw Table en het werkt correct).

5. Selecteer in het menu van Visual Query **Combineren -> Query's samenvoegen**.

    ![](../media/Lab-3/image30.png)

    Het venster **Query's samenvoegen** wordt geopend met **Customers** geselecteerd als bovenste tabel.

6. Selecteer bij **Rechtertabel voor samenvoegen** de tabel **BuyingGroups**.

7. Selecteer de kolommen **BuyingGroupID** uit beide tabellen. We gaan deze kolom gebruiken voor de koppeling.

8. Selecteer **Binnen (Inner)** als **Type samenvoeging**.

9. Selecteer **OK**.

    ![](../media/Lab-3/image31.png)

10. Klik in de **Data view** (onderste paneel) op de **dubbele pijl** naast de kolom **BuyingGroups** (de laatste kolom aan de rechterkant) om de benodigde kolommen uit BuyingGroups te selecteren.

11. Er wordt een paneel geopend. **Selecteer de kolom BuyingGroupName**.

12. Selecteer **OK**.

    ![](../media/Lab-3/image32.png)

    We hebben niet alle kolommen uit onze Customers-tabel nodig. Laten we alleen de benodigde kolommen selecteren.

13. Selecteer in het menu van Visual Query **Kolommen beheren -> Kolommen kiezen**.

    ![](../media/Lab-3/image33.png)

14. Het venster **Kolommen kiezen** wordt geopend. **Selecteer** de volgende kolommen:

    1. ResellerID

    2. ResellerName

    3. PostalCityID

    4. PhoneNumber

    5. FaxNumber

    6. WebsiteURL

    7. DeliveryAddressLine1

    8. DeliveryAddressLine2

    9. DeliveryPostalCode

    10. PostalAddressLine1

    11. PostalAddressLine2

    12. PostalPostalCode

    13. BuyingGroupName

15. Selecteer **OK**.

    ![](../media/Lab-3/image34.png)

16. Laten we de kolom **BuyingGroupName** hernoemen. Dubbelklik in de **Gegevensweergave** op de kolomkop **BuyingGroupName** om deze bewerkbaar te maken.

17. **Wijzig de naam** van de kolom naar **ResellerCompany**.

    ![](../media/Lab-3/image35.png)

    Merk op dat de tabel **Customers** nu alle stappen heeft vastgelegd. Laten we deze weergave nu opslaan.

18. We moeten de query **Customers** opslaan, omdat deze alle stappen bevat. We moeten **Laden inschakelen** activeren. Selecteer de **drie puntjes** in het queryvak **Customers**.

19. Controleer of **Laden inschakelen** is aangevinkt.

    ![](../media/Lab-3/image36.png)

    >**Opmerking:** Het vak **Customer** moet een blauwe rand hebben wanneer **Laden inschakelen** is geactiveerd.

20. Selecteer in het menu van Visual Query **Opslaan als weergave**.

    ![](../media/Lab-3/image37.png)

    Het venster **Opslaan als weergave** wordt geopend. Merk op dat de SQL-query beschikbaar is. U kunt deze bekijken door erop te klikken.

21. Voer **Reseller** in als **Naam van de weergave**.

22. Selecteer **OK** om de weergave op te slaan.

    ![](../media/Lab-3/image38.png)

    U ontvangt een melding zodra de weergave is opgeslagen.

23. Vouw in het paneel **Verkenner** (links) **Weergaven** uit. U ziet nu de nieuw aangemaakte **Reseller-weergave**.

    ![](../media/Lab-3/image39.png)

## Taak 4: Sales-weergave maken met Visual Query

Laten we de Sales-weergave maken, die wordt gecreëerd door de tabellen InvoiceLineItems en Invoices samen te voegen met de Reseller-weergave. We hebben deze query al in Power BI Desktop. We gaan de code kopiëren vanuit de Advanced Editor. Maar voordat we de code kopiëren, moeten we een Merge-tabel maken met Visual Query, omdat het niet mogelijk is om een lege query te maken in Visual Query. Laten we deze methode proberen.

1. Klik in het bovenste menu op de vervolgkeuzelijst naast **Nieuwe SQL-query** en selecteer vervolgens **Nieuwe visuele query**.

    ![](../media/Lab-3/image40.png)

2. Vanuit de sectie **Verkenner -> Tabellen** moeten we tabellen toevoegen aan het Visual Query-paneel. Klik op de drie puntjes naast de tabel **InvoiceLineItems** en selecteer **Invoegen in canvas**.

3. Herhaal dezelfde stappen voor de tabel **Invoices**.

4. Vanuit de sectie **Verkenner -> Weergaven** moeten we tabellen toevoegen aan het Visual Query-paneel. Klik op de drie puntjes naast de tabel **Reseller** en selecteer **Invoegen in canvas**.

5. Selecteer in de Visual Query-editor **Openen in pop-upvenster** om de Power Query-editor te openen.

    ![](../media/Lab-3/image41.png)

6. Terwijl de query **InvoiceLineItems** geselecteerd is, selecteert u in het lint **Start (2) -> Combineren (3) -> vervolgkeuzelijst Query's samenvoegen (4) -> Query's samenvoegen als nieuwe query (5)**. Het venster **Query's samenvoegen** wordt geopend.

    ![](../media/Lab-3/image42.png)

7. Selecteer bij **Linkertabel voor samenvoegen** de tabel **InvoiceLineItems**.

8. Selecteer bij **Rechtertabel voor samenvoegen** de tabel **Invoices**.

9. Selecteer de kolommen **InvoiceID** uit beide tabellen. We gaan deze kolom gebruiken voor de koppeling.

10. Selecteer **Binnen (Inner)** als **Type samenvoeging**.

11. Selecteer **OK**.

    ![](../media/Lab-3/image43.png)

    We gaan code uit Power BI Desktop kopiëren en plakken via de **Advanced Editor**.

12. Als u dit nog niet hebt gedaan, open dan **FAIAD.pbix**, die zich bevindt in de map **Reports** op het bureaublad van uw labomgeving.

13. Selecteer in het lint **Start -> Gegevens transformeren**. Het venster **Power Query** wordt geopend. Zoals u in het vorige lab hebt gezien, zijn de query's in het linkerpaneel georganiseerd per gegevensbron.

    ![](../media/Lab-3/image44.png)

14. Selecteer in het linker **Query's**-paneel, onder de map **ADLSData (1)**, de query **Sales (2)**.

15. Selecteer in het lint **Start -> Geavanceerde editor (3)**. Het venster **Geavanceerde editor** wordt geopend.

    ![](../media/Lab-3/image45.png)

    >**Opmerking:** Als u de **Geavanceerde editor** niet kunt vinden, kunt u deze openen via **Start -> Query -> Geavanceerde editor**.

16. **Selecteer de code vanaf regel 3** tot en met de laatste regel code.

17. **Klik met de rechtermuisknop** en selecteer **Kopiëren**.

18. Selecteer **Annuleren** om de **Geavanceerde editor** te sluiten.

    ![](../media/Lab-3/image46.png)

19. **Ga terug naar de browser** waarin de **Power Query-editor** geopend is.

20. Zorg ervoor dat de query **Samenvoegen** geselecteerd is.

21. Selecteer in het lint **Start -> Geavanceerde editor**. Het venster **Geavanceerde editor** wordt geopend.

    ![](../media/Lab-3/image47.png)

22. Voeg **aan het einde van regel 2 een komma toe**:

    `Source = Table.NestedJoin(InvoiceLineItems, {"InvoiceID"}, Invoices, {"InvoiceID"}, "Invoices", JoinKind.Inner),`

23. Druk op **Enter** om een nieuwe regel te starten.

24. Druk op **Ctrl+V** op uw toetsenbord om de code te plakken die u uit **Power BI Desktop** hebt gekopieerd.

    >**Opmerking:** Als u in de labomgeving werkt, selecteer dan de **drie puntjes (…)** rechtsboven in het scherm. Gebruik de schuifregelaar om **VM Native Clipboard** **in te schakelen**. Selecteer **OK** in het dialoogvenster. Nadat u de query's hebt geplakt, kunt u deze optie weer uitschakelen.

    ![](../media/Lab-3/image48.png)

    ![](../media/Lab-3/image49.png)

25. Markeer de laatste twee regels code (in **Source**) en **verwijder** deze.

26. Selecteer **OK** om de wijzigingen op te slaan.

    ![](../media/Lab-3/image50.png)

    Als dit eenvoudiger is, verwijder dan alle code in de Advanced Editor en plak de onderstaande code in de Advanced Editor.

    ```
    let
    Source = Table.NestedJoin(InvoiceLineItems, {"InvoiceID"}, Invoices, {"InvoiceID"}, "Invoices", JoinKind.Inner),
        #"Expanded Invoice" = Table.ExpandTableColumn(Source, "Invoices", {"CustomerID", "BillToCustomerID", "SalespersonPersonID", "InvoiceDate"}, {"CustomerID", "BillToCustomerID", "SalespersonPersonID", "InvoiceDate"}),
        #"Removed Other Columns" = Table.SelectColumns(#"Expanded Invoice",{"InvoiceLineID", "InvoiceID", "StockItemID", "Quantity", "UnitPrice", "TaxRate", "TaxAmount", "LineProfit", "ExtendedPrice", "CustomerID", "SalespersonPersonID", "InvoiceDate"}),
        #"Renamed Columns" = Table.RenameColumns(#"Removed Other Columns",{{"CustomerID", "ResellerID"}}),
        #"Merged Queries" = Table.NestedJoin(#"Renamed Columns", {"ResellerID"}, Reseller, {"ResellerID"}, "Customer", JoinKind.Inner),
        #"Added Custom" = Table.AddColumn(#"Merged Queries", "Sales Amount", each [ExtendedPrice] - [TaxAmount]),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Sales Amount", type number}}),
        #"Removed Columns" = Table.RemoveColumns(#"Changed Type",{"Customer"})
    in
        #"Removed Columns"
    ```

27. U wordt teruggeleid naar de **Power Query Editor**. Dubbelklik in het linker **Queries**-paneel op de query **Samenvoegen** om deze te hernoemen.

28. **Wijzig de naam** van de query **Samenvoegen** naar **Sales**.

29. Klik met de rechtermuisknop op de query **Sales** en selecteer **Laden inschakelen** om het laden van deze query in te schakelen.

    ![](../media/Lab-3/image51.png)

30. Selecteer **Opslaan** om het **Power Query**-venster op te slaan en te sluiten. U wordt doorgestuurd naar de **Visual Query-editor**.

31. Selecteer in het menu van Visual Query **Opslaan als weergave**. Het venster **Opslaan als weergave** wordt geopend. Merk op dat de SQL-query beschikbaar is. U kunt deze bekijken indien gewenst.

32. Voer **Sales** in als **Naam van de weergave (1)**.

33. Selecteer **OK (2)** om de weergave op te slaan.

    ![](../media/Lab-3/image52.png)

    U ontvangt een melding zodra de weergave is opgeslagen.

34. Vouw in het paneel **Verkenner** (links) **Weergaven** uit. U ziet nu de nieuw aangemaakte **Sales-weergave**.

    ![](../media/Lab-3/image53.png)

## Taak 5: Product-weergave maken met Visual Query

Laten we de Product-weergave maken, die wordt gecreëerd door de tabellen **ProductItem**, **ProductItemGroup** en **ProductGroups** samen te voegen. Om het proces sneller te laten verlopen, gaan we code kopiëren naar de **Advanced Editor**.

1. Klik in het bovenste menu op de vervolgkeuzelijst naast **New SQL query (1)** en selecteer vervolgens **New visual query (2)**.

    ![](../media/Lab-3/image54.png)

2. Vanuit de sectie **Explorer** moeten we tabellen toevoegen aan het Visual Query-paneel. Klik op de drie puntjes naast de tabel **ProductItem (1)** en selecteer **Insert into canvas (2)**.

    ![](../media/Lab-3/image55.png)

3. Herhaal dezelfde stappen voor de tabellen **ProductItemGroup** en **ProductGroups**.

4. Selecteer in de Visual Query-editor **Open in popup** om de Power Query-editor te openen.

    ![](../media/Lab-3/image56.png)

5. Terwijl de query **ProductItem (1)** is geselecteerd, selecteert u in het lint **Home (2) -> Combine (3) -> vervolgkeuzelijst Merge queries (4) -> Merge queries as new (5)**. Het venster **Merge** wordt geopend.

    ![](../media/Lab-3/image57.png)

6. Selecteer bij **Left table for merge** de tabel **ProductItem**.

7. Selecteer bij **Right table for merge** de tabel **ProductItemGroup**.

8. Selecteer de kolommen **StockItemID** uit beide tabellen. We gaan deze kolom gebruiken voor de koppeling.

9. Selecteer **Left outer** als **Join kind**.

10. Selecteer **OK**. Er wordt een nieuwe query **Merge** aangemaakt.

    ![](../media/Lab-3/image58.png)

11. Terwijl de query **Merge** geselecteerd is, selecteert u in het lint **Home -> Advanced editor**. Het venster **Advanced editor** wordt geopend.

    ![](../media/Lab-3/image59.png)

    >**Opmerking:** Als u de **Advanced Editor** niet kunt vinden, kunt u deze openen via **Home -> Query -> Advanced Editor**.

12. **Selecteer alle code** in de **Advanced editor** en **verwijder** deze.

13. **Plak** de onderstaande code in de **Advanced editor**.

    ```
    let
       Source = Table.NestedJoin(ProductItem, {"StockItemID"}, ProductItemGroup, {"StockItemID"}, "ProductItemGroup", JoinKind.LeftOuter),
       #"Expanded ProductItemGroup" = Table.ExpandTableColumn(Source, "ProductItemGroup", {"StockGroupID"}, {"StockGroupID"}),
       #"Merged queries" = Table.NestedJoin(#"Expanded ProductItemGroup", {"StockGroupID"}, ProductGroups, {"StockGroupID"}, "ProductGroups", JoinKind.LeftOuter),
       #"Expanded ProductGroups" = Table.ExpandTableColumn(#"Merged queries", "ProductGroups", {"StockGroupName"}, {"StockGroupName"}),
       #"Choose columns" = Table.SelectColumns(#"Expanded ProductGroups", {"StockItemID", "StockItemName", "SupplierID", "Size", "IsChillerStock", "TaxRate", "UnitPrice", "RecommendedRetailPrice", "TypicalWeightPerUnit", "StockGroupName"})
    in
       #"Choose columns"
    ```

14. Selecteer **OK** om de Advanced Editor te sluiten. U wordt teruggeleid naar de **Power Query-editor**.

    ![](../media/Lab-3/image60.png)

15. Dubbelklik in het **Queries**-paneel aan de linkerkant op de query **Merge** om deze te hernoemen.

16. **Wijzig de naam** van de query **Merge** naar **Product**.

17. Klik met de rechtermuisknop op de query **Product** en selecteer **Enable load** om het laden van deze query in te schakelen.

18. Selecteer **Save** om het Power Query-venster op te slaan en te sluiten. U wordt doorgestuurd naar **Visual Query**.

    ![](../media/Lab-3/image61.png)

19. Selecteer in het menu van Visual Query **Save as view**. Het venster **Save as view** wordt geopend. Merk op dat de SQL-query beschikbaar is. U kunt deze bekijken indien gewenst.

20. Voer **Product** in als **View name**.

21. Selecteer **OK** om de weergave op te slaan.

    ![](../media/Lab-3/image62.png)

    U ontvangt een melding zodra de weergave is opgeslagen.

22. Vouw in het **Explorer**-paneel (links) **Views** uit. U ziet nu de nieuw aangemaakte **Product**-weergave.

    ![](../media/Lab-3/image63.png)

    We hebben de gegevens van de ADLS Gen2-gegevensbron getransformeerd. In dit lab hebben we geleerd hoe we Shortcuts kunnen maken en hebben we verschillende opties verkend voor het gebruik van Visual Query-weergaven om gegevens te transformeren.

    In het volgende lab leren we hoe we **Dataflow Gen2** kunnen gebruiken en een **Shortcut** naar een ander Lakehouse kunnen maken.

# Referenties

Fabric Analyst in a Day (FAIAD) introduceert u aan enkele van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service bevat de sectie **Help (?)** koppelingen naar een aantal waardevolle bronnen.

![](../media/Lab-1/image29.png)

Hieronder vindt u nog enkele aanvullende bronnen die u helpen bij uw volgende stappen met Microsoft Fabric.

* Bekijk het blogbericht om de volledige [Microsoft Fabric GA-aankondiging](https://aka.ms/Fabric-Hero-Blog-Ignite23) te lezen.

* Verken Fabric via de [Rondleiding](https://aka.ms/Fabric-GuidedTour).

* Meld u aan voor de [gratis proefversie van Microsoft Fabric](https://aka.ms/try-fabric).

* Bezoek de [Microsoft Fabric-website](https://aka.ms/microsoft-fabric).

* Leer nieuwe vaardigheden door de [Fabric-leermodules](https://aka.ms/learn-fabric) te verkennen.

* Verken de [technische documentatie van Fabric](https://aka.ms/fabric-docs).

* Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook).

* Neem deel aan de [Fabric-community](https://aka.ms/fabric-community) om vragen te stellen, feedback te delen en van anderen te leren.

Lees de meer uitgebreide aankondigingsblogs over Fabric:

* [Blog over Data Factory-ervaring in Fabric](https://aka.ms/Fabric-Data-Factory-Blog)

* [Blog over Synapse Data Engineering-ervaring in Fabric](https://aka.ms/Fabric-DE-Blog)

* [Blog over Synapse Data Science-ervaring in Fabric](https://aka.ms/Fabric-DS-Blog)

* [Blog over Synapse Data Warehousing-ervaring in Fabric](https://aka.ms/Fabric-DW-Blog)

* [Blog over Synapse Real-Time Analytics-ervaring in Fabric](https://aka.ms/Fabric-RTA-Blog)

* [Power BI-aankondigingsblog](https://aka.ms/Fabric-PBI-Blog)

* [Blog over Data Activator-ervaring in Fabric](https://aka.ms/Fabric-DA-Blog)

* [Blog over beheer en governance in Fabric](https://aka.ms/Fabric-Admin-Gov-Blog)

* [Blog over OneLake in Fabric](https://aka.ms/Fabric-OneLake-Blog)

* [Blog over Dataverse- en Microsoft Fabric-integratie](https://aka.ms/Dataverse-Fabric-Blog)

© 2026 Microsoft Corporation. Alle rechten voorbehouden.

Door deze demo/dit lab te gebruiken, gaat u akkoord met de volgende voorwaarden:

De technologie/functionele mogelijkheden die in deze demo/dit lab worden beschreven, worden door Microsoft Corporation geleverd om uw feedback te verkrijgen en u een leerervaring te bieden. U mag deze demo/dit lab uitsluitend gebruiken om dergelijke technologische functies en mogelijkheden te evalueren en feedback aan Microsoft te geven. U mag deze niet voor andere doeleinden gebruiken. U mag deze demo/dit lab of enig onderdeel daarvan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, licentiëren, afgeleide werken maken, overdragen of verkopen.

HET KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF ENIG DEEL ERVAN) NAAR EEN ANDERE SERVER OF LOCATIE VOOR VERDERE REPRODUCTIE OF HERDISTRIBUTIE IS UITDRUKKELIJK VERBODEN.

DEZE DEMO/HET LAB BIEDT BEPAALDE SOFTWARETECHNOLOGIE-/PRODUCTFUNCTIES EN MOGELIJKHEDEN, INCLUSIEF MOGELIJKE NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF CONFIGURATIE VOOR HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN DIE IN DEZE DEMO/HET LAB WORDEN WEERGEGEVEN, VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIONALITEIT EN WERKEN MOGELIJK NIET OP DEZELFDE MANIER ALS EEN DEFINITIEVE VERSIE. WIJ KUNNEN OOK BESLUITEN GEEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN UIT TE BRENGEN. UW ERVARING BIJ HET GEBRUIK VAN DERGELIJKE FUNCTIES EN MOGELIJKHEDEN IN EEN FYSIEKE OMGEVING KAN OOK AFWIJKEN.

**FEEDBACK**. Als u feedback geeft aan Microsoft over de technologie, functies, mogelijkheden en/of concepten die in deze demo/dit lab worden beschreven, verleent u Microsoft kosteloos het recht om uw feedback op welke manier dan ook en voor welk doel dan ook te gebruiken, delen en commercialiseren. U verleent ook kosteloos aan derden eventuele octrooirechten die nodig zijn voor hun producten, technologieën en diensten om specifieke onderdelen van Microsoft-software of -services waarin uw feedback is opgenomen te gebruiken of ermee te communiceren. U zult geen feedback verstrekken die onder een licentie valt die Microsoft verplicht om haar software of documentatie aan derden in licentie te geven omdat wij uw feedback daarin opnemen. Deze rechten blijven van kracht na beëindiging van deze overeenkomst.

MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN MET BETREKKING TOT DE DEMO/HET LAB AF, INCLUSIEF ALLE GARANTIES EN VOORWAARDEN VAN VERHANDELBAARHEID, HETZIJ UITDRUKKELIJK, IMPLICIET OF WETTELIJK, GESCHIKTHEID VOOR EEN BEPAALD DOEL, EIGENDOMSRECHTEN EN NIET-INBREUK. MICROSOFT GEEFT GEEN GARANTIES OF VERTEGENWOORDIGINGEN MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, UITVOER DIE VOORTVLOEIT UIT HET GEBRUIK VAN DE DEMO/HET LAB OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR WELK DOEL DAN OOK.

**DISCLAIMER**

Deze demo/dit lab bevat slechts een gedeelte van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen in toekomstige versies van het product worden gewijzigd. In deze demo/dit lab leert u enkele, maar niet alle, nieuwe functies kennen.

