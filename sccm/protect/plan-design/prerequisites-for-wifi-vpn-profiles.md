---
title: Requisitos previos de los perfiles de Wi-Fi y VPN| Microsoft Docs
description: "Obtenga información sobre los permisos de seguridad necesarios para administrar perfiles de certificado, perfiles de Wi-Fi y perfiles de VPN en System Center Configuration Manager."
ms.custom: na
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
caps.latest.revision: 5
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 31b68ede677df8b86412a334d1d100041a0e659e
ms.openlocfilehash: 309b0363f9b3ec4a31b8323b9e64c9f73060c281


---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Requisitos previos de los perfiles de Wi-Fi y VPN en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Los perfiles de Wi-Fi y VPN de System Center Configuration Manager solo contienen dependencias dentro del producto.  

 Debe tener los siguientes permisos de seguridad para administrar la configuración de acceso a los recursos de la compañía, como perfiles de certificado, perfiles de Wi-Fi y perfiles de VPN:  

-   Para ver y administrar alertas e informes de los perfiles de Wi-Fi y VPN: **Crear**, **Eliminar**, **Modificar**, **Modificar informe**, **Leer** y **Ejecutar informe** para el objeto **Alertas**.  

-   Para crear y administrar perfiles de certificado: **Directiva de autor**, **Modificar informe**, **Leer**y **Ejecutar informe** para el objeto **Perfil de certificado** .  

-   Para administrar redes Wi-Fi, certificados e implementaciones de perfiles VPN: **Implementar directivas de configuración**, **Modificar alerta de estado de cliente**, **Leer**y **Leer recurso** para el objeto **Recopilación** .  

-   Para administrar todas las directivas de configuración: **Crear**, **Eliminar**, **Modificar**, **Leer**y **Establecer ámbito de seguridad** para el objeto **Directiva de configuración** .  

-   Para ejecutar consultas relacionadas con los perfiles de Wi-Fi y VPN: permiso **Leer** para el objeto **Consulta**.  

-   Para consultar información de los perfiles de Wi-Fi y VPN en la consola de System Center Configuration Manager: permiso **Leer** para el objeto **Sitio**.  

-   Para consultar los mensajes de estado de los perfiles de Wi-Fi y VPN: permiso **Leer** para el objeto **Mensajes de estado**.  

-   Para crear y administrar el perfil de certificado de la entidad de certificación de confianza: **Directiva de autor**, **Modificar informe**, **Leer**y **Ejecutar informe** para el objeto **Perfil de certificado de CA de confianza** .  

-   Para crear y administrar perfiles de VPN: **Directiva de autor**, **Modificar informe**, **Leer**y **Ejecutar informe** para el objeto **Perfil de VPN** .  

-   Para crear y administrar perfiles de Wi-Fi: **Directiva de autor**, **Modificar informe**, **Leer**y **Ejecutar informe** para el objeto **Perfil de Wi-Fi** .  

 El rol de seguridad **Administrador de acceso de recursos de la compañía** incluye estos permisos necesarios para administrar los perfiles de Wi-Fi en System Center Configuration Manager. Para obtener más información, consulte [Configurar la seguridad en System Center Configuration Manager](../../core/plan-design/security/configure-security.md).



<!--HONumber=Dec16_HO3-->

