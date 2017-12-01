---
title: Funcionalidades no Technical Preview 1610
titleSuffix: Configuration Manager
description: "Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1610."
ms.custom: na
ms.date: 01/23/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: article
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
caps.latest.revision: "2"
author: erikje
ms.author: erikje
manager: angrobe
ms.openlocfilehash: 1ab5ce458b4892422aa82ae99ed69ae2eb671583
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="capabilities-in-technical-preview-1610-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1610 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*



Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1610. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão do technical preview, reveja o tópico introdutórias, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrar pelo tamanho do conteúdo nas regras de implementação automática
Agora pode filtrar o tamanho do conteúdo para atualizações de software nas regras de implementação automática. Por exemplo, pode definir o **conteúdo tamanho (KB)** filtrar para **< 2048** para transferir apenas atualizações de software que são inferior a 2 MB. Utilizar este filtro impede que as atualizações de software grande automaticamente a transferência para um melhor suporte simplificado Windows quando a largura de banda de rede é limitada de manutenção de nível inferior. Para obter mais informações, consulte [do Configuration Manager e simplificada manutenção do Windows em baixo nível de sistemas operativos](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).

#### <a name="to-configure-the-content-size-field"></a>Para configurar o campo de tamanho do conteúdo
Para configurar o **conteúdo tamanho (KB)** campo, acedo ao **atualizações de Software** página no Assistente de criação automática implementação regra quando criar uma ADR ou vá para o **atualizações de Software** separador nas propriedades de uma ADR existente.

![Campo de tamanho do conteúdo](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>Funcionalidade melhorada para caixas de diálogo de software necessárias
Quando um utilizador recebe o software necessário, do **Snooze e avisar-me Depois:** definição, podem selecionar a partir da seguinte na lista pendente de valores:
- Mais tarde: Especifica que as notificações são agendadas baseada nas definições de notificação configuradas nas definições do agente de cliente.
- Fixo de tempo: Especifica que a notificação será agendada a apresentar depois do tempo selecionado. Por exemplo, se um utilizador seleccionar 30 minutos, irá apresentar a notificação novamente dentro de 30 minutos.

![Página de agente do computador nas definições do agente de cliente](media/computeragentsettings.png)

O tempo máximo de suspensão é sempre com base nos valores de notificação configurados nas definições do agente do cliente em sempre ao longo da linha cronológica de implementação. Por exemplo, se o **implementação prazo superior a 24 horas, lembrar utilizadores cada (horas)** definição no computador agente página está configurada para 10 horas e é mais de 24 horas antes do prazo quando é iniciada a caixa de diálogo, o utilizador deverá ser apresentado com um conjunto de opções de suspensão até mas nunca superior a 10 horas. Como se aproxima do prazo, a caixa de diálogo irá mostrar menos opções, consistentes com as definições de agente do cliente relevantes para cada componente da linha cronológica de implementação.

Além disso, para uma implementação de alto risco, como uma sequência de tarefas que implementa um sistema operativo, a experiência de notificação do utilizador final é agora mais intrusivo. Em vez de uma notificação de barra de tarefas transitório, sempre que o utilizador é notificado de que a manutenção crítica do software é necessária, um caixa de diálogo, tais como a apresenta seguintes no computador do utilizador:

![Caixa de diálogo de Software necessária](media/requiredsoftwaredialog.png)


Para obter mais informações:
- [Definições para gerir implementações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Como configurar as definições do cliente](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>Negar pedidos de aplicação anteriormente aprovados

Como um administrador pode agora negar um pedido de aplicação anteriormente aprovados. Uma vez negado, para instalar esta aplicação utilizadores posteriores tem de submeter um pedido. Negação não desinstala a aplicação; em vez disso, força reapproval qualquer pedido de novo para essa aplicação do utilizador. Anteriormente, a recusa do pedido de aplicação só estava disponível para pedidos de aplicação que não tinham sido aprovados.

#### <a name="try-it-out"></a>Experimente
Para negar uma aplicação aprovou o pedido:

1.  Na consola do Configuration Manager, [criar e implementar uma aplicação](https://docs.microsoft.com/sccm/apps/deploy-use/create-applications) que necessita de aprovação.
2.  Num computador cliente, abra o Centro de Software e submeter um pedido para a aplicação.
3.  Na consola do Configuration Manager, aprove o pedido de aplicação.
4.  Negar o pedido de aplicação aprovados: Na consola do Configuration Manager, navegue **biblioteca de Software** > **descrição geral** > **gestão de aplicações** > **pedidos de aprovação** e selecione o pedido de aplicação que pretende negar.  No Friso, clique em **negar**.

## <a name="exclude-clients-from-automatic-upgrade"></a>Excluir os clientes da atualização automática
1610 do Technical Preview introduz uma nova definição, que pode utilizar para excluir uma coleção de clientes a instalar automaticamente as versões de cliente atualizado.  Isto aplica-se a atualização automática, bem como outros métodos, tais como a atualização baseada em atualização de software, scripts de início de sessão e política de grupo. Isto pode ser utilizado para uma coleção de computadores que necessitam de maior cuidado ao atualizar o cliente. Um cliente que está a ser uma coleção excluída ignora os pedidos para instalar o software de cliente atualizado.

### <a name="configure-exclusion-from-automatic-upgrade"></a>Configurar a exclusão de atualização automática
Para configurar exclusões de atualização automáticas:
1.  Na consola do Configuration Manager, abra **definições de hierarquia** em **administração > Configuração do Site > Sites**e, em seguida, selecione o **atualização de cliente** separador.
2.  Selecione a caixa de verificação **excluir especificado de clientes de atualização**e, em seguida, para **coleção de exclusão**, selecione a coleção que pretende excluir. Só pode selecionar uma única coleção para exclusão.
3.  Clique em **OK** para fechar e guardar a configuração. Em seguida, depois de política de atualização de clientes, os clientes na coleção excluída automaticamente já não irão instalar atualizações para o software de cliente.

  ![Definições de exclusão de atualização automática](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> Embora a interface de utilizador de Estados de que os clientes não serão atualizados através de qualquer método, existem dois métodos que pode utilizar para substituir estas definições. Instalação push do cliente e uma instalação de cliente manual podem ser utilizadas para substituir esta configuração. Para obter mais detalhes, consulte a secção seguinte.

### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Como atualizar um cliente que está a ser uma coleção excluída
Uma coleção é configurada a serem excluídos, desde que os membros dessa coleção só podem ter atualizado por um dos dois métodos que substituem a exclusão do respetivo software de cliente:
 - **Instalação Push do cliente** – pode utilizar a instalação push do cliente para atualizar um cliente que está a ser uma coleção excluída. Isto é permitido como é considerada a intenção do administrador e permite-lhe atualizar os clientes sem remover o conjunto completo de exclusão.       
 - **Instalação de cliente manual** – pode atualizar manualmente os clientes que estejam numa coleção excluída quando utilizar o seguinte parâmetro de linha de comandos com ccmsetup: ***/ignoreskipupgrade***

  Se tentar atualizar manualmente um cliente que é um membro da coleção excluída e não utilize este parâmetro, o cliente não irá instalar o software de cliente novo. Para obter mais informações consulte [como instalar o Configuration Manager clientes manualmente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-configuration-manager-clients-manually).

Para obter mais informações sobre métodos de instalação de cliente, consulte [como implementar clientes em computadores Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).

## <a name="windows-defender-configuration-settings"></a>Definições de configuração do Windows Defender

Agora, pode configurar as definições de cliente do Windows Defender em computadores Windows 10 inscritos no Intune, utilizar itens de configuração na consola do Configuration Manager.

Especificamente, pode configurar as seguintes definições do Windows Defender:
- Permitir monitorização em tempo real
- Permitir a monitorização de comportamento
- Ativar o Sistema de Inspeção de Rede
- Analisar todas as transferências
- Permitir análise de script
- Monitorizar a atividade de programas e ficheiros
  - Ficheiros monitorizados
- Dias para controlar o software maligno resolvido
- Permitir acesso à IU de cliente
- Agendar uma análise do sistema
  - Dia agendado
  - Hora agendada
- Agendar uma análise rápida diária
  - Hora agendada
- % De utilização de limite de CPU durante uma análise da análise ficheiros de arquivo
- Analisar mensagens de e-mail
- Analisar unidades amovíveis
- Analisar unidades mapeadas
- Analisar ficheiros abertos a partir de partilhas de redes
- Intervalo de atualização de assinatura
- Permitir proteção da nuvem
- Solicitar aos utilizadores de amostras
- Deteção de aplicação indesejável potencialmente
- Ficheiros/pastas excluídas
- Extensões de ficheiro excluídos
- Processos excluídos

> [!NOTE]
> Estas definições só podem ser configuradas em computadores cliente com a atualização de Novembro de 10 do Windows (versão 1511) e superior.

### <a name="try-it-out"></a>Experimente!

1.  Na consola do Configuration Manager, vá **ativos e compatibilidade** > **descrição geral** > **as definições de compatibilidade** > **itens de configuração**e criar um novo **Item de configuração**.
2.  Introduza um nome, em seguida, selecione **Windows 8.1 e Windows 10** em **definições para dispositivos geridos sem o cliente do Configuration Manager** e clique em **seguinte**.
3.  Certifique-se **todos os Windows 10 (64-bit)** e **todos os Windows 10 (32-bit)** estão selecionadas no **plataformas suportadas** página, em seguida, clique em **seguinte**.
4.  Selecione o **Windows Defender** definição de grupo, em seguida, clique em **seguinte**.
5.  Configure as definições pretendidas nesta página, em seguida, clique em **seguinte**.
6.  Conclua o assistente.
7.  Adicionar este item de configuração para uma linha de base de configuração e implementar esta linha de base em computadores com Windows 10 Novembro Update (versão 1511) ou acima.

> [!NOTE]
> Não se esqueça de verificar o **remediar definições incompatíveis** caixa de verificação ao implementar a linha de base de configuração.

## <a name="request-policy-sync-from-administrator-console"></a>Política de pedido de sincronização da consola do administrador

Agora pode pedir uma sincronização de política para um dispositivo móvel da consola do Configuration Manager, em vez de que necessita pedir uma sincronização do próprio dispositivo. Informações de estado de pedido de sincronização estão disponíveis como uma nova coluna nas vistas de dispositivo, denominado **estado de sincronização remoto**. Estado também aparece no **dados de deteção** secção o **propriedades** caixa de diálogo para cada dispositivo móvel.

### <a name="try-it-out"></a>Experimente!

1.  Na consola do Configuration Manager, vá **ativos e compatibilidade** > **descrição geral** > dispositivos.
2.  No **ações do dispositivo remoto** menu, selecione **enviar pedido de sincronização**.

Sincronização poderá demorar cinco a dez minutos. As alterações na política são sincronizadas para o dispositivo. Pode controlar o estado do pedido de sincronização no **estado de sincronização remoto** coluna no **dispositivos** vista, ou o dispositivo **propriedades** caixa de diálogo.

## <a name="additional-security-role-support"></a>Suporte de função de segurança adicionais

Para além de administrador global, as seguintes funções de segurança incorporadas agora tem acesso total aos itens a **todos os dispositivos pertencentes** nó, incluindo **Predeclared dispositivos**, **perfis de inscrição iOS**, e **perfis de inscrição do Windows**: • **Gestor do Asset Intelligence** • **Gestor de acesso a recursos da empresa**

Ainda é concedido o acesso só de leitura para estas áreas da consola do Configuration Manager para o **analista só de leitura** função.

## <a name="conditional-access-for-windows-10-vpn-profiles"></a>Acesso condicional para perfis de VPN do Windows 10

Agora pode exigir a Windows 10 dispositivos inscritos no Azure Active Directory para estar em conformidade para ter acesso VPN através de perfis de VPN do Windows 10 criadas na consola do Configuration Manager. Isto é possível através de novo **ativar o acesso condicional para esta ligação VPN** caixa de verificação no **método de autenticação** página no Assistente do perfil VPN e propriedades de perfil VPN para perfis de VPN do Windows 10. Também pode especificar um certificado diferente para autenticação de início de sessão único se ativar o acesso condicional para o perfil.

## <a name="see-also"></a>Consulte Também
[Pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md)
