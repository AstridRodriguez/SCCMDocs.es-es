---
title: Crear e implementar una directiva de cumplimiento de dispositivos | Microsoft Docs
description: "Obtenga información sobre cómo crear e implementar directivas de cumplimiento de dispositivos en System Center Configuration Manager."
ms.custom: na
ms.date: 11/15/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0cba232e-319f-4ae6-9ffa-4cd76c8bcb29
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
robots: noindex
translationtype: Human Translation
ms.sourcegitcommit: c13c6268fa76ade7feb0981f9c4a6e325e393aca
ms.openlocfilehash: 4cc7148be602367b579d63535a4938919bacf829

---

# <a name="create-and-deploy-a-device-compliance-policy"></a>Crear e implementar una directiva de cumplimiento de dispositivos

*Se aplica a: System Center Configuration Manager (rama actual)*


## <a name="create-a-compliance-policy"></a>Crear una directiva de cumplimiento

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.

2.  En el área de trabajo **Activos y compatibilidad** , expanda **Configuración de cumplimiento**y, a continuación, haga clic en **Directivas de cumplimiento**.

3. En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear directiva de cumplimiento**.

4. En la página **General** del **Asistente para crear directivas de cumplimiento**, especifique la información siguiente:

  * **Nombre**: escriba un nombre único para la directiva de cumplimiento. Puede utilizar un máximo de 256 caracteres.
  * **Descripción**: escriba una descripción general del perfil de VPN que ayude a identificarlo en la consola de Configuration Manager. Puede utilizar un máximo de 256 caracteres.
  * **Tipo de directiva de cumplimiento**: seleccione el tipo de directiva que quiere crear en función de si Configuration Manager administra el dispositivo. **Se aplica a la versión o posterior**.<br /><br /> En el caso de dispositivos administrados por Intune, elija la opción **Reglas de compatibilidad para dispositivos administrados sin el cliente de Configuration Manager** .  Al seleccionar esta opción, también puede seleccionar el tipo de plataforma a la que quiere que se aplique esta directiva.
  * **Gravedad de no compatibilidad para informes**: especifique el nivel de gravedad que indica si esta directiva de cumplimiento se evalúa como no compatible. Los niveles de gravedad disponibles son los siguientes:<br /><br />
    * **Ninguno**: los dispositivos que no cumplan esta regla de compatibilidad no notificarán ninguna gravedad de error en los informes de Configuration Manager.
    *  **Información**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Información** en los informes de Configuration Manager.   
    * **Advertencia**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Advertencia** en los informes de Configuration Manager.
    * **Crítico**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Crítico** en los informes de Configuration Manager.
    * **Crítico con evento**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Crítico** en los informes de Configuration Manager. Este nivel de gravedad también se registra como evento de Windows en el registro de eventos de la aplicación.|      

5.  En la página **Plataformas admitidas** , elija las plataformas de dispositivo en las que se va a evaluar esta directiva de cumplimiento o haga clic en **Seleccionar todo** para elegir todas las plataformas de dispositivo.

6.  En la página **Reglas** , se establecen una o varias reglas que definen la configuración que los dispositivos deben tener para poder ser evaluados como compatibles. Cuando se crea una directiva de cumplimiento, algunas de las reglas se habilitan de forma predeterminada, pero puede editarlas o eliminarlas. Para obtener una lista completa de todas las reglas, consulte la sección **Reglas de directivas de cumplimiento** más adelante en este tema.

> [!NOTE]  
>  En equipos con Windows, la versión 8.1 del sistema operativo Windows se notifica como 6.3 en lugar de 8.1.    Si la regla de la versión de SO se establece en Windows 8.1 para Windows, el dispositivo se notificará como no compatible incluso aunque tenga Windows OS 8.1. Asegúrese de que está estableciendo la versión **notificada** correcta de Windows para las reglas de SO mínimo y máximo. El número de versión debe coincidir con la versión devuelta por el comando winver. Windows Phone no tiene este problema, ya que la versión se notifica como 8.1 según lo previsto.  
>   
>  En equipos con sistema operativo Windows 10, la versión debe establecerse en "10.0" + el número de compilación del sistema operativo devuelto por el comando winver. Por ejemplo, podría ser similar a 10.0.10586.  
> Windows 10 Mobile no tiene este problema.  
>   
>  ![CA&#95;Win10OSversion](../media/CA_Win10OSversion.png)  

7.  En la página **Resumen** del asistente, revise la configuración realizada y, a continuación, complete el asistente.

 La nueva directiva se muestra en el nodo **Directivas de cumplimiento** del área de trabajo **Activos y compatibilidad** .

## <a name="deploy-a-compliance-policy"></a>Implementar una directiva de cumplimiento

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.

2.  En el área de trabajo **Activos y compatibilidad** , expanda **Configuración de cumplimiento**y, a continuación, haga clic en **Directivas de cumplimiento**.

3.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Implementar**.

4.  En el cuadro de diálogo **Implementar directiva de cumplimiento** , haga clic en **Examinar** para seleccionar la recopilación de usuarios en la que se va a implementar la directiva.

     Además, puede seleccionar opciones para generar alertas cuando la directiva no es compatible y también para configurar la programación por medio de la cual se evaluará esta directiva para el cumplimiento.

5.  Cuando haya terminado, haga clic en **Aceptar**.

## <a name="monitor-the-compliance-policy"></a>Supervisar la directiva de cumplimiento

### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Para ver los resultados de compatibilidad en la consola de Configuration Manager

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.

2.  En el área de trabajo **Supervisión** , haga clic en **Implementaciones**.

3.  En la lista **Implementaciones** , seleccione la implementación de directiva de cumplimiento para la que desea revisar la información de compatibilidad.

4.  Puede revisar la información de resumen sobre la compatibilidad de la implementación de la directiva en la página principal. Para ver información más detallada, seleccione la implementación y, a continuación, en la pestaña **Inicio** del grupo **Implementación** , haga clic en **Ver estado** para abrir la página **Estado de implementación** .

     La página **Estado de implementación** contiene las siguientes pestañas:

    -   **Compatible**: muestra la compatibilidad de la directiva en función del número de activos afectados. Puede hacer clic en una regla para crear un nodo temporal en el nodo **Usuarios** o **Dispositivos** en el área de trabajo **Activos y compatibilidad** , que contiene todos los usuarios o dispositivos compatibles con esta regla. En el panel **Detalles del activo** se muestran los usuarios o los dispositivos compatibles con la directiva. Haga doble clic en un usuario o dispositivo de la lista para mostrar información adicional.

    -   **Error**: muestra una lista de todos los errores de la implementación de directiva seleccionada, en función del número de activos afectados. Puede hacer clic en una regla para crear un nodo temporal en el nodo **Usuarios** o **Dispositivos** , en el área de trabajo **Activos y compatibilidad** , que contiene todos los usuarios o los dispositivos que generaron errores con esta regla. Cuando se selecciona un usuario o dispositivo, el panel **Detalles del activo** muestra los usuarios o dispositivos afectados por el problema seleccionado. Haga doble clic en un dispositivo o usuario de la lista para mostrar información adicional sobre el problema.

    -   **No compatible**: muestra una lista de todas las reglas no compatibles en la directiva en función del número de activos afectados. Puede hacer clic en una regla para crear un nodo temporal en el nodo **Usuarios** o **Dispositivos** en el área de trabajo **Activos y compatibilidad** , que contiene todos los usuarios o los dispositivos no compatibles con esta regla. Cuando se selecciona un usuario o dispositivo, el panel **Detalles del activo** muestra los usuarios o dispositivos afectados por el problema seleccionado. Haga doble clic en un usuario o dispositivo de la lista para mostrar información adicional sobre el problema.

    -   **Desconocido**: muestra una lista de todos los usuarios y dispositivos que no notificaron la compatibilidad de la implementación de directiva seleccionada y el estado de cliente actual de los dispositivos.

### <a name="to-view-intune-compliance-policies-charts"></a>Para ver los gráficos de directivas de cumplimiento de Intune
1. A partir de la versión 1610 de Configuration Manager, en la consola de Configuration Manager, haga clic en **Supervisión**.
2. En el área de trabajo **Supervisión**, vaya a **Información general** > **Configuración de cumplimiento** >  **Directivas de cumplimiento**.
3. Se muestran los gráficos siguientes:
    - **Cumplimiento general de dispositivos**: muestra el cumplimiento general de los dispositivos de todas las directivas de cumplimiento.
    - **Razones principales de no cumplimiento**: muestra las directivas principales por las que los dispositivos son no conformes.
4. Haga clic en una sección del gráfico para explorar en profundidad una lista de los dispositivos de esa categoría.

### <a name="to-view-a-health-attestation-report"></a>Para ver un informe de atestación de estado

1.  **A partir de la versión 1602 de Configuration Manager**, en la consola de Configuration Manager, haga clic en **Supervisión**.

2.  Para ver un informe de resumen del estado actual de los dispositivos por su estado de compatibilidad, haga clic en **Seguridad**. A continuación, haga clic en **Atestación de estado**.

3.  Para ver un informe que muestre todos los dispositivos y todos los atributos de atestación de estado, haga clic en **Seguridad**. A continuación, haga clic en **Atestación de estado**.

## <a name="compliance-policy-rules"></a>Reglas de directivas de cumplimiento
* **Requerir configuración de contraseña en dispositivos móviles:** exija a los usuarios que escriban una contraseña para poder obtener acceso al dispositivo.

  **Compatible con:**
    * Windows Phone 8+
    * iOS 6+
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
* **Requerir contraseña para desbloquear un dispositivo inactivo (actualización 1602):** exija a los usuarios que escriban una contraseña para obtener acceso a un dispositivo bloqueado.

  **Compatible con:**
  * Windows Phone 8+
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Minutos de inactividad antes de que sea necesaria la contraseña (actualización 1602):** especifica el tiempo de inactividad antes de que el usuario deba volver a escribir su contraseña. Establezca el valor en una de las opciones disponibles: **1 minuto**, **5 minutos**, **15 minutos**, **30 minutos**, **1 hora**.

  Esta regla se debe usar con la regla **Requerir una contraseña para desbloquear un dispositivo inactivo**. El valor establecido aquí determina cuándo se considera que el dispositivo está inactivo y se bloquea. Si  **Requerir una contraseña para desbloquear un dispositivo inactivo** está establecida en **True**, se exige al usuario que escriba una contraseña para acceder al dispositivo bloqueado.

  **Compatible con:**
  * Windows Phone 8+
  * Windows RT/8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Requerir actualizaciones automáticas (actualización 1602):** puede exigir que los dispositivos con Windows 8.1 o versiones posteriores instalen de forma automática actualizaciones y especificar de qué clase.

  El valor debe establecerse en **Ninguno** para evitar la instalación automática, en **Recomendado** para instalar automáticamente todas las actualizaciones recomendadas, o en **Importante** para instalar solo las actualizaciones clasificadas como importantes.

  **Compatible con:**
  * Windows Phone 8+

* **Permitir contraseñas sencillas:** permita a los usuarios crear contraseñas sencillas como "1234" o "1111". Esta configuración está **deshabilitada de manera predeterminada**.

  **Compatible con:**
  * Windows Phone 8+
  * iOS 6+

* **Longitud mínima de la contraseña:** especifica el número mínimo de dígitos o caracteres que debe contener la contraseña del usuario (**6** de manera predeterminada).

  **Compatible con:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  >[!NOTE]
  >En los dispositivos que ejecutan Windows y están protegidos con una cuenta de Microsoft, la directiva de cumplimiento no podrá evaluarse correctamente si la **longitud mínima de la contraseña** es superior a 8 caracteres o el **número mínimo de conjuntos de caracteres** es superior a 2.

* **Cifrado de archivos en dispositivos móviles:** requiere que el dispositivo esté cifrado para conectarse a los recursos. Los dispositivos que ejecutan **Windows Phone 8** se **cifran de forma automática**. Los dispositivos que ejecutan **iOS** se cifran al configurar la opción **Requerir configuración de contraseña en dispositivos móviles** (habilitada de forma predeterminada).

  **Compatible con:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **El dispositivo no debe tener Jailbreak o rooting:** si se habilita, los dispositivos con Jailbreak (iOS) o rooting (Android) no serán compatibles (deshabilitada de forma predeterminada).

  **Compatible con:**
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **Intune debe administrar el perfil de correo electrónico:** cuando esta opción está establecida en Sí, el dispositivo debe usar el perfil de correo electrónico implementado en el dispositivo. El dispositivo se considerará no compatible si el perfil de correo electrónico no está implementado en el mismo grupo de usuarios que el grupo de usuarios al que va dirigida la directiva de compatibilidad.

  También será no compatible si el usuario ya ha configurado en él una cuenta de correo electrónico que coincide con el perfil de correo electrónico de Intune implementado en dicho dispositivo. En este caso, Intune no puede sobrescribir el perfil implementado por el usuario y, por tanto, no puede administrarlo. Para que el dispositivo sea compatible, el usuario puede eliminar la configuración de correo electrónico existente, lo que permitirá a Intune instalar el perfil de correo electrónico administrado.

  Para obtener información sobre los perfiles de correo electrónico, consulte [Habilitar el acceso al correo electrónico corporativo mediante perfiles de correo electrónico con Microsoft Intune](https://technet.microsoft.com/library/dn800672.aspx). Esta configuración está deshabilitada de manera predeterminada.

  **Compatible con:**
  * iOS 6+

* **Perfil de correo electrónico:** si se selecciona la opción **Intune debe administrar la cuenta de correo electrónico**, haga clic en **Seleccionar** para elegir el perfil de correo mediante el cual deben administrarse los dispositivos. El perfil de correo electrónico debe estar presente en el dispositivo.

  **Compatible con:**
  * iOS 6+

* **SO mínimo requerido:** cuando un dispositivo no cumpla el requisito de versión de SO mínima, se notificará como no compatible. Se mostrará un vínculo con información sobre cómo realizar la actualización. El usuario final puede optar por actualizar el dispositivo, tras lo cual podrá acceder a los recursos de la empresa.

  **Compatible con:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **Versión de SO máxima permitida:** cuando un dispositivo usa una versión de SO posterior a la especificada en la regla, se bloquea el acceso a los recursos de la empresa y se le pide al usuario que se ponga en contacto con el administrador de TI. Mientras no se cambie la regla para permitir la versión de SO, este dispositivo no podrá usarse para acceder a los recursos de la empresa.

  **Compatible con:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **Requerir que se informe del estado correcto de los dispositivos (actualización 1602):** puede establecer una regla para exigir que se informe del mantenimiento correcto de los dispositivos Windows 10 en las directivas de cumplimiento nuevas o existentes. Si habilita esta configuración, los dispositivos Windows 10 se evaluarán a través del servicio de atestación de estado (HAS) con respecto a los siguientes puntos de datos:
 - **BitLocker está habilitado:** cuando Bitlocker está activado, el dispositivo puede proteger los datos almacenados en la unidad frente al acceso no autorizado cuando el sistema está apagado o entra en estado de hibernación.

   El Cifrado de unidad BitLocker de Windows cifra todos los datos almacenados en el volumen del sistema operativo Windows. BitLocker usa el TPM como ayuda para proteger el sistema operativo Windows y los datos de usuario, y contribuye a garantizar que un equipo no ha sido manipulado aunque se deje desatendido, se pierda o se lo roben.<br />Si el equipo está equipado con un TPM compatible, BitLocker usa este para bloquear las claves de cifrado que protegen los datos. Como resultado, las claves no son accesibles hasta que el TPM ha comprobado el estado del equipo.
  - **La integridad de código está habilitada:** la integridad de código es una característica que valida la integridad de un controlador o un archivo del sistema cada vez que se carga en memoria. Detecta si se está cargando en el kernel un controlador o un archivo del sistema sin firma, o si un archivo del sistema ha sido objeto de alteraciones por parte de software malintencionado que se ejecuta mediante una cuenta de usuario con privilegios elevados.
  - **El arranque seguro está habilitado:** cuando el arranque seguro está habilitado, se obliga al sistema a arrancar en un estado de fábrica de confianza. Además, cuando el arranque seguro está habilitado, los componentes principales que se utilizan para arrancar el equipo deben tener las firmas de cifrado correctas en las que confía la organización que ha fabricado el dispositivo. El firmware UEFI comprueba esto antes de permitir que se inicie el equipo. Si los archivos han sido alterados, se ha vulnerado la forma, el sistema no arrancará.
  - **El antimalware de inicio temprano está habilitado (esta configuración solo se aplica a los equipos):** el antimalware de inicio temprano (ELAM) proporciona protección para los equipos de la red cuando se inician y antes de que se inicialicen los controladores de terceros.<br />Esta regla está desactivada de forma predeterminada.

  Para más información sobre cómo funciona el servicio HAS, consulte [Health Attestation CSP](https://msdn.microsoft.com/library/dn934876.aspx)(CSP de atestación de estado).
  **Compatible con:**
  * Windows 10 y Windows 10 Mobile



<!--HONumber=Dec16_HO3-->

