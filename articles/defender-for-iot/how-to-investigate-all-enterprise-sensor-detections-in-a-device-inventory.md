---
title: Más información acerca de los dispositivos detectados por todos los sensores de la empresa
description: Use el inventario de dispositivos de la consola de administración local para obtener una vista completa con la información de dispositivo de los sensores conectados. Use las herramientas de importación, exportación y filtrado para administrar esta información.
author: shhazam-ms
manager: rkarlin
ms.author: shhazam
ms.date: 12/02/2020
ms.topic: how-to
ms.service: azure
ms.openlocfilehash: 9da5c8c89ee124e527584164b21b096ac815e5ca
ms.sourcegitcommit: a0c1d0d0906585f5fdb2aaabe6f202acf2e22cfc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/21/2021
ms.locfileid: "98625471"
---
# <a name="investigate-all-enterprise-sensor-detections-in-the-device-inventory"></a>Análisis de las detecciones de todos los sensores de la empresa del inventario de dispositivos

La información sobre los dispositivos procedente de los sensores conectados se puede ver desde la consola de administración local en el *inventario de dispositivos*. Esta característica ofrece una vista completa de toda la información de la red. Use las herramientas de importación, exportación y filtrado para administrar esta información. También aparece la información de estado acerca de las versiones de los sensores conectados.

:::image type="content" source="media/how-to-work-with-asset-inventory-information/device-inventory-data-table.png" alt-text="Captura de pantalla de la tabla de datos del inventario de dispositivos.":::

En la tabla siguiente se describen las columnas de la tabla del inventario de dispositivos.

| Parámetro | Descripción |
|--|--|
| **Alertas no confirmadas** | Número de alertas no controladas asociadas a este dispositivo. |
| **Unidad de negocio** | Unidad de negocio que contiene este dispositivo. |
| **Región** | Región que contiene este dispositivo. |
| **Sitio** | Sitio que contiene este dispositivo. |
| **Zona** | Zona que contiene este dispositivo. |
| **Dispositivo** | Sensor de Azure Defender para IoT que protege este dispositivo. |
| **Nombre** | Nombre de este dispositivo tal y como Defender para IoT lo ha detectado. |
| **Type** | Tipo de dispositivo, como PLC o HMI. |
| **Proveedor** | Nombre del proveedor del dispositivo, tal y como se define en la dirección MAC. |
| **Sistema operativo** | Sistema operativo del dispositivo. |
| **Firmware** | Firmware del dispositivo. |
| **Dirección IP** | Dirección IP del dispositivo. |
| **VLAN** | VLAN del dispositivo. |
| **Dirección MAC** | La dirección MAC del dispositivo. |
| **Protocolos** | Protocolos que usa el dispositivo. |
| **Alertas no confirmadas** | Número de alertas no controladas asociadas a este dispositivo. |
| **Estado de autorización** | Estado de autorización del dispositivo:<br />- **True**: El dispositivo se ha autorizado.<br />- **False**: El dispositivo no se ha autorizado. |
| **Conocido como escáner** | Indica si este dispositivo realiza actividades de análisis en la red. |
| **Dispositivo de programación** | Indica si se trata de un dispositivo de programación:<br />- **True**: El dispositivo realiza actividades de programación para PLC, RTU y controladores, que son pertinentes para las estaciones de ingeniería.<br />- **False**: El dispositivo no es un dispositivo de programación. |
| **Grupos** | Grupos en los que participa este dispositivo. |
| **Última actividad** | Última actividad realizada por el dispositivo. |
| **Discovered** | Cuándo apareció por primera vez en la red este dispositivo. |

## <a name="integrate-data-into-the-enterprise-device-inventory"></a>Integración de datos en el inventario de dispositivos de la empresa

Las funcionalidades de integración de datos le permiten mejorar los datos del inventario de dispositivos con información de otros recursos de la empresa. Entre estos recursos se incluyen CMDB, DNS, firewalls y API web.

Puede utilizar esta información para aprender. Por ejemplo:

- Fechas de compra del dispositivo y fechas de final de garantía

- Usuarios responsables de cada dispositivo

- Incidencias abiertas de los dispositivos

- Última fecha en que se actualizó el firmware

- Dispositivos con acceso permitido a Internet

- Dispositivos que ejecutan aplicaciones antivirus activas

- Usuarios que iniciaron sesión en los dispositivos

:::image type="content" source="media/how-to-work-with-asset-inventory-information/asset-inventory-screen-with-items-highlighted-v2.png" alt-text="Tabla de datos en la pantalla de inventario de dispositivos.":::

Puede integrar los datos de cualquiera de estas dos maneras:

- Agregándolos manualmente

- Ejecutando los scripts personalizados que ofrece Defender para IoT

:::image type="content" source="media/how-to-work-with-asset-inventory-information/enterprise-data-integrator-graph.png" alt-text="Diagrama del integrador de datos de la empresa.":::

Puede colaborar con el soporte técnico de Defender para IoT para configurar el sistema de forma que reciba consultas de la API web.

Para agregar datos manualmente:

1. En el menú lateral, seleccione **Inventario de dispositivos** y, después, seleccione :::image type="icon" source="media/how-to-work-with-asset-inventory-information/menu-icon.png" border="false":::.

   :::image type="content" source="media/how-to-work-with-asset-inventory-information/asset-inventory-settings-v2.png" alt-text="Edite la configuración del inventario del dispositivo.":::

2. En el cuadro de diálogo **Device Inventory Settings** (Configuración de inventario de dispositivos), seleccione **AGREGAR COLUMNA PERSONALIZADA**.

   :::image type="content" source="media/how-to-work-with-asset-inventory-information/add-custom-column.png" alt-text="Agregue una columna personalizada al inventario.":::

3. En el cuadro de diálogo **Agregar columna personalizada**, agregue el nuevo nombre de columna (hasta 250 caracteres UTF), seleccione **Manual** y seleccione **GUARDAR**. El nuevo elemento aparece en el cuadro de diálogo **Device Inventory Settings** (Configuración de inventario de dispositivos).

4. En la esquina superior derecha de la ventana **Inventario de dispositivos**, seleccione :::image type="icon" source="media/how-to-work-with-asset-inventory-information/menu-icon-device-inventory.png" border="false"::: y, después, seleccione **Export All Device Inventory** (Exportar todo el inventario de dispositivos). Se genera el archivo CSV.

   :::image type="content" source="media/how-to-work-with-asset-inventory-information/sample-exported-csv-file.png" alt-text="El archivo CSV exportado.":::

5. Agregue manualmente la información a la nueva columna y guarde el archivo.

6. En la esquina superior derecha de la ventana **Inventario de dispositivos**, seleccione :::image type="icon" source="media/how-to-work-with-asset-inventory-information/menu-icon-device-inventory.png" border="false"::: y, luego, seleccione **Import Manual Input Columns** (Importar manualmente columnas de entrada) y busque el archivo CSV. Los nuevos datos aparecerán en la tabla **Inventario de dispositivos**.

Para integrar datos de otras entidades empresariales:

1. En la esquina superior derecha de la ventana **Inventario de dispositivos**, seleccione :::image type="icon" source="media/how-to-work-with-asset-inventory-information/menu-icon-device-inventory.png" border="false"::: y, después, seleccione **Export All Device Inventory** (Exportar todo el inventario de dispositivos).

2. En el cuadro de diálogo **Device Inventory Settings** (Configuración de inventario de dispositivos), seleccione **AGREGAR COLUMNA PERSONALIZADA**.

   :::image type="content" source="media/how-to-work-with-asset-inventory-information/add-custom-column.png" alt-text="Agregue una columna personalizada al inventario.":::

3. En el cuadro de diálogo **Agregar columna personalizada**, agregue el nuevo nombre de columna (hasta 250 caracteres UTF) y seleccione **Automático**. Aparecerán las opciones **UPLOAD SCRIPT** (CARGAR SCRIPT) y **TEST SCRIPT** (PROBAR SCRIPT).

   :::image type="content" source="media/how-to-work-with-asset-inventory-information/add-custom-column-automatic.png" alt-text="Agregar automáticamente columnas personalizadas.":::

4. Cargue y pruebe el script que recibió de [Soporte técnico de Microsoft](https://support.serviceshub.microsoft.com/supportforbusiness/create?sapId=82c88f35-1b8e-f274-ec11-c6efdd6dd099).

## <a name="retrieve-information-from-the-device-inventory"></a>Recuperación de información del inventario de dispositivos

Puede recuperar una amplia gama de la información sobre los dispositivos que detectan los sensores administrados e integrar esa información con los sistemas asociados. Por ejemplo, puede recuperar el sensor, la zona, el identificador de sitio, la dirección IP, la dirección MAC, el firmware, el protocolo y la información del proveedor. Filtre la información que ha recuperado según:

- Los dispositivos autorizados y no autorizados.

- Los dispositivos asociados con sitios específicos.

- Los dispositivos asociados con zonas específicas.

- Los dispositivos asociados con sensores específicos.

Usa los comandos de la API de Defender para IoT para recuperar e integrar esta información. Para más información, consulte [API del sensor y la consola de administración de Defender para IoT](references-work-with-defender-for-iot-apis.md).

## <a name="filter-the-device-inventory"></a>Filtrado del inventario de dispositivos

Puede filtrar el inventario de dispositivos para mostrar las columnas de interés. Por ejemplo, puede ver la información del dispositivo PLC.

:::image type="content" source="media/how-to-work-with-asset-inventory-information/asset-inventory-view-v2.png" alt-text="Captura de pantalla del inventario de dispositivos.":::

El filtro se borra al salir de la ventana.

Para usar el mismo filtro varias veces, puede guardar el filtro o combinación de filtros que necesite. Puede abrir el panel izquierdo y ver los filtros que ha guardado:

:::image type="content" source="media/how-to-work-with-asset-inventory-information/view-your-asset-inventories-v2.png" alt-text="Pantalla de inventario de dispositivos.":::

Para filtrar el inventario de dispositivos:

1. Seleccione :::image type="icon" source="media/how-to-work-with-asset-inventory-information/filter-a-column-icon.png" border="false"::: en la columna que desea filtrar.

2. En el cuadro de diálogo **Filtro**, seleccione el tipo de filtro:

   - **Equals** (es igual a): Valor exacto según el cual se desea filtrar la columna. Por ejemplo, si filtra la columna de protocolo según **Equals** y `value=ICMP`, la columna presentará los dispositivos que solo usen el protocolo ICMP.

   - **Contains** (contiene): Valor que se encuentra entre otros valores de la columna. Por ejemplo, si filtra la columna de protocolo según **Contains** y `value=ICMP`, la columna presentará los dispositivos que solo usen el protocolo ICMP como parte de la lista de protocolos que usa el dispositivo.

3. Para organizar la información de la columna por orden alfabético, seleccione :::image type="icon" source="media/how-to-work-with-asset-inventory-information/alphabetical-order-icon.png" border="false":::. Modifique el orden seleccionando las flechas :::image type="icon" source="media/how-to-work-with-asset-inventory-information/alphabetical-a-z-order-icon.png" border="false"::: y :::image type="icon" source="media/how-to-work-with-asset-inventory-information/alphabetical-z-a-order-icon.png" border="false":::.

4. Para guardar un filtro nuevo, defina el filtro y seleccione **Guardar como**.

5. Para cambiar las definiciones de filtro, cambie las definiciones y seleccione **Guardar cambios**.

## <a name="view-device-information-per-zone"></a>Visualización de la información de dispositivos por zona

Puede obtener la siguiente información acerca de los dispositivos de una zona.

### <a name="view-a-device-map"></a>Visualización de un mapa de dispositivos

Para ver un mapa de los dispositivos de sensores de una zona seleccionada:

- En la ventana **Administración de sitio**, seleccione **View Zone Map** (Ver mapa de zonas) en la barra que contiene el nombre de la zona.

  :::image type="content" source="media/how-to-work-with-asset-inventory-information/default-region-to-default-business-unit-v2.png" alt-text="Región predeterminada a unidad de negocio predeterminada.":::

Aparece la ventana **Mapa del dispositivo**. Muestra todos los elementos de red relacionados con la zona seleccionada, incluidos los sensores, los dispositivos conectados a ellos, etc.

:::image type="content" source="media/how-to-work-with-asset-inventory-information/zone-map-screenshot.png" alt-text="Captura de pantalla del mapa de la zona.":::

Las siguientes herramientas están disponibles para ver los dispositivos y la información del dispositivo desde el mapa. Para más información sobre cada una de estas características, consulte la *guía del usuario de la plataforma Defender para IoT*.

- **Vistas de zoom del mapa**: vista simplificada, vista de conexiones y vista detallada. La vista del mapa que se muestra varía en función del nivel de zoom del mapa. Puede cambiar entre las vistas del mapa ajustando los niveles de zoom.

  :::image type="icon" source="media/how-to-work-with-asset-inventory-information/zoom-icon.png" border="false":::

- **Herramientas de diseño y búsqueda del mapa**: herramientas que se usan para mostrar diversos segmentos de red, dispositivos, grupos de dispositivos o capas.

  :::image type="content" source="media/how-to-work-with-asset-inventory-information/search-and-layout-tools.png" alt-text="Captura de pantalla de la vista de herramientas de diseño y búsqueda.":::

- **Etiquetas e indicadores en dispositivos:** por ejemplo, el número de dispositivos agrupados en una subred de una red de TI. En este ejemplo, es 8.

  :::image type="content" source="media/how-to-work-with-asset-inventory-information/labels-and-indicators.png" alt-text="Captura de pantalla de etiquetas e indicadores.":::

- **Visualización de las propiedades del dispositivo**: por ejemplo, el sensor que supervisa el dispositivo y las propiedades básicas de este. Haga clic con el botón derecho en el dispositivo para ver las propiedades del dispositivo.

  :::image type="content" source="media/how-to-work-with-asset-inventory-information/asset-properties-v2.png" alt-text="Captura de pantalla de la vista de propiedades del dispositivo.":::

- **Alertas asociadas con un dispositivo:** haga clic con el botón derecho en el dispositivo para ver las alertas relacionadas.

  :::image type="content" source="media/how-to-work-with-asset-inventory-information/show-alerts.png" alt-text="Captura de pantalla de la ventana Mostrar alertas.":::

### <a name="view-alerts-associated-with-a-zone"></a>Visualización de las alertas asociadas con una zona

Para ver las alertas asociadas con una zona específica:

- Seleccione el icono de alerta de la ventana **Zona**. 

  :::image type="content" source="media/how-to-work-with-asset-inventory-information/business-unit-view-v2.png" alt-text="Vista de la unidad de negocio predeterminada con ejemplos.":::

Para más información, consulte [Introducción a la continuidad Uso de alertas](how-to-work-with-alerts-on-premises-management-console.md).

### <a name="view-the-device-inventory-of-a-zone"></a>Visualización del inventario de dispositivos de una zona

Para ver el inventario de dispositivos asociado a una zona específica:

- Seleccione **View Device Inventory** (Ver inventario de dispositivos) en la ventana **Zona**.

  :::image type="content" source="media/how-to-work-with-asset-inventory-information/default-business-unit.png" alt-text="Aparecerá la pantalla de inventario de dispositivos.":::

Para más información, consulte [Investigación de todas las detecciones de los sensores de empresa en un inventario de dispositivos](how-to-investigate-all-enterprise-sensor-detections-in-a-device-inventory.md).

### <a name="view-additional-zone-information"></a>Visualización de información adicional de la zona

La siguiente información adicional de la zona está disponible:

- **Detalles de la zona**: vea el número de dispositivos, alertas y sensores asociados a la zona.

- **Detalles del sensor**: vea el nombre, la dirección IP y la versión de cada uno de los sensores asignados a la zona.

- **Estado de conectividad:** si un sensor está desconectado, conéctelo desde el sensor. Consulte [Conexión de los sensores a una consola de administración local](how-to-activate-and-set-up-your-on-premises-management-console.md#connect-sensors-to-the-on-premises-management-console). 

- **Progreso de la actualización**: si el sensor conectado se está actualizando, se mostrarán los estados de actualización. Durante la actualización, la consola de administración local no recibe del sensor la información del dispositivo.

## <a name="see-also"></a>Consulte también

[Investigación de las detecciones de sensores en un inventario de dispositivos](how-to-investigate-sensor-detections-in-a-device-inventory.md)
