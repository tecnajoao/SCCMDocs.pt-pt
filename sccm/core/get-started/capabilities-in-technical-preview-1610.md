---
title: "Capacidades na pré-visualização técnica 1610 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1610."
ms.custom: na
ms.date: 01/23/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.topic: article
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
caps.latest.revision: 2
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 5d08d1f9ccd995d544c3c21c4af52ede73343077
ms.openlocfilehash: 59633ce68e2bb2d722900215751f345d6d098721
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1610-for-system-center-configuration-manager"></a>Funcionalidades de pré-visualização técnica 1610 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*



Este artigo apresenta as funcionalidades que estão disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1610. Pode instalar esta versão para atualizar e adicionar novas capacidades para o seu site de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão da pré-visualização técnica, consulte o tópico de introdução, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com geral requisitos e limitações à utilização de uma pré-visualização técnica, como atualizar entre as versões e como fornecer comentários sobre as funcionalidades numa pré-visualização técnica.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrar por tamanho do conteúdo nas regras de implementação automática
Agora pode filtrar o tamanho do conteúdo para atualizações de software nas regras de implementação automática. Por exemplo, pode definir o **conteúdo tamanho (KB)** filtro para **< 2048** apenas transfere atualizações de software que são mais pequenas do que 2 MB. Utilizar este filtro impede que as atualizações de software grande transferência automaticamente para um melhor suporte simplificado Windows de nível de manutenção quando a largura de banda de rede é limitada. Para obter mais detalhes, consulte o artigo [do Configuration Manager e simplificado Windows manutenção para baixo nível de sistemas operativos](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).

#### <a name="to-configure-the-content-size-field"></a>Para configurar o campo de tamanho do conteúdo
Para configurar o **conteúdo tamanho (KB)** campo, acedo ao **atualizações de Software** página no Assistente de criação automática implementação regra quando cria um ADR ou ir para o **atualizações de Software** separador nas propriedades de um ADR existente.

![Campo de tamanho do conteúdo](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>Melhoria da funcionalidade para caixas de diálogo de software necessárias
Quando um utilizador recebe software necessário, a partir de **suspender e avisar-me:** definição, podem selecionar a partir da seguinte na lista pendente de valores:
- Mais tarde: Especifica se as notificações estão agendadas baseada nas definições de notificação configuradas nas definições do agente de cliente.
- Fixo de tempo: Especifica que a notificação será agendada para apresentar novamente após o tempo selecionado. Por exemplo, se um utilizador seleciona 30 minutos, a notificação apresentará novamente dentro de 30 minutos.

![Página de agente de computador nas definições do agente de cliente](media/computeragentsettings.png)

O tempo máximo premir suspender sempre é baseado nos valores de notificação configurados nas definições de agente do cliente em cada vez ao longo da linha cronológica de implementação. Por exemplo, se o **implementação prazo superior a 24 horas, lembrar utilizadores cada (horas)** definição no computador agente página está configurada para 10 horas e é mais do que 24 horas antes do prazo quando a caixa de diálogo for iniciada, apresentada ao utilizador faria com um conjunto de opções de premir suspender até mas nunca maior que 10 horas. Como se aproximar do prazo, a caixa de diálogo irá mostrar menos opções, consistentes com as definições de agente do cliente relevantes para cada componente da linha de tempo de implementação.

Além disso, para uma implementação de alto risco, tal como uma sequência de tarefas que implementa um sistema operativo, a experiência de notificação do utilizador final é agora mais intrusivo. Em vez de uma notificação da barra de tarefas transitório sempre que o utilizador será notificado que manutenção crítica do software é necessária, um caixa de diálogo, tais como a seguinte apresenta no computador do utilizador:

![Caixa de diálogo de Software necessária](media/requiredsoftwaredialog.png)


Para obter mais informações:
- [Definições para gerir implementações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Como configurar as definições de cliente](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>Negar pedidos de aplicações anteriormente aprovados

Como administrador pode agora recusar um pedido de aplicação anteriormente aprovados. Uma vez negado, para instalar esta aplicação utilizadores posteriores tem de submeter um pedido de. Negação não desinstalar a aplicação; em vez disso obriga reapproval qualquer pedido de novo para essa aplicação desse utilizador. Anteriormente, recusa do pedido de aplicação só estava disponível para pedidos de aplicações que não tinham sido aprovados.

#### <a name="try-it-out"></a>Experimente
Para negar uma aplicação aprovou o pedido:

1.    Na consola do Configuration Manager, [criar e implementar uma aplicação](https://docs.microsoft.com/en-us/sccm/apps/deploy-use/create-applications) que necessite de aprovação.
2.    Num computador cliente, abra o Centro de Software e submeter um pedido para a aplicação.
3.    Na consola do Configuration Manager, aprove o pedido de aplicação.
4.    Negar o pedido de aplicação aprovados: Na consola do Configuration Manager, navegue **biblioteca de Software** > **descrição geral** > **gestão de aplicações** > **pedidos de aprovação** e seleccione o pedido de aplicação que pretende negar.  No Friso, clique em **negar**.

## <a name="exclude-clients-from-automatic-upgrade"></a>Excluir os clientes da atualização automática
1610 de pré-visualização técnica introduz uma nova definição que pode utilizar para excluir uma coleção de clientes a partir de versões de cliente atualizado a instalar automaticamente.  Isto aplica-se a atualização automática, bem como outros métodos, tais como a atualização baseada em atualização de software, scripts de início de sessão e política de grupo. Isto pode ser utilizado para uma coleção de computadores que necessitam de maior cuidado quando atualizar o cliente. Um cliente que está a ser uma coleção excluída ignora os pedidos para instalar o software de cliente atualizado.

### <a name="configure-exclusion-from-automatic-upgrade"></a>Configurar a exclusão de atualização automática
Configurar exclusões de atualização automáticas:
1.    Na consola do Configuration Manager abrir **definições de hierarquia** em **administração > Configuração do Site > Sites**e, em seguida, selecione o **atualização de cliente** separador.
2.    Selecione a caixa de verificação **excluir especificada de clientes a partir da atualização**e, em seguida, para **coleção de exclusão**, selecione a coleção que pretende excluir. Só pode selecionar uma única coleção para exclusão.
3.    Clique em **OK** fechar e guardar a configuração. Em seguida, após política de atualização de clientes, clientes da coleção de excluídos instalará não ajustarão automaticamente atualizações de software de cliente.

  ![Definições de exclusão de atualização automática](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> Embora a interface de utilizador indica que os clientes não serão atualizados através de qualquer método, existem dois métodos que pode utilizar para substituir estas definições. Instalação de push de cliente e uma instalação manual de cliente podem ser utilizados para esta configuração de substituição. Para obter mais detalhes, consulte a secção seguinte.

### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Como atualizar um cliente que está a ser uma coleção de excluídos
Uma coleção é configurada para ser excluídos, desde que os membros da coleção de que só podem ter o software de cliente atualizado por um de dois métodos, que substituem a exclusão:
 - **Instalação Push do cliente** – pode utilizar a instalação push do cliente para atualizar um cliente que está a ser uma coleção de excluídos. Isto é permitido como é considerada a intenção do administrador e permite que a atualização dos clientes sem remover o conjunto completo de exclusão.       
 - **Instalação manual de cliente** – pode atualizar manualmente os clientes com uma coleção excluídas ao utilizar o seguinte parâmetro de linha de comandos com o ccmsetup: ***/ignoreskipupgrade***

  Se tentar atualizar manualmente um cliente que seja um membro da coleção de excluídos e não utilize este parâmetro, o cliente não irá instalar o novo software de cliente. Para mais informações consulte [como instalar clientes do Configuration Manager manualmente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-configuration-manager-clients-manually).

Para obter mais informações sobre os métodos de instalação de cliente, consulte o artigo [como implementar clientes em computadores com Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).

## <a name="windows-defender-configuration-settings"></a>Definições de configuração do Windows Defender

Agora pode configurar as definições de cliente do Windows Defender em computadores Windows 10 inscritos Intune utilizar itens de configuração na consola do Configuration Manager.

Especificamente, pode configurar as seguintes definições do Windows Defender:
- Permitir a monitorização em tempo real
- Permitir a monitorização de comportamento
- Ativar o Sistema de Inspeção de Rede
- Analisar todas as transferências
- Permitir a análise de scripts
- Monitorizar a atividade de programas e ficheiros
  - Ficheiros monitorizados
- Dias para controlar software maligno resolvido
- Permitir acesso à IU de cliente
- Agendar uma análise do sistema
  - Dia agendado
  - Período de tempo agendado
- Agendar uma análise rápida diária
  - Período de tempo agendado
- % De utilização do limite da CPU durante uma análise análise arquivar ficheiros
- Analisar mensagens de e-mail
- Analisar unidades amovíveis
- Analisar unidades mapeadas
- Analisar ficheiros abertos a partir de partilhas líquidas
- Intervalo de atualização de assinatura
- Permitir proteção da nuvem
- Utilizadores de linha de comandos para amostras
- Deteção de aplicação indesejados potencialmente
- Ficheiros/pastas excluídas
- Extensões de ficheiro excluídos
- Processos excluídos

> [!NOTE]
> Estas definições só podem ser configuradas em computadores cliente a executar o Windows 10 Novembro Update (1511) e superior.

### <a name="try-it-out"></a>Experimente!

1.    Na consola do Configuration Manager, vá **ativos e compatibilidade** > **descrição geral** > **definições de compatibilidade** > **itens de configuração**e criar um novo **Item de configuração**.
2.    Introduza um nome, em seguida, selecione **Windows 8.1 e Windows 10** em **as definições dos dispositivos geridos sem cliente do Configuration Manager** e clique em **seguinte**.
3.    Certifique-se **todos os Windows 10 (64-bit)** e **todos os Windows 10 (32-bit)** estão selecionadas no **plataformas suportadas** página, em seguida, clique em **seguinte**.
4.    Selecione o **Windows Defender** definição de grupo, em seguida, clique em **seguinte**.
5.    Configure as definições pretendidas nesta página, em seguida, clique em **seguinte**.
6.    Conclua o assistente.
7.    Adicionar este item de configuração para uma linha de base de configuração e implementar esta linha de base para computadores que executam o Windows 10 Novembro Update (1511) ou superior.

> [!NOTE]
> Não se esqueça de verificar a **remediar as definições não conformes** caixa de verificação ao implementar a linha de base de configuração.

## <a name="request-policy-sync-from-administrator-console"></a>Política de pedido de sincronização a partir da consola de administrador

Agora pode pedir uma sincronização de política para um dispositivo móvel da consola do Configuration Manager, em vez de necessário especificá-las pedir uma sincronização do dispositivo próprio. Informações de estado do pedido de sincronização estão disponíveis como uma nova coluna em vistas de dispositivo, denominado **estado da sincronização de remoto**. Estado também aparece no **dados de deteção** secção a **propriedades** caixa de diálogo para cada dispositivo móvel.

### <a name="try-it-out"></a>Experimente!

1.    Na consola do Configuration Manager, vá **ativos e compatibilidade** > **descrição geral** > dispositivos.
2.    No **ações de dispositivo remotas** menu, selecione **enviar pedido de sincronização**.

Sincronização poderá demorar cinco a dez minutos. Quaisquer alterações na política são sincronizadas para o dispositivo. Pode controlar o estado do pedido de sincronização no **estado da sincronização de remoto** coluna no **dispositivos** vista, ou o dispositivo **propriedades** caixa de diálogo.

## <a name="additional-security-role-support"></a>Suporte de função de segurança adicionais

Para além de administrador global, as seguintes funções de segurança incorporadas agora tem acesso total aos itens no **todos os dispositivos pertencentes** nó, incluindo **Predeclared dispositivos**, **perfis de inscrição de iOS**, e **perfis de inscrição do Windows**: • **Gestor do Asset Intelligence** • **Gestor de acesso a recursos da empresa**

Acesso só de leitura a estas áreas da consola do Configuration Manager ainda é concedido ao **analista só de leitura** função.

## <a name="conditional-access-for-windows-10-vpn-profiles"></a>Acesso condicional para perfis VPN do Windows 10

Agora pode exigir o Windows 10 dispositivos inscritos no Azure Active Directory para estar em conformidade para ter acesso VPN através de perfis VPN do Windows 10 criados na consola do Configuration Manager. Isto é possível através da nova **ativar o acesso condicional para esta ligação VPN** caixa de verificação no **método de autenticação** página no Assistente do perfil VPN e propriedades de perfil da VPN para perfis VPN do Windows 10. Também pode especificar um certificado separado para autenticação de início de sessão único se permitir o acesso condicional para o perfil.

## <a name="see-also"></a>Consulte Também
[Pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md)

