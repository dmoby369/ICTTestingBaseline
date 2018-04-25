# 12. Tables
## Accessibility Requirements
* **[WCAG SC 1.3.1 Info and Relationships](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html)** -- Information, structure, and relationships conveyed through presentation can be programmatically determined or are available in text.

## Test Method Rationale
For assistive technology (AT) users, data tables must explicitly associate table data with table row and column headers via programmatic markup. Table markup also facilitates navigation for AT users by providing programmatic landmarks via column and row headers.

When `<table>` elements are used for layout purposes, data table structure elements are not permitted, such as `<th>`, `summary=` (HTML4), or `<caption>`.

## Limitations, Assumptions, Exceptions
* Data tables are those tables where information in a cell requires a row or column header to adequately describe the cell's contents. If a table is used for placement of components on the page for visual aesthetics, then it is considered a layout table. This requirement applies to data tables only.
* Some content may visually appear to require a data table structure, but, linearizing the content and/or viewing the code reveals that the content is understandable without the table. This technique may be used for responsive design. These elements use CSS and/or other styling methods to present content in columns or rows. The information conveyed does not rely on programmatic relationships between column or row headers to be understood. This content is not a data table and should not use the element, ARIA role="table", and associated programmatic table attributes. It should be tested using other baseline tests, such as [13. Headings](13Headings.md) and/or possibly [10. Forms (associated instructions)](10Forms.md).
* Rows of data that are related must have a row header so assistive technology users can understand the relationship of the row's data cells. Not every table requires a row header. For example, a calendar month is a data table, typically with the days of the week as column headers. The dates in a row are not related so typically, there is no row header present. However, if there was a cell in each row to indicate the week of the year, this cell would serve as a row header for the dates within that row.

## Test Procedures for 1.3.1 Info and Relationships
### Identify Content
All content/data visually presented in a table with column and/or row headers where the content, when linearized, is not in a meaningful sequence.

Note: Linearization of table content is the presentation of a table’s two-dimensional content in one-dimensional order of the content in the source, beginning with the first cell in the first row and ending with the last cell in the last row, from left to right, top to bottom. 

### Test Instructions
#### Data Tables
1. Table: Check that each data table has programmatic markup to identify it as a table using only one of the following techniques:
   * HTML `<table>`. 
   * ARIA `role="table"`
   * **NOTE**: according to HTML5 specifications, the `<table>` element and associated elements and attributes may not be used in combination with ARIA `role="table"` and associated roles and attributes. If a table combines these techniques, it fails this test.
2. Table data cell: Check that each data cell uses only one of the following methods to identify it as a data cell within a table row depending on the technique identified in the first step:
   * For HTML `<table>`: `<td>` for the cell, which must be within a `<tr>` row. 
   * For ARIA `role="table"`: ARIA `role="cell"`, which must be within an ARIA `role="row"`
3. Header cells and data cell association: Identify all column and row headers for each data cell. Check that all data cells are programmatically associated with relevant headers using one of the following techniques:
    * For a simple HTML `<table>`, with all headers in the first row OR column, each header cell can be marked up with `<th>` without additional attributes.
    * For any HTML `<table>`, header cells can be marked up with `<th scope=>` if all data cells that follow the header belong to the header. In HTML4, `<td scope>` is supported. In HTML5, `<td scope>` is not supported so all header cells must be `<th>`. Acceptable values for scope are `col|row|colgroup|rowgroup`. The scope only applies to cells that occur after the header cell(s) in the reading order.
    * For any HTML `<table>`, each header cell (`<th>` or `<td>`) can be marked up with a unique id attribute AND associated to its data cells by including the ID value in the `<td headers=>` attribute. 
        * Data cells must refer to the id(s) of all relevant header cells via the headers attribute in order for the row and column headers to be properly associated.
        * The order of the IDs referenced in the headers attribute are consistent and in a meaningful sequence.
    * For any HTML `<table>` that uses BOTH `<th scope=>` AND refers to header IDs using `<td headers=>` attributes in the same table, any data cell with a `headers=` reference will override any scope= attributes for associated table headers for that particular data cell. Therefore, data cells with a `headers=` reference, must identify all relevant headers, independent from and regardless of scope= attributes in associated headers.
    * For ARIA `role="table"`: each column header must have `role=”columnheader”` and each row header must have `role="rowheader"`. 

#### Layout Tables
1. Check that tables used purely for layout purposes:
    1. Do NOT designate the layout as a table using ARIA `role="table"` and associated ARIA table attributes. 
    1. Do NOT include table structure and relationship elements and/or associated attributes (i.e., `<th>`, `summary=` (HTML4), `<caption>`, `scope=`, and/or `headers=`).

### Test Results
If any of the above tests fail, SC 1.3.1 and Baseline Requirement 12 fail.

## Advisory
Content that is presented with a CSS table appearance, but does not rely on header association, can most easily be identified by linearization. Another helpful indicator is the table only has row headers or column headers but not both.

### WCAG 2.0 Techniques
The following sufficient techniques  were considered when developing this test procedure for this baseline requirement:
* [H43: Using id and headers attributes to associate data cells with header cells in data tables](https://www.w3.org/TR/WCAG20-TECHS/H43.html)
* [H51: Using table markup to present tabular information](https://www.w3.org/TR/WCAG20-TECHS/H51.html)
* [H63: Using the scope attribute to associate header cells and data cells in data tables](https://www.w3.org/TR/WCAG20-TECHS/H63.html)
* [F49: Failure of Success Criterion 1.3.2 due to using an HTML layout table that does not make sense when linearized](https://www.w3.org/TR/WCAG20-TECHS/F49.html)
* [F46: Failure of Success Criterion 1.3.1 due to using th elements, caption elements, or non-empty summary attributes in layout tables](http://www.w3.org/TR/WCAG20-TECHS/F46.html)

----------------------------------------
[Home/Table of Contents](index.md) | [Previous Baseline](11PageTitles.md) | [Next Baseline](13Headings.md)