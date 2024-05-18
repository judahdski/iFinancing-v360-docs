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
    TItem=""
    LoadData=""
    AllowSelected=""></DataGrid>


-   DataGridColumn

/**
Attributes:
    TextAlign=[TextAlign.Center | TextAlign.Right | TextAlign.Left]
*/

<DataGridColumn
    TItem=""
    Property=""
    Title=""
    Width=""
    Link=""
    TextAlign=""
    FormatString="" />
```

---

<br>

## Form (HTML)

```razor
<RadzenTemplateForm>
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
</RadzenTemplateForm>
```

```razor
- RadzenTemplateForm

<RadzenTemplateForm
    TItem=""
    Data=""
    Submit=""></RadzenTemplateForm>


- FormFieldTextBox

<FormFieldTextBox
    Label=""
    Name=""
    @bind-Value=""
    Max=""
    Required=""
    Disabled="" />


-   FormFieldTextArea

<FormFieldTextArea
    Label=""
    Name=""
    @bind-Value=""
    Max=""
    Required=""
    Disabled="" />


-   FormFieldSwitch

<FormFieldSwitch
    Label=""
    Name=""
    @bind-Value=""
    Disabled />


-   FormFieldNumeric

<FormFieldNumeric
    Label=""
    Name=""
    @bind-Value=""
    Min=""
    Required="" />


-   FormFieldDropdown

<FormFieldDropdown
    Label=""
    Name=""
    @bind-Value=""
    Items=""
    Required="" />


-   FormFieldRadioButton

<FormFieldDropdown
    Label=""
    Name=""
    @bind-Value=""
    Items=""
    Required="" />


-   FormFieldDatePicker

<FormFieldDatePicker
    Label=""
    Name=""
    @bind-Value=""
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
    @bind-Value=""
    @bind-Text=""
    Target=""
    Required="true" />

<SingleSelectLookup
    ID=""
    @ref=""
    TItem=""
    LoadData=""
    Title=""
    Select="(select) => {
        row.GradeId = select.ID;
        row.GradeDescription = select.Description;
    }">
  <DataGridColumn TItem="" Property="" Title="" />
</SingleSelectLookup>


- Multiple Select Lookup

<RadzenButton
    ButtonStyle=""
    Text=""
    Click=@(() => { lookupRef.Open(); }) />

<MultipleSelectLookup
    ID=""
    @ref=""
    TItem=""
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
        TItem=""
        Property=""
        Title="" />
  </ColumnsTemplate>
</MultipleSelectLookup>
```
