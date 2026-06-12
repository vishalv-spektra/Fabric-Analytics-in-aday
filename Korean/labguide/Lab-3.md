# Microsoft Fabric - Fabric Analyst in a Day - 랩 3

![](../media/Lab-1/krn3.png)

## 목차

- 소개
- ADLS Gen2 바로 가기
  - 작업 1: 바로 가기 만들기
- 시각적 쿼리를 사용하여 데이터 변환
  - 작업 2: 시각적 쿼리를 사용하여 Geo 뷰 만들기
  - 작업 3: SQL 쿼리를 사용하여 Reseller, Sales 및 Product 뷰 만들기
- 참조


# 소개

우리 시나리오에서 매출 데이터는 ERP 시스템에서 제공되며 ADLS Gen2에 저장됩니다. 매일 정오/오후 12시에 업데이트됩니다. 이 데이터를 레이크하우스로 변환하고 수집하여 모델에서 사용해야 합니다.

데이터를 수집할 수 있는 방법은 다양합니다.

- **바로 가기:** 이렇게 하면 데이터에 대한 링크가 만들어지고 시각적 쿼리 뷰를 사용하여 데이터를 변환할 수 있습니다. 이 랩에서는 바로 가기를 사용하겠습니다.

- **Notebooks:** 이를 위해서는 코드를 작성해야 합니다. 이는 개발자 친화적인 방식입니다.

- **데이터 흐름 2세대:** 아마도 Power Query 또는 데이터 흐름 1세대에 익숙할 것입니다. 데이터 흐름 2세대는 이름에서 알 수 있듯이 데이터 흐름의 최신 버전입니다. 이는 데이터를 여러 데이터 원본으로 변환하고 수집하는 추가 기능과 함께 Power Query / 데이터 흐름 1세대의 모든 기능을 제공합니다. 다음 두 랩에서 이것을 소개할 것입니다.

- **파이프라인:** 이는 오케스트레이션 도구입니다. 데이터를 추출, 변환, 수집하도록 활동을 조정할 수 있습니다. 파이프라인을 사용하여 데이터 흐름 2세대 활동을 실행하여 추출, 변환, 수집이 수행되도록 할 수 있습니다.

먼저 ADLS Gen2 데이터 원본의 데이터를 레이크하우스로 수집하는 바로 가기를 생성하겠습니다. 수집된 후에는 시각적 쿼리 뷰를 사용하여 변환합니다.

이 랩을 마치면 다음 사항을 알게 됩니다.

- 레이크하우스에서 바로 가기 생성 방법

- 시각적 쿼리 기능을 사용하여 데이터를 변환하는 방법

# ADLS Gen2 바로 가기

## 작업 1: 바로 가기 만들기

바로 가기를 사용하여 대상 위치로 이동하는 링크를 생성할 수 있습니다. 바로 가기를 통해 데이터를 레이크하우스로 물리적으로 이동하지 않고도 데이터에 액세스할 수 있습니다. 이것은 Windows 바탕 화면에 바로 가기를 만드는 것과 같습니다.

1. 화면 상단에서 **lh_FAIAD** 탭을 선택하여 레이크하우스로 이동합니다.

    1) 탭이 없는 경우 작업 영역으로 돌아가서 레이크하우스 열 수 있습니다.

2. **탐색기** 창에서 **테이블** 옆의 **줄임표**를 선택합니다.

3. **새 바로 가기**를 선택합니다.

    ![](../media/Lab-3/image2.png)

4. **새 바로 가기** 대화 상자가 열립니다. **외부 원본**에서 **Azure Data Lake Storage Gen2**를 선택합니다.

    ![](../media/Lab-3/image3.png)

5. **새 연결(1)** 을 선택합니다.

6. **URL** 속성:에 <https://stvnextblobstorage.dfs.core.windows.net/fabrikam-sales> **(2):** 을 입력합니다.

7. 연결 섹션에서 **새 연결 만들기(3)** 를 클릭합니다.

8. 인증 종류 드롭다운에서 **SAS(공유 액세스 서명)(4)** 를 선택합니다.

9. SAS 토큰을 복사하여 SAS 토큰 (5) 필드에 붙여넣습니다.

    - **SAS 토큰:** <inject key="Sas token"></inject>

10. 화면 오른쪽 하단에서 **다음 (6)** 을 선택합니다.

    ![](../media/Lab-3/image4.png)

11. 왼쪽 패널에 디렉터리 구조가 표시된 ADLS Gen2에 연결됩니다. **Delta-Parquet-Format-FY25 (1)** 를 확장합니다.

12. 다음 디렉터리 **(2)**를** 선택**한 후 **다음 (3)** 을 클릭합니다.

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

    **참고:** Sales.Invoice_May는 선택되지 않은 유일한 디렉터리입니다.

    ![](../media/Lab-3/image5.png)

13. 이름을 편집할 수 있는 다음 대화 상자로 이동합니다. **Application.Cities** 에 대한 작업에서 **편집 아이콘 (1)** 을 선택합니다.

14. **Application.Cities를 Cities (2)** 로 이름을 변경합니다.

15. 이름 옆의 확인 표시를 선택하여 변경 사항을 저장합니다 **(3)**.

    ![](../media/Lab-3/image6.png)

16. 마찬가지로 바로 가기 이름도 아래와 같이 이름을 바꿉니다.
    1. Application.Countries에서 **Countries**로

    2. Application.StateProvinces에서 **States**로

    3. DateDim에서 **Date**로

    4. Sales.BuyingGroups에서 **BuyingGroups**로

    5. Sales.Customers에서 **Customers**로

    6. Sales.InvoiceLines에서 **InvoiceLineItems**로

    7. Sales.Invoices에서 **Invoices**로

    8. Warehouse.StockGroups에서 **ProductGroups**로

    9. Warehouse.StockItemStockGroups에서 **ProductItemGroup**로

    10. Warehouse.StockItems에서 **ProductItem**로

    **참고:** 이름을 다시 확인하세요. 랩 도중 오타로 인해 오류가 발생합니다.

17. **만들기**를 선택하여 바로 가기를 만듭니다.

    ![](../media/Lab-3/image7.png)

18. 모든 바로 가기가 Tables로 생성되는 것을 확인할 수 있습니다. **BuyingGroups** 테이블을 선택하면 데이터 창에서 데이터 미리 뷰를 볼 수 있습니다.

    ![](../media/Lab-3/image8.png)

    다음 단계는 의미 체계 모델을 만들 수 있도록 데이터를 변환하는 것입니다. 데이터를 변환하는 뷰를 만들겠습니다.

# 시각적 쿼리를 사용하여 데이터 변환

## 작업 2: 시각적 쿼리를 사용하여 Geo 뷰 만들기

1. SQL 엔드포인트를 사용하여 **레이크하우스**에 액세스할 수 있습니다. 이를 통해 데이터를 쿼리하고 뷰를 만들 수 있습니다. 화면 **오른쪽 상단**에서 **Lakehouse (1) -> SQL 분석 엔드포인트 (2)** 를 선택합니다.

    ![](../media/Lab-3/image9.png)

    SQL 분석 엔드포인트로 이동합니다. 이제 상단 탐색에 새 항목이 추가되었으며, 해당 탭을 선택하면 레이크하우스로 돌아갈 수 있습니다. 탐색기 패널이 변경된 것을 확인할 수 있습니다. 이제 뷰, 저장 프로시저, 쿼리 등을 만들 수 있습니다. Power Query와 같은 로우 코드 인터페이스를 제공하는 시각적 쿼리를 만들려고 합니다. 결과를 뷰로 저장합니다.

    먼저 Geo 뷰를 생성하겠습니다. Geo 뷰를 생성하기 위해 Cities, States, Countries 테이블의 데이터를 병합해야 합니다.

2. 상단 메뉴에서 **새 SQL 쿼리 (1)** 옆의 드롭다운을 클릭하고 **새 시각적 쿼리 (2)** 를 선택합니다.

    ![](../media/Lab-3/image10.png)

3. 쿼리를 작성하려면 시각적 쿼리 패널에 테이블을 추가해야 합니다. **Cities (1)** 테이블 옆의 말줄임표를 클릭하고 **캔버스에 삽입(2)** 을 선택합니다.

    ![](../media/Lab-3/image11.png)

4. **States**와 **Countries** 테이블에 대해서도 동일한 단계를 반복합니다.

    다음으로, 이 쿼리들을 병합해야 합니다. 시각적 쿼리 편집기에는 Power Query 편집기를 사용할 수 있는 옵션이 있습니다. Power BI 때문에 익숙한 기능이니 이 기능을 사용해보겠습니다.

5. **시각적 쿼리 편집기 메뉴** 오른쪽의 **팝업으로 열기** 아이콘을 선택합니다. Power Query 편집기로 이동합니다.

    **참고:** 이 아이콘이 즉시 표시되지 않으면 오른쪽으로 스크롤하거나 시각적 쿼리 탭을 다시 열어야 할 수 있습니다.

    ![](../media/Lab-3/image12.png)

6. **Cities (1)** 쿼리를 선택한 상태에서 Power Query 편집기 리본 메뉴에서 **홈 (2) -> 결합 (3) -> 쿼리 병합 드롭다운 (4) -> 쿼리를 새 항목으로 병합 (5)을 선택합니다.** 쿼리 병합 대화 상자가 열립니다.

    ![](../media/Lab-3/image13.png)

7. **병합할 왼쪽 테이블**에서 **Cities**를 선택합니다.

8. **병합할 오른쪽 테이블**에서 **States**를 선택합니다.

9. 두 테이블에서 **StateProvinceID** 열을 선택합니다. 이 열을 사용하여 조인할 것입니다.

10. **조인 종류**로 **안쪽**을 선택합니다.

11. **확인**을 선택합니다.

    ![](../media/Lab-3/image14.png)

    **병합**이라는 새 쿼리가 생성되었음을 알 수 있습니다. States에서 열이 몇 개 필요합니다.

12. **Data 뷰**(아래쪽 패널)에서 **States** 열(오른쪽 마지막 열) 옆에 있는 **이중 화살표**를 클릭합니다.

13. 패널이 열립니다. 다음 열만 선택되었는지 확인합니다.

    1. StateProvinceCode

    2. StateProvinceName

    3. CountryID

    4. SalesTerritory

14. **확인**을 선택합니다.

    ![](../media/Lab-3/image15.png)

    이제 Countries 쿼리를 병합해야 합니다.

15. 쿼리 병합을 선택한 상태 (1)에서 리본 메뉴에서 **홈 (2) -> 결합 (3) -> 쿼리 병합 드롭다운 (4) -> 쿼리 병합 (5)** 을 선택합니다.

    ![](../media/Lab-3/image16.png)

16. 쿼리 병합 대화 상자가 열립니다. **병합할 오른쪽 테이블**에서 **Countries**를 선택합니다.

17. 두 테이블에서 **CountryID** 열을 선택합니다. 이 열을 사용하여 조인할 것입니다.

18. **조인 종류**로 **안쪽**을 선택합니다.

19. **확인**을 선택합니다.

    ![](../media/Lab-3/image17.png)

    Countries에서 열이 몇 개 필요합니다.

20. **Data 뷰**(하단 패널)에서 **Countries** 열 옆의 **이중 화살표**를 클릭합니다.

21. 패널이 열립니다. 다음 열만 선택되었는지 확인합니다.

    1. CountryName

    2. FormalName

    3. IsoAlpha3Code

    4. IsoNumericCode

    5. CountryType

    6. Continent

    7. Region

    8. Subregion

22. **확인**을 선택합니다.

    **중요:** 아래로 스크롤하여 21단계에 나열된 8개 열을 모두 선택해야 합니다. 아래 스크린샷은 UI 제한으로 인해 처음 5개의 열만 표시합니다.

    ![](../media/Lab-3/image18.png)

    **병합** 테이블의 모든 열이 필요한 것은 아닙니다. 필요한 항목만 선택해야 합니다.

23. 쿼리 **병합**을 선택한 상태 (1)에서 리본 메뉴에서 **홈 (2) -> 열 선택 (3) -> 열 선택 (4)** 을 선택합니다.

    **참고:** 열 선택 옵션이 보이지 않는 경우 열 관리 항목 하단에서 찾을 수 있습니다.

    ![](../media/Lab-3/image19.png)

24. 열 선택 대화 상자가 열립니다. 다음 열을 **선택 취소**합니다.

    1. StateProvinceID

    2. Location

    3. LastEditedBy

    4. ValidFrom

    5. ValidTo

    6. CountryID

25. **확인**을 선택합니다.

    ![](../media/Lab-3/image20.png)

    오른쪽의 적용된 단계 패널과 시각적 뷰 모두에 모든 단계가 기록되어 있으며, 프로세스는 Power Query와 같습니다. 이 쿼리에서 데이터가 로드되도록 쿼리 병합 및 로드 활성화의 이름을 변경하겠습니다.

26. 쿼리(왼쪽) 패널에서 **Merge** 쿼리를 **마우스 오른쪽 버튼으로 클릭**합니다. **이름 바꾸기**를 선택하고 쿼리 이름을 **Geo**로 바꿉니다.

27. 쿼리(왼쪽) 패널에서 **Geo** 쿼리를 **마우스 오른쪽 버튼으로 클릭**합니다.**로드 사용**을 선택하여 이 쿼리를 활성화합니다.

28. Cities, States 및 Countries쿼리가 **비활성화**되어 있는지 확인합니다.

29. Power Query 편집기의 오른쪽 하단에서 **저장**을 선택합니다.

    ![](../media/Lab-3/image21.png)

    시각적 쿼리 편집기로 이동합니다. 이제 이 쿼리를 뷰로 저장해 보겠습니다.

    **참고:** Power Query 편집기를 사용하여 수행한 모든 단계는 시각적 쿼리 편집기를 통해서도 수행할 수 있습니다.

30. 시각적 쿼리 편집기 메뉴에서 **뷰로 저장**을 선택합니다.

    ![](../media/Lab-3/image22.png)

    뷰로 저장 대화 상자가 열립니다. SQL 쿼리가 사용 가능하다는 것을 알 수 있습니다. SQL을 검토하고 싶다면 확인할 수 있습니다.

31. **뷰 이름**으로 **Geo**를 입력합니다.

32. **확인**을 선택하여 뷰를 저장합니다.

    ![](../media/Lab-3/image23.png)

    뷰가 저장되면 알림을 받게 됩니다.

33. 탐색기(왼쪽) 패널에서 **Views**를 펼칩니다. 새로 생성된 Geo 뷰가 있습니다.

    ![](../media/Lab-3/image24.png)

## 작업 3: SQL 쿼리를 사용하여 Reseller, Sales 및 Product 뷰 만들기

1. Fabric에서는 SQL 쿼리를 사용하여 뷰를 생성할 수도 있습니다. 상단의 리본 메뉴에서 새 SQL 쿼리를 선택합니다.

    ![](../media/Lab-3/image25.png)

2. 여기에서는 필요한 뷰를 생성하는 데 도움이 되는 TSQL을 작성할 수 있습니다.

3. 아래 SQL 쿼리를 쿼리 창에 붙여 넣습니다. 이렇게 하면 ‘Reseller, Sales, Product라는 세 개의 뷰가 생성됩니다.

    ```sql
    CREATE VIEW dbo.Reseller AS
    select [$Outer].[ResellerID] as [ResellerID],
        [$Outer].[ResellerName] as [ResellerName],
        [$Outer].[PostalCityID] as [PostalCityID],
        [$Outer].[PhoneNumber] as [PhoneNumber],
        [$Outer].[FaxNumber] as [FaxNumber],
        [$Outer].[WebsiteURL] as [WebsiteURL],
        [$Outer].[DeliveryAddressLine1] as [DeliveryAddressLine1],
        [$Outer].[DeliveryAddressLine2] as [DeliveryAddressLine2],
        [$Outer].[DeliveryPostalCode] as [DeliveryPostalCode],
        [$Outer].[PostalAddressLine1] as [PostalAddressLine1],
        [$Outer].[PostalAddressLine2] as [PostalAddressLine2],
        [$Outer].[PostalPostalCode] as [PostalPostalCode],
        [$Inner].[BuyingGroupName] as [ResellerCompany]
    from [lh_FAIAD].[dbo].[Customers] as [$Outer]
    inner join (
        select [_].[BuyingGroupID] as [BuyingGroupID2],
            [_].[BuyingGroupName] as [BuyingGroupName],
            [_].[LastEditedBy] as [LastEditedBy2],
            [_].[ValidFrom] as [ValidFrom2],
            [_].[ValidTo] as [ValidTo2]
        from [lh_FAIAD].[dbo].[BuyingGroups] as [_]
    ) as [$Inner] on ([$Outer].[BuyingGroupID] = [$Inner].[BuyingGroupID2] or [$Outer].[BuyingGroupID] is null and [$Inner].[BuyingGroupID2] is null)
    GO

    CREATE VIEW dbo.Sales AS
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
    from (
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
        from (
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
            inner join (
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
                from [lh_FAIAD].[dbo].[Invoices] as [_]
            ) as [$Inner] on ([$Outer].[InvoiceID] = [$Inner].[InvoiceID2] or [$Outer].[InvoiceID] is null and [$Inner].[InvoiceID2] is null)
        ) as [_]
    ) as [$Outer]
    where exists (
        select 1
        from (
            select [ResellerID]
            from [lh_FAIAD].[dbo].[Reseller] as [$Table]
        ) as [$Inner]
        where [$Outer].[CustomerID] = [$Inner].[ResellerID] or [$Outer].[CustomerID] is null and [$Inner].[ResellerID] is null
    )
    GO

    CREATE VIEW dbo.Product AS
    select [$Outer].[StockItemID],
        [$Outer].[StockItemName],
        [$Outer].[SupplierID],
        [$Outer].[Size],
        [$Outer].[IsChillerStock],
        [$Outer].[TaxRate],
        [$Outer].[UnitPrice],
        [$Outer].[RecommendedRetailPrice],
        [$Outer].[TypicalWeightPerUnit],
        [$Inner].[StockGroupName]
    from (
        select [$Outer].[StockItemID],
            [$Outer].[StockItemName],
            [$Outer].[SupplierID],
            [$Outer].[ColorID],
            [$Outer].[UnitPackageID],
            [$Outer].[OuterPackageID],
            [$Outer].[Brand],
            [$Outer].[Size],
            [$Outer].[LeadTimeDays],
            [$Outer].[QuantityPerOuter],
            [$Outer].[IsChillerStock],
            [$Outer].[Barcode],
            [$Outer].[TaxRate],
            [$Outer].[UnitPrice],
            [$Outer].[RecommendedRetailPrice],
            [$Outer].[TypicalWeightPerUnit],
            [$Outer].[MarketingComments],
            [$Outer].[InternalComments],
            [$Outer].[Photo],
            [$Outer].[CustomFields],
            [$Outer].[Tags],
            [$Outer].[SearchDetails],
            [$Outer].[LastEditedBy],
            [$Outer].[ValidFrom],
            [$Outer].[ValidTo],
            [$Inner].[StockGroupID]
        from [lh_FAIAD].[dbo].[ProductItem] as [$Outer]
        left outer join (
            select [_].[StockItemStockGroupID] as [StockItemStockGroupID],
                [_].[StockItemID] as [StockItemID2],
                [_].[StockGroupID] as [StockGroupID],
                [_].[LastEditedBy] as [LastEditedBy2],
                [_].[LastEditedWhen] as [LastEditedWhen]
            from [lh_FAIAD].[dbo].[ProductItemGroup] as [_]
        ) as [$Inner] on ([$Outer].[StockItemID] = [$Inner].[StockItemID2] or [$Outer].[StockItemID] is null and [$Inner].[StockItemID2] is null)
    ) as [$Outer]
    left outer join (
        select [_].[StockGroupID] as [StockGroupID2],
            [_].[StockGroupName] as [StockGroupName],
            [_].[LastEditedBy] as [LastEditedBy2],
            [_].[ValidFrom] as [ValidFrom2],
            [_].[ValidTo] as [ValidTo2]
        from [lh_FAIAD].[dbo].[ProductGroups] as [_]
    ) as [$Inner] on ([$Outer].[StockGroupID] = [$Inner].[StockGroupID2] or [$Outer].[StockGroupID] is null and [$Inner].[StockGroupID2] is null)
    GO
    ```
    
4. 붙여넣기를 마친 후 실행을 선택합니다.

    ![](../media/Lab-3/image26.png)

5. 탐색기(왼쪽) 패널에서 Views를 펼칩니다. 새로 생성된 뷰와 바로 사용할 수 있는 데이터가 준비되어 있습니다.

    ![](../media/Lab-3/image27.png)

    ![](../media/Lab-3/image28.png)

    ADLS Gen2 데이터 원본에서 데이터를 변환했습니다. 이 랩에서는 바로 가기를 만드는 방법을 배우고 시각적 쿼리 뷰를 사용하여 데이터를 변환하는 다양한 옵션을 살펴보았습니다.

    다음 랩에서는 데이터 흐름 2세대를 사용하고 다른 레이크하우스로 바로 가기를 만드는 방법에 대해 알아보겠습니다.

# 참조

Fabric Analyst in a Day(FAIAD)는 Microsoft Fabric에서 사용할 수 있는 몇 가지 주요 기능을 소개합니다. 서비스의 메뉴에 있는 도움말(?) 섹션에는 유용한 리소스로 연결되는 링크가 있습니다.

![](../media/Lab-3/image29.png)

아래는 Microsoft Fabric의 다음 단계에 도움이 되는 몇 가지 추가 자료입니다.

- [Microsoft Fabric GA 발표](https://aka.ms/Fabric-Hero-Blog-Ignite23) 전문을 블로그 포스트로 읽기

- [가이드 투어](https://aka.ms/Fabric-GuidedTour)로 Fabric 탐색

- [Microsoft Fabric 무료 평가판](https://aka.ms/try-fabric) 신청

- [Microsoft Fabric 웹사이트](https://aka.ms/microsoft-fabric) 방문

- [Fabric 학습 모듈](https://aka.ms/learn-fabric)을 탐색해서 새로운 기술 익히기

- [Fabric 기술 문서](https://aka.ms/fabric-docs) 검토

- [Fabric 시작하기 무료 e북](https://aka.ms/fabric-get-started-ebook) 읽기

- [Fabric 커뮤니티](https://aka.ms/fabric-community)에 가입하여 질문을 게시하고 피드백을 공유하며 다른 사람들로부터 배우기

더 많은 심층 Fabric 환경 발표 블로그 포스트 읽기:

- [Fabric 블로그의 Data Factory 환경](https://aka.ms/Fabric-Data-Factory-Blog)

- [Fabric 블로그의 Synapse Data Engineering 환경](https://aka.ms/Fabric-DE-Blog)

- [Fabric 블로그의 Synapse Data Science 환경](https://aka.ms/Fabric-DS-Blog)

- [Fabric 블로그의 Synapse Data Warehousing 환경](https://aka.ms/Fabric-DW-Blog)

- [Fabric 블로그의 Synapse Real-Time Analytics 환경](https://aka.ms/Fabric-RTA-Blog)

- [Power BI 발표 블로그](https://aka.ms/Fabric-PBI-Blog)

- [Fabric 블로그의 Data Activator 환경](https://aka.ms/Fabric-DA-Blog)

- [Fabric 블로그의 관리 및 거버넌스](https://aka.ms/Fabric-Admin-Gov-Blog)

- [Fabric 블로그의 OneLake](https://aka.ms/Fabric-OneLake-Blog)

- [Dataverse 및 Microsoft Fabric 통합 블로그](https://aka.ms/Dataverse-Fabric-Blog)

© 2026 Microsoft Corporation. All rights reserved.

이 데모/랩을 사용하면 다음 조건에 동의하게 됩니다.

이 데모/랩에 설명된 기술/기능은 학습 환경을 제공하고 사용자 의견을 얻기 위해 Microsoft Corporation에서 제공합니다. 데모/랩을 통해서만 이러한 기술적 특성과 기능을 평가하고 사용자 의견을 Microsoft에 제시할 수 있습니다. 다른 용도로는 사용할 수 없습니다. 이 데모/랩 또는 그 일부에 대해 수정, 복사, 배포, 전송, 표시, 수행, 재현, 게시, 라이선스 허여, 파생 작업 생성, 양도 또는 판매할 수 없습니다.

추가 복제 또는 재배포를 위한 다른 서버 또는 위치에 대한 데모/랩(또는 그 일부)의 복사 또는 재현은 명시적으로 금지됩니다.

이 데모/랩은 위에서 명시한 목적을 위해 복잡한 설정 또는 설치가 없는 시뮬레이션된 환경에서 잠재적인 새로운 기능과 개념을 포함하여 특정 소프트웨어 기술/제품의 특성 및 기능을 제공합니다. 이 데모/랩에서 서술된 기술/개념은 전체 기능을 나타내지 않을 수 있으며, 최종 버전이 작동하지 않을 수도 있습니다. 또한 해당 기능 또는 개념의 최종 버전을 릴리스하지 않을 수도 있습니다. 또한 실제 환경에서 이러한 특성과 기능을 사용한 경험이 다를 수도 있습니다.

**피드백.** 이 데모/랩에서 서술된 기술적 특성, 기능 및/또는 개념에 대한 사용자 의견을 Microsoft에 제시하면 Microsoft는 이 사용자 의견을 어떤 방식과 목적으로든 무료로 사용, 공유 및 상용화할 수 있습니다. 또한 제품, 기술 및 서비스에서 사용자 의견이 포함된 Microsoft 소프트웨어 또는 서비스의 특정 부분을 사용하거나 인터페이스하는 데 필요한 모든 특허권을 제3자에게 무료로 제공합니다. Microsoft에서 사용자 의견을 포함하기 때문에 Microsoft에서 해당 소프트웨어 또는 설명서의 사용을 인가해야 하는 라이선스에 종속된 사용자 의견은 제공할 수 없습니다. 이러한 권리는 본 계약에 의거하여 유효합니다.

Microsoft Corporation은 이에 따라 명시적, 묵시적 또는 법적 특정 목적에의 적합성, 권리 및 비침해 여부에 관계없이 모든 보증과 조건을 포함하여 데모/랩과 관련된 모든 보증 및 조건을 부인합니다. Microsoft는 어떤 목적으로든 결과의 정확성, 데모/랩의 사용으로 파생된 출력 또는 데모/랩에 포함된 정보의 적합성과 관련하여 어떠한 보증이나 진술도 하지 않습니다.

**고지 사항**

이 데모/랩에는 Microsoft Power BI의 새로운 기능 및 향상된 기능 중 일부만 포함되어 있습니다. 일부 기능은 제품의 향후 릴리스에서 변경될 수 있습니다. 이 데모/랩에서는 새로운 기능 모두가 아닌 일부에 대해 학습하게 됩니다.
