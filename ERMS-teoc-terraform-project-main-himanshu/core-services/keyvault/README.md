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
| [azurerm_key_vault.keyVault](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/key_vault) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_keyVault"></a> [keyVault](#input\_keyVault) | Key Vault | <pre>map(<br>    object(<br>      {<br>        Name                   = string,<br>        ResourceGroup          = string,<br>        Location               = string,<br>        Tenant                 = string,<br>        SoftDeleteRetention    = number,<br>        DiskEncryptionEnabled  = bool,<br>        PurgeProtectionEnabled = bool,<br>        SKU                    = string<br>      }<br>    )<br>  )</pre> | n/a | yes |

## Outputs

No outputs.
