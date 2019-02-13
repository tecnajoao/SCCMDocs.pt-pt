---
title: 'Inscrever dispositivos pertencentes à empresa '
titleSuffix: Configuration Manager
description: Saiba mais sobre os diferentes métodos para inscrever dispositivos pertencentes à empresa para implementações híbridas com o Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e2754ce6-1460-4ddd-9050-2cc87e7964f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a3586f51b7112f8667b7e120ea278ceb9adbbe89
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129447"
---
# <a name="enroll-company-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Inscrever dispositivos pertencentes à empresa para implementações híbridas com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Organização ou os dispositivos da empresa (COD) podem ser colocados em gestão de variadas formas consoante o dispositivo e como foi comprado.  

## <a name="enroll-device-enrollment-program-ios-devices"></a>Inscrever dispositivos do programa de inscrição de dispositivos iOS  
 Implementa um perfil de inscrição "por ondas eletromagnéticas" para dispositivos adquiridos através do programa de inscrição de dispositivos da Apple. Quando o utilizador executa o Assistente de configuração no dispositivo, o dispositivo é inscrito no Intune.  Dispositivos inscritos através do DEP não podem ser anulados por utilizadores. Ver [inscrição do iOS Device Enrollment Program (DEP) para implementações híbridas com o Configuration Manager](../../mdm/deploy-use/ios-device-enrollment-program-for-hybrid.md).  

## <a name="enroll-ios-devices-with-apple-configurator"></a>Inscrever dispositivos iOS com o Apple Configurator  
 Este método requer que o administrador para USB ligue o dispositivo iOS a um computador Mac com o Apple Configurator para pré-configurar a inscrição. Em seguida, são entregues dispositivos aos seus utilizadores que executam o processo de Assistente de configuração, configurar o dispositivo com as respetivas credenciais escolares ou profissionais e concluir o processo de inscrição. Ver [inscrição do iOS híbrida com o Apple Configurator com o Configuration Manager](../../mdm/deploy-use/ios-hybrid-enrollment-using-apple-configurator.md).  

## <a name="device-enrollment-manager"></a>Gestor de inscrição de dispositivos  
 As organizações podem utilizar o Intune para gerir um grande número de dispositivos móveis com uma conta de utilizador único denominada uma conta de Gestor de inscrição de dispositivos. Depois de criar uma conta de Gestor de inscrição de dispositivos, essa conta pode ser utilizada por um gestor para inscrever mais do que os cinco dispositivos padrão permitidos por predefinição para os utilizadores normais. Inscrição de dispositivos com um Gestor de inscrição de dispositivos funciona apenas para dispositivos que não são utilizados por um utilizador específico. Estes dispositivos são ideais para o ponto de venda ou utilitários aplicações, por exemplo, mas inadequados para utilizadores que necessitam de aceder a recursos ou e-mails da empresa. Ver [inscrever dispositivos com o Gestor de inscrição de dispositivos com o Configuration Manager](../../mdm/deploy-use/enroll-devices-with-device-enrollment-manager.md).  

## <a name="user-affinity-for-managed-devices"></a>Afinidade de utilizador para dispositivos geridos  
 Ao configurar perfis de dispositivos pertencentes à empresa, o administrador pode especificar se os dispositivos geridos suportam *afinidade de utilizador* que identifica um utilizador específico com o dispositivo. Os dispositivos configurados com **user affinity** podem instalar e executar a aplicação Portal da Empresa para transferir aplicações e gerir dispositivos. Ver [afinidade de utilizador para híbrida geridos os dispositivos no Configuration Manager](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md).  

## <a name="manage-devices-with-activation-lock"></a>Gerir dispositivos com o bloqueio de ativação  
 Microsoft Intune pode ajudá-lo a gerir o bloqueio de ativação, uma funcionalidade do veja iOS a minha aplicação do iPhone para iOS 7.1 e dispositivos posteriores. O Bloqueio de Ativação é ativado automaticamente ao utilizar a aplicação Encontrar o Meu iPhone num dispositivo. Ver [gerir o bloqueio de ativação com o System Center Configuration Manager iOS](../../mdm/deploy-use/manage-ios-activation-lock.md).

 ## <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Pré-declarar dispositivos com números de série IMEI ou iOS

É possível identificar os dispositivos pertencentes ao importar os números do internacional do equipamento móvel (IMEI) de identidade ou números de série iOS. Pode carregar um ficheiro de valores separados por vírgulas (. csv) que contenha números IMEI de dispositivos ou pode introduzir manualmente as informações do dispositivo.  Ver [pré-declarar dispositivos com números de ID de hardware](../../mdm/deploy-use/predeclare-devices-with-hardware-id.md).
