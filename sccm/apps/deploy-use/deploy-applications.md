---
title: Implementar aplicaciones | Microsoft Docs
description: "Cree un tipo de implementación o simule la implementación de una aplicación con System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 7be9abadeb51d4f9e862f69c332756b19ce3e110
ms.openlocfilehash: a52bef3c8d12ffe2d9b13dc79cbc8950d3f36aea


---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Implementar aplicaciones con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

 Antes de implementar una aplicación de System Center Configuration Manager, debe crear al menos un tipo de implementación para la aplicación. Para obtener más información sobre la creación de aplicaciones y los tipos de implementación, consulte [Create applications](../../apps/deploy-use/create-applications.md) (Crear aplicaciones).

 También puede simular la implementación de una aplicación. Este tipo de implementación prueba la aplicabilidad de una implementación de aplicación en equipos sin instalar o desinstalar la aplicación. Una implementación simulada evalúa el método de detección, los requisitos y las dependencias de un tipo de implementación y muestra los resultados en el nodo **Implementaciones** del área de trabajo **Supervisión**. Para obtener más información, consulte [Simulate application deployments ](../../apps/deploy-use/simulate-application-deployments.md) (Simular implementaciones de aplicaciones).

> [!IMPORTANT]
>  Puede implementar (instalar o desinstalar) aplicaciones necesarias, pero no paquetes o actualizaciones de software. Los dispositivos inscritos en MDM tampoco admiten implementaciones simuladas, la experiencia del usuario o la configuración de programación.

## <a name="deploy-an-application"></a>Implementar una aplicación

1.  En la consola de Configuration Manager, vaya a **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.

2.  En la lista de **Aplicaciones** , seleccione la aplicación que desee implementar. A continuación, en la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Implementar**.

### <a name="specify-general-information-about-the-deployment"></a>Especificar información general sobre la implementación

En la página **General** del Asistente para implementar software, especifique la información siguiente:

- **Software**: muestra la aplicación que se va a implementar. Puede hacer clic en **Examinar** para seleccionar otra aplicación.
- **Recopilación**: haga clic en **Examinar** para seleccionar la recopilación en la que se va a implementar la aplicación.
- **Usar grupos de puntos de distribución predeterminados asociados a esta recopilación**: seleccione esta opción si quiere almacenar el contenido de la aplicación en el grupo de puntos de distribución predeterminados de la recopilación. Si no asocia la recopilación seleccionada con un grupo de puntos de distribución, esta opción aparecerá atenuada.
- **Distribuir contenido automáticamente para las dependencias**: si esta opción está habilitada y cualquiera de los tipos de implementación de la aplicación contiene dependencias, el contenido de la aplicación dependiente se enviará también a los puntos de distribución.

    >[!IMPORTANT]
    > Si actualiza la aplicación dependiente después de haber implementado la aplicación principal, cualquier contenido nuevo para la dependencia no se distribuirá automáticamente.

- **Comentarios (opcional)** : si lo desea, escriba una descripción de esta implementación.

### <a name="specify-content-options-for-the-deployment"></a>Especificar las opciones de contenido de la implementación

En la página **Contenido**, haga clic en **Agregar** para agregar el contenido asociado a esta implementación a los puntos de distribución o grupos de puntos de distribución. Si ha seleccionado **Use default distribution points associated to this collection** (Usar puntos de distribución predeterminados asociados a esta recopilación) en la página **General**, esta opción se rellenará automáticamente y solo podrá modificarla un miembro del rol de seguridad Administrador de aplicaciones.

### <a name="specify-deployment-settings"></a>Especificar la configuración de implementación

En la página **Configuración de implementación** del Asistente para implementar software, especifique la información siguiente:

- **Acción**: en la lista desplegable, seleccione si la finalidad de la implementación es **Instalar** o **Desinstalar** la aplicación.

    > [!NOTE]
    >  Si una aplicación se implementa dos veces en un dispositivo, una vez con una acción de **Instalar** y otra con una acción de **Desinstalar**, la implementación de la aplicación con una acción de **Instalar** tendrá prioridad.

No puede cambiar la acción de una implementación después de haberla creado.

- **Propósito**: en la lista desplegable, seleccione una de las opciones siguientes:
    - **Disponible**: si la aplicación se implementa en un usuario, este la verá publicada en el Centro de software y la podrá instalar a petición.
    - **Requerido**: la aplicación se implementa automáticamente según la programación. Si el estado de implementación de la aplicación no está oculto, cualquier persona que use la aplicación puede realizar un seguimiento de su estado de implementación e instalar la aplicación desde el Centro de software antes de la fecha límite.

    > [!NOTE]   
    >  Cuando la acción de implementación se establece en **Desinstalar**, el propósito de la implementación se establece automáticamente en **Requerido** y no se puede cambiar.  

- **Deploy automatically according to schedule whether or not a user is logged on** (Implementar automáticamente según la programación tanto si un usuario inició sesión como si no): si la implementación es en un usuario, seleccione esta opción para implementar la aplicación en los dispositivos primarios del usuario. Esta configuración no requiere que el usuario inicie sesión para ejecutar la implementación. No seleccione esta opción si el usuario debe proporcionar entrada para completar la instalación. Esta opción solo está disponible cuando la implementación tiene un propósito **Requerido**.


- **Enviar paquetes de reactivación**: si el propósito de la implementación se establece en **Requerido** y se selecciona esta opción, se enviará un paquete de reactivación a los equipos antes de instalar la implementación. Este paquete reactiva el equipo a la hora límite de instalación. Para poder utilizar esta opción, los equipos y las redes deben configurarse para Wake on LAN.
- **Permitir a los clientes de una conexión a Internet de uso medido descargar contenido una vez cumplida la fecha límite de instalación, lo cual podría suponer costes adicionales**: esta opción solo está disponible para implementaciones con un propósito **Requerido**.
- **Solicitar aprobación del administrador si los usuarios solicitan esta aplicación**: si esta opción está seleccionada, el administrador debe aprobar las solicitudes de la aplicación de cualquier usuario antes de poder instalarla. Esta opción aparece atenuada si el propósito de la implementación es **Requerido** o si se implementa la aplicación en una recopilación de dispositivos.

    > [!NOTE]
    >  Las solicitudes de aprobación de aplicación se muestran en el nodo **Solicitudes de aprobación** , en **Administración de aplicaciones** en el área de trabajo **Biblioteca de software** . Si una solicitud no se aprueba antes de 45 días, se quitará. Además, volver a instalar el cliente de Configuration Manager puede cancelar las solicitudes de aprobación pendientes.
    > Después de aprobar una aplicación para la instalación, puede denegar la solicitud. Para ello, haga clic en **Denegar** en la consola de Configuration Manager (antes, este botón aparecía atenuado tras la aprobación).
    > Esta acción no desinstala la aplicación de los dispositivos, pero impide que los usuarios instalen copias nuevas de la aplicación desde el Centro de software.



- **Automatically upgrade any superseded version of this application** (Actualizar automáticamente cualquier versión reemplazada de esta aplicación): si se selecciona esta opción, cualquier versión reemplazada de la aplicación se actualizará con la aplicación nueva.

### <a name="specify-scheduling-settings-for-the-deployment"></a>Especificar la configuración de programación de la implementación

En la página **Programación** del Asistente para implementar software, establezca cuándo se implementará o estará disponible para dispositivos clientes esta aplicación.
Las opciones de esta página variarán dependiendo de si la acción de la implementación se establece en **Disponible** o **Requerido**.

En algunos casos, es posible que quiera dar más tiempo a los usuarios para instalar las implementaciones de aplicaciones o las actualizaciones de software necesarias más allá de los plazos que ha establecido. Normalmente esto es necesario cuando un equipo ha estado apagado durante un largo período de tiempo y tiene que instalar muchas implementaciones de aplicaciones o actualizaciones. Por ejemplo, si un usuario final acaba de volver de vacaciones, es posible que tenga que esperar bastante mientras se instalan las implementaciones de aplicaciones vencidas. Para solucionar este problema, puede definir un período de gracia de cumplimiento mediante la implementación de la configuración de cliente de Configuration Manager en una colección.

Para configurar el período de gracia, haga lo siguiente:

- En la página **Agente de equipo** de la configuración de cliente, configure la nueva propiedad **Período de gracia para el cumplimiento tras la fecha límite de la implementación (horas)** con un valor entre **1** y **120** horas.
- En la página **Programación** de una nueva implementación de aplicación obligatoria, o en las propiedades de una implementación existente, active la casilla **Delay enforcement of this deployment according to user preferences, up to the grace period defined in client settings** (Retrasar el cumplimiento de esta implementación de acuerdo con las preferencias del usuario hasta el período de gracia definido en la configuración del cliente). Todas las implementaciones que tienen activada esta casilla y que están destinadas a dispositivos en los que también se ha implementado la configuración de cliente usarán el período de gracia de cumplimiento.

Una vez que se alcance la fecha límite de instalación de la aplicación, esta se instalará en la primera ventana que no sea de empresa configurada por el usuario hasta ese período de gracia. No obstante, el usuario puede abrir el Centro de software e instalar la aplicación en cualquier momento que quiera. Una vez que expira el período de gracia, el cumplimiento vuelve al comportamiento normal para implementaciones vencidas.

Si la aplicación que se va a implementar reemplaza a otra aplicación, puede establecer la fecha límite de instalación cuando los usuarios recibirán la nueva aplicación. Haga esto mediante la configuración de **Fecha límite de instalación** para actualizar los usuarios con una aplicación sustituida.

### <a name="specify-user-experience-settings-for-the-deployment"></a>Especificar la configuración de la experiencia del usuario para la implementación


En la página **Experiencia del usuario** del Asistente para implementar software, especifique información sobre cómo pueden interactuar los usuarios con la instalación de la aplicación.

Cuando implemente aplicaciones en dispositivos de Windows Embedded habilitados para filtro de escritura, puede especificar que se instale la aplicación en la superposición temporal y confirmar los cambios más tarde, o puede confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento. Al confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento, es necesario reiniciar el dispositivo. Los cambios se conservan en el dispositivo.

>[!NOTE]
    >  Cuando implemente una aplicación en un dispositivo de Windows Embedded, asegúrese de que el dispositivo es miembro de una recopilación que tenga una ventana de mantenimiento configurada. Para obtener más información sobre cómo se usan las ventanas de mantenimiento al implementar aplicaciones en dispositivos de Windows Embedded, consulte el tema [Create Windows Embedded applications](../../apps/get-started/creating-windows-embedded-applications.md) (Crear aplicaciones de Windows Embedded).

    >  The options **Software Installation** and **System restart (if required to complete the installation)** are not used if the deployment purpose is set to **Available**. You can also configure the level of notification a user sees when the application is installed.

### <a name="specify-alert-options-for-the-deployment"></a>Especificar las opciones de alerta de la implementación

En la página **Alertas** del Asistente para implementar software, establezca cómo Configuration Manager y System Center Operations Manager generarán alertas para esta implementación. Puede configurar umbrales para alertas de generación de informes y desactivar los informes durante la implementación.

### <a name="associate-the-deployment-with-an-ios-app-configuration-policy"></a>Asociar la implementación con una directiva de configuración de aplicaciones iOS

En la página **Directivas de configuración de aplicaciones**, haga clic en **Nuevo** para asociar esta implementación con una directiva de configuración de aplicaciones iOS (si ha creado una). Para obtener más información sobre este tipo de directiva, consulte [Configure iOS apps with app configuration policies](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md) (Configurar aplicaciones iOS con directivas de configuración de aplicaciones).

### <a name="finish-up"></a>Finalizar

En la página **Resumen** del Asistente para implementar software, revise las acciones que llevará a cabo esta implementación y, después, haga clic en **Siguiente** para finalizar el asistente.

La nueva implementación se mostrará en la lista de **Implementaciones** en el nodo **Implementaciones** del área de trabajo **Supervisión** . Puede editar las propiedades de esta implementación o eliminar la implementación de la pestaña **Implementaciones** del panel de detalles de la aplicación.

## <a name="delete-an-application-deployment"></a>Eliminar la implementación de una aplicación

1.  En la consola de Configuration Manager, vaya a **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.

3.  En la lista de **Aplicaciones**, seleccione la aplicación que incluya la implementación que se va a eliminar.

4.  En la pestaña **Implementaciones** de la lista *<nombre de aplicación\>*, seleccione la implementación de la aplicación que desee eliminar. Después, en la pestaña **Implementación**, en el grupo **Implementación**, haga clic en **Eliminar**.

 Cuando se elimina la implementación de una aplicación, no se quitan las instancias de la aplicación que ya se han instalado. Para quitar estas aplicaciones, debe implementar la aplicación en los equipos con la opción **Desinstalar**. Si elimina una implementación de aplicación o quita un recurso de la recopilación en la que está implementando, la aplicación ya no estará visible en el Centro de software.

## <a name="user-notifications-for-required-deployments"></a>Notificaciones de usuario para las implementaciones requeridas
Cuando recibe software obligatorio a través de la opción **Snooze and remind me** (Posponer y volver a recordármelo), puede seleccionar los siguientes valores en la lista desplegable:
- **Más adelante**: especifica que las notificaciones se programan según la configuración de notificaciones establecida en Configuración de agente de cliente.
- **Hora fija**: especifica que la notificación se programará para mostrarse de nuevo después de la hora seleccionada. Por ejemplo, si selecciona 30 minutos, la notificación se mostrará de nuevo transcurridos 30 minutos.

![Página Agente de equipo de Configuración de agente de cliente](media/ComputerAgentSettings.png)

El tiempo máximo que se puede posponer siempre se basa en los valores de notificación configurados en Configuración de agente de cliente en cada momento a lo largo de la escala de tiempo de implementación. Por ejemplo, si la opción **La fecha límite de la implementación es de más de 24 horas. Recordar al usuario cada (horas)** de la página **Agente de equipo** se configura para 10 horas y pasan más de 24 horas antes de la fecha límite en que se inicia el cuadro de diálogo, verá un conjunto de opciones para posponer de 10 horas como máximo. Cuando se acerca la fecha límite, el cuadro de diálogo muestra menos opciones, en consonancia con la configuración de agente de cliente correspondiente a cada componente de la escala de tiempo de implementación.

Además, en una implementación de alto riesgo, como una secuencia de tareas que implementa un sistema operativo, la experiencia de notificación del usuario es ahora más intrusiva. En lugar de una notificación transitoria en la barra de tareas, cada vez que se le notifica que se necesita mantenimiento de software crítico, aparece un cuadro de diálogo como el siguiente en el equipo:

![Cuadro de diálogo Software requerido](media/client-toast-notification.png)

## <a name="for-more-information"></a>Para obtener más información:
- [Settings to manage high-risk deployments (Configuración para administrar implementaciones de alto riesgo)](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Cómo configurar el cliente](../../core/clients/deploy/configure-client-settings.md)



<!--HONumber=Dec16_HO3-->

