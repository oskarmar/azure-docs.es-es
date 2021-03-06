---
title: Puntuación de seguridad de Azure Security Center
description: Descripción de Puntuación de seguridad de Azure Security Center y sus controles de seguridad
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.assetd: c42d02e4-201d-4a95-8527-253af903a5c6
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2021
ms.author: memildin
ms.openlocfilehash: 24822777b06fadf87ca446d9b7ff8ba4df34adc5
ms.sourcegitcommit: 49ea056bbb5957b5443f035d28c1d8f84f5a407b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2021
ms.locfileid: "100007688"
---
# <a name="secure-score-in-azure-security-center"></a>Puntuación de seguridad de Azure Security Center

## <a name="introduction-to-secure-score"></a>Introducción a Puntuación de seguridad

Azure Security Center tiene dos objetivos principales: 

- ayudarle a entender su situación de seguridad actual
- ayudarle a mejorar la seguridad de forma eficaz

La característica principal de Security Center que le ayuda a conseguir estos objetivos es la **puntuación de seguridad**.

Security Center evalúa continuamente los recursos, suscripciones y la organización en busca de problemas de seguridad. A continuación, agrega todos los resultados a una sola puntuación para que pueda conocer de un vistazo la situación de la seguridad actual: cuanto mayor sea la puntuación, menor será el nivel de riesgo identificado.

La puntuación de seguridad se muestra en las páginas de Azure Portal como un valor de porcentaje, pero los valores subyacentes también se presentan claramente:

:::image type="content" source="./media/secure-score-security-controls/single-secure-score-via-ui.png" alt-text="Puntuación de seguridad general como se muestra en el portal":::

Para aumentar la seguridad, revise la página de recomendaciones de Security Center en busca de las acciones pendientes necesarias para aumentar la puntuación. Cada recomendación incluye instrucciones para ayudarle a corregir el problema específico.

Las recomendaciones se agrupan en **controles de seguridad**. Cada control es un grupo lógico de recomendaciones de seguridad relacionadas y refleja las superficies de ataque vulnerables. La puntuación solo mejora cuando corrige *todas* las recomendaciones para un solo recurso de un control. Para ver cómo protege su organización cada todas y cada una de las superficies expuesta a ataques, revise las puntuaciones de cada control de seguridad.

Para más información, consulte [Cálculo de la puntuación de seguridad](secure-score-security-controls.md#how-your-secure-score-is-calculated) a continuación. 


## <a name="access-your-secure-score"></a>Acceso a la puntuación de seguridad

Encontrará la puntuación de seguridad general, así como la puntuación por suscripción, mediante Azure Portal o mediante programación, tal como se describe en las secciones siguientes:

- [Obtención de la puntuación de seguridad desde el portal](#get-your-secure-score-from-the-portal)
- [Obtención de la puntuación de seguridad desde la API de REST](#get-your-secure-score-from-the-rest-api)
- [Obtención de la puntuación de seguridad desde Azure Resource Graph (ARG)](#get-your-secure-score-from-azure-resource-graph-arg)

### <a name="get-your-secure-score-from-the-portal"></a>Obtención de la puntuación de seguridad desde el portal

Security Center muestra la puntuación de forma destacada en el portal: es el primer icono principal de la página de información general de Security Center. Al seleccionar este icono, irá a la página dedicada de puntuación de seguridad, donde verá la puntuación dividida por suscripciones. Seleccione una suscripción única para ver la lista detallada de las recomendaciones prioritarias y del posible impacto que su corrección tendrá en la puntuación de la suscripción. 

En resumen, la puntuación de seguridad se muestra en las siguientes ubicaciones en las páginas del portal de Security Center.

- En un icono en la página **Información general** (panel principal) de Security Center:

    :::image type="content" source="./media/secure-score-security-controls/score-on-main-dashboard.png" alt-text="Puntuación de seguridad en el panel de Security Center":::

- En la página dedicada **Puntuación de seguridad**, puede ver la puntuación de seguridad de la suscripción y los grupos de administración:

    :::image type="content" source="./media/secure-score-security-controls/score-on-dedicated-dashboard.png" alt-text="Puntuación de seguridad de las suscripciones en la página de puntuación de seguridad de Security Center":::

    :::image type="content" source="./media/secure-score-security-controls/secure-score-management-groups.png" alt-text="Puntuación de seguridad de los grupos de administración en la página de puntuación de seguridad de Security Center":::

    > [!NOTE]
    > Los grupos de administración para los que no tenga permisos suficientes mostrarán su puntuación como "Restringido". 

- En la parte superior de la página **Recomendaciones**:

    :::image type="content" source="./media/secure-score-security-controls/score-on-recommendations-page.png" alt-text="Puntuación de seguridad en la página de recomendaciones de Security Center":::

### <a name="get-your-secure-score-from-the-rest-api"></a>Obtención de la puntuación de seguridad desde la API de REST

Puede acceder a la puntuación a través de la API de puntuación segura. Los métodos de API proporcionan la flexibilidad necesaria para consultar los datos y crear su propio mecanismo de creación de informes de las puntuaciones seguras a lo largo del tiempo. Por ejemplo, puede usar [Secure Scores](/rest/api/securitycenter/securescores) API para obtener la puntuación de una suscripción específica. Además, puede usar [Secure Score Controls API](/rest/api/securitycenter/securescorecontrols) para mostrar los controles de seguridad y la puntuación actual de las suscripciones.

![Recuperación de una sola puntuación de seguridad a través de la API](media/secure-score-security-controls/single-secure-score-via-api.png)

Para ver ejemplos de herramientas basadas en la API de puntuación de seguridad, consulte el [área de puntuación de seguridad de la comunidad de GitHub](https://github.com/Azure/Azure-Security-Center/tree/master/Secure%20Score). 

### <a name="get-your-secure-score-from-azure-resource-graph-arg"></a>Obtención de la puntuación de seguridad desde Azure Resource Graph (ARG)

Azure Resource Graph proporciona acceso instantáneo a la información de los recursos en los entornos en la nube con funcionalidades sólidas para filtrar, agrupar y ordenar. Es una forma rápida y eficaz de consultar información en las suscripciones de Azure mediante programación o desde Azure Portal. [Más información sobre Azure Resource Graph](../governance/resource-graph/index.yml).

Para acceder a la puntuación de seguridad de varias suscripciones con ARG:

1. Desde Azure Portal, abra el **Explorador de Azure Resource Graph**.

    :::image type="content" source="./media/security-center-identity-access/opening-resource-graph-explorer.png" alt-text="Inicio de la página de recomendaciones de Azure Resource Graph Explorer**" :::

1. Escriba la consulta de Kusto (utilice los ejemplos siguientes como guía).

    - Esta consulta devuelve el identificador de la suscripción, la puntuación actual en puntos y como porcentaje, y la puntuación máxima de la suscripción. 

        ```kusto
        SecurityResources 
        | where type == 'microsoft.security/securescores' 
        | extend current = properties.score.current, max = todouble(properties.score.max)
        | project subscriptionId, current, max, percentage = ((current / max)*100)
        ```

    - Esta consulta devuelve el estado de todos los controles de seguridad. Para cada control, obtendrá el número de recursos incorrectos, la puntuación actual y la puntuación máxima. 

        ```kusto
        SecurityResources 
        | where type == 'microsoft.security/securescores/securescorecontrols'
        | extend SecureControl = properties.displayName, unhealthy = properties.unhealthyResourceCount, currentscore = properties.score.current, maxscore = properties.score.max
        | project SecureControl , unhealthy, currentscore, maxscore
        ```

1. Seleccione **Ejecutar consulta**.




## <a name="tracking-your-secure-score-over-time"></a>Seguimiento de la puntuación de seguridad a lo largo del tiempo

Si es un usuario de Power BI con una cuenta Pro, puede usar el panel de Power BI de **puntuación de seguridad a lo largo del tiempo** para realizar un seguimiento de la puntuación de seguridad a lo largo del tiempo e investigar los cambios.

> [!TIP]
> Puede encontrar este panel, así como otras herramientas para trabajar mediante programación con la puntuación de seguridad, en el área dedicada de la comunidad de Azure Security Center en GitHub: https://github.com/Azure/Azure-Security-Center/tree/master/Secure%20Score.

El panel contiene los dos informes siguientes para ayudarle a analizar el estado de seguridad:

- **Resumen de los recursos**: proporciona datos resumidos sobre el estado de los recursos.
- **Resumen de la puntuación de seguridad**: proporciona datos resumidos sobre el progreso de la puntuación. Use el gráfico "Secure score over time per subscription" para ver los cambios en la puntuación. Si observa un cambio drástico en la puntuación, consulte la tabla "detected changes that may affect your secure score" para buscar posibles cambios que puedan haber producido la variación. En esta tabla se presentan recursos eliminados, recursos recién implementados o recursos que su estado de seguridad cambió para una de las recomendaciones.

:::image type="content" source="./media/secure-score-security-controls/power-bi-secure-score-dashboard.png" alt-text="Panel de Power BI de puntuación de seguridad opcional a lo largo del tiempo para realizar un seguimiento de la puntuación de seguridad a lo largo del tiempo e investigar los cambios":::





## <a name="how-your-secure-score-is-calculated"></a>Cálculo de la puntuación de seguridad 

La contribución de cada control de seguridad en la puntuación de seguridad total aparece con claridad en la página de recomendaciones.

[![La puntuación de seguridad mejorada presenta controles de seguridad](media/secure-score-security-controls/security-controls.png)](media/secure-score-security-controls/security-controls.png#lightbox)

Para obtener todos los puntos posibles de un control de seguridad, todos sus recursos deben cumplir todas las recomendaciones de seguridad de dicho control. Por ejemplo, Security Center tiene varias recomendaciones sobre cómo proteger los puertos de administración. Deberá corregirlas todas para que la puntuación de seguridad mejore.

Por ejemplo, el control de seguridad denominado "Aplicar actualizaciones del sistema" tiene una puntuación máxima de seis puntos, como puede ver en la información sobre herramientas sobre el potencial valor de mejora del control:

[![Control de seguridad "Aplicar actualizaciones del sistema"](media/secure-score-security-controls/apply-system-updates-control.png)](media/secure-score-security-controls/apply-system-updates-control.png#lightbox)

La puntuación máxima para este control, "Aplicar actualizaciones del sistema", es siempre 6. En este ejemplo, hay 50 recursos. Por tanto, dividimos la puntuación máxima entre 50 y el resultado es que cada recurso aporta 0,12 puntos. 

* **Mejora potencial** (0,12 x 8 recursos con estado incorrecto = 0,96): los puntos restantes disponibles para el usuario en el control. Esto significa que si corrige todas las recomendaciones de este control, la puntuación aumentará en un 2 % (en este caso, 0,96 puntos, que se redondean en 1 punto). 
* **Puntuación actual** (0,12 x 42 recursos con estado correcto = 5,04): puntuación actual para este control. Cada control contribuye a la puntuación total. En este ejemplo, el control contribuye con 5,04 puntos a la puntuación total de seguridad actual.
* **Puntuación máxima**: el número máximo de puntos que puede obtener al completar todas las recomendaciones de un control. La puntuación máxima de un control indica la importancia relativa de ese control. Use los valores de puntuación máxima para evaluar la prioridad de los problemas. 


### <a name="calculations---understanding-your-score"></a>Cálculos: Descripción de la puntuación

|Métrica|Fórmula y ejemplo|
|-|-|
|**Puntuación actual del control de seguridad**|<br>![Ecuación para calcular la puntuación de un control de seguridad](media/secure-score-security-controls/secure-score-equation-single-control.png)<br><br>Cada control de seguridad individual contribuye a la puntuación de seguridad. Cada recurso afectado por una recomendación dentro del control contribuye a la puntuación actual de este. La puntuación actual de cada control es una medida del estado de los recursos que están *dentro* del control.<br>![Información sobre herramientas que muestra los valores usados al calcular la puntuación actual del control de seguridad](media/secure-score-security-controls/security-control-scoring-tooltips.png)<br>En este ejemplo, la puntuación máxima de 6 se divide entre 78, ya que esta es la suma de los recursos correctos e incorrectos.<br>6 / 78 = 0,0769<br>La multiplicación de esa cifra por el número de recursos correctos (4) da como resultado la puntuación actual:<br>0.0769 * 4 = **0.31**<br><br>|
|**Puntuación segura**<br>Suscripción única|<br>![Ecuación para calcular la puntuación de seguridad de una suscripción](media/secure-score-security-controls/secure-score-equation-single-sub.png)<br><br>![Puntuación de seguridad de una suscripción única con todos los controles habilitados](media/secure-score-security-controls/secure-score-example-single-sub.png)<br>En este ejemplo, hay una suscripción única con todos los controles de seguridad disponibles (una puntuación máxima posible de 60 puntos). La puntuación muestra 28 puntos de los 60 posibles y los 32 puntos restantes se reflejan en las cifras de "Posible aumento de puntuación" de los controles de seguridad.<br>![Lista de controles y posible aumento de puntuación](media/secure-score-security-controls/secure-score-example-single-sub-recs.png)|
|**Puntuación segura**<br>Varias suscripciones|<br>![Ecuación para calcular la puntuación de seguridad de varias suscripciones](media/secure-score-security-controls/secure-score-equation-multiple-subs.png)<br><br>Al calcular la puntuación combinada para varias suscripciones, Security Center incluye una *ponderación* para cada suscripción. Las ponderaciones relativas de las suscripciones se determinan mediante Security Center en función de factores como el número de recursos.<br>La puntuación actual de cada suscripción se calcula de la misma manera que para una sola suscripción, pero la ponderación se aplica como se muestra en la ecuación.<br>Cuando se ven varias suscripciones, la puntuación de seguridad evalúa todos los recursos de todas las directivas habilitadas y agrupa su impacto combinado en la puntuación máxima de cada control de seguridad.<br>![Puntuación de seguridad de varias suscripciones con todos los controles habilitados](media/secure-score-security-controls/secure-score-example-multiple-subs.png)<br>La puntuación combinada **no** es un promedio; en vez de eso, es la posición evaluada del estado de todos los recursos de todas las suscripciones.<br>También en este caso, si va a la página de recomendaciones y suma los puntos posibles disponibles, observará que esta es la diferencia entre la puntuación actual (24) y la puntuación máxima disponible (60).|
||||

### <a name="which-recommendations-are-included-in-the-secure-score-calculations"></a>¿Qué recomendaciones se incluyen en los cálculos de la puntuación de seguridad?

Solo las recomendaciones integradas afectan a la puntuación de seguridad.

Las recomendaciones marcadas como **Versión preliminar** no se incluyen en los cálculos de la puntuación de seguridad. Aun así, deben corregirse siempre que sea posible, de tal forma que, cuando finalice el período de versión preliminar, contribuyan a la puntuación.

Un ejemplo de una recomendación en versión preliminar:

:::image type="content" source="./media/secure-score-security-controls/example-of-preview-recommendation.png" alt-text="Recomendación con la marca de versión preliminar":::

## <a name="improve-your-secure-score"></a>Mejora de su puntuación de seguridad

Para mejorar la puntuación de seguridad, corrija las recomendaciones de seguridad de la lista de recomendaciones. Puede corregir cada recomendación manualmente para cada recurso o utilizar la opción **Corrección rápida** (si está disponible) para aplicar rápidamente una corrección de una recomendación a un grupo de recursos. Para más información, consulte [Corrección de recomendaciones](security-center-remediate-recommendations.md).

Otra forma de mejorar la puntuación y de asegurarse de que los usuarios no creen recursos que afecten negativamente a la puntuación es configurar las opciones de aplicar y denegar en las recomendaciones pertinentes. Más información en [Evitar errores de configuración con Aplicar/Denegar](prevent-misconfigurations.md).

## <a name="security-controls-and-their-recommendations"></a>Controles de seguridad y sus recomendaciones

En la tabla siguiente se enumeran los controles de seguridad de Azure Security Center. Para cada control, puede ver el número máximo de puntos que puede sumar a la puntuación de seguridad si corrige *todas* las recomendaciones enumeradas en el control, para *todos* los recursos. 

El conjunto de recomendaciones de seguridad proporcionadas con Security Center se adapta a los recursos disponibles en el entorno de cada organización. Las recomendaciones se pueden personalizar aún más [deshabilitando directivas](tutorial-security-policy.md#disable-security-policies-and-disable-recommendations) y [excluyendo recursos específicos de una recomendación](exempt-resource.md). 
 
Se recomienda que cada organización revise cuidadosamente sus iniciativas de Azure Policy asignadas. 

> [!TIP]
> Para obtener información detallada sobre cómo revisar y editar iniciativas, vea [Trabajo con directivas de seguridad](tutorial-security-policy.md). 

Aunque la iniciativa de seguridad predeterminada de Security Center se basa en los estándares y procedimientos recomendados del sector, hay escenarios en los que es posible que las recomendaciones integradas que se indican a continuación no se ajusten completamente a su organización. Por lo tanto, a veces será necesario ajustar la iniciativa predeterminada, sin comprometer la seguridad, para asegurarse de que está alineada con las directivas propias de su organización, así como con estándares del sector, estándares normativos y pruebas comparativas que tiene la obligación de cumplir.<br><br>
<div class="foo">

<style type="text/css"> .tg  {border-collapse:collapse;border-spacing:0;} .tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px; overflow:hidden;padding:10px 5px;word-break:normal;} .tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:18px; font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;} .tg .tg-cly1{text-align:left;vertical-align:middle} .tg .tg-lboi{border-color:inherit;text-align:left;vertical-align:middle} </style>

[!INCLUDE [security-center-controls-and-recommendations](../../includes/asc/security-control-recommendations.md)]

</div>




## <a name="secure-score-faq"></a>Preguntas frecuentes sobre la puntuación de seguridad

### <a name="if-i-address-only-three-out-of-four-recommendations-in-a-security-control-will-my-secure-score-change"></a>Si solo se corrigen tres de las cuatro recomendaciones de un control de seguridad, ¿cambiará mi puntuación de seguridad?
No. No cambiará hasta que corrija todas las recomendaciones para un único recurso. Para obtener la puntuación máxima de un control, debe corregir todas las recomendaciones de todos los recursos.

### <a name="if-a-recommendation-isnt-applicable-to-me-and-i-disable-it-in-the-policy-will-my-security-control-be-fulfilled-and-my-secure-score-updated"></a>Si una recomendación no es aplicable a mí y la deshabilito en la directiva, ¿se cumplirá mi control de seguridad y se actualizará mi puntuación de seguridad?
Sí. Se recomienda deshabilitar las recomendaciones cuando no son aplicables a su entorno. Para obtener instrucciones sobre cómo deshabilitar una recomendación específica, consulte [Deshabilitar las directivas de seguridad](./tutorial-security-policy.md#disable-security-policies-and-disable-recommendations).

### <a name="if-a-security-control-offers-me-zero-points-towards-my-secure-score-should-i-ignore-it"></a>Si un control de seguridad ofrece cero puntos a mi puntuación de seguridad, ¿debería ignorarlo?
En algunos casos verá una puntuación máxima del control mayor que cero, pero el impacto es nulo. Cuando la puntuación incremental para corregir recursos es insignificante, se redondea a cero. Aún así, no ignore estas recomendaciones ya que pueden aportarle mejoras en seguridad. La única excepción es el control de "procedimiento recomendado adicional". La corrección de estas recomendaciones no aumentará la puntuación, pero mejorará la seguridad en general.

## <a name="next-steps"></a>Pasos siguientes

En este artículo se describe la puntuación de seguridad y los controles de seguridad que presenta. Para obtener material relacionado, consulte los siguientes artículos:

- [Más información sobre los distintos elementos de una recomendación](security-center-recommendations.md)
- [Recomendaciones de corrección](security-center-remediate-recommendations.md)
- [Ver las herramientas basadas en GitHub para trabajar mediante programación con la puntuación de seguridad](https://github.com/Azure/Azure-Security-Center/tree/master/Secure%20Score)