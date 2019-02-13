---
title: Afinidade de utilizador para híbrida de dispositivos geridos
titleSuffix: Configuration Manager
description: Configure a afinidade de utilizador para dispositivos geridos no Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b5d520a7-e9e5-40ee-91f9-f2684214beb6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 54ca57956db37a26e2edad27c6cf6b92aecd1645
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138913"
---
# <a name="user-affinity-for-hybrid-managed-devices-in-configuration-manager"></a>Afinidade de utilizador para híbrida geridos os dispositivos no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Ao configurar perfis de dispositivos pertencentes à empresa, o administrador pode especificar se os dispositivos geridos podem ter *afinidade de utilizador* que identifica um utilizador específico com o dispositivo.  

##  <a name="BKMK_iOSCP"></a> Dispositivos geridos com afinidade do utilizador  
 Os dispositivos configurados com **user affinity** podem instalar e executar a aplicação Portal da Empresa para transferir aplicações e gerir dispositivos. Assim que os utilizadores recebem os respetivos dispositivos, tem de executar vários passos adicionais para concluir o Assistente de configuração e instalar a aplicação Portal da empresa.  

#### <a name="how-to-enroll-ios-devices-with-user-affinity"></a>Como inscrever dispositivos iOS com afinidade de utilizador  

1.  Quando os utilizadores ligam-se primeiro nos respetivos dispositivos novos, é-lhes pedido que concluam o Assistente de configuração. O perfil de inscrição, pode especificar para solicitar credenciais durante a configuração. Os utilizadores podem utilizar as credenciais (ou seja, o nome pessoal exclusivo ou UPN) associadas à respetiva subscrição no Intune.  

2.  Durante a configuração, também podem ser pedido aos utilizadores para um ID Apple. Deve ser fornecido um Apple ID antes do dispositivo pode instalar o Portal da empresa. Os utilizadores podem fornecer um Apple ID após a configuração estar concluída no iOS **definições** menu.  

3.  Depois de concluir a configuração, o dispositivo iOS tem de instalar a aplicação Portal da empresa partir da App Store, por exemplo [aplicação Portal da empresa](https://itunes.apple.com/us/app/id719171358).  

4.  O utilizador pode agora iniciar sessão no Portal da empresa com o UPN utilizado quando configurou o dispositivo.  

5.  Após iniciar sessão, é pedido ao utilizador para inscrever o dispositivo. O primeiro passo é **Identificar o dispositivo**. A aplicação apresenta uma lista de dispositivos iOS pertencentes à empresa e atribuídos à conta do Intune do utilizador final. Selecione o dispositivo correspondente.  

     Se este dispositivo não estiver já pertencentes à empresa, selecione "novo dispositivo" para continuar o fluxo de inscrição padrão.  

6.  No ecrã seguinte, o utilizador tem de confirmar o número de série do novo dispositivo. O utilizador pode tocar na ligação “confirme o número de série” de modo a iniciar a aplicação Definições para verificar o número de série. Em seguida, o utilizador tem de introduzir os últimos 4 carateres do número de série na aplicação Portal da Empresa.  

     Este passo verifica se o dispositivo é o dispositivo da empresa inscrito no Intune. Se o número de série do dispositivo não coincidir, significa que foi selecionado o dispositivo errado. Voltar ao ecrã anterior e selecione um dispositivo diferente.  

7.  Depois de verificar o número de série, a aplicação Portal da empresa redireciona para o site do Portal da empresa para finalizar a inscrição e, em seguida, pede ao utilizador para regressar à aplicação.  

8.  A inscrição está agora concluída. Agora, pode utilizar este dispositivo com o conjunto completo de capacidades.  

##  <a name="BKMK_noUA"></a> Dispositivos geridos sem afinidade do utilizador  
 Os dispositivos configurados com **no user affinity** não suportam o Portal da Empresa e não devem instalar a aplicação. O Portal da Empresa foi concebido para utilizadores com credenciais da empresa e que necessitam de acesso a recursos empresariais personalizados (por exemplo, e-mail). Os dispositivos inscritos **sem afinidade de utilizador** não se destinam a ter um início de sessão de utilizador dedicado. Os dispositivos de quiosque, ponto de venda (POS) ou utilitário partilhado são casos de utilização típicos para dispositivos inscritos sem afinidade de utilizador. Se for necessária afinidade de utilizador, certifique-se de que o perfil de inscrição do dispositivo tem a opção **Afinidade de Utilizador** selecionada antes de inscrever o dispositivo. Para alterar o estado de afinidade num dispositivo, tem de extinguir e voltar a inscrever o dispositivo.
