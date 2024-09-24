# Azure Virtual Network with Subnets

This repository contains Terraform code to create an Azure Virtual Network (VNet) with three subnets.

## Prerequisites
- [Terraform](https://www.terraform.io/downloads.html) installed on your machine
- An Azure account with the necessary permissions to create resources

## Getting Started

1. **Clone the repository**:
   ```
   git clone https://github.com/your-username/azure-vnet-with-subnets.git
   ```

2. **Navigate to the project directory**:
   ```
   cd azure-vnet-with-subnets
   ```

3. **Create the `main.tf` file**:
   ```
   touch main.tf
   ```

4. **Add the Terraform code to the `main.tf` file**:
   ```hcl
   # Define resource group
   resource "azurerm_resource_group" "vnet" {
     name     = "myVnet-RG"
     location = "West Europe"
   }

   # Define virtual network
   resource "azurerm_virtual_network" "vnet" {
     name                = "myVNet"
     address_space       = ["192.168.0.0/16"]
     location            = azurerm_resource_group.vnet.location
     resource_group_name = azurerm_resource_group.vnet.name
   }

   # Define subnet 1
   resource "azurerm_subnet" "subnet1" {
     name                 = "mySubnet1"
     resource_group_name  = azurerm_resource_group.vnet.name
     virtual_network_name = azurerm_virtual_network.vnet.name
     address_prefixes     = ["192.168.10.0/24"]
   }

   # Define subnet 2
   resource "azurerm_subnet" "subnet2" {
     name                 = "mySubnet2"
     resource_group_name  = azurerm_resource_group.vnet.name
     virtual_network_name = azurerm_virtual_network.vnet.name
     address_prefixes     = ["192.168.20.0/24"]
   }

   # Define subnet 3
   resource "azurerm_subnet" "subnet3" {
     name                 = "mySubnet3"
     resource_group_name  = azurerm_resource_group.vnet.name
     virtual_network_name = azurerm_virtual_network.vnet.name
     address_prefixes     = ["192.168.30.0/24"]
   }
   ```

5. **Initialize Terraform**:
   ```
   terraform init
   ```

6. **Plan the deployment**:
   ```
   terraform plan
   ```

7. **Apply the changes**:
   ```
   terraform apply
   ```

   This will create the Azure Virtual Network with the three subnets in the "myVnet-RG" resource group.

8. **Verify the deployment**:
   - Go to the Azure portal and navigate to the "myVnet-RG" resource group.
   - Verify that the "myVNet" virtual network and the three subnets ("mySubnet1", "mySubnet2", and "mySubnet3") have been created.

## Cleanup

To remove the resources created by this Terraform configuration, run:

```
terraform destroy
```

## Contributing

If you find any issues or have suggestions for improvements, please feel free to open an issue or submit a pull request.

## License

This project is licensed under the [MIT License](LICENSE).
