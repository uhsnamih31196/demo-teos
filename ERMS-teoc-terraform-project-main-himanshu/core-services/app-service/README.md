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
| [azurerm_app_service.app](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/app_service) | resource |
| [azurerm_app_service_source_control.sourcecontroldeployment](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/app_service_source_control) | resource |
| [azurerm_application_insights.appInsights](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/application_insights) | data source |
| [azurerm_resource_group.rg](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/resource_group) | data source |
| [azurerm_service_plan.dataServicePlan](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/service_plan) | data source |
| [azurerm_user_assigned_identity.userAssignedIdentityProvision](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/user_assigned_identity) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_appService"></a> [appService](#input\_appService) | appService | <pre>map(<br>    object(<br>      {<br>        rg_name           = string<br>        service_plan_name = string<br>        service_plan_rg   = string<br>        web_appName       = string<br>        SKU               = string<br>        site_config = map(object({<br>          always_on     = optional(bool)<br>          ftps_state    = optional(bool)<br>          http2_enabled = optional(bool)<br>          application_stack = map(object({<br>            current_stack  = string<br>            dotnet_version = string<br>          }))<br>        }))<br>      }<br>    )<br>  )</pre> | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_App_Name"></a> [App\_Name](#output\_App\_Name) | The name of the App service plan |
