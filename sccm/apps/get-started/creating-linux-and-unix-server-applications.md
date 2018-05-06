---
title: Criar aplicações de servidor Linux e UNIX
titleSuffix: Configuration Manager
description: Consulte as considerações deve ter em conta quando criar e implementar aplicações em dispositivos de Linux e Unix.
ms.date: 04/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 79cd131a-1a24-4751-87c8-7f275e45d847
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 35ccc4944359b89bad3ccac52309a289f69933f7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="create-linux-and-unix-server-applications-with-system-center-configuration-manager"></a>Criar aplicações de servidor Linux e UNIX com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Ter em conta as seguintes considerações ao criar e implementar aplicações para computadores que executam o Linux e UNIX.  

## <a name="general-considerations"></a>Considerações gerais  
 O cliente do Configuration Manager para Linux e UNIX suporta **implementações de software que utilizem pacotes e programas**. Não é possível implementar aplicações do Configuration Manager em computadores que executam o Linux e UNIX.  

 As capacidade de implementação de software do Linux e UNIX incluem:  

-   Instalação de software para servidores Linux e UNIX, incluindo o seguinte:  

    -   Implementação de novo software  

    -   Atualizações de software para programas que já estão num computador  

    -   Patches do sistema operativo  

-   Os comandos nativo Linux e UNIX e scripts que estão localizados em servidores Linux e UNIX  

-   Implementações que estejam limitadas para os sistemas operativos que especificar ao selecionar a opção de programa **apenas nas plataformas cliente especificadas**

-   Janelas de manutenção para controlar quando instala o software

-   Mensagens de estado de implementação para monitorizar implementações  

-   A opção para o cliente para a limitação da utilização de rede ao-lo é transferir software a partir de um ponto de distribuição  

### <a name="differences-between-deploying-to-linux-and-unix-computers-and-deploying-to-windows-devices"></a>Diferenças entre a implementar em computadores Linux e UNIX e implementar em dispositivos Windows
As principais diferenças entre a implementação de pacotes e programas para computadores Linux e UNIX e implementar pacotes e programas em dispositivos Windows são os seguintes:  

|Configuração|Detalhes|  
|-------------------|-------------|  
|Utilize apenas configurações destinadas a computadores e não utilizam configurações que foram concebidas para utilizadores.|O cliente do Configuration Manager para Linux e UNIX suporta configurações destinadas a utilizadores.|  
|Configure os programas para transferir software a partir do ponto de distribuição e executar os programas da cache do cliente local.|O cliente do Configuration Manager para Linux e UNIX não suporta a execução de software a partir do ponto de distribuição. Em vez disso, tem de configurar o software de transferir para o cliente e, em seguida, obter instalado.<br /><br /> Por predefinição, depois de o cliente para Linux e UNIX instalar o software, esse software é eliminado da cache do cliente. No entanto, os pacotes configurados com a opção **Manter conteúdo na cache do cliente** não são eliminados do cliente, permanecendo na respetiva cache após a instalação do software.<br /><br /> O cliente para Linux e UNIX não suporta configurações da cache do cliente. O tamanho máximo da cache do cliente só se encontra limitado pelo espaço livre em disco no computador cliente.|  
|Configurar a Conta de Acesso à Rede para acesso aos pontos de distribuição|Os computadores com Linux e UNIX são concebidos para serem computadores de grupo de trabalho. Para aceder aos pacotes a partir do ponto de distribuição no domínio do servidor de site do Configuration Manager, tem de configurar a conta de acesso de rede para o site. Terá de especificar esta conta como uma propriedade do componente de distribuição de software e configurar a conta antes da implementação do software.<br /><br /> Pode configurar várias Contas de Acesso de Rede em cada site. O cliente para Linux e UNIX poderá utilizar cada uma das contas que configurar como Conta de Acesso à Rede.<br /><br /> Para obter mais informações, veja [Componentes do site para o System Center Configuration Manager](../../core/servers/deploy/configure/site-components.md).|  

 Poderá implementar pacotes e programas para coleções que contenham apenas clientes Linux ou UNIX ou implementá-los em coleções que contenham uma mistura de tipos de cliente, como a **Coleção Todos os Sistemas**. No entanto, os clientes não Linux e UNIX não não conseguem instalar a falha de software ou no relatório.  

 Quando o cliente do Configuration Manager para Linux e UNIX recebe e executa uma implementação, gera mensagens de estado. Poderá visualizar estas mensagens de estado na consola do Configuration Manager, ou utilizando relatórios para monitorizar o estado de implementação.  

 Para obter informações sobre como utilizar pacotes e programas, consulte [pacotes e programas](../../apps/deploy-use/packages-and-programs.md).  

##  <a name="configure-packages-programs-and-deployments-for-linux-and-unix-servers"></a>Configurar pacotes, programas e implementações para servidores Linux e UNIX  
 Pode criar e implementar pacotes e programas utilizando as opções de predefinidas disponíveis na consola do Configuration Manager. O cliente não requer quaisquer configurações exclusivas.  

 Utilize as informações das secções seguintes para configurar pacotes e programas, bem como implementações.  

### <a name="packages-and-programs"></a>Pacotes e programas  
 Para criar um pacote e programa para um servidor Linux ou UNIX, utilize o **criar pacote e programa assistente** partir da consola do Configuration Manager. O cliente para Linux e UNIX suporta a maior parte das definições de pacotes e programas. No entanto, diversas definições não são suportadas. Ao criar ou configurar um pacote e programa, tenha em consideração:  

-   Inclua os tipos de ficheiro suportados pelos computadores de destino.  

-   Defina as linhas de comandos que são adequadas para utilização no computador de destino.  

-   Tenha em atenção que as definições que interajam com os utilizadores não são suportadas.  

A tabela seguinte lista as propriedades de pacotes e programas que não são suportados:  

|Propriedade de pacote e programa|Comportamento|Mais informações|  
|----------------------------------|--------------|----------------------|  
|Definições de partilha de pacote:<br /><br /> -Todas as opções|É gerado um erro e a instalação do software falha|O cliente não suporta esta configuração. Em vez disso, o cliente terá de transferir o software utilizando HTTP ou HTTPS e executar a linha de comandos a partir da respetiva cache local.|  
|Definições de atualização do pacote:<br /><br /> -Desligar utilizadores de pontos de distribuição|As definições são ignoradas|O cliente não suporta esta configuração.|  
|Definições de implementação do sistema operativo:<br /><br /> -Todas as opções|As definições são ignoradas|O cliente não suporta esta configuração.|  
|Relatórios:<br /><br /> -Utilize as propriedades do pacote para correspondência MIF de estado<br /><br /> -Utilizar estes campos para correspondência MIF de estado|As definições são ignoradas|O cliente não suporta a utilização de ficheiros MIF de estado.|  
|**Executar**:<br /><br /> -Todas as opções|As definições são ignoradas|O cliente executa sempre os pacotes sem interface do utilizador.<br /><br /> O cliente ignora todas as opções de configuração de Executar.|  
|Após a execução:<br /><br />-Configuration Manager reinicia o computador<br /><br /> -O programa controla o reinício<br /><br /> -Configuration Manager termina a sessão do utilizador|É gerado um erro e a instalação do software falha|Definição de reinício do sistema e definições específicas do utilizador não são suportadas.<br /><br /> Quando é utilizada qualquer definição exceto **Não é necessária nenhuma ação** , o cliente gera um erro e continua a instalar o software sem tomar qualquer ação.|  
|Programa pode ser executado:<br /><br /> -Apenas quando um utilizador tem sessão iniciada|É gerado um erro e a instalação do software falha|Não são suportadas definições específicas do utilizador.<br /><br /> Quando esta opção se encontra configurada, o cliente gera um erro e a instalação do software falha.<br /><br /> As outras opções são ignoradas e a instalação do software continua.|  
|Modo de execução:<br /><br /> -Executar com direitos de utilizador|As definições são ignoradas|Não são suportadas definições específicas do utilizador.<br /><br /> No entanto, o cliente suporta a configuração com direitos administrativos.<br /><br /> Quando especificar **executar com direitos administrativos**, o cliente do Configuration Manager utiliza as credenciais de raiz.<br /><br /> Esta definição não gera um erro ou entrada de registo. Em vez disso, a instalação do software falha quando o cliente gera um erro para o pré-requisito de configuração **programa pode ser executado** = **apenas quando um utilizador tem sessão iniciado**.|  
|Permitir que os utilizadores visualizem e interajam com a instalação do programa|As definições são ignoradas|Não são suportadas definições específicas do utilizador.<br /><br /> Esta configuração é ignorada e a instalação do software continua.|  
|Modo de unidade:<br /><br /> -Todas as opções|As definições são ignoradas|Esta definição não é suportada porque o conteúdo é sempre transferido para o cliente e executado localmente.|  
|Executar outro programa primeiro|É gerado um erro e a instalação do software falha|A instalação recursiva de programas não é suportada.<br /><br /> Quando um programa é configurado para executar primeiro outro programa, a instalação do software falha e a instalação do outro programa não é iniciada.|  
|Quando este programa é atribuído a um computador:<br /><br /> -Executar uma vez para cada utilizador que inicia sessão|As definições são ignoradas|Não são suportadas definições específicas do utilizador.<br /><br /> No entanto, o cliente suporta a configuração a ser executado uma vez para o computador.<br /><br /> Esta definição não gera um erro ou entrada de registo porque já são criados um erro e entrada de registo para o pré-requisito de configuração **Programa pode ser executado** = **Apenas quando um utilizador tiver sessão iniciada**.|  
|Suprimir notificações de programas|As definições são ignoradas|O cliente não implementa uma interface de utilizador.<br /><br /> Se esta configuração for selecionada, será ignorada e a instalação do software continuará.|  
|Desativar este programa em computadores nos quais tenha sido implementado|As definições são ignoradas|Esta definição não é suportada, não afetando a instalação do software.|  
|Permitir que este programa ser instalado a partir da sequência de tarefas Instalar pacote sem ser implementada||O cliente não suporta sequências de tarefas.<br /><br /> Esta definição não é suportada, não afetando a instalação do software.|  
|Windows Installer:<br /><br /> -Todas as opções|As definições são ignoradas|O cliente não suporta ficheiros e definições do Windows Installer.|  
|Modo de Manutenção do OpsMgr:<br /><br /> -Todas as opções|As definições são ignoradas|O cliente não suporta esta configuração.|  

### <a name="deploy-software-to-a-linux-or-unix-server"></a>Implementar software num servidor Linux ou UNIX
 Para implementar software num servidor Linux ou UNIX utilizando um pacote e programa, pode utilizar o **Assistente de implementação de Software** partir da consola do Configuration Manager. A maioria das definições de implementação são suportadas pelo cliente para Linux e UNIX. No entanto diversas definições não são suportadas. Ao implementar software, considere o seguinte:  

-   Terá de aprovisionar o pacote em pelo menos um ponto de distribuição que se encontre associado a um grupo de limites configurado para localização de conteúdo.  

-   O cliente para Linux e UNIX que recebe esta implementação tem de ser capaz de aceder este ponto de distribuição da respetiva localização de rede.  

-   O cliente para Linux e UNIX transfere o pacote a partir do ponto de distribuição e executa o programa no computador local.  

-   O cliente para Linux e UNIX não consegue transferir pacotes a partir de pastas partilhadas. Transfere os pacotes dos pontos de distribuição preparados para IIS que suportem HTTP ou HTTPS.  

 A tabela seguinte lista as propriedades de implementações que não são suportadas:  

|Propriedade de implementação|Comportamento|Mais informações|  
|-------------------------|--------------|----------------------|  
|Definições de implementação - objetivo:<br /><br /> -Disponíveis<br /><br /> -Necessário|As definições são ignoradas|Não são suportadas definições específicas do utilizador.<br /><br /> No entanto, o cliente suporta a definição **Necessário**, que impõe a hora de instalação agendada, mas não suporta a instalação manual antes dessa hora.|  
|Enviar pacotes de reativação|As definições são ignoradas|O cliente não suporta esta configuração.|  
|Agenda da atribuição:<br /><br /> -início de sessão<br /><br /> -terminar sessão|É gerado um erro e a instalação do software falha|Não são suportadas definições específicas do utilizador.<br /><br /> No entanto, o cliente suporta a definição **Logo que possível**.|  
|Definições de notificação:<br /><br /> -Permitir que os utilizadores executem o programa independentemente das atribuições|As definições são ignoradas|O cliente não implementa uma interface de utilizador.|  
|Quando for atingida a hora agendada da atribuição, permitir a execução das seguintes atividades fora da janela de manutenção:<br /><br /> -Reinício de sistema (se for necessário para concluir a instalação)|É gerado um erro|O cliente não suporta um reinício do sistema.|  
|Opção de implementação para redes (LAN) rápidas:<br /><br /> -Executar programa a partir do ponto de distribuição|É gerado um erro e a instalação do software falha|O cliente não consegue executar software a partir do ponto de distribuição e, em vez disso, terá de transferir o programa para que este possa ser executado.|  
|Opção de implementação para uma zona de rede lenta ou pouco fiável ou uma localização de origem de contingência para o conteúdo:<br /><br /> -Permitir que os clientes partilhem conteúdos com outros clientes na mesma sub-rede|As definições são ignoradas|O cliente não suporta a partilha de conteúdo entre elementos.|  

 Para obter mais informações sobre localizações de conteúdo, consulte [gerir a infraestrutura de conteúdo e o conteúdo para o System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 Para obter mais informações sobre como criar uma implementação, consulte [implementar aplicações](../../apps/deploy-use/deploy-applications.md).  

##  <a name="manage-network-bandwidth-for-software-downloads-from-distribution-points"></a>Gerir a largura de banda de rede para transferências de software dos pontos de distribuição  
 O cliente Linux e UNIX suporta controlos de largura de banda de rede ao-lo é transferir software a partir de um ponto de distribuição.  

 O cliente utiliza as definições de transferência inteligente em segundo plano (BITS) que configurar como definições de cliente no Configuration Manager, mas não implementa o BITS. Em vez disso, para otimizar a utilização da largura de banda de rede, o cliente controla o tamanho dos segmentos de pedidos HTTP e o atraso entre segmentos na transferência de software.  

 Para configurar um cliente para utilizar controlos de largura de banda de rede, configure as definições de cliente para **Transferência Inteligente em Segundo Plano** e aplique as definições ao computador cliente. Para utilizar controlos de largura de banda, o cliente tem de receber as definições de cliente para **transferência de inteligente em segundo plano** com as seguintes definições configuradas como **Sim**:  

-   **Limitar a largura de banda de rede máxima para transferências BITS em segundo plano**  

 O cliente suporta as seguintes configurações de Transferência Inteligente em Segundo Plano:  

    -   **Hora de início da janela de limitação**  

    -   **Hora de fim da janela de limitação**  

    -   **Velocidade máxima de transferência durante a janela de limitação (Kbps)**  

    -   **Velocidade máxima de transferência fora da janela de limitação (Kbps)**  

A seguinte configuração de Transferência Inteligente em Segundo Plano não é suportada, sendo ignorada pelo cliente para Linux e UNIX:  

-   **Permitir transferências BITS fora da janela de limitação**  

 Se a transferência de software para o cliente a partir de um ponto de distribuição for interrompida, o cliente para Linux e UNIX não retomará a transferência. Em vez disso, este reiniciará a transferência do pacote de software completo.  

##  <a name="configure-operations-for-software-deployments"></a>Configurar operações para implementações de software  
 Da mesma forma para o cliente do Windows, o cliente do Configuration Manager para Linux e UNIX Deteta novas implementações de software quando consulta e verifica a existência de nova política. A frequência com que o cliente verifica a existência de novas políticas depende das definições de cliente. Poderá configurar janelas de manutenção para controlar quando ocorrem implementações de software.  

 Poderá configurar as implementações de software em servidores Linux e UNIX utilizando propriedades de pacote, propriedades de programa e propriedades de implementação.  

 Ao receber a política para uma implementação, o cliente submete uma mensagem de estado. Submete também mensagens de estado quando inicia a instalação de software e quando a instalação conclusão ou falha.  

 Programas para implementação de software são executados com as credenciais de raiz que executa o cliente do Configuration Manager para Linux e UNIX com. O código de saída do comando do programa é utilizado para determinar o êxito ou falha. O código de saída 0 (zero) é tratado como êxito. Além disso, o **stdout** (sequência de saída padrão) e o **stderr** (sequência de erro padrão) são copiados para o ficheiro de registo quando o nível de registo é definido como INFO ou RASTREIO.  

> [!TIP]  
>  Se o software que pretender implementar estiver localizado numa partilha NFS (Network File System) a que o servidor Linux ou UNIX consiga aceder, não precisará de utilizar um ponto de distribuição para transferir o pacote. Em vez disso, ao criar o pacote, não selecione a caixa de verificação **Este pacote contém ficheiros de origem**. Em seguida, ao configurar o programa, especifique a linha de comandos adequada para aceder diretamente ao pacote no ponto de montagem NFS.  
