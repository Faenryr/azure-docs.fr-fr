---
title: Download Azure Stack tools from GitHub | Microsoft Docs
description: Learn how to download tools required to work with Azure Stack.
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.translationtype: HT
ms.sourcegitcommit: 1c730c65194e169121e3ad1d1423963ee3ced8da
ms.openlocfilehash: e8e4c7381e0bd9c036c6601fd0df9dba2a46391a
ms.contentlocale: fr-fr
ms.lasthandoff: 08/30/2017

---

# <a name="download-azure-stack-tools-from-github"></a>Download Azure Stack tools from GitHub

AzureStack-Tools is a GitHub repository that hosts PowerShell modules that you can use to manage and deploy resources to Azure Stack. You can download and use these PowerShell modules to the Azure Stack Development Kit, or to a windows-based external client if you are planning to establish VPN connectivity. To obtain these tools, clone the GitHub repository or download the AzureStack-Tools folder. 

To clone the repository, download [Git](https://git-scm.com/download/win) for Windows, open a Command Prompt window and run the following script:

```PowerShell
# Change directory to the root directory 
cd \

# clone the repository
git clone https://github.com/Azure/AzureStack-Tools.git --recursive

# Change to the tools directory
cd AzureStack-Tools
```

To download the tools folder, run the following script:

```PowerShell
# Change directory to the root directory 
cd \

# Download the tools archive
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

# Expand the downloaded files
expand-archive master.zip `
  -DestinationPath . `
  -Force

# Change to the tools directory
cd AzureStack-Tools-master

```

## <a name="functionalities-provided-by-the-modules"></a>Functionalities provided by the modules

The AzureStack-Tools repository contains PowerShell modules that support the following functionalities for Azure Stack:  

| Functionality | Description | who can use this module? |
| --- | --- | --- |
| [Cloud capabilities](azure-stack-validate-templates.md) | Use this module to get the cloud capabilities of a cloud. For example, you can get the cloud capabilities such as API version, Azure Resource Manager resources, VM extensions etc. for Azure Stack and Azure clouds using this module. | Azure Stack operators and users. |
| [Azure Stack compute administration](azure-stack-add-vm-image.md) | Use this module to add or remove a VM image from the Azure Stack marketplace. | Azure Stack operators. |
| [Azure Stack Infrastructure administration](https://github.com/Azure/AzureStack-Tools/blob/master/Infrastructure/README.md) | Use this module to manage Azure Stack infrastructure VMs, alerts, updates etc. |  Azure Stack operators.|
| [Resource Manager policy for Azure Stack](azure-stack-policy-module.md) | Use this module to configure an Azure subscription or an Azure resource group with the same versioning and service availability as Azure Stack. | Azure Stack operators and users. |
| [Register with Azure](azure-stack-register.md) | Use this module to register your development kit instance with Azure. After registering, you can download the marketplace items from Azure and use them in Azure Stack. | Azure Stack operators. |
| [Azure Stack deployment](azure-stack-run-powershell-script.md) | Use this module to prepare the Azure Stack host computer to deploy and redeploy by using the Azure Stack Virtual Hard Disk(VHD) image. | Azure Stack operators. |
| [Connecting to Azure Stack](azure-stack-connect-powershell.md) | Use this module to connect to an Azure Stack instance through PowerShell and to configure VPN connectivity to Azure Stack. |Azure Stack operators and users. |
| [Azure Stack service administration](azure-stack-create-offer.md) | Azure Stack operators can use this module to create a default tenant offer with unlimited quota across Compute, Storage, Network, and Key Vault services.   | Azure Stack operators.|
| [Template validator](azure-stack-validate-templates.md) | Use this module to verify if an existing or a new template can be deployed to Azure Stack. | Azure Stack operators and users. |


## <a name="next-steps"></a>Next steps
* [Configure the Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md)   
* [Connect to Azure Stack Development Kit over a VPN](azure-stack-connect-azure-stack.md)  

