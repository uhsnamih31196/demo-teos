## Requirements

No requirements.

## Providers

| Name | Version |
|------|---------|
| <a name="provider_azurerm"></a> [azurerm](#provider\_azurerm) | n/a |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [azurerm_application_insights.appInsights](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/application_insights) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_appInsights"></a> [appInsights](#input\_appInsights) | App Insights | <pre>map(<br>    object(<br>      {<br>        Name            = string,<br>        ResourceGroup   = string,<br>        Location        = string,<br>        ApplicationType = string<br>      }<br>    )<br>  )</pre> | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_App_insights_connection_string"></a> [App\_insights\_connection\_string](#output\_App\_insights\_connection\_string) | The instrumentation key of the Application Insights |
| <a name="output_App_insights_instrumentation_key"></a> [App\_insights\_instrumentation\_key](#output\_App\_insights\_instrumentation\_key) | The instrumentation key of the Application Insights |
