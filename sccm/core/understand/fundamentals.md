---
title: Conceptos básicos
titleSuffix: Configuration Manager
description: Obtenga información sobre los conceptos básicos de System Center Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cc4cdb35-f0b4-42b5-9cec-6431a8c30793
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4bb48ebf1bcf5be503505efd2b84d364e655a6e5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131190"
---
# <a name="fundamentals-of-system-center-configuration-manager"></a>Aspectos básicos de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Si no está familiarizado con System Center Configuration Manager, lea los temas fundamentales para obtener información sobre los conceptos básicos de Configuration Manager antes de ejecutar el programa de instalación para instalar el primer sitio. Si está familiarizado con Configuration Manager, puede empezar directamente. Se recomienda que empiece con [Novedades de System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).  

 Para obtener información sobre los sistemas operativos y los entornos compatibles, los requisitos de hardware y la información de capacidad, consulte [Supported configurations for System Center Configuration Manager (Configuraciones compatibles con System Center Configuration Manager)](../../core/plan-design/configs/supported-configurations.md).  

 Al implementar Configuration Manager, implementa uno o varios sitios:  

- **Si se implementan varios sitios**, los sitios establecen relaciones de elementos secundarios a elementos primarios que se denominan colectivamente jerarquía. Use una jerarquía para administrar de forma centralizada un mayor número de sitios y dispositivos.  Los datos y la información fluyen de forma descendente por la jerarquía hasta llegar a los dispositivos que administra. La información sobre dispositivos y los resultados de las solicitudes y las tareas de configuración fluyen de forma ascendente en la jerarquía.  

- **Si se implementa un único sitio**, también se denomina jerarquía.  

  Algunas opciones y tareas de configuración se aplican a todos los sitios de una jerarquía, mientras que otras se aplican a sitios individuales.  

## <a name="fundamental-concepts-for-system-center-configuration-manager"></a>Conceptos básicos de System Center Configuration Manager
Vea los temas siguientes para obtener información acerca de los conceptos básicos de System Center Configuration Manager:  

-   [Fundamentals of sites and hierarchies for System Center Configuration Manager (Aspectos básicos de sitios y jerarquías para System Center Configuration Manager)](../../core/understand/fundamentals-of-sites-and-hierarchies.md)  

-   [Fundamentals of managing devices with System Center Configuration Manager (Aspectos básicos de la administración de dispositivos con System Center Configuration Manager)](../../core/understand/fundamentals-of-managing-devices.md)  

-   [Fundamentals of client management tasks for System Center Configuration Manager (Aspectos básicos de las tareas de administración de clientes de System Center Configuration Manager)](../../core/understand/fundamentals-of-client-management-tasks.md)  

-   [Fundamentals of security for System Center Configuration Manager (Aspectos básicos de la seguridad en System Center Configuration Manager)](../../core/understand/fundamentals-of-security.md)  
