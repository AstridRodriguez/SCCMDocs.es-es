---
title: Seguridad y privacidad de la administración de energía
titleSuffix: Configuration Manager
description: Obtenga información sobre seguridad y privacidad aplicadas a la administración de energía en System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: a7bba23bf35d60d83fcff01acb20c8f404b6445d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123427"
---
# <a name="security-and-privacy-for-power-management-in-system-center-configuration-manager"></a>Seguridad y privacidad de la administración de energía en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Esta sección contiene información sobre la seguridad y privacidad en la administración de energía en System Center Configuration Manager.  

## <a name="security-best-practices-for-power-management"></a>Procedimientos recomendados de seguridad para la administración de energía  
 No hay ningún procedimiento recomendado relacionado con la seguridad para la administración de energía.  

## <a name="privacy-information-for-power-management"></a>Información de privacidad para la administración de energía  
 Administración de energía usa características integradas en Windows para supervisar el uso de energía y para aplicar la configuración de energía a equipos durante el horario laboral y fuera del horario comercial. Configuration Manager recopila información sobre el uso de energía de los equipos, por ejemplo, los datos sobre cuándo un usuario utiliza un equipo. Aunque Configuration Manager supervisa el uso de energía de una recopilación en lugar de cada equipo, una recopilación puede contener un solo equipo. La administración de energía no está habilitada de forma predeterminada y un administrador debe configurarla.  

 La información de uso de energía se almacena en la base de datos de Configuration Manager y no se envía a Microsoft. La información detallada se conserva en la base de datos durante 31 días y la información resumida durante 13 meses. No puede configurar el intervalo de eliminación.  

 Antes de configurar la administración de energía, tenga en cuenta los requisitos de privacidad.  
