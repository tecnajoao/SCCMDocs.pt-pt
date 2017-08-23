---
title: "Безопасность и конфиденциальность запросов | Документы Майкрософт"
description: "Рекомендации по обеспечению безопасности и конфиденциальности при запросе информации из базы данных сайта."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: e42b13c68ecaeac94245838c2f42e2790799de2b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>Безопасность и конфиденциальность запросов в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Запросы в System Center Configuration Manager позволяют получать сведения из базы данных сайта в соответствии с заданными условиями. Configuration Manager выполняет сбор сведений базы данных сайта в ходе стандартных операций. Например, используя сведения, собранные в ходе операций обнаружения или инвентаризации, вы можете настроить запрос для идентификации устройств, отвечающих заданным критериям.  

 Дополнительные сведения о запросах см. в разделе [Общие сведения о запросах в Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). См. рекомендации по [обеспечению в Configuration Manager безопасности и конфиденциальности](../../../core/plan-design/security/security-and-privacy.md) операций по сбору данных, которые могут быть извлечены запросами.  

## <a name="security-best-practices-for-queries"></a>Рекомендации по обеспечению безопасности для запросов  
 Примите во внимание следующие рекомендации по обеспечению безопасности при выполнении запросов.  

|Рекомендация по безопасности|Дополнительные сведения|  
|----------------------------|----------------------|  
|При импорте и экспорте запроса, сохраненного в сетевой папке, обеспечьте безопасность расположения и сетевого канала.|Ограничьте доступ пользователей к сетевой папке.<br /><br /> Используйте подписывание SMB или протокол IPsec при обмене данными между сетевой папкой и сервером сайта, чтобы предотвратить изменение данных запроса злоумышленником до их импорта.|  

## <a name="see-also"></a>См. также  
 [Технический справочник по запросам для System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)
