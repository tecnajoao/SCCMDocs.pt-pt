---
title: 'Inscrever dispositivos pertencentes à empresa '
titleSuffix: Configuration Manager
description: Saiba mais sobre métodos diferentes para inscrever dispositivos pertencentes à empresa para implementações híbridas com o Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e2754ce6-1460-4ddd-9050-2cc87e7964f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 36b4169f3bed1957f8ea14159902f408ba642944
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346554"
---
# <a name="enroll-company-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Inscrever dispositivos pertencentes à empresa para implementações híbridas com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os dispositivos pertencentes à empresa (COD) ou organização podem ser colocados em gestão de variadas formas consoante o dispositivo e como foi comprado.  

## <a name="enroll-device-enrollment-program-ios-devices"></a>Inscrever dispositivos iOS de programa de inscrição de dispositivos  
 Implementa um perfil de inscrição "por ondas eletromagnéticas" para os dispositivos adquiridos através do programa de inscrição de dispositivos da Apple. Quando o utilizador executar o Assistente de configuração no dispositivo, o dispositivo é inscrito no Intune.  Dispositivos inscritos através do DEP não não possível anular a inscrição por utilizadores. Consulte [inscrição do iOS Device Enrollment Program (DEP) para implementações híbridas com o Configuration Manager](../../mdm/deploy-use/ios-device-enrollment-program-for-hybrid.md).  

## <a name="enroll-ios-devices-with-apple-configurator"></a>Inscrever dispositivos iOS com o Apple Configurator  
 Este método requer que o administrador USB ligue o dispositivo iOS ao computador Mac com o Apple Configurator para pré-configurar a inscrição. Dispositivos, em seguida, são fornecidos aos respetivos utilizadores que utilizam o processo de Assistente de configuração, configurar o dispositivo com as respetivas credenciais de conta escolar ou profissional e concluir o processo de inscrição. Consulte [inscrição do iOS híbrida com o Apple Configurator com o Configuration Manager](../../mdm/deploy-use/ios-hybrid-enrollment-using-apple-configurator.md).  

## <a name="device-enrollment-manager"></a>Gestor de inscrição de dispositivos  
 As organizações podem utilizar o Intune para gerir um grande número de dispositivos móveis com uma única conta de utilizador denominada uma conta de Gestor de inscrição de dispositivos. Depois de criar uma conta de Gestor de inscrição de dispositivos, essa conta pode ser utilizada por um gestor para inscrever mais do que os cinco dispositivos padrão permitidos por predefinição para os utilizadores normais. Inscrição de dispositivos com o Gestor de inscrição de dispositivos funciona apenas para dispositivos que não são utilizados por um utilizador específico. Estes dispositivos são ideais para o ponto de venda ou utilitários aplicações, por exemplo, mas inadequados para utilizadores que necessitam de aceder a recursos de e-mail ou da empresa. Consulte [inscrever dispositivos com o Gestor de inscrição de dispositivos com o Configuration Manager](../../mdm/deploy-use/enroll-devices-with-device-enrollment-manager.md).  

## <a name="user-affinity-for-managed-devices"></a>Afinidade de utilizador para dispositivos geridos  
 Quando configurar perfis de dispositivos pertencentes à empresa, o administrador pode especificar se os dispositivos geridos suportam *afinidade de utilizador* que identifica um utilizador específico com o dispositivo. Os dispositivos configurados com **user affinity** podem instalar e executar a aplicação Portal da Empresa para transferir aplicações e gerir dispositivos. Consulte [afinidade de utilizador para híbrida geridos dispositivos no Configuration Manager](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md).  

## <a name="manage-devices-with-activation-lock"></a>Gerir dispositivos com o bloqueio de ativação  
 Microsoft Intune pode ajudar a gerir o bloqueio de ativação, uma funcionalidade de encontrar iOS a minha aplicação iPhone para iOS 7.1 ou dispositivos posteriores. O Bloqueio de Ativação é ativado automaticamente ao utilizar a aplicação Encontrar o Meu iPhone num dispositivo. Consulte [gerir o bloqueio de ativação com o System Center Configuration Manager iOS](../../mdm/deploy-use/manage-ios-activation-lock.md).

 ## <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Pré-declarar dispositivos com números de série iOS ou IMEI

Pode identificar dispositivos pertencentes ao importar os números de identidade (IMEI) estação internacional do equipamento móvel ou números de série iOS. Pode carregar um ficheiro de valores separados por vírgulas (. csv) contendo os números IMEI de dispositivo ou pode introduzir manualmente as informações do dispositivo.  Consulte [pré-declarar dispositivos com números de ID de hardware](../../mdm/deploy-use/predeclare-devices-with-hardware-id.md).
