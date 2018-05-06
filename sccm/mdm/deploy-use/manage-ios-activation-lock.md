---
title: Gerir o Bloqueio de Ativação do iOS
titleSuffix: Configuration Manager
description: Gerir o bloqueio de ativação com o System Center Configuration Manager iOS.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e2745bac-e1b4-4dac-8ac7-32f1c820bc9c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4550116bd4635e7320e9cbdf18997e2e17ae0466
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="manage-ios-activation-lock-with-system-center-configuration-manager"></a>Gerir o Bloqueio de Ativação do iOS com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


O System Center Configuration Manager pode ajudá-lo a gerir o Bloqueio de Ativação do iOS, uma funcionalidade da aplicação Encontrar iPhone para iOS 7.1 e dispositivos posteriores. Quando o Bloqueio de Ativação está ativado, o Apple ID e a palavra-passe do utilizador têm de ser introduzidos primeiro para que qualquer pessoa possa:

- Desativar a aplicação Encontrar o Meu iPhone
- Apagar o dispositivo
- Reativar o dispositivo

Em dispositivos **não supervisionados** , o Bloqueio de Ativação é ativado automaticamente quando a aplicação Encontrar iPhone é utilizada.

Em dispositivos **supervisionados** , tem de ativar o Bloqueio de Ativação através das definições de compatibilidade do Configuration Manager.

> [!TIP]
> O modo supervisionado para dispositivos iOS permite-lhe utilizar a Ferramenta de Configuração da Apple para bloquear um dispositivo, de forma a limitar a funcionalidade para fins empresariais específicos. O modo supervisionado destina-se, geralmente, apenas para dispositivos dos utilizadores da empresa.

Embora o Bloqueio de Ativação ajude a proteger os dispositivos iOS e melhore as possibilidades de recuperação em caso de roubo ou perda, esta funcionalidade pode apresentar-lhe, na qualidade de administrador de TI, vários desafios. Por exemplo:

- Um dos seus utilizadores configura o Bloqueio de Ativação num dispositivo. O utilizador sai da empresa e devolve o dispositivo. Sem o Apple ID e a palavra-passe do utilizador, não existe nenhuma forma de reativar o dispositivo, mesmo se o apagar.
- É necessário um relatório de todos os dispositivos que têm o Bloqueio de Ativação ativado.
- Durante a atualização do dispositivo na sua organização, deve reatribuir alguns dispositivos para outro departamento. Apenas pode reatribuir dispositivos que não têm o Bloqueio de Ativação ativado.


Para ajudar a resolver estes problemas, a Apple introduziu a desativação do Bloqueio de Ativação no iOS 7.1. Isto permite-lhe remover o Bloqueio de Ativação a partir de dispositivos supervisionados sem o Apple ID e a palavra-passe do utilizador. Os dispositivos supervisionados podem gerar um código de desativação do Bloqueio de Ativação específico para o dispositivo, que é armazenado no servidor de ativação da Apple.

Pode ler mais sobre o Bloqueio de Ativação [aqui](https://support.apple.com/HT201365).

## <a name="how-configuration-manager-helps-you-manage-activation-lock"></a>Como o Configuration Manager o ajuda a gerir o Bloqueio de Ativação

O Configuration Manager pode ajudá-lo a gerir o Bloqueio de Ativação de duas formas:

1. Ative o Bloqueio de Ativação em dispositivos supervisionados.
2. Ignore o Bloqueio de Ativação em dispositivos supervisionados.

> [!IMPORTANT]
> Não pode ignorar o Bloqueio de Ativação em dispositivos não supervisionados.

As vantagens comerciais desta funcionalidade para dispositivos pertencentes à empresa são:



- O utilizador obtém as vantagens de segurança da aplicação Encontrar o Meu iPhone
- Pode permitir que o utilizador trabalhe sabendo que quando o dispositivo tiver de ser reaproveitado, pode extinguí-lo ou desbloqueá-lo


## <a name="enable-activation-lock-on-supervised-devices"></a>Ativar o bloqueio de ativação em dispositivos supervisionados

Utilize as definições de compatibilidade do Configuration Manager para criar e implementar um item de configuração do tipo **iOS e Mac OS X** para ativar o Bloqueio de Ativação em dispositivos supervisionados:

1. Utilize as informações do tópico [Como criar itens de configuração para os dispositivos iOS e Mac OS X geridos sem o cliente System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client) para criar um item de configuração do tipo **iOS e Mac OS X**.
2. Na página **Segurança do Sistema** do Assistente de Criação de Item de Configuração, configure a definição **Permitir Bloqueio de Ativação (modo supervisionado apenas)** como **Permitido**.
3. [Adicione o item de configuração a uma linha de base da configuração](/sccm/compliance/deploy-use/create-configuration-baselines).
4. [Implemente esta linha de base da configuração](/sccm/compliance/deploy-use/deploy-configuration-baselines) numa coleção que contenha os dispositivos iOS para os quais pretende ativar o Bloqueio de Ativação.

> [!IMPORTANT]
> Certifique-se de que está na posse física do dispositivo antes de seguir este procedimento. Se não o fizer, o Bloqueio de Ativação será ignorado e quem estiver na posse do dispositivo terá acesso total ao mesmo, permitindo que essa pessoa desative a aplicação Encontrar iPhone, apague o dispositivo ou reative o dispositivo.

Só pode ignorar o Bloqueio de Ativação ou obter o código para ignorar o Bloqueio de Ativação em dispositivos supervisionados. Tentar ignorar o bloqueio de ativação num dispositivo não supervisionado ou ver o código para ignorar resulta num erro.



## <a name="view-the-activation-lock-bypass-code"></a>Vista de código de ignorabilidade do bloqueio de ativação

1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2. Na área de trabalho **Ativos e Compatibilidade** , clique em **Dispositivos**.
3. Selecione um dispositivo inscrito que esteja no modo supervisionado e que tenha o Bloqueio de Ativação ativado.
4. No separador **Base** , no grupo **Dispositivo** , clique em **Ações do Dispositivo Remoto** > **Ver o Código para Ignorar o Bloqueio da Ativação**.
5. A caixa de diálogo **Código para Ignorar o Bloqueio da Ativação** apresenta o código para ignorar para o dispositivo selecionado.

## <a name="bypass-activation-lock"></a>Ignorar bloqueio de ativação

1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2. Na área de trabalho **Ativos e Compatibilidade** , clique em **Dispositivos**.
3. Selecione um dispositivo inscrito que esteja no modo supervisionado e que tenha o Bloqueio de Ativação ativado.
3. No separador **Base** , no grupo **Dispositivos** , clique em **Ações do Dispositivo Remoto** > **Ignorar Bloqueio de Ativação**.
5. Leia as mensagens na caixa de diálogo de aviso e clique em **Sim** quando estiver pronto para continuar.
6. Pode examinar o estado do pedido de desbloqueio a partir:

    - Dos dados de deteção para o dispositivo na caixa de diálogo de propriedades do dispositivo.
    - Da coluna **Estado da Ação Ignorar o Bloqueio da Ativação** na vista **Dispositivos** (esta coluna está oculta por predefinição).
    - Da secção **Informações sobre Ações do Dispositivo Remoto** no separador **Resumo** do painel de detalhes (quando um dispositivo está selecionado).
