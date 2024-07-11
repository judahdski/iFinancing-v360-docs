# Radzen Syntax

## General

```razor
-   RadzenStack

<RadzenStack></RadzenStack>


-   RadzenRow

<RadzenRow Gap=""></RadzenRow>


-   RoleAccess

<RoleAccess Code=""></RoleAccess>


-   RadzenButton

/**
Attributes:
    ButtonType=[ButtonType.Submit]
    ButtonStyle=[ButtonStyle.Primary | ButtonStyle.Success | ButtonStyle.Warning | ButtonStyle.Info | ButtonStyle.Danger]
*/

<RadzenButton
    ButtonType=""
    ButtonStyle=""
    Text=""
    Click=""
    Disabled=""></RadzenButton>
```

---

<br>

## Data Grid (HTML)

```razor
<RadzenStack>
	<!-- #region Toolbar -->
	<RadzenRow>
		<RadzenButton />
	</RadzenRow>
	<!-- #endregion -->

	<!-- #region List Data -->
	<DataGrid>
		<DataGridColumn />
		<DataGridColumn />
	</DataGrid>
	<!-- #endregion -->
</RadzenStack>
```

```razor
-   DataGrid

<DataGrid
    ID=""
    @ref=""
    TItem="JsonObject"
    LoadData=""
    AllowSelected=""></DataGrid>


-   DataGridColumn

/**
Attributes:
    TextAlign=[TextAlign.Center | TextAlign.Right | TextAlign.Left]
*/

<DataGridColumn
    TItem="JsonObject"
    Property=""
    Title=""
    Type=""
    Width=""
    Link=""
    TextAlign=""
    FormatString="" />
```

---

<br>

## Form (HTML)

```razor
<TemplateForm>
	<RadzenStack>
		<!-- #region Toolbar -->
		<RadzenRow>
			<RadzenButton />
		</RadzenRow>
		<!-- #endregion -->

		<RadzenStack>
			<!-- #region -->
			<RadzenRow>
				<!-- #region -->
				<FormFieldTextBox />
				<!-- #endregion -->
			</RadzenRow>
			<!-- #endregion -->
		</RadzenStack>
	</RadzenStack>
</TemplateForm>
```

```razor
- TemplateForm

<TemplateForm
    Submit=""></TemplateForm>


- FormFieldTextBox

<FormFieldTextBox
    Label=""
    Name=""
    Value=""
    Max=""
    Required=""
    Disabled="" />


-   FormFieldTextArea

<FormFieldTextArea
    Label=""
    Name=""
    Value=""
    Max=""
    Required=""
    Disabled="" />


-   FormFieldSwitch

<FormFieldSwitch
    Label=""
    Name=""
    Value=""
    Disabled />


-   FormFieldNumeric

<FormFieldNumeric
    Label=""
    Name=""
    Value=""
    Min=""
    Required="" />


-   FormFieldDropdown

<FormFieldDropdown
    Label=""
    Name=""
    Value=""
    Items=""
    Required="" />


-   FormFieldRadioButton

<FormFieldDropdown
    Label=""
    Name=""
    Value=""
    Items=""
    Required="" />


-   FormFieldDatePicker

<FormFieldDatePicker
    Label=""
    Name=""
    Value=""
    Required="" />
```

---

<br>

## Pages (HTML)

```razor
- List page

@page "/systemsetting/generalcode"

@using IFinancing360_SCR_UI.Components.SysGeneralCodeComponent

<RoleAccess>
    <Card>
        <Title />

        <SysGeneralCodeDataGrid />
    </Card>
</RoleAccess>


- Info page

@page "/systemsetting/generalcode/add"
@page "/systemsetting/generalcode/{ID}"

@using IFinancing360_SCR_UI.Components.SysGeneralCodeComponent
@using IFinancing360_SCR_UI.Components.SysGeneralSubcodeComponent

<RoleAccess>
    <Card>
        <Title />

        <SysGeneralCodeForm />

        @if (ID != null)
        {
            <SysGeneralSubcodeDataGrid />
        }
    </Card>
</RoleAccess>

@code {
    [Parameter] public string? ID { get; set; }
}
```

---

<br>

## Lookup

```razor
- Single Select Lookup

<FormFieldButtonLookup
    Label=""
    Name=""
    Value=""
    Text=""
    Target=""
    Required="true" />

<SingleSelectLookup
    ID=""
    @ref=""
    TItem="JsonObject"
    LoadData=""
    Title=""
    Select="(select) => {
        row.GradeId = select.ID;
        row.GradeDescription = select.Description;
    }">
  <DataGridColumn TItem="JsonObject" Property="" Title="" />
</SingleSelectLookup>


- Multiple Select Lookup

<RadzenButton
    ButtonStyle=""
    Text=""
    Click=@(() => { lookupRef.Open(); }) />

<MultipleSelectLookup
    ID=""
    @ref=""
    TItem="JsonObject"
    LoadData=""
    Title="">
  <ToolbarTemplate>
    <RadzenButton
        ButtonStyle=""
        Text=""
        Click="" />
  </ToolbarTemplate>

  <ColumnsTemplate>
    <DataGridColumn
        TItem="JsonObject"
        Property=""
        Title="" />
  </ColumnsTemplate>
</MultipleSelectLookup>
```
