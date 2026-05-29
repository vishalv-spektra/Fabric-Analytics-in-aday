# Microsoft Fabric - Fabric Analyst in a Day - Oefening 6

![](../media/Lab-1/main6.png)

# Inhoudsopgave

- Inleiding

- Lakehouse – Gegevens analyseren

    - Taak 1: Gegevens opvragen met SQL

    - Taak 2: T-SQL-resultaat visualiseren

- Lakehouse – Semantisch modelleren

    - Taak 3: Semantisch model aanmaken

    - Taak 4: Relaties aanmaken

    - Taak 5: Metingen aanmaken

    - Taak 6: Optioneel gedeelte – Relaties aanmaken

    - Taak 7: Optioneel gedeelte – Metingen aanmaken

- Referenties

# Inleiding

We hebben gegevens uit verschillende bronnen ingeladen in de Lakehouse. In dit lab werkt u met het semantisch model. Doorgaans voerden we modelleringsactiviteiten zoals het aanmaken van relaties, toevoegen van metingen, enzovoort uit in Power BI Desktop. Hier leren we hoe u deze modelleringsactiviteiten uitvoert in de service.

Aan het einde van dit lab heeft u geleerd:

- SQL-weergave gebruiken in SQL analytics endpoint

- Hoe u een semantisch model aanmaakt

# Lakehouse – Gegevens analyseren

## Taak 1: Gegevens opvragen met SQL

1. Laten we teruggaan naar de Fabric-werkruimte **FAIAD_<inject key="Deployment ID" enableCopy="false"/>** die u heeft aangemaakt in Lab 2, Taak 8.

2. Indien gewenst kunt u de **taakstroom minimaliseren** om de volledige lijst met items te bekijken.

3. U ziet drie onderdelen die gekoppeld zijn aan **lh_FAIAD**: **Lakehouse**, **Semantic model** en **SQL endpoint**. We hebben het Lakehouse al verkend en in een eerder lab visuele query’s gemaakt met behulp van het **SQL analytics endpoint**. Selecteer in de linkernavigatie **FAIAD_<inject key="Deployment ID" enableCopy="false"/>** en kies vervolgens de optie **lh_FAIAD SQL analytics endpoint** om deze functionaliteit verder te verkennen. U wordt doorgestuurd naar de **SQL-weergave** van de Explorer.

    ![](../media/Lab-6/image6.png)

    Als u gegevens wilt verkennen voordat u een datamodel maakt, kunt u hiervoor SQL gebruiken. Er zijn twee manieren om SQL te gebruiken. De eerste optie is de **visuele query**, die we in het eerdere lab hebben gebruikt. De tweede optie is het schrijven van **T-SQL-code**. Dit is een meer ontwikkelaarsgerichte aanpak. Laten we dit verder bekijken.

    Stel dat u snel de verkochte **Units per Supplier** wilt opvragen met behulp van SQL.

    In het **Lakehouse SQL analytics endpoint** ziet u in het linkerpaneel de tabellen. Wanneer u de tabellen uitvouwt, kunt u de kolommen bekijken waaruit de tabel bestaat. Er zijn ook opties beschikbaar om **SQL-weergaven**, **functies** en **stored procedures** aan te maken. Als u ervaring heeft met SQL, kunt u deze opties gerust verder verkennen. Laten we nu proberen een eenvoudige SQL-query te schrijven.

4. Selecteer **Nieuwe SQL-query** in het **bovenste menu** of klik op **Nieuwe SQL-query** in het midden van het scherm. U wordt doorgestuurd naar de weergave **SQL-query**.

    ![](../media/Lab-6/image7.png)

5. Plak de **onderstaande SQL-query** in het **queryvenster**. Deze query retourneert het aantal verkochte eenheden per leveranciersnaam. De query koppelt de tabellen **Sales**, **Product** en **Supplier** om dit resultaat te verkrijgen.

   ```
   SELECT su.SupplierName, SUM(Quantity) as Units
   FROM dbo.Sales s
   JOIN dbo.Product p on p.StockItemID = s.StockItemID
   JOIN dbo.Supplier su on su.SupplierID = p.SupplierID
   GROUP BY su.SupplierName
   ```

6. Klik in het menu van de SQL-editor op **Run** om de resultaten te bekijken.

7. U ziet dat er een optie beschikbaar is om deze query als een **View** op te slaan door **Save as view** te selecteren.

8. In het linker **Explorer**-deelvenster, onder de sectie **Queries**, ziet u dat deze query is opgeslagen onder **My queries** als **SQL query 1**. Dit biedt de mogelijkheid om de query een andere naam te geven en op te slaan voor toekomstig gebruik. Er is ook een optie om query’s te bekijken die met u zijn gedeeld via de map **Shared queries**.

    >**Opmerking:** De visuele query’s die u in eerdere labs heeft aangemaakt, zijn ook beschikbaar in de map **My queries**.

    ![](../media/Lab-6/image8.png)

## Taak 2: T-SQL-resultaat visualiseren

1. We kunnen het resultaat van deze query ook visualiseren. **Markeer de query** in het queryvenster.

2. Selecteer in het menu van het resultatenvenster het vervolgkeuzepictogram **-> Resultaten visualiseren**.

    ![](../media/Lab-6/image9.png)

3. Het dialoogvenster **Resultaten visualiseren** wordt geopend. Selecteer **Doorgaan**.

    Het dialoogvenster **Resultaten visualiseren** lijkt op de rapportweergave van **Power BI Desktop**. Het bevat alle functies die beschikbaar zijn in de rapportweergave van Power BI Desktop. U kunt de pagina opmaken, verschillende visualisaties selecteren, visualisaties formatteren, filters toevoegen, enzovoort. We zullen deze opties in deze cursus niet verder behandelen.

    ![](../media/Lab-6/image10.png)

4. Vouw het deelvenster **Gegevens** uit en vouw vervolgens **SQL query 1** uit.

5. Selecteer de velden **Supplier_Name** en **Units**. Er wordt een tabelvisualisatie aangemaakt.

    ![](../media/Lab-6/image11.png)

6. Wijzig het type visualisatie in de sectie **Visualisatie** door **Stacked column chart** te selecteren.

7. Selecteer rechtsonder in het scherm **Opslaan als rapport**.

    ![](../media/Lab-6/image12.png)

8. Het dialoogvenster **Rapport opslaan** wordt geopend. Voer **Units by Supplier** in het tekstvak **Voer een naam in voor uw rapport** in.

9. Controleer of de doelwerkruimte is ingesteld op uw Fabric-werkruimte **FAIAD_<inject key="Deployment ID" enableCopy="false"/>**.

10. Selecteer **Opslaan**.

    ![](../media/Lab-6/image13.png)

    U wordt teruggeleid naar het scherm met de SQL-query.

# Lakehouse – Semantisch modelleren

## Taak 3: Semantisch model aanmaken

1. Selecteer **Nieuw semantisch model** in het menu van het **SQL analytics endpoint**.

    ![](../media/Lab-6/image13(1).png)

2. Het dialoogvenster **Nieuw semantisch model** wordt geopend. Voer **sm_FAIAD** in als naam voor het **Direct Lake-semantisch model**.

3. We hebben de mogelijkheid om standaard een subset van tabellen te selecteren. Vergeet niet dat we in het eerdere lab views hebben aangemaakt. We willen deze views opnemen in het model. Vouw het schema **dbo** uit; hier ziet u alle tabellen en views in uw lakehouse.

    ![](../media/Lab-6/image14.png)

4. **Selecteer** de volgende tabellen/views:

    1. **Customer**

    2. **Date**

    3. **People**

    4. **PO**

    5. **Supplier**

    6. **Geo**

    7. **Product**

    8. **Reseller**

    9. **Sales**

5. Selecteer **Bevestigen**.

    ![](../media/Lab-6/image15.png)

    U wordt doorgestuurd naar het nieuwe semantische model met de geselecteerde tabellen. U kunt de tabellen naar wens **herschikken**. U zult merken dat sommige tabellen (**Geo**, **Reseller**, **Sales** en **Product**) een waarschuwingssymbool rechtsboven op de tabel hebben. Dit komt doordat het views zijn. Visualisaties die worden gemaakt met velden uit deze views, werken in **Direct query-modus** en niet in **Direct Lake-modus**.

    >**Opmerking:** De modus **Direct Lake** is sneller dan de modus **Direct query**.

## Taak 4: Relaties aanmaken

Als u zich momenteel niet in het zojuist aangemaakte semantische model bevindt, laten we dan naar de juiste locatie navigeren.

1. Navigeer terug naar de **Fabric-werkruimte** en selecteer het semantische model **sm_FAIAD**.

    ![](../media/Lab-6/image16.png)

2. Klik op **Semantisch model openen**.

    ![](../media/Lab-6/image17.png)

3. Controleer rechtsboven of u zich in de modus **Bewerken** bevindt.

    ![](../media/Lab-6/image18.png)

4. De eerste stap is het aanmaken van relaties tussen deze tabellen.

    ![](../media/Lab-6/image19.png)

5. Laten we een relatie maken tussen de tabellen **Sales** en **Reseller**. Selecteer **ResellerID** uit de tabel **Sales** en sleep deze naar **ResellerID** in de tabel **Reseller**.

    ![](../media/Lab-6/image20.png)

6. Het dialoogvenster **Nieuwe relatie** wordt geopend. Controleer of **From table** is ingesteld op **Sales** en **Column** op **ResellerID**.

7. Controleer of **To table** is ingesteld op **Reseller** en **Column** op **ResellerID**.

8. Controleer of **Cardinality** is ingesteld op **Many to one (*:1)**.

9. Controleer of **Cross filter direction** is ingesteld op **Single**.

10. Selecteer **Opslaan**.

    ![](../media/Lab-6/image21.png)

11. Maak op vergelijkbare wijze een relatie aan tussen de tabellen **Sales** en **Date**. Selecteer **InvoiceDate** uit de tabel **Sales** en sleep deze naar **Date** in de tabel **Date**.

12. Het dialoogvenster **Nieuwe relatie** wordt geopend. Controleer of **From table** is ingesteld op **Sales** en **Column** op **InvoiceDate**.

13. Controleer of **To table** is ingesteld op **Date** en **Column** op **Date**.

14. Controleer of **Cardinality** is ingesteld op **Many to one (*:1)**.

15. Controleer of **Cross filter direction** is ingesteld op **Single**.

16. Selecteer **Opslaan**.

    ![](../media/Lab-6/image22.png)

17. Maak op vergelijkbare wijze een **veel-op-één**-relatie aan tussen de tabellen **Sales** en **Product**. Selecteer **StockItemID** uit de tabel **Sales** en **StockItemID** uit de tabel **Product**.

    >**Opmerking:** Al onze wijzigingen worden automatisch opgeslagen.

    **Controlepunt:** Uw model moet nu drie relaties bevatten tussen de tabellen **Sales** en **Reseller**, **Sales** en **Date**, en **Sales** en **Product**, zoals weergegeven in de onderstaande schermafbeelding:

    ![](../media/Lab-6/image23.png)

    Vanwege tijdsbeperkingen zullen we niet alle relaties aanmaken. Als er tijd beschikbaar is, kunt u het optionele gedeelte aan het einde van het lab voltooien. In dat gedeelte worden de stappen beschreven om de resterende relaties aan te maken.

## Taak 5: Metingen aanmaken

Laten we een aantal metingen toevoegen die we nodig hebben om het Sales-dashboard aan te maken.

1. Selecteer de tabel **Sales** in de modelweergave. We willen de metingen toevoegen aan de tabel **Sales**.

2. Selecteer in het bovenste menu **Start -> Nieuwe meting**. U ziet dat de formulebalk wordt weergegeven.

3. Voer **Sales = SUM(Sales[Sales Amount])** in de **formulebalk** in.

4. Klik op het **vinkje** links van de formulebalk of druk op **Enter**.

5. Vouw het deelvenster **Eigenschappen** aan de rechterkant uit.

6. Vouw de sectie **Opmaak** uit.

7. Selecteer **Valuta** in de vervolgkeuzelijst **Indeling**.

8. Stel **Aantal decimalen** in op **0**.

    ![](../media/Lab-6/image24.png)

9. Terwijl de tabel **Sales** geselecteerd is, selecteert u in het bovenste menu **Start -> Nieuwe meting**. U ziet dat de formulebalk wordt weergegeven.

10. Voer **Units = SUM(Sales[Quantity])** in de **formulebalk** in.

11. Klik op het **vinkje** links van de formulebalk of druk op **Enter**.

12. Vouw in het deelvenster **Eigenschappen** aan de rechterkant de sectie **Opmaak** uit (het kan enkele seconden duren voordat het deelvenster **Eigenschappen** wordt geladen).

13. Selecteer **Geheel getal** in de vervolgkeuzelijst **Indeling**.

14. Gebruik de schuifregelaar om **Duizendtalscheidingsteken** in te stellen op **Ja**.

    ![](../media/Lab-6/image25.png)

15. Terwijl de tabel **Sales** geselecteerd is, selecteert u in het bovenste menu **Start -> Nieuwe meting**. U ziet dat de formulebalk wordt weergegeven.

16. Voer **Sales Orders = DISTINCTCOUNT(Sales[InvoiceID])** in de **formulebalk** in.

17. Klik op het **vinkje** links van de formulebalk of druk op **Enter**.

18. Vouw in het deelvenster **Eigenschappen** aan de rechterkant de sectie **Opmaak** uit.

19. Selecteer **Geheel getal** in de vervolgkeuzelijst **Indeling**.

20. Gebruik de schuifregelaar om **Duizendtalscheidingsteken** in te stellen op **Ja**.

    ![](../media/Lab-6/image26.png)

21. Selecteer in het deelvenster **Gegevens** (aan de rechterkant) **Model**. U ziet dat dit een weergave biedt waarmee u alle onderdelen in het semantische model kunt ordenen.

22. Vouw **Semantic model -> Measures** uit om alle metingen te bekijken die u zojuist hebt aangemaakt.

23. U kunt ook **afzonderlijke tabellen uitvouwen** om de **Columns**, **Hierarchies** en **Measures** binnen elke tabel te bekijken.

    ![](../media/Lab-6/image27.png)

    Vanwege tijdsbeperkingen zullen we niet alle metingen aanmaken. Als er tijd beschikbaar is, kunt u het optionele gedeelte aan het einde van het lab voltooien. In dat gedeelte worden de stappen beschreven om de resterende metingen aan te maken.

    We hebben nu een semantisch model aangemaakt; de volgende stap is het maken van een rapport. Dat doen we in het volgende lab.

## Taak 6: Optioneel gedeelte – Relaties aanmaken

Laten we de resterende relaties toevoegen.

1. Selecteer in het menu **Start -> Relaties beheren**.

2. Het dialoogvenster **Relaties beheren** wordt geopend. Selecteer **+ Nieuwe relatie**.

    ![](../media/Lab-6/image28.png)

    ![](../media/Lab-6/image28(1).png)

3. Het dialoogvenster **Nieuwe relatie** wordt geopend. Controleer of **From table** is ingesteld op **Sales** en **Column** op **SalespersonPersonID**.

4. Controleer of **To table** is ingesteld op **People** en **Column** op **PersonID**.

5. Controleer of **Cardinality** is ingesteld op **Many to one (*:1)**.

6. Controleer of **Cross-filter direction** is ingesteld op **Single**.

7. Selecteer **Opslaan**. Het dialoogvenster **Relaties beheren** wordt geopend met de nieuw toegevoegde relatie.

    ![](../media/Lab-6/image29.png)

8. Laten we nu een relatie aanmaken tussen **Product** en **Supplier**. Selecteer **+ Nieuwe relatie**.

9. Controleer of **From table** is ingesteld op **Product** en **Column** op **SupplierID**.

10. Controleer of **To table** is ingesteld op **Supplier** en **Column** op **SupplierID**.

11. Controleer of **Cardinality** is ingesteld op **Many to one (*:1)**.

12. Controleer of **Cross-filter direction** is ingesteld op **Both**.

13. Selecteer **Opslaan**.

    ![](../media/Lab-6/image30.png)

14. Laten we nu een relatie aanmaken tussen **Reseller** en **Geo**. Selecteer **+ Nieuwe relatie**.

15. Het dialoogvenster **Nieuwe relatie** wordt geopend. Controleer of **From table** is ingesteld op **Reseller** en **Column** op **PostalCityID**.

16. Controleer of **To table** is ingesteld op **Geo** en **Column** op **CityID**.

17. Controleer of **Cardinality** is ingesteld op **Many to one (*:1)**.

18. Controleer of **Cross-filter direction** is ingesteld op **Both**.

19. Selecteer **Opslaan**.

    ![](../media/Lab-6/image31.png)

20. Maak op vergelijkbare wijze een relatie aan tussen **Customer** en **Reseller**. Selecteer **+ Nieuwe relatie**.

21. Het dialoogvenster **Nieuwe relatie** wordt geopend. Controleer of **From table** is ingesteld op **Customer** en **Column** op **ResellerID**.

22. Controleer of **To table** is ingesteld op **Reseller** en **Column** op **ResellerID**.

23. Controleer of **Cardinality** is ingesteld op **Many to one (*:1)**.

24. Controleer of **Cross-filter direction** is ingesteld op **Single**.

25. Selecteer **Opslaan**.

    **Controlepunt:** Het venster **Relaties beheren** moet eruitzien zoals in de onderstaande schermafbeelding.

    ![](../media/Lab-6/image32.png)

26. Maak op vergelijkbare wijze een **veel-op-één**-relatie aan tussen **PO** en **Date**. Selecteer **Order_Date** uit **PO** en **Date** uit **Date**.

27. Maak op vergelijkbare wijze een **veel-op-één**-relatie aan tussen **PO** en **Product**. Selecteer **StockItemID** uit **PO** en **StockItemID** uit **Product**.

28. Maak op vergelijkbare wijze een **veel-op-één**-relatie aan tussen **PO** en **People**. Selecteer **ContactPersonID** uit **PO** en **PersonID** uit **People**.

29. Selecteer **Sluiten** om het dialoogvenster **Relaties beheren** te sluiten. Het aanmaken van alle relaties is nu voltooid.

    **Controlepunt:** Uw model moet eruitzien zoals in de onderstaande schermafbeelding.

    ![](../media/Lab-6/image33.png)

## Taak 7: Optioneel gedeelte – Metingen aanmaken

Laten we de resterende metingen toevoegen.

1. Selecteer de tabel **Sales** en selecteer in het bovenste menu **Start -> Nieuwe meting**.

2. Voer **Avg Order = DIVIDE([Sales], [Sales Orders])** in de formulebalk in.

3. Klik op het **vinkje** in de formulebalk of druk op **Enter**.

4. Vouw het deelvenster **Eigenschappen** aan de rechterkant uit.

5. Vouw de sectie **Opmaak** uit.

6. Selecteer **Valuta** in de vervolgkeuzelijst **Indeling**.

7. Stel **Aantal decimalen** in op **0**.

    ![](../media/Lab-6/image34.png)

8. Volg vergelijkbare stappen om de volgende metingen toe te voegen:

    1. In de tabel **Sales**: **GM = SUM(Sales[LineProfit])** opgemaakt als **Valuta met 0 decimalen**.

    2. In de tabel **Sales**: **GM% = DIVIDE([GM], [Sales])** opgemaakt als **Percentage met 0 decimalen**.

    3. In de tabel **Customer**: **No of Customers = COUNTROWS(Customer)** opgemaakt als **Geheel getal met duizendtalscheidingsteken ingeschakeld**.

# Referenties

Fabric Analyst in a Day (FAIAD) introduceert u een aantal van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service vindt u in de sectie Help (?) koppelingen naar een aantal uitstekende resources.

![](../media/Lab-1/image29.png)

Hieronder vindt u nog een aantal resources die u zullen helpen bij uw volgende stappen met Microsoft Fabric.

- Lees de blogpost voor de volledige [aankondiging van Microsoft Fabric GA](https://aka.ms/Fabric-Hero-Blog-Ignite23)

- Verken Fabric via de [Guided Tour](https://aka.ms/Fabric-GuidedTour)

- Meld u aan voor de [gratis proefversie van Microsoft Fabric](https://aka.ms/try-fabric)

- Bezoek de [Microsoft Fabric-website](https://aka.ms/microsoft-fabric)

- Leer nieuwe vaardigheden door de [Fabric Learning-modules](https://aka.ms/learn-fabric) te verkennen

- Verken de [technische documentatie van Fabric](https://aka.ms/fabric-docs)

- Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook)

- Word lid van de [Fabric-community](https://aka.ms/fabric-community) om vragen te stellen, feedback te delen en van anderen te leren

Lees de meer gedetailleerde aankondigingsblogs over Fabric-ervaringen:

- [Blog over Data Factory-ervaring in Fabric](https://aka.ms/Fabric-Data-Factory-Blog)

- [Blog over Synapse Data Engineering-ervaring in Fabric](https://aka.ms/Fabric-DE-Blog)

- [Blog over Synapse Data Science-ervaring in Fabric](https://aka.ms/Fabric-DS-Blog)

- [Blog over Synapse Data Warehousing-ervaring in Fabric](https://aka.ms/Fabric-DW-Blog)

- [Blog over Synapse Real-Time Analytics-ervaring in Fabric](https://aka.ms/Fabric-RTA-Blog)

- [Aankondigingsblog van Power BI](https://aka.ms/Fabric-PBI-Blog)

- [Blog over Data Activator-ervaring in Fabric](https://aka.ms/Fabric-DA-Blog)

- [Blog over beheer en governance in Fabric](https://aka.ms/Fabric-Admin-Gov-Blog)

- [Blog over OneLake in Fabric](https://aka.ms/Fabric-OneLake-Blog)

- [Blog over Dataverse- en Microsoft Fabric-integratie](https://aka.ms/Dataverse-Fabric-Blog)

© 2026 Microsoft Corporation. Alle rechten voorbehouden.

Door gebruik te maken van deze demo/dit lab, gaat u akkoord met de volgende voorwaarden:

De technologie/functionaliteit die in deze demo/dit lab wordt beschreven, wordt door Microsoft Corporation aangeboden met als doel uw feedback te verkrijgen en u een leerervaring te bieden. U mag de demo/het lab uitsluitend gebruiken om dergelijke technologische functies en functionaliteit te evalueren en feedback aan Microsoft te geven. U mag het niet voor enig ander doel gebruiken. U mag deze demo/dit lab of een deel daarvan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, in licentie geven, er afgeleide werken van maken, overdragen of verkopen.

HET KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF EEN DEEL DAARVAN) NAAR ENIGE ANDERE SERVER OF LOCATIE VOOR VERDERE REPRODUCTIE OF HERDISTRIBUTIE IS UITDRUKKELIJK VERBODEN.

DEZE DEMO/DIT LAB BIEDT BEPAALDE SOFTWARE TECHNOLOGIE-/PRODUCTFUNCTIES EN -FUNCTIONALITEIT, INCLUSIEF MOGELIJKE NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF CONFIGURATIE VOOR HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN DIE IN DEZE DEMO/DIT LAB WORDEN WEERGEGEVEN, VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIEFUNCTIONALITEIT EN WERKEN MOGELIJK NIET OP DE MANIER WAAROP EEN DEFINITIEVE VERSIE ZAL WERKEN. WE KUNNEN OOK GEEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN UITBRENGEN. UW ERVARING MET HET GEBRUIK VAN DERGELIJKE FUNCTIES EN FUNCTIONALITEIT IN EEN FYSIEKE OMGEVING KAN OOK ANDERS ZIJN.

**FEEDBACK**. Als u feedback geeft over de technologische functies, functionaliteit en/of concepten die in deze demo/dit lab worden beschreven aan Microsoft, verleent u Microsoft kosteloos het recht om uw feedback op welke manier dan ook en voor welk doel dan ook te gebruiken, te delen en te commercialiseren. U verleent derden ook kosteloos de eventuele octrooirechten die nodig zijn voor hun producten, technologieën en diensten om bepaalde onderdelen van een Microsoft-software of -service die de feedback bevat te gebruiken of te koppelen. U geeft geen feedback die onderworpen is aan een licentie die Microsoft verplicht zijn software of documentatie in licentie te geven aan derden omdat we uw feedback daarin opnemen. Deze rechten blijven van kracht na afloop van deze overeenkomst.

MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN MET BETREKKING TOT DE DEMO/HET LAB AF, MET INBEGRIP VAN ALLE GARANTIES EN VOORWAARDEN VAN VERKOOPBAARHEID, UITDRUKKELIJK, IMPLICIET OF WETTELIJK, GESCHIKTHEID VOOR EEN BEPAALD DOEL, EIGENDOM EN NIET-INBREUK. MICROSOFT GEEFT GEEN GARANTIES OF VERKLARINGEN MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, DE UITVOER DIE VOORTVLOEIT UIT HET GEBRUIK VAN DE DEMO/HET LAB, OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR ENIG DOEL.

**DISCLAIMER**

Deze demo/dit lab bevat slechts een deel van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen veranderen in toekomstige versies van het product. In deze demo/dit lab leert u over enkele, maar niet alle, nieuwe functies.
