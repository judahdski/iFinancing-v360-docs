# Radzen Syntax

## General

- RadzenStack <br>

```razor
<RadzenStack></RadzenStack>
```

- RadzenRow <br>

```razor
/**
Attributes:
    Gap="[untuk atur jarak antar child element]"
*/

<RadzenRow Gap="8"></RadzenRow>
```

- RoleAccess <br>

```razor
/**
Attributes:
    Code="[role access code from IFINSYS]"
*/

<RoleAccess Code="RC000041"></RoleAccess>
```

- RadzenButton <br>

```razor
/**
Attributes:
    ButtonType="<ButtonType.Submit>"
    ButtonStyle="<ButtonStyle.Primary | ButtonStyle.Success | ButtonStyle.Warning | ButtonStyle.Info | ButtonStyle.Danger>"
    Text="[text for button labeling button]"
    Click="[click function/method]"
    Disabled="[state condition]"
*/

<RadzenButton
    ButtonType="ButtonType.Submit"
    ButtonStyle="ButtonStyle.Primary"
    Text="Add"
    Click="@Add"
    Disabled="@(Loading.IsLoading)"></RadzenButton>
```

## Data Grid (HTML)

```razor
// Data Grid
<RadzenStack>
	<!-- #region Toolbar -->
	<RadzenRow Gap="8">
		<RadzenButton ButtonStyle="ButtonStyle.Primary" Text="Add" Click="@Add" />
		<RadzenButton ButtonStyle="ButtonStyle.Danger" Text="Delete" Click="@Delete" Disabled="@Loading.IsLoading" />
	</RadzenRow>
	<!-- #endregion -->

	<!-- #region List Data -->
	<DataGrid ID="SysGeneralSubcodeDataGrid" @ref=@dataGrid TItem="SysGeneralSubcodeModel" LoadData="LoadData"
		AllowSelected="true">
		<DataGridColumn TItem="SysGeneralSubcodeModel" Property="Code" Title="Code" Width="20%" TextAlign="TextAlign.Center"
			Link="@(row => $"/systemsetting/generalcode/{GeneralCodeID}/generalsubcode/{row.ID}")" />
		<DataGridColumn TItem="SysGeneralSubcodeModel" Property="Description" Title="Description" Width="50%" />
		<DataGridColumn TItem="SysGeneralSubcodeModel" Property="OrderKey" Title="Order Key" Width="10%"
			TextAlign="TextAlign.Right" />
		<DataGridColumn TItem="SysGeneralSubcodeModel" Property="IsActive" Title="Active" Width="20%"
			TextAlign="TextAlign.Center" FormatString="YN" />
	</DataGrid>
	<!-- #endregion -->
</RadzenStack>
```

- DataGrid <br>

```razor
/**
Attributes:
    ID="[TableName]DataGrid"
    @ref="[referenced variable]"
    TItem="[object untuk cetakan setiap item]"
    LoadData="[load data function/method]"
    AllowSelected="[apakah ada checkbox untuk select data atau tidak]"
*/

<DataGrid
    ID="MasterDashboardDataGrid"
    @ref="@dataGrid"
    TItem="MasterDashboardModel"
    LoadData="LoadData"
    AllowSelected="true"></DataGrid>
```

- DataGridColumn <br>

```razor
/**
Attributes:
    TItem="[object untuk cetakan setiap item]"
    Property="[object model property]"
    Title="[title untuk header]"
    Width="[width of the column]"
    Link="[untuk pengganti button action, seperti link/button ke halaman detail]"
    TextAlign="[ngatur posisi text di dalam kolom]"
    FormatString="[untuk kolom yang valuenya 1/-1]"
*/

<DataGridColumn
    TItem="TableNameModel"
    Property="Code"
    Title="Code"
    Width="20%"
    Link="@(row => $"/systemsetting/generalcode/{row.ID}
    TextAlign="TextAlign.Center"
    FormatString="YN") />
```

## Form (HTML)

```razor
<!-- #region Form -->
<RadzenTemplateForm TItem="SysGeneralSubcodeModel" Data="@row" Submit=@OnSubmit>
	<RadzenStack>
		<!-- #region Toolbar -->
		<RadzenRow Gap="8">
			<RadzenButton ButtonType="ButtonType.Submit" ButtonStyle="ButtonStyle.Primary" Text="Save" Disabled="@(Loading.IsLoading)" />
			@if (ID != null)
			{
				<RadzenButton ButtonStyle=@(row.IsActive == 1 ? ButtonStyle.Danger : ButtonStyle.Success) Text=@(row.IsActive ==
				1 ? "Non Active" : "Active") Click="@ChangeActive" />
			}
			<RadzenButton ButtonStyle="ButtonStyle.Danger" Text="Back" Click="@Back" />
		</RadzenRow>
		<!-- #endregion -->

		<RadzenStack>
			<!-- #region General Code -->
			<RadzenRow>
				<!-- #region Code -->
				<FormFieldTextBox Label="General Code Code" Name="Code" @bind-Value="@rowGeneralCode.Code" Max="50"
					Required="true" Disabled />
				<!-- #endregion -->
				<!-- #region Description -->
				<FormFieldTextBox Label="General Code Description" Name="Description"
					@bind-Value="@rowGeneralCode.Description" Max="50" Required="true" Disabled />
				<!-- #endregion -->
			</RadzenRow>
			<!-- #endregion -->

			<!-- #region Sub Code -->
			<RadzenRow>
				<!-- #region Code -->
				<FormFieldTextBox Label="Code" Name="Code" @bind-Value="@row.Code" Max="50" Required="true" Disabled=@(ID !=
					null) />
				<!-- #endregion -->

				<!-- #region Description -->
				<FormFieldTextArea Label="Description" Name="Description" @bind-Value="@row.Description" Max="4000"
					Required="true" />
				<!-- #endregion -->

				<!-- #region Is Active -->
				<FormFieldSwitch Name="IsActive" Label="Active" @bind-Value="@row.IsActive" Disabled />
				<!-- #endregion -->

				<!-- #region OrderKey -->
				<FormFieldNumeric Label="Order Key" Name="OrderKey" @bind-Value="@row.OrderKey" Min="0" Required="true" />
				<!-- #endregion -->
			</RadzenRow>
			<!-- #endregion -->
		</RadzenStack>
	</RadzenStack>
</RadzenTemplateForm>
<!-- #endregion -->
```

- RadzenTemplateForm <br>

```razor
/**
Attributes:
    TItem="[object untuk cetakan setiap item]"
    Data="[object data untuk formnya]"
    Submit="[on submit function/method]"
*/

<RadzenTemplateForm
    TItem="TableNameModel"
    Data="@row"
    Submit="@OnSubmit"></RadzenTemplateForm>
```

- FormFieldTextBox <br>

```razor
/**
Attributes:
    Label="[form field input label]"
    @bind-Value="[data per masing-masing form fieldnya, seperti property di datagridcolumn]"
*/

<FormFieldTextBox
    Label="Code"
    Name="Code"
    @bind-Value="@row.Code"
    Max="50"
    Required="true"
    Disabled="@(ID != null)" />
```

- FormFieldTextArea <br>

```razor
/**
Attributes:
    Label="[form field input label]"
    @bind-Value="[data per masing-masing form fieldnya, seperti property di datagridcolumn]"
*/

<FormFieldTextArea
    Label="Description"
    Name="Description"
    @bind-Value="@row.Description"
    Max="4000"
    Required="true"
    Disabled="@(ID == null)" />
```

- FormFieldSwitch <br>

```razor
<FormFieldSwitch
    Label="Editable"
    Name="IsEditable"
    @bind-Value="@row.IsEditable"
    Disabled />
```

- FormFieldNumeric <br>

```razor
<FormFieldNumeric
    Label="Order Key"
    Name="OrderKey"
    @bind-Value="@row.OrderKey"
    Min="0"
    Required="true" />
```

## Pages (HTML)

```razor
    // List page
    @page "/systemsetting/generalcode"

    @using IFinancing360_SCR_UI.Components.SysGeneralCodeComponent

    <RoleAccess Code="">
        <Card>
            <Title Text="General Code List" />

            <SysGeneralCodeDataGrid />
        </Card>
    </RoleAccess>

    // Info page
    @page "/systemsetting/generalcode/add"
    @page "/systemsetting/generalcode/{ID}"

    @using IFinancing360_SCR_UI.Components.SysGeneralCodeComponent
    @using IFinancing360_SCR_UI.Components.SysGeneralSubcodeComponent

    <RoleAccess Code="">
        <Card>
            <Title Text="General Code Info" />

            <SysGeneralCodeForm />

            @if (ID != null)
            {
                <SysGeneralSubcodeDataGrid GeneralCodeID=@ID />
            }
        </Card>
    </RoleAccess>

    @code {
        [Parameter] public string? ID { get; set; }
    }
```

- Card <br>

```razor
    <Card></Card>
```

- Title <br>

```razor
/**
Attributes:
    Text="[screen title]"
*/

    <Title Text="General Code List"/>
```

- @page <br>
  Import syntax

```razor
    @page "/path/to/file/{ID}"
```