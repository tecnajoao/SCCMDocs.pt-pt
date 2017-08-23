---
title: "Необходимые условия для коллекций | Документы Майкрософт"
description: "Ознакомьтесь с необходимыми условиями для использования коллекций в System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
caps.latest.revision: "7"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 41fc3eb20a7441939eb0dc80bc121c8f3ea322b2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>Необходимые условия для коллекций в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Коллекции в System Center Configuration Manager содержат только зависимости в пределах продукта.  

## <a name="configuration-manager-dependencies"></a>Зависимости Configuration Manager  

|Зависимость|Дополнительные сведения|  
|----------------|----------------------|  
|Точка служб отчетов|Чтобы создавать отчеты по коллекциям, необходимо установить роль системы сайта "точка служб отчетов". Дополнительные сведения см. в статье [Ведение отчетов в System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Для управления коллекциями должны быть предоставлены определенные разрешения системы безопасности|Для работы с параметрами соответствия необходимо иметь следующие разрешения.<br /><br /> Для создания коллекций и управления ими: **Создать**, **Удалить**, **Изменить**, **Изменить папку**, **Переместить объект**, **Чтение** и **Прочитать ресурс** для объекта **Коллекция**.<br /><br /> Для управления параметрами коллекции: **Изменить параметр коллекции** для объекта **Коллекция**.<br /><br /> Разрешение **Изменить папку** требуется для всех папок коллекции, включая корневую папку.|  
