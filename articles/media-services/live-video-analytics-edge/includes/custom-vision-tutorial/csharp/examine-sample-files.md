---
author: russell-cooks
ms.service: media-services
ms.topic: include
ms.date: 10/05/2020
ms.author: russellcooks
ms.openlocfilehash: 359c5f93516ea6f0561865bd86e4f51dedb4c3a5
ms.sourcegitcommit: 0b9fe9e23dfebf60faa9b451498951b970758103
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2020
ms.locfileid: "94358290"
---
1. En Visual Studio Code, vaya a src/edge. Verá el archivo .env que ha creado junto con algunos archivos de plantilla de implementación.

    La plantilla de implementación hace referencia al manifiesto de implementación del dispositivo perimetral con algunos valores de marcador de posición. El archivo .env contiene los valores de esas variables.
1. A continuación, vaya a la carpeta src/cloud-to-device-console-app. Aquí podrá ver el archivo appsettings.json que creó junto con algunos otros archivos:

    * c2d-console-app.csproj: archivo de proyecto de Visual Studio Code.
    * operations.json: en este archivo se enumeran las distintas operaciones que desea que ejecute el programa.
    * Program.cs: Este código de programa de ejemplo:

        * Carga la configuración de la aplicación.
        * Invoca Live Video Analytics en los métodos directos del módulo IoT Edge para crear la topología, crear una instancia del grafo y activar el grafo.
        * Se pone en pausa para que pueda examinar la salida del grafo en la ventana **TERMINAL** y los eventos enviados a IoT Hub en la ventana **SALIDA**.
        * Desactiva la instancia del grafo, la elimina y elimina la topología de grafos.
