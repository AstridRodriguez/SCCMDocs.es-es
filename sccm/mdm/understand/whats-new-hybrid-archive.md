---
title: "Archivo de novedades de MDM híbrido | Microsoft Docs"
description: "Archivo de características anteriores de administración de dispositivos móviles disponibles para implementaciones híbridas con System Center Configuration Manager e Intune."
ms.custom: na
ms.date: 10/25/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: Mtillman
ms.author: mtillman
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: bd870d66bb1a482cb5985f1fc0fe66a7dee206eb
ms.openlocfilehash: d286b038c900873154d3a0761aa1eaface47e186

---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>Características híbridas anteriores con System Center Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (rama actual)*

En este artículo se proporciona información sobre características anteriores de administración de dispositivos móviles (MDM) disponibles para implementaciones híbridas con System Center Configuration Manager y Microsoft Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilidad con versiones de Configuration Manager  

 En cada sección de este artículo se enumeran las características híbridas organizadas en tres categorías diferentes. Use las indicaciones siguientes para determinar la compatibilidad de las características de cada categoría con las diferentes versiones de Configuration Manager:  

|Categorías de características|
|-|  
|**Novedades de Microsoft Intune**: en general, todas las características que se enumeran en esta categoría deberían funcionar con todas las versiones de Configuration Manager, incluidas las versiones de System Center 2012 R2 Configuration Manager, ya que estas características solo necesitan el servicio de Intune y ninguna función adicional en Configuration Manager.<br /><br /> **Novedades de Configuration Manager Technical Preview**: todas las características que se enumeran en esta categoría funcionan únicamente con la versión especificada de Technical Preview. Para probar estas características, debe instalar la versión de Technical Preview especificada en la descripción de la característica. Para obtener más información, consulte [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) (Technical Preview para System Center Configuration Manager).<br /><br /> **Novedades de Configuration Manager (rama actual)**: todas las características que se enumeran en esta categoría funcionan únicamente con la versión especificada de Configuration Manager (rama actual), como la versión 1511 o 1602. Si usa una versión anterior de Configuration Manager para su implementación híbrida, debe actualizar a la versión de Configuration Manager (rama actual) que se especifica en la descripción de la característica. Para obtener más información, consulte [Upgrade to System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md) (Actualizar a System Center Configuration Manager).|  

## <a name="new-hybrid-features-in-october-2016"></a>Nuevas características híbridas de octubre de 2016

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

Las siguientes características de Intune que se incorporaron en octubre de 2016 funcionan en implementaciones híbridas.

- **Acceso condicional para la administración de aplicaciones móviles**

  Puede restringir el acceso a Exchange Online de forma que el acceso solo proceda de aplicaciones que admitan las directivas de administración de aplicaciones móviles de Intune, como Outlook. [Esta nueva característica](/intune/deploy-use/allow-policy-managed-apps-access-to-o365) se adapta perfectamente a las directivas de administración de aplicaciones móviles (MAM) de Intune, ya que puede bloquear el acceso a los clientes de correo integrado u otras aplicaciones que no se hayan configurado con las directivas de MAM de Intune. Esto garantiza que los usuarios accedan a los datos de la organización con aplicaciones que pueden estar protegidas mediante MAM de Intune. Puede empezar a trabajar en la administración de aplicaciones móviles de Intune mediante Azure Portal. Busque la nueva sección de acceso condicional en la hoja "Configuración".

-   **Herramienta de ajuste de aplicaciones Intune para Android**

  Puede habilitar las aplicaciones para que usen directivas de administración de aplicaciones móviles (MAM) de Intune mediante la herramienta de ajuste de aplicaciones de Intune.

- **Compatibilidad de Android Samsung KNOX Standard con Intune**

  Determinados modelos del teléfono Samsung Galaxy Ace no pueden administrarse con Intune como los dispositivos Samsung KNOX Standard. Cuando inscriba estos dispositivos con Intune, se administrarán como dispositivos estándar de Android.

  Los números de los modelos afectados son:

  - SM-G313HU
  - SM-G313HY
  - SM-G313M
  - SM-G313MY
  - SM-G313U

  Ni usted ni los usuarios finales deben realizar ninguna otra acción. Para obtener más información, visite el sitio web de Samsung KNOX.

### <a name="new-in-configuration-manager-technical-preview-1610"></a>Novedades de Configuration Manager Technical Preview 1610

Se han incorporado las siguientes características híbridas nuevas en octubre de 2016 para Configuration Manager Technical Preview 1610.

- **Solicitar la sincronización de directivas desde la consola de administración**

  Puede solicitar la sincronización de directivas en un dispositivo móvil inscrito desde la consola de Configuration Manager, en lugar de solicitar la sincronización en la aplicación de portal de empresa en el propio dispositivo. Se trata de una acción nueva denominada **Send Sync Request** (Enviar solicitud de sincronización) del menú Acciones de dispositivo remoto, que aparece en la cinta de opciones cuando se selecciona un dispositivo móvil en el nodo Dispositivos.

- **Opciones de configuración de Windows Defender**

  Ahora puede establecer la configuración de cliente de Windows Defender en equipos Windows 10 inscritos en Intune mediante elementos de configuración de la consola de Configuration Manager. Hay un nuevo grupo de configuración denominado **Windows Defender** en el Asistente para elemento de configuración. Tenga en cuenta que esto solo se admite en Windows 10 versión 1511 y superiores.


### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)

No se ha incorporado ninguna característica híbrida nueva en agosto de 2016 para Configuration Manager (rama actual).

## <a name="new-hybrid-features-in-september-2016"></a>Nuevas características híbridas de septiembre de 2016

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

Las siguientes características de Intune que se incorporaron en septiembre de 2016 funcionan en implementaciones híbridas.

- **Adición de "Notificaciones" en el portal de empresa para Android**

  Se ha agregado un nuevo icono Notificaciones al Portal de empresa para Android en la página principal. Al seleccionar este icono se obtiene acceso a la página Notificaciones, que muestra a todos los usuarios todos los elementos que requieren atención en la aplicación del Portal de empresa, como la falta de conformidad del dispositivo, la actualización de la inscripción o la activación de la inscripción. La aplicación del Portal de empresa de iOS ya tiene esta experiencia en notificaciones. Tener la nueva página Notificaciones significa que el usuario no verá la página Configuración de acceso de la empresa cada vez que inicien o reanuden el Portal de empresa siempre que el dispositivo ya esté inscrito. Si crea su propia guía de usuario final, es posible que quiera actualizar la documentación para reflejar este cambio. Busque las capturas de pantalla actualizadas [aquí](https://aka.ms/androidcpupdate).

- **Cambios en la compatibilidad de la aplicación de portal de empresa de iOS**

  Ahora, todos los usuarios de la aplicación de portal de empresa de Microsoft Intune para iOS tendrán que usar la versión más reciente. Los usuarios nuevos solo podrán descargar la versión más reciente y los usuarios actuales tendrán que llevar a cabo la actualización. La versión más reciente requiere iOS 8.0 o posterior, de modo que los dispositivos que ejecutan versiones anteriores de iOS no podrán usar el portal de empresa o inscribirse hasta que actualicen su dispositivo a iOS 8.0 o posterior y, después, actualicen la aplicación de portal de empresa a la versión más reciente. Los dispositivos inscritos que ejecutan versiones anteriores a iOS 8.0 seguirán administrándose y apareciendo en la consola de administración de Intune.

- **Botón de comentarios agregado a la aplicación de portal de empresa de Windows Phone 8.1**

  La aplicación de Portal de empresa de Windows Phone 8.1 permite a los usuarios finales pueden enviar comentarios acerca de la aplicación mediante un nuevo botón "Enviar comentarios". Para buscar el botón, los usuarios seleccionan el menú de "tres puntos" en la parte inferior derecha de la pantalla de la aplicación de Portal de empresa y, a continuación, seleccionan **Enviar comentarios**. Los comentarios recopilados y anónimos ayudarán a Microsoft a mejorar la experiencia de la aplicación del Portal de empresa para los usuarios.

### <a name="new-in-configuration-manager-technical-preview-1609"></a>Novedades de Configuration Manager Technical Preview 1609

Se han incorporado las siguientes características híbridas nuevas en septiembre de 2016 para Configuration Manager Technical Preview 1609.

- **Configuración adicional y una mejor experiencia para la configuración de elementos de configuración**

  Se han agregado opciones nuevas para Windows, iOS y Android. Además, solo se muestran en el asistente las opciones que se aplican a las plataformas que seleccione en la página Plataformas compatibles. Para obtener más información, consulte [New compliance settings for configuration items in TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#new-compliance-settings-for-configuration-items) (Nueva configuración de cumplimiento para elementos de configuración en TP 1609).

- **Configuración adicional para perfiles DEP**

  Se han agregado TouchID, ApplePay y Zoom como opciones configurables en perfiles DEP para dispositivos iOS.

- **Aplicaciones de pago en la Tienda Windows para empresas**

  Ahora puede agregar aplicaciones de pago y gratuitas en la Tienda Windows para empresas e implementarlas en los usuarios de la organización. Para obtener más información, consulte [Enhancements to Windows Store for Business in TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#enhancements-to-windows-store-for-business-integration-with-configuration-manager) (Mejoras en la Tienda Windows para empresas en TP 1609).

- **Tipos de conexión nativos para perfiles de VPN de Windows 10**

  Ahora, puede crear perfiles de VPN de Windows 10 para MDM con tipos de conexión Microsoft Automatic, IKEv2 y PPTP en la consola de Configuration Manager sin usar OMA-URI.

- **Gráficos de cumplimiento de Intune**

  Puede obtener una vista rápida del cumplimiento general del dispositivo y de los principales motivos de incumplimiento mediante los nuevos gráficos incluidos en el área de trabajo Supervisión. Para obtener más información, consulte [Intune compliance charts in TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#intune-compliance-charts) (Gráficos de cumplimiento de Intune en TP 1609).

### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)

La siguiente característica nueva incorporada en septiembre de 2016 está disponible en implementaciones híbridas con Microsoft Intune y la versión 1606 de Configuration Manager (rama actual).

- **Compatibilidad con iOS 10**

  Si tiene perfiles o elementos de configuración que se destinan a todas las plataformas iOS, también se insertarán en iOS 10. También hemos lanzado una actualización para la versión 1606 de Configuration Manager que permite tener como destino perfiles y elementos de configuración en plataformas iOS individuales, incluido iOS 10. Puede instalar la actualización con la consola de administración de Configuration Manager en **Administración > Información general > Cloud Services > Actualizaciones y mantenimiento**. Encontrará más información sobre la actualización en [http://support.microsoft.com/kb/3192616](http://support.microsoft.com/kb/3192616).

## <a name="new-hybrid-features-in-august-2016"></a>Nuevas características híbridas de agosto de 2016

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

Las siguientes características de Intune que se incorporaron en agosto de 2016 funcionan en implementaciones híbridas.

- **Compatibilidad con Android 7 en la aplicación de portal de empresa**

  La aplicación de portal de empresa de Intune para Android proporciona compatibilidad desde el principio para el próximo sistema operativo Android 7.0 para dispositivos móviles.

- **Eliminación de Google de la capacidad de restablecimiento del código de acceso remoto en dispositivos Android 7.0**

  Google está quitando la capacidad de los administradores de TI y usuarios finales de restablecer el código de acceso de dispositivos Android 7.0 de forma remota. Anteriormente, los administradores de TI podían restablecer remotamente la el código de acceso de un usuario y los usuarios finales podrían restablecer sus códigos de acceso desde el sitio web de Portal de empresa.

- **Directiva de aplicaciones permitidas y bloqueadas para dispositivos Samsung KNOX Standard**

  Ahora puede configurar una directiva personalizada para dispositivos Samsung KNOX Standard que le permite crear uno de los siguientes elementos:

  - Una lista de aplicaciones para las que se ha bloqueado la ejecución en el dispositivo. Aunque esté instalada, una aplicación definida en la lista bloqueada no puede activarse en el dispositivo.
  - Una lista de aplicaciones que los usuarios del dispositivo pueden instalar desde la tienda de Google Play. No se pueden instalar otras aplicaciones de la tienda.

  Esta configuración solo pueden usarla dispositivos que ejecutan Samsung KNOX Standard. Para más información, vea [Uso de directivas personalizadas para permitir y bloquear aplicaciones para dispositivos Samsung KNOX Standard](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps).

- **Vínculo de comentarios del portal de empresa a Microsoft**

   El sitio web de Portal de empresa permite a los usuarios finales seleccionar un nuevo vínculo "Comentarios", en la parte inferior de la página, para enviar comentarios a Microsoft acerca de su experiencia con el sitio. Los comentarios recopilados y anónimos ayudarán a Microsoft a mejorar la experiencia del sitio web del Portal de empresa para usuarios.

- **Versión mínima del explorador administrado de iOS actualizada a 8.0**

  La aplicación del explorador administrado de Microsoft Intune para iOS se actualizó para admitir los dispositivos que ejecutan iOS 8.0 o posterior. Aunque los dispositivos iOS 7.1 pueden seguir usando la aplicación del explorador administrado existente, asegúrese de que los usuarios actualizan a iOS 8.0 o superior para acceder a las nuevas funciones de explorador administrado y aprovecharlas al máximo.

### <a name="new-in-configuration-manager-technical-preview"></a>Novedades de Configuration Manager Technical Preview

No se ha incorporado ninguna característica híbrida nueva en agosto de 2016 para Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)

No se ha incorporado ninguna característica híbrida nueva en agosto de 2016 para Configuration Manager (rama actual).

## <a name="new-hybrid-features-in-july-2016"></a>Nuevas características híbridas de julio de 2016

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

Las siguientes características de Intune que se incorporaron en julio de 2016 funcionan en implementaciones híbridas.

- **El SDK de Xamarin para aplicaciones de Intune ya está disponible**

  El componente de Xamarin de SDK para aplicaciones de Intune permite habilitar las características de administración de aplicaciones móviles de Intune en las aplicaciones móviles de iOS y Android compiladas con Xamarin. Encontrará el componente en la [tienda de Xamarin](https://components.xamarin.com/view/Microsoft.Intune.MAM) o en la [página de Github de Microsoft Intune](https://github.com/msintuneappsdk).

- **Experiencia del usuario final mejorada al inscribir dispositivos de Windows**

  Al usar el acceso condicional, se han aclarado los pasos de inscripción para Windows 8.1, Windows 10 Desktop y Windows 10 Mobile en el sitio web del portal de empresa. Ahora, los usuarios verán los pasos **Inscripción de dispositivos** y **Unión al lugar de trabajo** por separado, lo que facilita ver el estado del dispositivo y completar el proceso si se produce un error al unirse al lugar de trabajo. El hecho de que los pasos se muestren por separado también debería simplificar el proceso de solución de problemas para los administradores de TI. Antes, cuando los usuarios finales intentaban realizar la inscripción y todos los pasos de inscripción se realizaban correctamente excepto la unión al lugar de trabajo, el dispositivo inscrito no aparecía en la lista de dispositivos para que los usuarios lo identificasen, lo que resultaba confuso.

 - **El borrado completo ya está disponible para dispositivos Windows 10**

    Es posible realizar el borrado de los equipos y portátiles Windows 10 inscritos como dispositivos móviles para restablecer el dispositivo a la configuración de fábrica. Para obtener más información, consulte [How to protect your devices with remote wipe](/sccm/mdm/deploy-use/wipe-lock-reset) (Cómo proteger los dispositivos con el borrado remoto).

- **Cambios en las cuentas de los administradores de inscripción de dispositivos en la aplicación de portal de empresa de iOS**

  Para mejorar el rendimiento y el escalado, Intune ya no muestra todos los dispositivos de los administradores de inscripción de dispositivos (DEM) en el panel Mis dispositivos de la aplicación de portal de empresa de iOS. Solo se muestra el dispositivo local que ejecuta la aplicación, en el caso de que se haya inscrito mediante la aplicación de portal de empresa.

  El usuario DEM puede realizar acciones en el dispositivo local, pero la administración remota de otros dispositivos inscritos solo se puede realizar desde la consola de administración de Intune. Además, el empleo en Intune de cuentas DEM con el Programa de inscripción de dispositivos de Apple o la herramienta Apple Configurator está quedando en desuso. Estos métodos de inscripción ya admiten la inscripción sin usuarios para dispositivos iOS compartidos.

  Use cuentas DEM únicamente cuando no esté disponible la inscripción sin usuarios para dispositivos compartidos. Para obtener más información, consulte [Enroll corporate-owned devices with the Device Enrollment Manager in Microsoft Intune](../deploy-use/enroll-devices-with-device-enrollment-manager.md) (Inscribir dispositivos propiedad de la empresa con el administrador de inscripción de dispositivos de Microsoft Intune).

- **Cambios en la aplicación de portal de empresa de Android**

  Si los usuarios finales de Android ven un mensaje de error que dice que al dispositivo le falta un certificado necesario, pueden pulsar el botón "Cómo solucionar este problema" para conocer los pasos necesarios para instalar el certificado que falta. Si los usuarios completan los pasos pero ven otro mensaje de error que indica que falta un certificado, se les solicitará que se pongan en contacto con su administrador de TI y le proporcionen este vínculo, que incluye los pasos que los administradores de TI pueden usar para solucionar el problema del certificado.

- **Restringir las instalaciones de aplicaciones de carga lateral para dispositivos Android inscritos**

  Los dispositivos Android ya no pueden instalar aplicaciones a través del sitio web del portal de empresa a menos que los dispositivos se hayan inscrito en Intune mediante la aplicación de portal de empresa para Android.


### <a name="new-in-configuration-manager-technical-preview"></a>Novedades de Configuration Manager Technical Preview

No se ha incorporado ninguna característica híbrida nueva en julio de 2016 para Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)

Las siguientes características que estaban disponibles en versiones de Configuration Manager Technical Preview están ahora disponibles en implementaciones híbridas con Intune y la versión 1606 de Configuration Manager (rama actual).

* Buscar, administrar y distribuir aplicaciones de la Tienda Windows para empresas para dispositivos Windows 10 desde la consola de Configuration Manager ([1604](#new-in-1604-technical-preview))
*   Configuración de SmartLock para dispositivos Android ([1604](#new-in-1604-technical-preview))
*   VPN desencadenada por la aplicación para dispositivos Windows 10 ([1605](#new-in-1605-technical-preview))
*   Nueva experiencia para acciones del dispositivo remoto ([1605](#new-in-1605-technical-preview))
*   Tienda Windows para aplicaciones empresariales ([1605](#new-in-1605-technical-preview))
*   Mejoras generales para aplicaciones adquiridas por volumen ([1605](#new-in-1605-technical-preview))
*   Windows Information Protection (WIP) ([1605](#new-in-1605-technical-preview))
*   Declarar previamente dispositivos corporativos con número de serie IMEI o iOS ([1605](#new-in-1605-technical-preview))
*   Clasificar automáticamente dispositivos en recopilaciones ([1606](#new-in-1606-technical-preview))

Para obtener información sobre la nueva funcionalidad, consulte la documentación de la versión de Technical Preview especificada.

## <a name="new-hybrid-features-in-june-2016"></a>Nuevas características híbridas de junio de 2016

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune
Las siguientes características de Intune que se incorporaron en junio de 2016 funcionan en implementaciones híbridas.

- **Mantenimiento del servicio de Intune** La información de mantenimiento del servicio de Intune se ha movido a una ubicación central con otros servicios de Microsoft. Ahora encontrará esta información en el portal de administración de Office 365 en Estado del servicio. Para obtener más información, consulte esta [entrada de blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/).

- **Mejor experiencia de configuración de directiva de datos de empresa de Windows 10 **

  Intune tiene ahora una mejor experiencia para configurar la directiva de protección de información de Windows 10. Las mejoras incluyen mejores formas de crear reglas de aplicaciones y especificar la definición de límite de red, así como otras opciones de Windows Information Protection. Para obtener más información, consulte [Crear una directiva de Windows Information Protection (WIP) con Microsoft Intune](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune).

- **Directiva de control de acceso a la red de ISE de Cisco para Intune**

  Los clientes que usan el motor de servicio de identidad (ISE) 2.1 de Cisco y también usan Microsoft Intune pueden establecer una directiva de control de acceso a la red en ISE. Con esta directiva, los dispositivos que necesitan conectarse a la red mediante Wi-Fi o VPN deben cumplir las condiciones siguientes para que se les permita el acceso:

  - Deben administrarse mediante Intune.
  - Deben cumplir todas las directivas de cumplimiento de Intune implementadas.

  Se solicitará a los usuarios finales de dispositivos no conformes que los inscriban y corrijan los problemas de cumplimiento para tener acceso.

- **Acceso condicional para el explorador**

  Puede establecer una directiva de acceso condicional para Exchange Online y SharePoint Online de modo que solo sean accesibles desde los exploradores web admitidos en dispositivos iOS y Android administrados y conformes. Se les solicitará a los usuarios finales que intenten iniciar sesión en sitios de Outlook Web Access (OWA) y SharePoint con dispositivos iOS y Android que inscriban sus dispositivos con Intune y que corrijan los posibles problemas de incumplimiento para poder completar el inicio de sesión. Para obtener más información, consulte

  * [Restringir el acceso de correo electrónico a Exchange Online y nuevo Exchange Online dedicado con Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
  * [Restringir el acceso a SharePoint Online con Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)

- **Compatibilidad de Dynamics CRM Online con el acceso condicional**

  Puede establecer una directiva de acceso condicional para Dynamics CRM Online de modo que solo sea accesible para dispositivos iOS y Android administrados y conformes. Se les solicitará a los usuarios finales que intenten iniciar sesión en la aplicación móvil de Dynamics CRM con dispositivos iOS y Android que los inscriban en Intune y que corrijan los posibles problemas de incumplimiento para poder completar el inicio de sesión. Para obtener más información, consulte [Restrict access to Dynamics CRM Online with Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune) (Restringir el acceso a Dynamics CRM Online con Microsoft Intune).

- **Actualizaciones en la aplicación de portal de empresa de Android**

  Intune tiene ahora las nuevas directivas siguientes que afectarán a los usuarios del portal de empresa Android:   

  Directiva  |Efecto en los usuarios  
  ---------|---------
  Requerir que los dispositivos impidan la instalación de aplicaciones desde orígenes desconocidos (Android 4.0 y versiones posteriores)     |  Los usuarios finales con dispositivos Android 4.0 o versiones posteriores verán el mensaje "Debe deshabilitarse la instalación desde orígenes desconocidos". Los usuarios tendrán que ir a **Ajustes > Seguridad** en sus dispositivos y desactivar **Orígenes desconocidos**. Un vínculo incluido en el mensaje de compatibilidad permite a los usuarios obtener más información sobre el mensaje y por qué deben desactivar esta opción de configuración.
  Requerir que los dispositivos impidan la instalación de aplicaciones desde orígenes desconocidos (Android 4.0 y versiones posteriores)  |    Los usuarios finales con dispositivos Android 4.0 o versiones posteriores verán el mensaje "Buscar amenazas de seguridad en el dispositivo". Los usuarios tendrán que ir a **Ajustes > Google > Seguridad** en sus dispositivos y activar **Buscar amenazas de seguridad en el dispositivo**. Un vínculo incluido en el mensaje de compatibilidad permite a los usuarios obtener más información sobre el mensaje y por qué deben activar esta opción de configuración.     
  Requerir que la depuración USB esté deshabilitada (Android 4.2 y versiones posteriores)  | Los usuarios finales con dispositivos Android 4.2 o versiones posteriores verán el mensaje "La depuración USB debe deshabilitarse". Los usuarios tendrán que ir a **Ajustes > Opciones del desarrollador** en sus dispositivos y desactivar **Depuración USB**. Un vínculo incluido en el mensaje de compatibilidad permite a los usuarios obtener más información sobre el mensaje y por qué deben desactivar esta opción de configuración.
  Nivel de revisión de seguridad mínimo de Android (Android 6.0 y versiones posteriores)  | Los usuarios finales con dispositivos Android 6.0 o versiones posteriores verán el mensaje "Este dispositivo no cumple el nivel mínimo de revisión de seguridad de Android". Los usuarios tendrán que instalar la revisión de seguridad necesaria. Un vínculo incluido en el mensaje de compatibilidad permite a los usuarios obtener información sobre cómo instalar la revisión de seguridad necesaria y ver la revisión de seguridad que está instalada actualmente.

- **Actualizaciones en la aplicación de portal de empresa de iOS**

  * Ahora, cuando los usuarios finales instalen aplicaciones de línea de negocio, verán una experiencia mejorada de instalación de aplicaciones. Si la instalación de la aplicación tarda mucho tiempo, los usuarios pueden sincronizar manualmente el dispositivo para forzar la reanudación del proceso de sincronización. Para revisar las instrucciones para el usuario final, consulte Sincronización manual del dispositivo iOS.
  * La aplicación de portal de empresa de Microsoft Intune para iOS se ha actualizado para admitir la versión de iOS 8.0 y posteriores. Esta actualización significa que los usuarios finales pueden instalar la aplicación de portal de empresa e inscribir nuevos dispositivos en Intune solo si el dispositivo ejecuta la versión de iOS 8.0 o posterior. Los usuarios que ya han inscrito dispositivos que se ejecutan con una versión no compatible de iOS pueden seguir utilizando la aplicación Portal de empresa que está en su dispositivo.


### <a name="new-in-1606-technical-preview"></a>Novedades de Technical Preview 1606
Las siguientes características nuevas incorporadas en junio de 2016 están disponibles en implementaciones híbridas con Intune y Configuration Manager Technical Preview 1606.

- **Clasificar automáticamente dispositivos en recopilaciones**

  Puede crear categorías de dispositivos, que se pueden usar para colocar automáticamente los dispositivos en recopilaciones de dispositivos cuando se usa Configuration Manager con Intune. Después, cuando los usuarios inscriben un dispositivo en Intune, tienen que elegir una categoría de dispositivos. Además, puede cambiar la categoría de un dispositivo desde la consola de Configuration Manager. Para obtener más información, consulte [Automatically categorize devices into collections](/sccm/core/get-started/capabilities-in-technical-preview-1606#dmp_category) (Clasificar automáticamente dispositivos en recopilaciones) en [Capabilities in Technical Preview 1606 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1606) (Capacidades de Technical Preview 1606 para System Center Configuration Manager).

  > [!IMPORTANT]
  > Esta capacidad funciona con la versión de junio de 2016 de Microsoft Intune. Asegúrese de haber actualizado a esta versión antes de probar estos procedimientos.

### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)
No se ha incorporado ninguna característica híbrida nueva en junio de 2016 para Configuration Manager (rama actual).

##  <a name="new-hybrid-features-in-may-2016"></a>Nuevas características híbridas de mayo de 2016  

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune  
 Las siguientes características de Intune que se incorporaron en mayo de 2016 funcionan en implementaciones híbridas.

- **SDK de MAM: compatibilidad con la configuración de la longitud del PIN**

  Ahora puede especificar la longitud del PIN para aplicaciones MAM como si se tratara de un PIN de dispositivo. Esto requiere que los usuarios finales cumplan las nuevas restricciones que establezca. La pantalla de PIN se ha modificado ligeramente para tener en cuenta la entrada más larga. Para obtener más información, consulte [Opciones de configuración de directiva de administración de aplicaciones móviles de Android](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings) y [Configuración de directiva de administración de aplicaciones móviles iOS](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings).  

- **Skype Empresarial para iOS y Android**

  Ahora puede tener como destino Skype Empresarial con [MAM sin directivas de inscripción](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune). Una vez que el usuario inicie sesión, se aplicarán las directivas de MAM.  

- **Nuevas aplicaciones disponibles para la administración con directivas de MAM**

  Ahora, las aplicaciones de Microsoft Word, Excel y PowerPoint para Android pueden asociarse con directivas de MAM en dispositivos que no estén inscritos con Intune. Para obtener una lista completa de las aplicaciones compatibles, vaya a la galería de aplicaciones móviles de Microsoft Intune en la página de [partners de aplicaciones de Microsoft Intune](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx).  

- **Aplicación de portal de empresa de Android: notificaciones del sistema de usuario final**

  Cuando los usuarios finales inscriben o eliminan sus dispositivos desde el portal de empresa, aparecen notificaciones del sistema de la aplicación de portal de empresa de Android.  

- **Sitio web del portal de empresa: el titular de identificación del dispositivo proporcionará más información a los usuarios finales**

  Ahora, los usuarios finales pueden identificar más fácilmente el dispositivo que han seleccionado al usar el sitio web del portal de empresa. Si se selecciona un dispositivo erróneo, pueden seleccionar el dispositivo correcto mediante el vínculo **Pulse aquí** situado en el titular de la página principal.  


### <a name="new-in-1605-technical-preview"></a>Novedades de Technical Preview 1605  
 Las siguientes características nuevas incorporadas en mayo de 2016 están disponibles en implementaciones híbridas con Intune y Configuration Manager Technical Preview 1605. Estas características requieren que se use la consola de Configuration Manager para la configuración y la administración.  

- **VPN desencadenada por la aplicación para dispositivos Windows 10**

  En los dispositivos Windows 10 administrados con Configuration Manager con Intune, puede agregar una lista de aplicaciones que abran automáticamente una conexión VPN que haya configurado mediante la consola de administración de Configuration Manager. Para obtener más información, consulte [App-triggered VPN for Windows 10 devices](/sccm/core/get-started/capabilities-in-technical-preview-1605) (VPN desencadenada por la aplicación para dispositivos Windows 10) en [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (Capacidades de Technical Preview 1605 para System Center Configuration Manager).  

- **Nueva experiencia para acciones de dispositivo remoto**

  Se ha mejorado la experiencia para realizar acciones de dispositivo remoto desde la consola de Configuration Manager.

  Acciones comunes como **Retirar/borrar**, **Restablecer contraseña**, **Bloqueo remoto** y **Omitir bloqueo de activación** ahora se encuentran en el menú **Acciones de dispositivo remoto**, al que se accede desde el área de trabajo **Activos y compatibilidad**.

  Para obtener más información, consulte [New experience for remote device actions](/sccm/core/get-started/capabilities-in-technical-preview-1605#new-experience-for-remote-device-actions) (Nueva experiencia para acciones del dispositivo remoto) en [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (Capacidades de Technical Preview 1605 para System Center Configuration Manager).  

- **Tienda Windows para aplicaciones empresariales**

  La [Tienda Windows para empresas](https://www.microsoft.com/en-us/business-store) es el lugar donde puede buscar y adquirir aplicaciones para su organización, individualmente o por volumen. Al conectar la tienda a Configuration Manager, puede administrar aplicaciones adquiridas por volumen desde la consola de Configuration Manager. Para obtener más información, consulte [Windows Store for Business apps](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#windows-store-for-business-apps) (Tienda Windows para aplicaciones empresariales) en [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (Capacidades de Technical Preview 1605 para System Center Configuration Manager).  

- **Mejoras generales para aplicaciones adquiridas por volumen**

  Las aplicaciones adquiridas por volumen en la Tienda Windows para empresas e iOS App Store se han consolidado en la misma vista, **Información de licencia para las aplicaciones de la Tienda**. Además, se ha mejorado la forma en que se crean aplicaciones adquiridas por volumen para iOS. Para obtener más información, consulte [General improvements for volume-purchased apps](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#general-improvements-for-volume-purchased-apps) (Mejoras generales para aplicaciones adquiridas por volumen) en [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (Capacidades de Technical Preview 1605 para System Center Configuration Manager).  

- **Declarar previamente dispositivos corporativos con número de serie IMEI o iOS**

  Ahora puede identificar los dispositivos corporativos si importa sus números de identidad internacional de equipo móvil (IMEI). Puede cargar un archivo de valores separados por comas (.csv) que incluya los números IMEI de los dispositivos o escribir la información de los dispositivos de forma manual.  También puede importar los números de serie de los dispositivos iOS.  Para obtener más información, consulte [Pre-declare corporate-owned devices with IMEI or iOS serial number](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_IMEI) (Declarar previamente dispositivos corporativos con número de serie IMEI o iOS) en [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (Capacidades de Technical Preview 1605 para System Center Configuration Manager).  

- **Windows Information Protection (WIP)**

  Puede crear elementos de configuración que le permitan implementar directivas de Windows Information Protection (WIP), incluso que le permitan elegir las aplicaciones protegidas, el nivel de protección WIP y cómo buscar datos empresariales en la red. Para obtener más información sobre WIP, consulte los temas siguientes:  

  -   [Protege los datos de tu empresa con Windows Information Protection (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [Crear e implementar una directiva de Windows Information Protection (WIP) con System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)  
 No se ha incorporado ninguna característica híbrida nueva en mayo de 2016 para Configuration Manager (rama actual).  

##  <a name="new-hybrid-features-in-april-2016"></a>Nuevas características híbridas de abril de 2016  

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune  
 Las siguientes características de Intune que se incorporaron en abril de 2016 funcionan en implementaciones híbridas.  

- **Compatibilidad con usuario MAM**

  Ahora puede ver el estado de las directivas de administración de aplicaciones para cualquier usuario del inquilino de Azure Active Directory (AAD).  Para obtener más información, consulte [Supervisión de directivas de administración de aplicaciones móviles con Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) en la biblioteca de Intune.  

- **Controles MAM para impedir la sincronización de contactos de Outlook (Android)**

  Hay disponible una nueva opción de configuración que permite impedir que una aplicación sincronice los contactos en la libreta de direcciones nativa de dispositivos Android. Esta nueva opción es compatible inicialmente con la aplicación de Outlook en dispositivos Android. Para obtener más información, consulte [Crear e implementar directivas de administración de aplicaciones móviles con Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) en la biblioteca de Intune.  

- **Mejoras en el sitio web del portal de empresa**

  Ahora, cuando los usuarios de Windows 10 Mobile y Windows Phone 8.1 instalen aplicaciones de línea de negocio, verán los siguientes estados nuevos que proporcionan más detalles sobre el estado de la instalación:  

  -   **Esperando a que se sincronice el dispositivo**: el usuario ha pulsado "Instalar" y el dispositivo intenta sincronizarse con la infraestructura de Intune. Es necesario que se lleve a cabo la sincronización para que se complete la instalación. El mensaje "Esperando a que se sincronice el dispositivo" también es un vínculo que los usuarios pueden pulsar para obtener instrucciones sobre cómo sincronizar manualmente sus dispositivos con Intune si el proceso de sincronización tarda demasiado o se detiene.  

  -   **Descargando**: se está procesando la solicitud de descarga del usuario y el dispositivo está descargando e instalando la aplicación.  

- **Mejoras en la aplicación de portal de empresa de Android**

  Los usuarios que no han inscrito el dispositivo en Intune y que no tienen instalado el certificado correcto no podrán iniciar sesión en la aplicación de portal de empresa de Android y verán el mensaje "No puede iniciar sesión porque falta un certificado necesario en su dispositivo". El mensaje incluye un vínculo "Cómo solucionar este problema" que los usuarios pueden pulsar para ver las instrucciones de instalación del certificado. Para ver los pasos que los usuarios finales siguen para resolver el problema, consulte [El dispositivo no tiene un certificado necesario](/intune/enduser/using-your-android-device-with-intune) en la biblioteca de Intune.  

- **Mejoras en la aplicación de portal de empresa de iOS**

  Se ha agregado compatibilidad con la acción de deslizar para actualizar como método de actualización del contenido de la pantalla principal, que incluye las aplicaciones de la lista, los dispositivos de la lista y la información de contacto de TI. La acción de deslizar para actualizar no comprueba la información de cumplimiento o de las directivas. Para hacerlo, es necesario seleccionar el icono del dispositivo actual y pulsar el botón **Sincronizar**.  

- **Mejoras en la aplicación de portal de empresa de Windows 10 Mobile y Windows Phone 8.1**

  Ahora, cuando los usuarios finales instalen aplicaciones de línea de negocio, verán una experiencia mejorada de instalación de aplicaciones. Si la instalación de la aplicación tarda mucho tiempo, los usuarios pueden sincronizar manualmente el dispositivo para forzar la reanudación del proceso de sincronización. Para revisar las instrucciones para el usuario final, consulte [Sync your device manually to speed up app installations](/intune/enduser/using-your-windows-device-with-intune) (Sincronización manual del dispositivo para acelerar las instalaciones de aplicaciones) en la biblioteca de Intune.  

###  <a name="new-in-1604-technical-preview"></a>Novedades de Technical Preview 1604
 Las siguientes características nuevas incorporadas en abril de 2016 están disponibles en implementaciones híbridas con Intune y Configuration Manager Technical Preview 1604. Estas características requieren que se use la consola de Configuration Manager para la configuración y la administración.  

- **Buscar, administrar y distribuir aplicaciones de la Tienda Windows para empresas para dispositivos Windows 10 desde la consola de Configuration Manager**


  Hay compatibilidad con la Tienda Windows para empresas en Configuration Manager Technical Preview 1604 para ayudarle a buscar, administrar y distribuir aplicaciones en los dispositivos Windows 10 que administre. Para obtener información, consulte [Manage volume-purchased apps from the Windows Store for Business](/sccm/core/get-started/capabilities-in-technical-preview-1604#manage-volume-purchased-apps-from-the-windows-store-for-business) (Administración de aplicaciones adquiridas por volumen de la Tienda Windows para empresas) en [Capabilities in Technical Preview 1604 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604) (Capacidades de Technical Preview 1604 para System Center Configuration Manager).  

- **Configuración de Smart Lock para dispositivos Android**

  Se ha agregado un nuevo valor de configuración al elemento de configuración de Android y Samsung KNOX Standard que le permite controlar la característica Smart Lock en dispositivos Android compatibles.  Puede utilizar esta opción para impedir que los usuarios finales configuren SmartLock. Consulte [SmartLock setting for Android devices](/sccm/get-started/capabilities-in-technical-preview-1604#smartlock-setting-for-android-devices) (Configuración de Smart Lock para dispositivos Android) en [Capabilities in Technical Preview 1604 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604.md) (Capacidades de Technical Preview 1604 para System Center Configuration Manager).  

### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)  
 No se ha incorporado ninguna característica híbrida nueva en abril de 2016 para Configuration Manager (rama actual).  

##  <a name="new-hybrid-features-in-march-2016"></a>Nuevas características híbridas de marzo de 2016  

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune  
 Las siguientes características de Intune que se incorporaron en marzo de 2016 funcionan en implementaciones híbridas.  

- **Controles MAM para impedir la sincronización de contactos de Outlook (iOS)**

  Hay disponible una nueva opción de configuración que permite impedir que una aplicación sincronice los contactos en la libreta de direcciones nativa de dispositivos iOS. Esta nueva opción es compatible con la aplicación de Outlook en dispositivos iOS. Para obtener más información sobre esta y otras opciones, consulte [Crear e implementar directivas de administración de aplicaciones móviles ](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) en la biblioteca de Intune.  

- **Skype Empresarial Online admite el acceso condicional**

  Puede establecer una directiva de acceso condicional para Skype Empresarial Online de modo que solo sea accesible para dispositivos iOS y Android administrados y conformes.  Para obtener más información, consulte [Manage access to Skype for Business Online](/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune) (Administrar el acceso a Skype Empresarial Online) en la biblioteca de Intune.  

- **Compatibilidad con iOS 9.3**

  El lunes 21 de marzo, Apple anunció la disponibilidad de iOS 9.3. Todas las características de Intune que están disponibles actualmente para administrar dispositivos iOS seguirán funcionando sin problemas cuando los usuarios actualicen sus dispositivos a iOS 9.3.  

- **Paquetes de aplicaciones de Windows disponibles directamente desde el sitio web del portal de empresa**

  Los usuarios de equipos Windows 8, Windows 8.1 y Windows RT ya pueden instalar paquetes de aplicaciones de Windows (con la extensión .appx) directamente desde el sitio web del portal de empresa. Antes, para poder instalar aplicaciones, tenía que ser usted quien implementara la aplicación de portal de empresa en los dispositivos de los usuarios, o bien tenían que instalarla ellos mismos.  

- **Los usuarios pueden bloquear de forma remota su dispositivo desde el sitio web del portal de empresa**

  Se ha agregado una nueva opción de bloqueo remoto al sitio web del portal de empresa para permitir que los usuarios bloqueen de forma remota su dispositivo desde el portal si lo pierden o se lo roban.  

- **Aprovechar las ventajas de la administración de "Open In" de iOS para dispositivos inscritos en una solución MDM de terceros**

  Puede usar su proveedor de administración de dispositivos móviles (MDM) de terceros para aprovechar las ventajas de la administración de "Open In" de iOS. Puede establecer las restricciones en los valores del perfil de configuración e implementar la aplicación con el software MDM. Cuando el usuario instala la aplicación administrada, se aplican las restricciones. Consulte todos los detalles en [Microsoft Intune mobile app management policies and iOS Open In](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune) (Directivas de administración de aplicaciones móviles de Microsoft Intune y característica Open In de iOS) en la biblioteca de Intune.  

- **Aplicaciones de Microsoft que admiten MAM**

  La lista de aplicaciones de Microsoft que se pueden usar con directivas de administración de aplicaciones móviles de Intune se ha actualizado para incluir las aplicaciones más recientes (para dispositivos inscritos únicamente con Intune).  

- **Implementar Adobe Reader para Microsoft Intune en dispositivos iOS administrados por Intune en la empresa**

  La aplicación Adobe Reader para iOS ahora puede administrarse en dispositivos inscritos con la directiva de administración de aplicaciones móviles de Intune.  

- Se admite la aplicación Rights Management sharing con Android

  Los administradores de TI pueden implementar directivas de administración de aplicaciones móviles para que los usuarios finales puedan ver imágenes, AV y archivos PDF de forma más segura, independientemente de si el departamento de TI usa Intune para administrar los dispositivos.  

- **Mejoras en la aplicación de portal de empresa de Android e iOS**

  -   Cuando los usuarios inicien una aplicación administrada mediante la administración de aplicaciones móviles (MAM), verán un mensaje que les informa de que la empresa administra la aplicación. Ahora, los usuarios pueden pulsar el vínculo "Más información" para obtener más información sobre el significado de las "aplicaciones administradas". También pueden pulsar "No mostrar de nuevo" para que el mensaje ya no aparezca al iniciar la aplicación.  

  -   Se han agregado pantallas nuevas para guiar a los usuarios a lo largo del proceso de inscripción y proporcionarles más detalles sobre los motivos por los que deben inscribir los dispositivos, así como información sobre lo que pueden y no pueden ver los administradores de TI en los dispositivos inscritos.  

  -   Ahora, los mensajes de error de inscripción se muestran en la aplicación de portal de empresa.  

### <a name="new-in-configuration-manager-technical-preview"></a>Novedades de Configuration Manager Technical Preview  
 No se ha incorporado ninguna característica híbrida nueva en marzo de 2016 para Configuration Manager Technical Preview.  

### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)  
 Las siguientes características nuevas incorporadas en marzo de 2016 están disponibles en implementaciones híbridas con Intune y la versión 1602 de Configuration Manager (rama actual). Estas características requieren que se use la consola de Configuration Manager para la configuración y la administración.  

- **Directivas de configuración de aplicaciones de iOS**

  En la versión 1602 de Configuration Manager (rama actual), puede usar las directivas de configuración de aplicaciones para proporcionar la configuración que puede ser necesaria cuando el usuario ejecuta una aplicación de iOS. Para obtener más información, consulte [Configure iOS apps with app configuration policies in System Center Configuration Manager](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies) (Configurar aplicaciones de iOS con directivas de configuración de aplicaciones en System Center Configuration Manager).  

- **Administración de aplicaciones de iOS adquiridas por volumen**

  En la versión 1602 de Configuration Manager (rama actual), puede implementar y administrar las aplicaciones que compró por volumen por medio del Programa de Compras por Volumen de Apple (VPP). Para ello, importe la información de licencia desde App Store y haga un seguimiento de la cantidad de licencias que se han usado. Para obtener más información, consulte [Manage volume-purchased iOS apps with System Center Configuration Manager](/sccm/apps/deploy-use/manage-volume-purchased-ios-apps) (Administrar aplicaciones de iOS compradas por volumen con System Center Configuration Manager).  

- **Creación automática de aplicaciones móviles de Office**

  A partir de la versión 1602 de Configuration Manager (rama actual), se crean las siguientes aplicaciones móviles de Microsoft Office para Android e iOS cuando se actualiza desde la versión 1511:  

  -   Microsoft Word  
  -   Microsoft Excel  
  -   Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote (solo iOS)  
  -   Microsoft Outlook  

  Encontrará estas aplicaciones en el nodo Aplicaciones de la consola de Configuration Manager. Para obtener más información sobre cómo implementar aplicaciones, consulte [How to deploy applications with System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md) (Implementación de aplicaciones con System Center Configuration Manager).  

- **Configuración de pantalla completa para dispositivos Samsung KNOX Standard con Android**

  El modo de quiosco permite bloquear un dispositivo para permitir que solo funcionen determinadas características.  A partir de la versión 1602 de Configuration Manager (rama actual), puede especificar la configuración de pantalla completa para dispositivos Samsung KNOX Standard. Para obtener más información, consulte [Crear elementos de configuración para dispositivos Android y Samsung KNOX Standard administrados sin el cliente de System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client).  

- **Bloqueo de activación de iOS**

  A partir de la versión 1602 de Configuration Manager (rama actual), puede administrar el bloqueo de activación de iOS, una característica de la aplicación Buscar mi iPhone disponible en dispositivos iOS 7.1 y versiones posteriores. El bloqueo de activación se habilita automáticamente cuando se usa la aplicación Buscar mi iPhone en un dispositivo.  Para obtener más información, consulte [Manage iOS Activation Lock bypass for System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock) (Administración de la omisión del bloqueo de activación de iOS para System Center Configuration Manager).  



<!--HONumber=Jan17_HO4-->

