---
title: Endpoint Protection | Microsoft Docs
description: "Obtenga información sobre cómo administrar las directivas antimalware y la seguridad del Firewall de Windows para equipos cliente de su jerarquía de Configuration Manager."
ms.custom: na
ms.date: 01/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
caps.latest.revision: 11
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0fa837c68eb073d2ceaf48c938137a94141a102e
ms.openlocfilehash: dd08e9ae6827e5f59eaf3414adbcc8667bc75140


---
# <a name="endpoint-protection"></a>Endpoint Protection

*Se aplica a: System Center Configuration Manager (rama actual)*

Endpoint Protection en System Center Configuration Manager permite administrar las directivas antimalware y la seguridad del Firewall de Windows para equipos cliente de su jerarquía de Configuration Manager.  

> [!IMPORTANT]  
>  Debe tener una licencia para usar Endpoint Protection para administrar clientes en su jerarquía de Configuration Manager.  

 Si usa Endpoint Protection con Configuration Manager, disfrutará de las siguientes ventajas:  

-   Configuración de directivas antimalware, configuración del Firewall de Windows y administración de la protección contra amenazas avanzada de Windows Defender en grupos de equipos seleccionados  

-   Uso de las actualizaciones de software de Configuration Manager para descargar los archivos de definición de antimalware más recientes a fin de mantener actualizados los equipos cliente  

-   Envíe notificaciones de correo electrónico, use la supervisión en la consola y vea informes para mantener a los usuarios administrativos informados cuando se detecte malware en los equipos cliente.  

Los equipos Windows 10 no requieren ningún cliente adicional para la administración de Endpoint Protection. En Windows 8.1 y versiones anteriores, Endpoint Protection instala su propio cliente además del cliente de Configuration Manager. Endpoint Protection puede llevar a cabo la administración. El cliente de Endpoint Protection tiene las siguientes capacidades:  

-   Detección y corrección de malware y spyware  

-   Detección y corrección de rootkit  

-   Evaluación y definición automática de vulnerabilidades críticas y actualizaciones del motor  

-   Detección de vulnerabilidades de red a través del Sistema de inspección de red  

-   Integración con Cloud Protection Service para informar a Microsoft sobre malware. Cuando se une a este servicio, el cliente de Endpoint Protection o Windows Defender pueden descargar las definiciones más recientes desde el Centro de protección contra malware cuando se detecta malware no identificado en un equipo.  

> [!NOTE]  
>  El cliente de Endpoint Protection se puede instalar en un servidor que ejecute Hyper-V y en máquinas virtuales invitadas con sistemas operativos compatibles. Para evitar el uso excesivo de la CPU, las acciones de Endpoint Protection tienen un retraso aleatorio integrado para que los servicios de protección no se ejecuten simultáneamente.  

 Además, Endpoint Protection en Configuration Manager le permite administrar la configuración del Firewall de Windows en la consola de Configuration Manager.  

 [Escenario de ejemplo: uso de System Center Endpoint Protection para proteger los equipos frente al malware en System Center Configuration Manager](scenarios-endpoint-protection.md) con Endpoint Protection y el Firewall de Windows.  


## <a name="managing-malware-with-endpoint-protection"></a>Administración de malware con Endpoint Protection  
 Endpoint Protection en Configuration Manager permite crear directivas antimalware que contengan opciones de configuración de cliente de Endpoint Protection. Después puede implementar estas directivas antimalware en los equipos cliente y supervisarlos en el nodo **Estado de Endpoint Protection** en **Seguridad** del área de trabajo **Supervisión**, o bien mediante informes de Configuration Manager.  

 Información adicional:  

-   [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md) (Cómo crear e implementar directivas antimalware para Endpoint Protection en System Center Configuration Manager): cree, implemente y supervise directivas antimalware con una lista con los ajustes que puede configurar.  

-   [How to monitor Endpoint Protection in System Center Configuration Manager](monitor-endpoint-protection.md) (Cómo supervisar Endpoint Protection en System Center Configuration Manager): supervise informes de actividad, equipos cliente infectados y mucho más.  

-   [How to manage antimalware policies and firewall settings for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-firewall.md) (Cómo administrar las directivas antimalware y la configuración de firewall para Endpoint Protection en System Center Configuration Manager): elimine el malware que se encuentra en los equipos cliente.  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Administración del Firewall de Windows con Endpoint Protection  
 Endpoint Protection en Configuration Manager proporciona administración básica del Firewall de Windows en los equipos cliente. Para cada perfil de red, puede configurar las siguientes opciones:  

-   Habilitar o deshabilitar el Firewall de Windows.  

-   Bloquear todas las conexiones entrantes, incluidas las de la lista de programas permitidos.  

-   Notificar al usuario cuando el Firewall de Windows bloquee un nuevo programa.  

> [!NOTE]  
>  Endpoint Protection es compatible solo con la administración del Firewall de Windows.  


 Para obtener más información sobre cómo crear e implementar las directivas del Firewall de Windows para Endpoint Protection, consulte [How to create and deploy Windows Firewall policies for Endpoint Protection in System Center Configuration Manager](create-windows-firewall-policies.md) (Cómo crear e implementar directivas de Firewall de Windows para Endpoint Protection en System Center Configuration Manager).  


## <a name="windows-defender-advanced-threat-protection"></a>Protección contra amenazas avanzada de Windows Defender

A partir de la versión 1606 de Configuration Manager (rama actual), Endpoint Protection puede ayudar a administrar y supervisar la protección contra amenazas avanzadas de Windows Defender (ATP). La Protección contra amenazas avanzada de Windows Defender es un nuevo servicio que ayuda a las empresas a detectar ataques avanzados en sus redes, a investigarlos y a responder a ellos. Consulte [Windows Defender Advanced Threat Protection](windows-defender-advanced-threat-protection.md) (Protección contra amenazas avanzada de Windows Defender).

## <a name="endpoint-protection-workflow"></a>Flujo de trabajo de Endpoint Protection  
 Use el siguiente diagrama para entender mejor el flujo de trabajo para implementar Endpoint Protection en su jerarquía de Configuration Manager.  

 ![Flujo de trabajo de Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)  

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Cliente de Endpoint Protection para equipos Mac y servidores Linux  
 System Center Endpoint Protection incluye un cliente de Endpoint Protection para Linux y para equipos Mac. A estos clientes no se les suministra Configuration Manager, por lo que debe descargar los siguientes productos del [Centro de servicios de licencias por volumen de Microsoft](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

-   System Center 2012 Endpoint Protection para Mac  

-   System Center 2012 Endpoint Protection para Linux  


> [!IMPORTANT]  
>  Debe ser un cliente de licencia por volumen de Microsoft para descargar los archivos de instalación de Endpoint Protection para Linux y Mac.  

 Estos productos no se pueden administrar desde la consola de Configuration Manager. Sin embargo, se suministra un módulo de administración de System Center Operations Manager con los archivos de instalación, que permite administrar el cliente para Linux mediante Operations Manager.  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Cómo obtener el cliente de Endpoint Protection para equipos Mac y servidores Linux

Siga estos pasos para descargar el archivo de imagen que contiene el software cliente de Endpoint Protection y la documentación para equipos Mac y servidores Linux.
1. Inicie sesión en el [Centro de servicios de licencias por volumen de Microsoft](https://www.microsoft.com/licensing/servicecenter/default.aspx).
2. Seleccione la pestaña **Descargas y claves** de la parte superior del sitio web.
3. Filtre por el producto **System Center Endpoint Protection (rama actual)**.
4. Haga clic en el vínculo **Descargar**.
5. Haga clic en **Continue**. Debería ver varios archivos, incluido uno denominado: **System Center Endpoint Protection (current branch - version 1606) for Linux OS and Macintosh OS Multilanguage 32/64 bit 1507 MB ISO**.
6. Haga clic en el icono de flecha para descargar el archivo. El nombre del archivo es **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_EptProt_Lin_Mac_MLF_X21-30777.ISO**.

 Para más información acerca de cómo instalar y administrar los clientes de Endpoint Protection para equipos Linux y equipos Mac, use la documentación que acompaña a estos productos, que se encuentra en la carpeta **Documentation** .



<!--HONumber=Jan17_HO4-->

