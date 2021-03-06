---
title: Ejemplos de plantillas de Resource Manager para las reglas de recopilación de datos
description: Ejemplos de plantillas de Azure Resource Manager para crear asociaciones entre las reglas de recopilación de datos y las máquinas virtuales en Azure Monitor.
ms.subservice: logs
ms.topic: sample
author: bwren
ms.author: bwren
ms.date: 11/17/2020
ms.openlocfilehash: bff13c24e0b5818b352e76df1d8ecd8251a5f12c
ms.sourcegitcommit: eb546f78c31dfa65937b3a1be134fb5f153447d6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2021
ms.locfileid: "99430232"
---
# <a name="resource-manager-template-samples-for-data-collection-rules-in-azure-monitor"></a>Ejemplos de plantillas de Azure Resource Manager para reglas de recopilación de datos en Azure Monitor
Este artículo incluye [plantillas de Azure Resource Manager](../../azure-resource-manager/templates/template-syntax.md) de ejemplo para implementar y configurar la [extensión de diagnóstico](../platform/diagnostics-extension-overview.md) y el [agente de Log Analytics](../platform/log-analytics-agent.md) para máquinas virtuales en Azure Monitor. Cada ejemplo incluye un archivo de plantilla y un archivo de parámetros con valores de ejemplo para la plantilla.

[!INCLUDE [azure-monitor-samples](../../../includes/azure-monitor-resource-manager-samples.md)]


## <a name="create-association-with-azure-vm"></a>Creación de una asociación con una máquina virtual de Azure

En el siguiente ejemplo se crea una asociación entre una máquina virtual de Azure y una regla de recopilación de datos.

### <a name="template-file"></a>Archivo de plantilla

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "vmName": {
            "type": "string",
            "metadata": {
                "description": "Name of the virtual machine."
            }
        },
        "associationName": {
            "type": "string",
            "metadata": {
                "description": "Name of the association."
            }
        },
        "dataCollectionRuleId": {
            "type": "string",
            "metadata": {
                "description": "Resource ID of the data collection rule."
            }
        }
    },
    "resources": [
        {
            "type": "Microsoft.Compute/virtualMachines/providers/dataCollectionRuleAssociations",
            "name": "[concat(parameters('vmName'),'/microsoft.insights/', parameters('associationName'))]",
            "apiVersion": "2019-11-01-preview",
            "properties": {
                "description": "Association of data collection rule. Deleting this association will break the data collection for this virtual machine.",
                "dataCollectionRuleId": "[parameters('dataCollectionRuleId')]"
            }
        }
    ]
}
```

### <a name="parameter-file"></a>Archivo de parámetros

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "vmName": {
        "value": "my-windows-vm"
      },
      "location": {
        "value": "eastus"
      }
  }
}
```

## <a name="create-association-with-azure-arc"></a>Creación de una asociación con Azure Arc

En el ejemplo siguiente, se instala el agente de Azure Monitor en una máquina virtual de Microsoft Azure. Se crea una asociación entre una máquina de servidor habilitada para Azure Arc y una regla de recopilación de datos.

### <a name="template-file"></a>Archivo de plantilla

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "vmName": {
            "type": "string",
            "metadata": {
                "description": "Name of the virtual machine."
            }
        },
        "associationName": {
            "type": "string",
            "metadata": {
                "description": "Name of the association."
            }
        },
        "dataCollectionRuleId": {
            "type": "string",
            "metadata": {
                "description": "Resource ID of the data collection rule."
            }
        }
    },
    "resources": [
        {
            "type": "Microsoft.HybridCompute/machines/providers/dataCollectionRuleAssociations",
            "name": "[concat(parameters('machineName'),'/microsoft.insights/', parameters('associationName'))]",
            "apiVersion": "2019-11-01-preview",
            "properties": {
                "description": "Association of data collection rule. Deleting this association will break the data collection for this Arc server.",
                "dataCollectionRuleId": "[parameters('dataCollectionRuleId')]"
            }
        }
    ]
}
```

### <a name="parameter-file"></a>Archivo de parámetros

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "vmName": {
        "value": "my-windows-vm"
      },
      "location": {
        "value": "eastus"
      }
  }
}
```


## <a name="next-steps"></a>Pasos siguientes

* [Otras plantillas de ejemplo para Azure Monitor](resource-manager-samples.md).
* [Más información sobre el agente de Log Analytics](../platform/log-analytics-agent.md).
* [Más información sobre la extensión de diagnóstico](../platform/diagnostics-extension-overview.md).
