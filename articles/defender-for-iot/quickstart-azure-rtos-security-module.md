---
title: 'Inicio rápido: Configuración y habilitación de un módulo de seguridad para Azure RTOS'
description: Aprenda a incorporar y habilitar el módulo de seguridad para el servicio Azure RTOS en Azure IoT Hub.
services: defender-for-iot
ms.service: defender-for-iot
documentationcenter: na
author: rkarlin
manager: rkarlin
editor: ''
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/24/2020
ms.author: rkarlin
ms.openlocfilehash: 321c8d2b9e58aba943c5bf19adf54d6359c5be96
ms.sourcegitcommit: 9eda79ea41c60d58a4ceab63d424d6866b38b82d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2020
ms.locfileid: "96351783"
---
# <a name="quickstart-security-module-for-azure-rtos-preview"></a>Inicio rápido: Módulo de seguridad para Azure RTOS (versión preliminar)

En este artículo se proporciona una explicación de los requisitos previos al comienzo y se explica cómo habilitar el módulo de seguridad para el servicio Azure RTOS en IoT Hub. Si actualmente no tiene una instancia de IoT Hub, consulte [Creación de una instancia de IoT Hub mediante Azure Portal](../iot-hub/iot-hub-create-through-portal.md) para comenzar.

> [!NOTE]
> Security Module for Azure RTOS solo se admite en centros de IoT de nivel estándar.

## <a name="prerequisites"></a>Requisitos previos 

### <a name="supported-devices"></a>Dispositivos compatibles

- Kit de detección ST STM32F746G
- NXP i.MX RT1060 EVK
- Microchip SAM E54 Xplained Pro EVK

Descargue, compile y ejecute uno de los archivos .zip para la placa y la herramienta específicas (IAR, semi IDE o PC) que prefiera del [recurso Security Module for Azure RTOS de GitHub](https://github.com/azure-rtos/azure-iot-preview/releases).

### <a name="azure-resources"></a>Recursos de Azure

La siguiente fase de introducción es preparar los recursos de Azure. Necesitará un centro de IoT y, preferiblemente, un área de trabajo de Log Analytics. Para el centro de IoT, necesitará la cadena de conexión de IoT Hub para conectarse al dispositivo. 
  
### <a name="iot-hub-connection"></a>Conexión de IoT Hub

Se necesita una conexión de IoT Hub para comenzar. 

1. Abra **IoT Hub** en Azure Portal.
1. Copie la cadena de conexión de IoT en el [archivo de configuración](how-to-azure-rtos-security-module.md).


Las credenciales de conexión se toman de la configuración **HOST_NAME**, **DEVICE_ID** y **DEVICE_SYMMETRIC_KEY** de la aplicación de usuario.

El módulo de seguridad para Azure RTOS usa conexiones de middleware de IoT de Azure basadas en el protocolo **MQTT**.


### <a name="log-analytics-workspace"></a>Área de trabajo de Log Analytics

La ingesta de Log Analytics en IoT Hub está desactivada de forma predeterminada en la solución Defender para IoT. Para habilitarla para trabajar con Security Module for Azure RTOS, haga lo siguiente: 
1. En Azure Portal, vaya a su instancia de IoT Hub.
1. Seleccione **Configuración** en el menú **Seguridad**.
   :::image type="content" source="media/quickstart/azure-rtos-hub-settings.png" alt-text="Opción de recopilación de datos de acceso para Azure RTOS"::: 
1. Seleccione **Recopilación de datos**. 
1. En la opción **Configuración del área de trabajo**, cambie el control de alternancia a **Activado**. 
1. Cree un área de trabajo de Log Analytics o adjunte uno existente. Asegúrese de que la opción **Access to raw security data** (Acceder a los datos de seguridad sin procesar) está seleccionada. 
 :::image type="content" source="media/quickstart/azure-rtos-data-collection-on.png" alt-text="Configuración de Azure RTOS que muestra las opciones de recopilación de datos y de datos de seguridad sin procesar seleccionadas":::
1. Seleccione **Guardar**.
1. Vuelva a la lista de recursos de Azure y confirme que ve el área de trabajo de Log Analytics que ha creado o adjuntado habilitada para el centro de IoT.
    :::image type="content" source="media/quickstart/verify-azure-resource-list.png" alt-text="Comprobación de la lista de recursos de Azure para confirmar la incorporación del área de trabajo de Log Analytics correcta para un centro de IoT"::: 

## <a name="next-steps"></a>Pasos siguientes

Continúe con el siguiente artículo para finalizar la configuración y la personalización de la solución.

> [!div class="nextstepaction"]
> [Configuración de Security Module for Azure RTOS](how-to-azure-rtos-security-module.md)