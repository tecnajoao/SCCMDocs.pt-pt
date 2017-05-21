---
title: "Afinidade de utilizador para uma implementação híbrida geridos dispositivos no Configuration Manager | Documentos do Microsoft"
description: Configure a afinidade de utilizador para dispositivos geridos no Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5d520a7-e9e5-40ee-91f9-f2684214beb6
caps.latest.revision: 6
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: d039792a88b9e7704f37718a88f841dd9216d1b1
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="user-affinity-for-hybrid-managed-devices-in-configuration-manager"></a>Afinidade de utilizador para uma implementação híbrida geridos dispositivos no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando configurar perfis para os dispositivos da empresa, o administrador pode especificar se os dispositivos geridos podem ter *afinidade do utilizador* que identifica um utilizador específico com o dispositivo.  

##  <a name="BKMK_iOSCP"></a>Dispositivos geridos com a afinidade do utilizador  
 Os dispositivos configurados com **user affinity** podem instalar e executar a aplicação Portal da Empresa para transferir aplicações e gerir dispositivos. Uma vez, os utilizadores recebem os respetivos dispositivos, tem de concluir vários passos adicionais para concluir o Assistente de configuração e instalar a aplicação de Portal da empresa.  

#### <a name="how-to-enroll-ios-devices-with-user-affinity"></a>Como inscrever dispositivos iOS com o afinidade do utilizador  

1.  Quando os utilizadores do power primeiro nos respetivos dispositivos novos, são-lhe pedidos para concluir o Assistente de configuração. Pode especificar o perfil de inscrição para solicitar credenciais durante a configuração. Os utilizadores tem de utilizar as credenciais (ou seja, o nome exclusivo de pessoal ou o UPN) associadas a respetiva subscrição no Intune.  

2.  Durante a configuração, os utilizadores podem também ser-lhe pedidos para um ID Apple. Tem de ser fornecido um ID Apple antes do dispositivo pode instalar o Portal da empresa. Os utilizadores podem fornecer um ID Apple após a configuração está concluída a partir do iOS **definições** menu.  

3.  Após concluir a configuração, o dispositivo iOS tem de instalar a aplicação de Portal da empresa a partir da loja de aplicações, por exemplo [aplicação Portal da empresa](https://itunes.apple.com/us/app/id719171358).  

4.  O utilizador pode iniciar sessão no Portal da empresa com o UPN utilizada quando configurar o dispositivo.  

5.  Após iniciar sessão, o utilizador é pedido ao inscrever o respetivo dispositivo. O primeiro passo é **Identificar o dispositivo**. A aplicação apresenta uma lista de dispositivos iOS pertencentes e atribuídos a conta do Intune-do utilizador final. Selecione o dispositivo correspondente.  

     Se este dispositivo não estiver já pertencentes, selecione "device novo" para continuar com o fluxo de inscrição padrão.  

6.  No ecrã seguinte, o utilizador tem de confirmar a série do dispositivo novo. O utilizador pode tocar na ligação “confirme o número de série” de modo a iniciar a aplicação Definições para verificar o número de série. Em seguida, o utilizador tem de introduzir os últimos 4 carateres do número de série na aplicação Portal da Empresa.  

     Este passo verifica se o dispositivo é o dispositivo da empresa inscrito no Intune. Se o número de série do dispositivo não coincidir, significa que foi selecionado o dispositivo errado. Voltar ao ecrã anterior e selecione um dispositivo diferente.  

7.  Depois de verificar o número de série, a aplicação de Portal da empresa redireciona para o Web site do Portal da empresa para finalizar a inscrição e, em seguida, pede ao utilizador para voltar para a aplicação.  

8.  A inscrição está agora concluída. Agora, pode utilizar este dispositivo com o conjunto completo de capacidades.  

##  <a name="BKMK_noUA"></a>Dispositivos geridos sem afinidade de utilizador  
 Os dispositivos configurados com **no user affinity** não suportam o Portal da Empresa e não devem instalar a aplicação. O Portal da Empresa foi concebido para utilizadores com credenciais da empresa e que necessitam de acesso a recursos empresariais personalizados (por exemplo, e-mail). Os dispositivos inscritos **sem afinidade de utilizador** não se destinam a ter um início de sessão de utilizador dedicado. Os dispositivos de quiosque, ponto de venda (POS) ou utilitário partilhado são casos de utilização típicos para dispositivos inscritos sem afinidade de utilizador. Se for necessária afinidade de utilizador, certifique-se de que o perfil de inscrição do dispositivo tem a opção **Afinidade de Utilizador** selecionada antes de inscrever o dispositivo. Para alterar o estado de afinidade num dispositivo, tem de extinguir e voltar a inscrever o dispositivo.

