---
title: Actualizaciones en la consola | System Center Configuration Manager
description: System Center Configuration Manager se sincroniza con la nube de Microsoft para obtener las actualizaciones que puede instalar desde la consola.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: b9721737b4181d8f5e41224c3e2c32ae41647554


---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>Instalación de actualizaciones en la consola para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

System Center Configuration Manager se sincroniza con el servicio en la nube de Microsoft para obtener las actualizaciones que puede instalar después desde la consola de Configuration Manager.

## <a name="get-available-updates"></a>Obtención de actualizaciones disponibles
Solo las actualizaciones aplicables a su infraestructura y versión se descargan y habilitan, y se ponen a disposición de su jerarquía. Esta sincronización puede ser automática o manual, según cómo configure el punto de conexión de servicio para la jerarquía:

-   En **modo en línea**, el punto de conexión de servicio se conecta al servicio en la nube de Microsoft automáticamente y descarga las actualizaciones aplicables.  

     De manera predeterminada, Configuration Manager busca nuevas actualizaciones cada 24 horas. A partir de la versión 1602, también puede comprobar las actualizaciones inmediatamente; para ello, haga clic en **Buscar actualizaciones** en el nodo **Administración** > **Servicios en la nube** > **Actualizaciones y mantenimiento** de la consola de Configuration Manager.  

-   En el **modo sin conexión**, el punto de conexión de servicio no se conecta al servicio en la nube de Microsoft y es necesario [Usar la herramienta de conexión de servicio para System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md) de manera manual para descargar e importar las actualizaciones disponibles.  

> [!NOTE]  
>  Además de las actualizaciones que obtendrá al sincronizar con el servicio en la nube de Microsoft, las correcciones fuera de banda que se instalan con la [herramienta Actualizar registro](http://technet.microsoft.com/library/mt691544.aspx) también se importan en la consola, donde puede seleccionarlas para instalarlas.  

Una vez que las actualizaciones se sincronizan, puede verlas en la consola de Configuration Manager; para ello, desplácese hasta el nodo **Administración** > **Servicios en la nube** > **Actualizaciones y mantenimiento**:  

-   Las actualizaciones no instaladas se muestran como **Disponible**.

-   Las actualizaciones instaladas se muestran como **Instalado**.  A partir de la versión 1606, solo se muestra la última actualización instalada y puede hacer clic en el botón **Historial** en la cinta de opciones para ver las actualizaciones previamente instaladas.



Antes de configurar el punto de conexión de servicio, es conveniente conocer y planear sus usos adicionales, que pueden afectar al modo en que se configura este rol de sistema de sitio:  

-   El punto de conexión de servicio se usa para cargar la información de uso sobre su sitio. Esta información ayuda al servicio en la nube de Microsoft a identificar las actualizaciones que están disponibles para la versión actual de su infraestructura. Para obtener más información, consulte [Diagnósticos y datos de uso para System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

-   El punto de conexión de servicio se usa para administrar dispositivos con Microsoft Intune y con la administración local de dispositivos móviles de Configuration Manager. Para obtener más información, consulte [Administración híbrida de dispositivos móviles (MDM) con System Center Configuration Manager y Microsoft Intune](../../../mdm/plan-design/hybrid-mobile-device-management.md).  

Para entender mejor lo que ocurre cuando se descargan las actualizaciones, consulte:  

-   [Diagrama de flujo: descargar actualizaciones para System Center Configuration Manager](../../../core/servers/manage/download-updates-flowchart.md).  

-   [Diagrama de flujo: actualizar la replicación para System Center Configuration Manager](../../../core/servers/manage/update-replication-flowchart.md)  

## <a name="permissions-to-view-and-manage-updates-and-features"></a>Permisos para ver y administrar actualizaciones y características
Antes de instalar la actualización 1606, para ver las actualizaciones en la consola, un usuario debe tener asignado un rol de seguridad que incluya el permiso de **lectura** en el grupo de permisos **Sitio**y el ámbito de seguridad **Todos**. A partir de la actualización 1606, se incluye una nueva clase de seguridad de administración basada en roles llamada **Paquetes de actualización** , que concede acceso para ver y administrar las actualizaciones en la consola de Configuration Manager.    

**Acerca de la clase Paquetes de actualización:**  
De forma predeterminada, **Paquetes de actualización** (SMS_CM_Updatepackages) forma parte de los siguientes roles de seguridad integrados con los permisos de la lista:
 -  **Administrador total** con permisos **Modificar** y **Lectura** :
    -   Un usuario con este rol de seguridad y acceso al ámbito de seguridad **Todo** puede ver e instalar actualizaciones, así como habilitar características durante la instalación y características individuales después de la instalación.
    - Un usuario con este rol de seguridad y acceso al ámbito de seguridad **Predeterminado** puede ver e instalar actualizaciones, habilitar características durante la instalación y ver características después de la instalación, pero no puede habilitarlas.

- **Analista de solo lectura** con permisos **Lectura** :
  -  Un usuario con este rol de seguridad y acceso al ámbito **Predeterminado** puede ver las actualizaciones, pero no instalarlas y puede ver las características después de la instalación, pero no puede habilitarlas.

**Resumen de los permisos necesarios para la actualización y el mantenimiento:**   
  - Use una cuenta que tenga asignado un rol de seguridad que incluya la clase **Paquetes de actualización** con los permisos **Modificar** y **Lectura** .
  - La cuenta debe tener asignado el ámbito **Predeterminado** .

**Para ver solo las actualizaciones**:
  - Use una cuenta que se asigna un rol de seguridad que incluye la clase **Paquetes de actualización** solo con el permiso **Lectura** .
  - La cuenta debe tener asignado el ámbito **Predeterminado** .

**Para habilitar características después de haber instalado las actualizaciones:**
  -   Use una cuenta que tenga asignado un rol de seguridad que incluya la clase **Paquetes de actualización** con los permisos **Modificar** y **Lectura** .
  -  La cuenta debe tener asignado el ámbito **Todos** .






##  <a name="a-namebkmkbeforeinstalla-before-you-install-an-in-console-update"></a><a name="bkmk_beforeinstall"></a> Antes de instalar una actualización en la consola  
 Revise los siguientes pasos antes de instalar las actualizaciones desde la consola de Configuration Manager:  

###  <a name="a-namebkmkstep1a-step-1-review-the-update-checklist"></a><a name="bkmk_step1"></a> Paso 1: Revisar la lista de comprobación de actualización  
Antes de instalar una nueva actualización desde la consola de Configuration Manager, revise la lista de comprobación de actualización aplicable para las acciones que deben realizarse antes de iniciar la actualización:  

-   Actualización a 1511 desde [Actualizar a System Center Configuration Manager](../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)    

-   Actualización a 1602 desde 1511: consulte [Lista de comprobación para la instalación de la actualización 1602](../../../core/servers/manage/checklist-for-installing-update-1602.md).

- Actualización a 1606 desde 1511 o 1602: consulte [Lista de comprobación para la instalación de la actualización 1606](../../../core/servers/manage/checklist-for-installing-update-1606.md).  


###  <a name="a-namebkmkstep2a-step-2-test-the-database-upgrade-before-installing-an-update"></a><a name="bkmk_step2"></a> Paso 2: Probar la actualización de la base de datos antes de instalar una actualización  
Antes de instalar una nueva actualización en la jerarquía, como la 1602, debe probar la actualización de la base de datos del sitio. El nombre de la opción de línea de comandos que se utiliza para probar la instalación de una actualización a una copia de seguridad de la base de datos del sitio es **testdbupgrade**.  

A diferencia de las versiones anteriores de Configuration Manager, si se produce un error al instalar una actualización, no necesita realizar una recuperación del sitio y, en lugar de ello, puede reintentar la instalación de la actualización. Por lo tanto, aunque la actualización de prueba de la base de datos es menos crítica que en las versiones de producto anteriores, todavía se trata de un paso recomendado.  

##### <a name="to-run-testdbupgrade-before-installing-an-update"></a>Para ejecutar testdbupgrade antes de instalar una actualización  

1.  Obtenga un conjunto de archivos de origen de la carpeta **CD.Latest** de un sitio que ejecuta la versión a la que pretende actualizar. Esto podría requerir instalar primero un sitio en un entorno de laboratorio o de prueba que ejecuta esta versión de System Center Configuration Manager.  

     La carpeta **CD.Latest** de un sitio contiene los archivos de origen de esa versión. Debe utilizar estos archivos de origen para ejecutar la actualización de prueba de la base de datos del sitio. Para obtener más información, consulte [La carpeta CD.Latest para System Center Configuration Manager](../../../core/servers/manage/the-cd.latest-folder.md).  

     Por ejemplo, si el sitio ejecuta la versión 1501 y desea actualizar a 1602, debe obtener una carpeta CD.Latest de un sitio que ya ha actualizado a la versión 1602. Normalmente, puede instalar un sitio nuevo y temporal en un laboratorio y actualizarlo a la versión 1602 para crear la carpeta CD.Latest con los archivos necesarios.  

2.  Copie la carpeta CD.Latest a una ubicación de SQL Server que vaya a utilizar para ejecutar la actualización de la base de datos de prueba. (Consulte el paso siguiente).  

3.  Cree una copia de seguridad de la base de datos del sitio de la que quiera realizar una actualización de prueba y luego restaure una copia de dicha base de datos a una instancia de SQL Server que no hospede un sitio de Configuration Manager. SQL Server debe utilizar la misma edición de SQL Server como la base de datos del sitio.  

4.  Después de restaurar la copia de la base de datos, ejecute el **programa de instalación** desde la carpeta CD.Latest que copió desde el entorno de laboratorio o de prueba. Cuando se ejecute el programa de instalación, utilice la opción de línea de comandos **/TESTDBUPGRADE** . Si la instancia de SQL Server que hospeda la copia de la base de datos no es la instancia predeterminada, también deberá indicar los argumentos de la línea de comandos para identificar la instancia que hospeda la copia de la base de datos del sitio.  

     Por ejemplo, tiene previsto actualizar una base de datos de sitio con el nombre SMS_ABC. Restaura una copia de esta base de datos del sitio a una instancia compatible de SQL Server con el nombre de instancia DBTest. Para probar una actualización de esta copia de la base de datos del sitio, use la siguiente línea de comandos: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     Puede encontrar Setup.exe en la siguiente ubicación del medio de origen de System Center Configuration Manager: **SMSSETUP\BIN\X64**.  

5.  En la instancia de SQL Server donde se ejecuta la actualización de la base de datos de prueba, supervise el archivo ConfigMgrSetup.log en la raíz de la unidad del sistema para ver el progreso y el éxito.  

     Si se produce un error en la prueba de actualización, resuelva cualquier problema relacionado con la actualización de la base de datos del sitio, cree una nueva copia de seguridad de la base de datos del sitio y, a continuación, pruebe la actualización de la nueva copia de la base de datos.  

     Una vez completado el proceso correctamente, puede eliminar la copia de la base de datos.  

    > [!NOTE]  
    >  No se puede restaurar la copia de la base de datos del sitio que se utiliza para la actualización de prueba para su uso como una base de datos de sitio en cualquier sitio.  

###  <a name="a-namebkmkstep3a-step-3-run-the-prerequisite-checker-before-installing-an-update"></a><a name="bkmk_step3"></a> Paso 3: Ejecutar el Comprobador de requisitos previos antes de instalar una actualización  
Antes de instalar una actualización, puede ejecutar la comprobación de requisitos previos para la actualización. Si ejecuta la comprobación de requisitos previos antes de instalar una actualización:  

-   Los archivos de actualización se replican en otros sitios antes de instalar realmente la actualización.  

-   La comprobación de requisitos previos se volverá a ejecutará automáticamente cuando se decide instalar la actualización.  

Más adelante, cuando instale una actualización, tiene la opción de configurar la actualización para omitir las advertencias de comprobación de requisitos previos.  

##### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Para ejecutar el Comprobador de requisitos previos antes de instalar una actualización  

1.  En la consola de Configuration Manager, vaya a **Administración** > **Servicios en la nube** > **Actualizaciones y mantenimiento**.  

2.  Haga clic con el botón derecho en el paquete de actualización para el que desea ejecutar la comprobación de requisitos previos.  

3.  Seleccione **Ejecutar comprobación de requisitos previos**.  Puede ver lo siguiente:  

     Cuando se ejecuta la comprobación de requisitos previos, el contenido de la actualización se replica a los sitios secundarios.  Puede ver el archivo **distmgr.log** en el servidor de sitio para confirmar que el contenido se replica correctamente.  

4.  Para ver los resultados de la comprobación, en la consola de Configuration Manager, vaya a **Supervisión** > **Actualizaciones y estado de mantenimiento** y busque el estado de requisitos previos. También puede consultar el archivo ConfigMgrPrereq.log en el servidor de sitio para obtener más detalles.  



##  <a name="a-namebkmkinstalla-install-in-console-updates"></a><a name="bkmk_install"></a> Instalación de actualizaciones en la consola  
 Cuando esté listo para instalar actualizaciones en la consola de Configuration Manager, comience con el sitio de nivel superior de la jerarquía. Se trata del sitio de administración central o de un sitio primario independiente.  

 Se recomienda planear la instalación de la actualización fuera del horario comercial habitual para cada sitio, ya que será el momento en que el proceso de instalación de la actualización y sus acciones para volver a instalar los componentes del sitio y los roles de sistema de sitio afectarán menos a las operaciones comerciales.  

-   Los sitios primarios secundarios inician la instalación de la actualización automáticamente después de que el sitio de administración central haya terminado de instalarla. Este es el proceso recomendado y predeterminado. En cambio, puede usar [Periodos para tareas administrativas para los servidores de sitio](#bkmk_ServiceWindow) para controlar el momento en que un sitio primario instala actualizaciones.  

-   Debe actualizar manualmente los sitios secundarios desde la consola de Configuration Manager después de que el sitio principal primario haya terminado de instalar la actualización. No se admite la actualización automática de los servidores de sitio secundario.  

-   Cuando se usa una consola de Configuration Manager después de actualizar los sitios, también se le pide que actualice la consola.  

-  Después de que el servidor de sitio completa correctamente la instalación de una actualización, actualiza automáticamente todos los roles de sistema de sitio aplicables.  La única salvedad de esto es para los puntos de distribución:
  - debido a los cambios que se presentaron con la actualización 1606, al instalar una actualización en un sitio que ya ejecuta la versión 1606 o posterior, todos los puntos de distribución ya no se desconectan para actualizar al mismo tiempo. En su lugar, el servidor de sitio usa la configuración de distribución de contenido del sitio para distribuir la actualización a un subconjunto de puntos de distribución a la vez. El resultado es que solo algunos puntos de distribución se desconectan para instalar la actualización. Esto permite a los puntos de distribución que todavía no han comenzado a actualizarse o que han completado la actualización que permanezcan en línea y puedan proporcionar contenido a los clientes.


###  <a name="a-namebkmkoverviewa-overview-of-in-console-update-installation"></a><a name="bkmk_overview"></a> Información general sobre la instalación de actualizaciones en la consola  
**1. Cuando se inicia la instalación de la actualización**  
Aparecerá el asistente para actualizaciones que muestra una lista de las áreas de producto a las que se aplica la actualización.  

-   En la página **General** del asistente, puede configurar **Advertencias de requisitos previos**.  
      -   Los errores de requisitos previos siempre detienen la instalación de la actualización. Debe resolver los errores para poder reintentar la instalación de la actualización de manera satisfactoria. Consulte [Reintento de la instalación de una actualización con errores](#bkmk_retry) para más información.  

    -   Las advertencias de requisitos previos también pueden detener la instalación de la actualización. Debe resolver las advertencias antes de reintentar la instalación de la actualización.   Consulte [Reintento de la instalación de una actualización con errores](#bkmk_retry) para más información.  
    -   Al seleccionar la opción **Pase por alto las advertencias de las comprobaciones de requisitos previos e instale esta actualización aunque falten requisitos**, establece una condición para la instalación de la actualización que omite advertencias de requisitos previos y permite continuar con la instalación de la actualización. Si no selecciona esta opción, la instalación de la actualización se detendrá cuando se produce una advertencia. A menos que ya haya ejecutado la comprobación de requisitos previos y haya resuelto las advertencias de requisitos previos para un sitio, no se recomienda usar esta opción.  

      A partir de la versión 1606, en las áreas de trabajo **Administración** y **Supervisión** , el nodo Actualizaciones y mantenimiento incluye un botón en la cinta de opciones denominada **Omitir advertencias de requisitos previos**. Este botón está disponible cuando se produce un error al completar la instalación de un paquete de actualización debido a las advertencias de comprobación de los requisitos previos.  Por ejemplo, si instala una actualización sin utilizar la opción para omitir las advertencias de requisitos previos (desde el Asistente de actualizaciones), y esa instalación se detiene con un estado de advertencia de requisitos previos, pero sin errores, puede seleccionar más tarde **Omitir advertencias de requisitos previos** en la cinta de opciones para desencadenar una continuación automática de la instalación que, en ese caso, omitirá las advertencias de requisitos previos.  Cuando se utiliza esta opción, la instalación de la actualización continúa automáticamente después de unos minutos.



-   Si se aplica una actualización al cliente de Configuration Manager, se le ofrecerá la opción de probar la actualización de cliente con un conjunto limitado de clientes. Para obtener más información, consulte [Cómo probar las actualizaciones de cliente en una recopilación de preproducción en System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**2. Durante la instalación de la actualización**  
Como parte de la instalación de la actualización, Configuration Manager:  

-   Vuelve a instalar los componentes afectados, como los roles de sistema de sitio o la consola de Configuration Manager.  

-   Administra las actualizaciones de los clientes en función de las selecciones realizadas para las comprobaciones piloto de clientes y para las [actualizaciones de cliente automáticas](https://technet.microsoft.com/library/mt627885.aspx).  

-   No tendrá que reiniciar los servidores de sistema de sitio como parte de la actualización (a menos que esté instalado .NET como parte de un requisito previo para roles de sistema de sitio).  

> [!TIP]  
>  Cuando se instalan actualizaciones, Configuration Manager también actualiza la carpeta CD.Latest que se usa durante la recuperación del sitio.  

**3. Supervisar el progreso de las actualizaciones mientras se instalan**  
Para supervisar el progreso, utilice lo siguiente:  

-   En la consola de Configuration Manager: nodo **Administración** > **Servicios en la nube** > **Actualizaciones y mantenimiento**. En este nodo se muestra el estado de instalación de todos los paquetes de actualización.


-   En la consola de Configuration Manager: nodo **Supervisión** > **Información general** > **Actualizaciones y estado de mantenimiento**. En este nodo se muestra solamente el estado de instalación del paquete de actualización que se esté instalando actualmente.  

    A partir de la versión 1606, la instalación del paquete de actualización se divide en las siguientes fases para facilitar la supervisión. Para cada fase, ahora hay detalles adicionales, incluido el archivo de registro para ver más información:  
    -   **Descargar** (se aplica únicamente al sitio de nivel superior donde está instalado el rol de sistema de sitio del punto de conexión de servicio)
    -   **replicación**
    - **Comprobación de requisitos previos**
    - **Instalación**

-   Puede ver el archivo **CMUpdate.log** en **&lt;ConfigMgr_Installation_Directory>\Logs\\**.  

**4. Cuando se completa la instalación de la actualización**  
Después de que se completa la primera actualización del sitio:  

-   Los sitios primarios secundarios instalarán la actualización automáticamente. No es necesario hacer nada.  

-   Los sitios secundarios deben actualizarse manualmente desde la consola de Configuration Manager.
> [!TIP]
> Aunque la versión de un sitio secundario no se muestre en la consola, puede usar el SDK de Configuration Manager para confirmar la versión de los sitios. Consulte [SMS_Site Server WMI Class](https://technet.microsoft.com/library/hh442832(CMSDK.16).aspx).


-   Hasta el momento en que todos los sitios de la jerarquía estén actualizados a la nueva versión, la jerarquía funciona en modo de versión mixta. Para obtener más información, consulte [Interoperabilidad entre diferentes versiones de System Center Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

**5.   Actualizar consolas de Configuration Manager**  
Una vez que un sitio de administración central o un sitio primario se actualizan, cada consola de Configuration Manager que se conecta a ese sitio también debe actualizarse. Se le pide que actualice una consola:  

-   Cuando abre la consola.  

-   Cuando se desplaza a un nuevo nodo en una consola abierta.  

Se recomienda que instale la actualización inmediatamente y que no la posponga.  

Cuando se complete la actualización de la consola, puede comprobar que la versión de la consola y del sitio es correcta. Vaya a **Acerca de System Center Configuration Manager** en la esquina superior izquierda de la consola, donde se muestra la nueva versión del sitio y la consola.  

###  <a name="a-namebkmktoptiera-to-start-the-update-installation-at-the-top-tier-site"></a><a name="bkmk_toptier"></a> Para iniciar la instalación de la actualización en el sitio de nivel superior  
En el sitio de nivel superior de la jerarquía, en la consola de Configuration Manager, vaya a **Administración** > **Servicios en la nube** > **Actualizaciones y mantenimiento**, seleccione una actualización **Disponible** y haga clic en **Instalar el paquete de actualización**.  

###  <a name="a-namebkmksecondarya-to-start-the-update-installation-at-a-secondary-site"></a><a name="bkmk_secondary"></a> Para iniciar la instalación de la actualización en un sitio secundario  
Una vez que un sitio primario principal de sitios secundarios se actualiza, puede actualizar el sitio secundario desde la consola de Configuration Manager.  Para ello, utilice el **Asistente para actualizar sitios secundarios**.  

1.  En la consola de Configuration Manager, vaya a **Administración** > **Configuración del sitio** > **Sitios**, seleccione el sitio que quiere actualizar y luego, en la pestaña Inicio, en el grupo Sitio, haga clic en **Actualizar**.  

2.  Haga clic en **Sí** para iniciar la actualización del sitio secundario.  

Para supervisar la instalación de la actualización en un sitio secundario, seleccione el servidor del sitio secundario y, luego, en la pestaña Inicio, en el grupo Sitio, haga clic en **Mostrar estado de instalación**. También puede agregar la columna **Versión** a la consola para que pueda ver la versión de cada sitio secundario.  

Después de que un sitio secundario se actualice correctamente, si el estado de la consola no se actualiza o sugiere que la actualización ha producido errores, puede usar la opción **Reintentar instalación**. Esta opción no vuelve a instalar la actualización del sitio secundario que instaló correctamente la actualización, pero hará que la consola actualice el estado.


##  <a name="a-namebkmkretrya-retry-installation-of-a-failed-update"></a><a name="bkmk_retry"></a> Reintento de la instalación de una actualización con errores  
Si no puede instalar una actualización, revise los comentarios en la consola para identificar las soluciones de errores y las advertencias.  También puede consultar el archivo ConfigMgrPrereq.log en el servidor de sitio para obtener más detalles. Antes de reintentar la instalación de una actualización, debe resolver los errores y las advertencias.  

Cuando esté listo para volver a intentar la instalación de una actualización, seleccione la actualización con errores y elija una opción adecuada. El comportamiento del reintento de instalación de la actualización depende del nodo desde el que inicia el reintento y la opción de reintento que utiliza:  

1.  **Vuelva a intentar la instalación en la jerarquía:**  
Puede volver a intentar la instalación de una actualización en toda la jerarquía si la actualización presenta alguno de los estados siguientes:  

    -   La comprobación de requisitos previos se realiza satisfactoriamente con una o varias advertencias, y la opción para ignorar las advertencias de la comprobación de requisitos previos no estaba configurada en el asistente de actualizaciones; el valor de las actualizaciones para **Ignorar advertencia sobre requisitos previos** en el nodo Actualizaciones y mantenimiento es **No**.   
    -   Errores en la comprobación de requisitos previos    
    -   Error de instalación
    -   Error en la replicación del contenido en el sitio   

    Vaya a **administración** > **Servicios en la nube** > **Actualizaciones y mantenimiento**, seleccione la actualización y haga clic en uno de los siguientes:  

    -   **Reintentar** : al ejecutar Reintentar desde este nodo, la instalación de la actualización vuelve a empezar, y omitirá automáticamente las advertencias de requisitos previos. También volverá a replicar el contenido para la actualización si no se pudo realizar la replicación previamente.
    - **Omitir advertencias de requisitos previos** : a partir de la versión 1606, si se detiene la instalación de la actualización debido a una advertencia, puede hacer clic en Omitir advertencias de requisitos previos. Esta acción reinicia la instalación de la actualización y utiliza la opción para ignorar las advertencias de requisitos previos.   

2.  **Vuelva a intentar la instalación en el sitio:**  
 Puede volver a intentar la instalación de una actualización en un sitio específico si la actualización presenta alguno de los estados siguientes:  

    -   La comprobación de requisitos previos se realiza satisfactoriamente con una o varias advertencias, y la opción para ignorar las advertencias de la comprobación de requisitos previos no estaba configurada en el asistente de actualizaciones; el valor de las actualizaciones para **Ignorar advertencia sobre requisitos previos** en el nodo Actualizaciones y mantenimiento es **No**.  
    -   Errores en la comprobación de requisitos previos    
    -   Error de instalación    

    Vaya a **Supervisión** > **Introducción** > **Site Servicing Status**(Estado de mantenimiento del sitio), seleccione la actualización y haga clic en uno de los siguientes:

       - **Reintentar** : al ejecutar Reintentar desde este nodo, se reinicia la instalación de la actualización solo en ese sitio. A diferencia de ejecutar Reintentar en el nodo Actualizaciones y mantenimiento, este reintento no omite las advertencias de requisitos previos.
       -    **Omitir advertencias de requisitos previos** : a partir de la versión 1606, si se detiene la instalación de la actualización debido a una advertencia, puede hacer clic en Omitir advertencias de requisitos previos. Esta acción reinicia la instalación de la actualización y utiliza la opción para ignorar las advertencias de requisitos previos.

##  <a name="a-namebkmkaftera-after-a-site-installs-an-update"></a><a name="bkmk_after"></a> Después de que un sitio instala una actualización  
Use la siguiente lista de comprobación para completar tareas comunes y configuraciones que se realizan después de las actualizaciones de un sitio:  

**Confirme que la replicación de sitio a sitio está activa:** en la consola de Configuration Manager, vaya a las siguientes ubicaciones para ver el estado y asegurarse de que la replicación está activa:  

-   **Supervisión** > **Introducción** > **Jerarquía del sitio**  

-   **Supervisión** > **Introducción** > **Replicación de base de datos**  

Para obtener más información, consulte [Supervisar la infraestructura de la jerarquía y replicación de System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) y [Acerca de Replication Link Analyzer](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA).  

 **Confirme si los servidores de sitio y los servidores del sistema de sitio remoto se han reiniciado (si es necesario):** revise la infraestructura de sitio y asegúrese de que los servidores de sitio aplicables y los servidores de sistema de sitio (remotos desde el servidor de sitio) se han reiniciado correctamente.  Normalmente, esto se espera solo si Configuration Manager instala .NET como un requisito previo para un rol de sistema de sitio.  

 **Actualice consolas independientes de Configuration Manager:** asegúrese de que todas las consolas remotas de Configuration Manager se actualizan a la misma versión. Se le pide que actualice una consola:  

-   Cuando se desplaza a un nuevo nodo en la consola.  

-   Cuando abre la consola.  

**Vuelva a configurar réplicas de base de datos para puntos de administración en sitios primarios:** si utiliza réplicas de base de datos para puntos de administración en sitios primarios, debe desinstalar las réplicas de base de datos antes de actualizar el sitio. Después de actualizar un sitio primario, vuelva a configurar la réplica de base de datos de los puntos de administración. Para obtener más información, consulte [Réplicas de bases de datos para puntos de administración de System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Vuelva a configurar todas las tareas de mantenimiento de base de datos deshabilitadas antes de la actualización:** si deshabilitó [Tareas de mantenimiento para System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) de la base de datos en un sitio antes de la actualización, vuelva a configurar esas tareas en el sitio con la misma configuración que había antes de la actualización.  

**Actualizar clientes:** para obtener más información sobre cómo actualizar clientes existentes y cómo instalar nuevos clientes, consulte [Actualizar clientes de equipos Windows con System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

**Configuraciones adicionales:** revise los cambios realizados antes de iniciar la actualización y restaure esas configuraciones a sus sitios y jerarquías.  

##  <a name="a-namebkmkoptionsa-enable-optional-features-from-updates"></a><a name="bkmk_options"></a> Habilitar características opcionales de las actualizaciones  
Cuando instala una actualización que incluye una o más características opcionales, tendrá la oportunidad de habilitarlas en la jerarquía.  Puede hacerlo en el momento en que instala la actualización, o bien volver a la consola en un momento posterior y habilitar las características opcionales.

Para ver las características disponibles y su estado, en la consola, vaya a **Administración** > **Servicios en la nube** > **Actualizaciones y mantenimiento** > **Características**.

Cuando una característica no es opcional, se instala automáticamente y no aparece en el nodo **Características** .  

##  <a name="a-namebkmkprereleasea-use-pre-release-features-from-updates"></a><a name="bkmk_prerelease"></a> Uso de las características de versión preliminar de las actualizaciones
A partir de la versión 1606, debe dar su consentimiento para usar características de la versión preliminar de System Center Configuration Manager antes de poder seleccionarlas y permitir su uso.  

Se incluyen características de versión preliminar en el producto para la realización de las primeras pruebas en un entorno de producción, pero no se debe considerar que ya estén listas para él.

Para dar su consentimiento, en la consola vaya a **Administración** > **Configuración de sitio** > **Sitios**y seleccione **Configuración de jerarquía**. En la pestaña **General** , seleccione **Consentimiento para usar características de versiones preliminares**.
 -  Dar el consentimiento es una acción que se realiza una sola vez por jerarquía y que no se puede deshacer.  
 -  Hasta que dé su consentimiento, no puede habilitar nuevas características de una versión preliminar incluidas con las versiones de actualización 1606 o posteriores.

 > [!NOTE]
 > Si ha habilitado características de versiones preliminares desde la actualización 1602 antes de instalar la actualización 1606, esas características permanecerán habilitadas para su uso después de instalar 1606, aunque no dé su consentimiento para utilizarlas.

Cuando la jerarquía ejecuta la versión 1606 o posterior y, a continuación, instala una actualización que incluye características de versiones preliminares, dichas características están visibles en el Asistente de actualizaciones y mantenimiento con las características normales incluidas en la actualización:
  - **Si ha dado su consentimiento:** puede habilitar las características de versiones preliminares en el Asistente de actualizaciones y mantenimiento al instalar la actualización. Para ello, seleccione las características de versiones preliminares como lo haría con cualquier otra característica.     

    Opcionalmente, puede esperar a habilitar una característica de la versión preliminar posteriormente desde el nodo **Administración** > **Servicios en la nube** > **Actualizaciones y mantenimiento** > **Características** de la consola. Para ello, en el nodo Características, seleccione la característica y haga clic en **Activar**. (Esta opción aparece atenuada y no está disponible hasta que dé su consentimiento).  
  -   **Si no ha dado su consentimiento:** al instalar una actualización, las características de versiones preliminares están visibles en el Asistente de actualizaciones y mantenimiento, pero están atenuadas y no se pueden habilitar. Una vez instalada la actualización, puede ver estas características en el nodo Características, pero no puede habilitarlas hasta después de dar su consentimiento en Configuración de jerarquía.

 > [!TIP]
 > Al instalar la actualización 1606, las características de versiones preliminares que se incluyen con ella no están visibles en el Asistente de actualizaciones y mantenimiento y no se pueden habilitar en ese momento. Después de instalar la actualización 1606, puede ver las características de las versiones preliminares que se incluyen en el nodo Características.

Si proporcionó consentimiento en un sitio primario independiente y, después, expande la jerarquía mediante la instalación de un nuevo sitio de administración central, entonces debe proporcionar consentimiento de nuevo en el sitio de administración central.

**Las siguientes características de versión preliminar están disponibles:**

 |Característica                    |Agregado como versión preliminar |Agregado como característica completa |  
|----------------------------|---------------------|------------------------|
| Conector de Microsoft Operations Management Suite (OMS)  | [Versión 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![Todavía no](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Mantenimiento de una recopilación compatible con clústeres (Dar servicio a un grupo de servidores).| [Versión 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#bkmk_servergroups)|![Todavía no](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|Acceso condicional para equipos administrados por System Center Configuration Manager | [Versión 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     |![Todavía no](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)                        |




##  <a name="a-namebkmkservicewindowa-service-windows-for-site-servers"></a><a name="bkmk_ServiceWindow"></a> ventanas de servicio para los servidores de sitio  
En un servidor de sitio, puede configurar períodos para tareas administrativas para controlar cuándo se pueden aplicar actualizaciones de infraestructura para Configuration Manager en ese servidor de sitio.  Cada servidor de sitio admite varias ventanas, con la ventana permitida para la instalación de actualizaciones de infraestructura que están determinadas por una combinación de todas las ventanas configuradas para ese servidor de sitio.  

**Cómo configurar una ventana de servicio:**  

1.  En la consola de Configuration Manager, abra **Administración** > **Configuración del sitio** > **Sitios** y seleccione el servidor de sitio en el que quiere configurar un periodo para tareas administrativas.  

2.  A continuación, modifique las **Propiedades** de los servidores de sitio y seleccione la pestaña **Ventana de servicio** , donde puede establecer una o varias ventanas de servicio para ese servidor de sitio.  

##  <a name="a-namebkmkfaqa-why-dont-i-see-certain-updates-in-my-console"></a><a name="bkmk_faq"></a> ¿Por qué no se ven determinadas características en la consola?  
 Si no encuentra una actualización específica o todas las actualizaciones en la consola después de una sincronización correcta con el servicio en la nube de Microsoft, esto podría deberse a que:  

-   La actualización requiere una configuración que no utiliza la infraestructura o la versión de producto actual no cumple un requisito previo para recibir la actualización.  

     Si cree que tiene las configuraciones necesarias o cumple otros requisitos previos para una actualización que falta, confirme que su punto de conexión de servicio está en modo en línea y luego utilice la opción **Buscar actualizaciones** en el nodo Actualizaciones y mantenimiento para forzar una comprobación.  Si está establecido el modo sin conexión, debe usar la herramienta de conexión de servicio para realizar manualmente la sincronización con el servicio en la nube.  

-   La cuenta no dispone de los permisos de administración basada en roles correctos para ver las actualizaciones en la consola de Configuration Manager.

    Consulte [Permisos para administrar actualizaciones](../../../core/servers/manage/install-in-console-updates.md#Permissions-to-view-and-manage-updates-and-features) en este tema para obtener información sobre los permisos necesarios para ver las actualizaciones y habilitar las características desde la consola.



<!--HONumber=Nov16_HO1-->

