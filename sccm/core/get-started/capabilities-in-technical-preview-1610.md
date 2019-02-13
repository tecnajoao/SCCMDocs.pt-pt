---
title: Funcionalidades no Technical Preview versão 1610
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1610.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7b164dfe1ea175f0f2141039c3a4a800de1404b9
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132358"
---
# <a name="capabilities-in-technical-preview-1610-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview versão 1610 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*



Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1610. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para a utilização de um Technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.    


**Seguem-se os novos recursos, que pode experimentar com esta versão.**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrar por tamanho do conteúdo nas regras de implementação automática
Agora pode filtrar o tamanho do conteúdo para atualizações de software nas regras de implementação automática. Por exemplo, pode definir o **conteúdo tamanho (KB)** filtrar para **< 2048** para transferir apenas atualizações de software que são mais pequenas do que 2 MB. Utilizar este filtro impede que as atualizações de software grandes sejam transferidas automaticamente para melhor Windows de suporte simplificado de manutenção quando a largura de banda de rede de nível inferior. Para obter detalhes, consulte [Configuration Manager e simplificado de Windows manutenção em baixo nível de sistemas operativos](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).

#### <a name="to-configure-the-content-size-field"></a>Para configurar o campo de tamanho do conteúdo
Para configurar o **conteúdo tamanho (KB)** campo, vá para o **atualizações de Software** página Criar regra de Assistente de implementação automática quando criar uma ADR ou vá para o **atualizações de Software**separador nas propriedades de uma ADR existente.

![Campo de tamanho do conteúdo](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>Funcionalidade aprimorada para caixas de diálogo do software necessário
Quando um utilizador recebe o software necessário, do **suspender e lembrar-me:** definir, podem selecionar da lista pendente seguinte de valores:
- Mais tarde: Especifica que as notificações estão agendadas com base nas definições de notificação configuradas nas definições do agente de cliente.
- Fixo de tempo: Especifica que a notificação será agendada para apresentar novamente após o tempo selecionado. Por exemplo, se um usuário selecionar 30 minutos, irá apresentar a notificação novamente dentro de 30 minutos.

![Página de agente do computador nas definições do agente de cliente](media/computeragentsettings.png)

O tempo máximo suspender baseia-se sempre nos valores de notificação configurados nas definições de agente do cliente em cada tempo ao longo da linha do tempo de implementação. Por exemplo, se o **implementação prazo superior a 24 horas, lembrar os usuários a cada (horas)** definição no computador agente página está configurada para dez horas, e é mais de 24 horas antes do prazo quando a caixa de diálogo é iniciada, o utilizador verá um conjunto de opções de suspender até mas nunca maiores do que 10 horas. À medida que o prazo aproxima, a caixa de diálogo irá mostrar menos opções, consistentes com as definições de agente do cliente relevantes para cada componente da linha da tempo de implementação.

Além disso, para uma implementação de alto risco, como uma sequência de tarefas que implementa um sistema operativo, a experiência de notificação do utilizador final é agora mais intrusiva. Em vez de uma notificação de barra de tarefas transitório, sempre que o utilizador é notificado de que a manutenção crítica do software é necessária, um caixa de diálogo, como o seguinte é apresentado no computador do usuário:

![Caixa de diálogo de Software necessária](media/requiredsoftwaredialog.png)


Para obter mais informações:
- [Definições para gerir implementações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Como configurar as definições do cliente](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>Negar pedidos de aplicações previamente aprovados

Como administrador agora pode negar um pedido de aplicação aprovado anteriormente. Uma vez negado, para instalar esta aplicação posteriores utilizadores devem reenviar um pedido. Negação não desinstala a aplicação; em vez disso, ela força reapproval para todas as novas solicitações para essa aplicação do utilizador. Anteriormente, a negação de pedido de aplicação só estava disponível para pedidos de aplicações que não tinham sido aprovados.

#### <a name="try-it-out"></a>Experimentar
Para negar um aplicativo aprovou o pedido:

1.  Na consola do Configuration Manager, [criar e implementar uma aplicação](https://docs.microsoft.com/sccm/apps/deploy-use/create-applications) que requer aprovação.
2.  Num computador cliente, abra o Centro de Software e submeter um pedido para a aplicação.
3.  Na consola do Configuration Manager, aprove o pedido de aplicação.
4.  Negar o pedido de aplicação aprovada: Na consola do Configuration Manager, navegue até **biblioteca de Software** > **descrição geral** > **gestão de aplicações**  >  **Pedidos de aprovação** e selecione o pedido de aplicação que pretende negar.  No Friso, clique em **negar**.

## <a name="exclude-clients-from-automatic-upgrade"></a>Excluir clientes da atualização automática
1610 do Technical Preview introduz uma nova definição que pode utilizar para excluir uma coleção de clientes instalem automaticamente as versões de cliente atualizado.  Isto aplica-se a atualização automática, bem como outros métodos, como a atualização baseada em atualização de software, scripts de logon e a política de grupo. Isso pode ser usado para uma coleção de computadores que necessitam de maior cuidado ao atualizar o cliente. Um cliente que está numa coleção excluída ignora os pedidos para instalar o software de cliente atualizado.

### <a name="configure-exclusion-from-automatic-upgrade"></a>Configurar a exclusão de atualização automática
Para configurar exclusões de atualização automática:
1. Na consola do Configuration Manager, abra **definições de hierarquia** sob **administração > Configuração do Site > Sites**e, em seguida, selecione o **atualização de cliente** separador.
2. Selecione a caixa de verificação **excluir os clientes especificados da atualização**e, em seguida, para **coleção de exclusão**, selecione a coleção que pretende excluir. Só pode selecionar uma única coleção de exclusão.
3. Clique em **OK** para fechar e guardar a configuração. Em seguida, depois de clientes de atualização de política, os clientes na coleção excluída já não instalará automaticamente atualizações para o software de cliente.

   ![Definições de atualização automática de exclusão](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> Embora a interface do usuário indica que os clientes não serão atualizados através de qualquer método, existem dois métodos que pode utilizar para substituir estas definições. Instalação push do cliente e uma instalação de cliente manual podem ser utilizados para substituir esta configuração. Para obter mais detalhes, consulte a secção seguinte.

### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Como atualizar um cliente que está numa coleção excluída
Uma coleção é configurada para ser excluído, desde que os membros dessa coleção só podem ter seu software de cliente atualizado por um dos dois métodos, substituem a exclusão:
- **Instalação Push do cliente** – pode utilizar a instalação de push de cliente para atualizar um cliente que está numa coleção excluída. Isso é permitido uma vez que ele é considerado como estando a intenção do administrador e permite-lhe atualizar os clientes sem remover toda a coleção de exclusão.       
- **Instalação de cliente manual** – pode atualizar manualmente os clientes que estão numa coleção excluída ao utilizar o seguinte comutador de linha de comandos com o ccmsetup: ***/ignoreskipupgrade***

  Se tenta atualizar manualmente um cliente que seja membro da coleção excluída e não utilize este parâmetro, o cliente não será instalado o novo software de cliente. Para obter mais informações, consulte [como instalar clientes manualmente do Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-configuration-manager-clients-manually).

Para obter mais informações sobre métodos de instalação de cliente, consulte [como implementar clientes em computadores do Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).

## <a name="windows-defender-configuration-settings"></a>Definições de configuração do Windows Defender

Agora, pode configurar definições de cliente do Windows Defender em computadores Windows 10 inscritos no Intune com itens de configuração na consola do Configuration Manager.

Especificamente, pode configurar as seguintes definições do Windows Defender:
- Permitir monitorização em tempo real
- Permitir monitorização de comportamento
- Ativar o Sistema de Inspeção de Rede
- Analisar todas as transferências
- Permitir análise de scripts
- Monitorizar a atividade de programas e ficheiros
  - Ficheiros monitorizados
- Dias para controlar o software maligno resolvido
- Permitir acesso à IU de cliente
- Agendar uma análise de sistema
  - Dia agendado
  - Hora agendada
- Agendar uma análise rápida diária
  - Hora agendada
- % De utilização de limite da CPU durante uma análise de análise de ficheiros de arquivo
- Analisar mensagens de e-mail
- Analisar unidades amovíveis
- Analisar unidades mapeadas
- Analisar ficheiros abertos a partir de partilhas de redes
- Intervalo de atualização de assinatura
- Permitir proteção da cloud
- Pedir aos utilizadores de exemplos
- Deteção de aplicação indesejável potencialmente
- Ficheiros/pastas excluídas
- Extensões de ficheiro excluídos
- Processos excluídos

> [!NOTE]
> Estas definições só podem ser configuradas em computadores cliente com a atualização de Novembro do Windows 10 (versão 1511) e superior.

### <a name="try-it-out"></a>Experimente!

1.  Na consola do Configuration Manager, aceda **ativos e compatibilidade** > **descrição geral** > **as definições de compatibilidade**  >   **Itens de configuração**e crie um novo **Item de configuração**.
2.  Introduza um nome, em seguida, selecione **Windows 8.1 e Windows 10** sob **definições para dispositivos geridos sem o cliente de Configuration Manager** e clique em **seguinte**.
3.  Certifique-se **todos os Windows 10 (64-bit)** e **todos os Windows 10 (32-bit)** são selecionadas no **plataformas suportadas** página, em seguida, clique em **seguinte**.
4.  Selecione o **o Windows Defender** Definir grupo, em seguida, clique em **próxima**.
5.  Configure as definições pretendidas nesta página, em seguida, clique em **seguinte**.
6.  Conclua o assistente.
7.  Adicionar este item de configuração para uma linha de base de configuração e implementar esta linha de base para computadores que executam a atualização de Novembro do Windows 10 (versão 1511) ou superior.

> [!NOTE]
> Não se esqueça das **remediar definições incompatíveis** caixa de verificação ao implementar a linha de base de configuração.

## <a name="request-policy-sync-from-administrator-console"></a>Política de pedido de sincronização da consola do administrador

Agora pode pedir uma sincronização de política para um dispositivo móvel a partir da consola do Configuration Manager, em vez de terem de pedir uma sincronização a partir do próprio dispositivo. Informações de estado do pedido de sincronização estão disponíveis como uma nova coluna em modos de exibição do dispositivo, chamado **estado de sincronização de remoto**. Estado também aparece na **dados de deteção** secção a **propriedades** caixa de diálogo para cada dispositivo móvel.

### <a name="try-it-out"></a>Experimente!

1.  Na consola do Configuration Manager, aceda **ativos e compatibilidade** > **descrição geral** > dispositivos.
2.  Na **ações do dispositivo remoto** menu, selecione **enviar pedido de sincronização**.

A sincronização pode demorar de cinco a dez minutos. Todas as alterações na política são sincronizadas no dispositivo. Pode controlar o estado do pedido de sincronização no **estado de sincronização de remoto** coluna na **dispositivos** vista, ou em do dispositivo **propriedades** caixa de diálogo.

## <a name="additional-security-role-support"></a>Suporte de função de segurança adicionais

Além de administrador completo, as seguintes funções de segurança incorporadas agora tem acesso total aos itens no **todos os dispositivos da empresa** nó, incluindo **dispositivos pré-declarados**, **iOS Perfis de inscrição**, e **perfis de inscrição do Windows**: • **Gestor do Asset Intelligence** • **Gestor de acesso de recursos da empresa**

Acesso só de leitura para essas áreas da consola do Configuration Manager ainda é concedido para o **analista só de leitura** função.

## <a name="conditional-access-for-windows-10-vpn-profiles"></a>Acesso condicional para perfis de VPN do Windows 10

Agora pode exigir a Windows 10 inscritos no Azure Active Directory para estar em conformidade, para ter acesso VPN através de perfis de VPN do Windows 10 criadas na consola do Configuration Manager. Isso é possível por meio do novo **ativar o acesso condicional para esta ligação VPN** caixa de seleção o **método de autenticação** página no Assistente de perfil VPN e propriedades de perfil VPN para a VPN do Windows 10 perfis. Também pode especificar um certificado diferente para autenticação de início de sessão único se ativar o acesso condicional para o perfil.

## <a name="see-also"></a>Consulte Também
[Pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md)
