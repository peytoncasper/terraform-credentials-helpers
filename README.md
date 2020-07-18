# Vault

1. Enabled KV Engine at terraform/

```
vault secrets enable -path="terraform" kv
```

2. Add TF API Token to Vault

```
vault kv put terraform/token token=TF_API_TOKEN
```

3. Add Vault Credentials Helper to plugins directory

```
cp terraform-credentials-vault ~/.terraform.d/plugins/
```

4. Setup Credentials Helper Block in .terraformrc

```
credentials_helper "vault" {
  args = []
}
```

# Azure KeyVault

1. Create Resource Group

```
az group create -l westus -n terraform-resource-group
```

2. Create Azure KeyVault

```
az keyvault create --location westus2 --name terraformkeyvault145 --resource-group terraform-resource-group
```

3. Add TF Token to KeyVault

```
az keyvault secret set --vault-name terraformkeyvault145 --name token --value TF_API_TOKEN
```

4. Add KeyVault Credentials Helper to plugins directory

```
cp terraform-credentials-keyvault ~/.terraform.d/plugins/
```

5. Setup Credentials Helper Block in .terraformrc

```
credentials_helper "keyvault" {
  args = ["KEY_VAULT_NAME"]
}
```