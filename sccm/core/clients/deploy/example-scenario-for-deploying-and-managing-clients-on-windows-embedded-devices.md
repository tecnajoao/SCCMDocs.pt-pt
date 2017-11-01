---
title: "Cenário de exemplo - implementar clientes Windows Embedded"
titleSuffix: Configuration Manager
description: "Ver um cenário de exemplo para implementar e gerir clientes do System Center Configuration Manager em dispositivos Windows Embedded."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10049c89-b37c-472b-b317-ce4f56cd4be7
caps.latest.revision: "8"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: fc55aacfc1eae7a427ca4a0ae1bb3197b74fd2be
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="example-scenario-for-deploying-and-managing-system-center-configuration-manager-clients-on-windows-embedded-devices"></a>Cenário de exemplo para implementação e gestão de clientes do System Center Configuration Manager em dispositivos Windows Embedded

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este cenário demonstra como pode gerir com filtro escrita ativado Windows Embedded dispositivos com Manager.If de configuração, os dispositivos embedded não suportarem filtros de escrita, comportam-se como clientes padrão do Configuration Manager e não aplicam estes procedimentos.  

A empresa Caves Coho está a abrir um centro de visitantes e tem de quiosques com o Windows Embedded para executar apresentações interativas. O edifício para o novo Centro de visitantes não está perto do departamento de TI, para que os quiosques têm de ser geridos remotamente. Para além do software que executa as apresentações, estes dispositivos têm de executar o software de proteção antimalware atualizado para estar em conformidade com as políticas de segurança da empresa. Os quiosques têm de funcionar 7 dias por semana, sem período de indisponibilidade enquanto o Centro de visitantes estiver aberto.  

 A empresa já é executado o Configuration Manager para gerir dispositivos na sua rede. O Configuration Manager está configurado para executar o Endpoint Protection e instalar atualizações de software e aplicações. No entanto, porque a equipa de TI não geriu dispositivos Windows Embedded, a Joana, o administrador do Configuration Manager, executa um piloto para gerir dois quiosques na sala de espera de receção.   

 Para gerir estes dispositivos Windows Embedded que com filtro escrita ativado, a Joana efetua os seguintes passos para instalar o cliente do Configuration Manager, proteger o cliente utilizando o Endpoint Protection e instalar o software de apresentação interativa.  

1.  Leituras de Joana como dispositivos Windows Embedded que utiliza filtros de escrita e como do Configuration Manager pode facilitar automaticamente desativando e voltando a reativar o escritor filtros, para manter uma instalação de software.  

     Para obter mais informações, consulte [planear a implementação do cliente em dispositivos Windows Embedded no System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

2.  Antes de instalar o cliente do Configuration Manager, a Joana cria uma nova coleção de dispositivos baseada em consulta para os dispositivos Windows Embedded. Uma vez que a empresa utiliza formatos de nomenclatura padrão para identificar os computadores, Joana consegue identificar exclusivamente os dispositivos Windows Embedded pelas primeiras seis letras do nome do computador: **WEMDVC**. Ela utiliza a seguinte consulta WQL para criar esta coleção: **select SMS_R_System.NetbiosName from SMS_R_System where SMS_R_System.NetbiosName like "WEMDVC%"**  

     Esta coleção permite-lhe gerir os dispositivos Windows Embedded com opções de configuração diferentes de outros dispositivos. A Joana utilizará esta coleção para controlar reinícios, implementar o Endpoint Protection com definições de cliente e implementar a aplicação de apresentação interativa.  

     Consulte [como criar coleções no System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

3.  A Joana configura a coleção para uma janela de manutenção para assegurar que os reinícios que possam ser necessários para instalar a aplicação de apresentação e quaisquer atualizações não ocorrem durante as horas de abertura do centro de visitantes. As horas de abertura serão das 9:00 às 18:00, de segunda a domingo. A Joana configura a janela de manutenção diariamente, das 18:30 às 6:00.  

4.  Para obter mais informações, consulte [como utilizar janelas de manutenção no System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

5.  Em seguida, a Joana configura uma definição de cliente personalizada do dispositivo para instalar o cliente do Endpoint Protection selecionando **Sim** nas definições seguintes e, depois, implementa esta definição de cliente personalizada na coleção de dispositivos Windows Embedded:  

    -   **Instalar o cliente do Endpoint Protection nos computadores cliente**  

    -   **Para dispositivos Windows Embedded com filtros de escrita, consolidar a instalação de cliente do Endpoint Protection (necessita de reinicialização)**  

    -   **Permitir a instalação de cliente Endpoint Protection e reiniciar fora das janelas de manutenção**  

     Quando o cliente do Configuration Manager está instalado, estas definições instalam o cliente Endpoint Protection e certifique-se de que se torna persistente no sistema operativo como parte da instalação, vez escrita apenas na sobreposição. As políticas de segurança da empresa exigem que esteja sempre instalado software antimalware e a Joana não quer correr o risco de os quiosques estarem desprotegidos, mesmo que por um breve período de tempo caso reiniciem.  

    > [!NOTE]  
    >  Os reinícios necessários para instalar o cliente do Endpoint Protection ocorrem apenas uma vez, durante o período de configuração dos dispositivos e antes de o centro de visitantes estar operacional. Ao contrário da implementação periódica de aplicações ou atualizações de definições de software, o da próxima vez que o cliente do Endpoint Protection está instalado no mesmo dispositivo será, provavelmente, quando a empresa atualizar para a próxima versão do Configuration Manager.  

     Para obter mais informações, consulte [configurar o Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/configure-endpoint-protection.md).  

6.  Com as definições de configuração para o cliente implementadas, a Joana prepara-se para instalar clientes do Configuration Manager. Para poder instalar os clientes, a Joana tem de desativar manualmente o filtro de escrita nos dispositivos Windows Embedded. Lê a documentação do OEM que acompanha os quiosques e segue as instruções para desativar os filtros de escrita.  

     A Joana muda o nome do dispositivo para utilizar o formato de nomenclatura padrão da empresa e, em seguida, instala o cliente manualmente executando CCMSetup com o seguinte comando a partir de uma unidade mapeada cliente os ficheiros de origem: **CCMSetup.exe /MP:mpserver.cohovineyardandwinery.com SMSSITECODE = CO1**  

     Este comando instala o cliente, atribui o cliente ao ponto de gestão que tem o FQDN da Intranet de **mpserver.cohovineyardandwinery.com**e atribui o cliente ao site primário denominado **CO1**.  

     A Joana sabe que a instalação dos clientes e o envio do respetivo estado para o site demora sempre algum tempo. Por isso, aguarda para confirmar a instalação com êxito dos clientes, a sua atribuição ao site e a apresentação como clientes na coleção que criou para dispositivos Windows Embedded.  

     Como confirmação adicional, a Joana verifica as propriedades do Configuration Manager no painel de controlo nos dispositivos e compara-as com computadores com Windows padrão geridos pelo site. Por exemplo, no separador **Componentes** , **Agente de Inventário de Hardware** apresenta **Ativado**e, no separador **Ações** , existem 11 ações disponíveis, que incluem **Ciclo de Avaliação da Aplicação de Implementação** e **Ciclo de coleção de dados de deteção**.  

     Confiante de que os clientes foram instalados, atribuídos e recebem com êxito políticas de cliente a partir do ponto de gestão, a Joana ativa manualmente os filtros de escrita seguindo as instruções do OEM.  

     Para obter mais informações, consulte:  

    -   [Como implementar clientes em computadores Windows no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

    -   [Como atribuir clientes a um site no System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md)  

7.  Agora que o cliente do Configuration Manager está instalado nos dispositivos Windows Embedded, a Joana confirma se consegue geri-los da mesma forma que gere os clientes Windows padrão. Por exemplo, da consola do Configuration Manager, ela pode geri-las remotamente utilizando o controlo remoto, a política de cliente de iniciação para e como inventário de hardware e as propriedades de cliente de vista.  

     Dado que estes dispositivos estão associados a um domínio do Active Directory, a Joana não tem de aprová-los manualmente como clientes fidedignos e confirma a partir da consola do Configuration Manager que estão aprovados.  

     Para obter mais informações, veja [Como gerir clientes no System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

8.  Para instalar o software de apresentação interativa, a Joana executa o **Assistente de Implementação de Software** e configura uma aplicação necessária. Na página **Experiência do Utilizador** do assistente, na secção **Processamento do filtro de escrita para dispositivos Windows Embedded** , a Joana aceita a opção predefinida que seleciona **Confirmar alterações dentro do prazo ou durante a janela de manutenção (requer reinicialização)**.  

     A Joana mantém esta opção predefinida para os filtros de escrita para garantir que a aplicação permanece após um reinício, para que esteja sempre disponível para os visitantes que utilizem os quiosques. A janela de manutenção diária fornece um período seguro durante o qual podem ocorrer os reinícios para instalação e atualizações.  

     A Joana implementa a aplicação na coleção de dispositivos Windows Embedded.  

     Para obter mais informações, veja [Como implementar aplicações no System Center Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

9. Para configurar atualizações de definições para o Endpoint Protection, a Joana utiliza atualizações de software e executa o Assistente de Criação de Regra de Implementação Automática. Seleciona o modelo **Atualizações de Definição** para pré-povoar o assistente com definições que sejam adequadas para o Endpoint Protection.  

     Estas definições incluem as seguintes na página **Experiência do Utilizador** do assistente:  

    -   **Comportamento do prazo**: O **instalação de Software** não estiver selecionada a caixa de verificação.  

    -   **Para dispositivos Windows Embedded de processamento do filtro de escrita**: O **Confirmar alterações dentro do prazo ou durante uma janela de manutenção (requer reinicialização)** não estiver selecionada a caixa de verificação.  

     A Joana mantém estas predefinições. Em conjunto, estas duas opções com esta configuração permitem a instalação de quaisquer definições de atualização de software para o Endpoint Protection na sobreposição durante o dia, sem aguardar para serem instaladas e consolidadas durante a janela de manutenção. Esta configuração cumpre melhor a política de segurança da empresa relativa à execução de proteção antimalware atualizada nos computadores.  

    > [!NOTE]  
    >  Ao contrário das instalações de software para aplicações, as definições de atualização de software para o Endpoint Protection podem ocorrer com muita frequência, inclusivamente várias vezes por dia. São frequentemente ficheiros pequenos. Para estes tipos de implementações relacionadas com segurança, geralmente é vantajoso instalar sempre na sobreposição em vez de aguardar até à janela de manutenção. O cliente do Configuration Manager reinstalará rapidamente as atualizações de definições de software se o dispositivo reiniciar porque esta ação inicia uma verificação de avaliação e não aguarda até à avaliação agendada seguinte.  

     A Joana seleciona a coleção de dispositivos Windows Embedded para a regra de implementação automática.  

     Para mais informações, consulte  
                  Passo 3: Configurar atualizações de Software do Configuration Manager para fornecer atualizações de definições em computadores cliente na [configurar o Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/configure-endpoint-protection.md)  

10. A Joana decide configurar uma tarefa de manutenção que consolide periodicamente todas as alterações na sobreposição. Esta tarefa destina-se a suportar a implementação de definições de atualização de software, para reduzir o número de atualizações que se acumulam e têm de ser instaladas novamente sempre que o dispositivo reinicia. Na sua experiência, isto ajuda a tornar mais eficiente a execução dos programas antimalware.  

    > [!NOTE]  
    >  Estas definições de atualização de software seriam consolidadas automaticamente na imagem se os dispositivos Embedded executassem outra tarefa de gestão que suportasse a consolidação de alterações. Por exemplo, a instalação de uma nova versão do software de apresentação interativa também consolidaria as alterações das definições de atualização de software. Em alternativa, a instalação de atualizações de software padrão todos os meses durante a janela de manutenção também poderia consolidar as alterações das definições de atualização de software. No entanto, neste cenário, em que as atualizações de software padrão não são executadas e o software de apresentação interativa não é atualizado com muita frequência, poderão decorrer meses até as atualizações de definições de software serem automaticamente consolidadas na imagem.  

     A Joana cria primeiro uma sequência de tarefas personalizada sem outras definições que não o nome. Executa o Assistente de Criação de Sequência de Tarefas:  

    1.  Na página **Criar uma Nova Sequência de Tarefas** , seleciona **Criar uma nova sequência de tarefas personalizada**e clica em **Seguinte**.  

    2.  Na página **Informações da Sequência de tarefas** , ela introduza **Maintenance task to commit changes on embedded devices** como o nome da sequência de tarefas e clica em **Seguinte**.  

    3.  Na página **Resumo** , a Joana seleciona **Seguinte**e conclui o assistente.  

     Em seguida, a Joana implementa esta sequência de tarefas personalizada na coleção de dispositivos Windows Embedded e agenda a execução mensal da mesma. Como parte integrante das definições de implementação, seleciona a caixa de verificação **Confirmar alterações dentro do prazo ou durante a janela de manutenção (requer reinicialização)** para manter as alterações após um reinício. Para configurar esta implementação, a Joana seleciona a sequência de tarefas personalizada que acabou de criar e, no grupo **Implementação** do separador **Home Page** , clica em **Implementar** para iniciar o Assistente de Implementação de Software:  

    1.  Na página **Geral** , seleciona a coleção de dispositivos Windows Embedded e clica em **Seguinte**.  

    2.  Na página **Definições de Implementação** , seleciona **Necessário** para o **Objetivo**e clica em **Seguinte**.  

    3.  Na página **Agendamento** , clica em **Novo** para especificar um agendamento semanal durante a janela de manutenção e clica em **Seguinte**.  

    4.  A Joana conclui o assistente sem mais nenhuma alteração.  

     Para mais informações, consulte  
                  [Gerir sequências de tarefas para automatizar tarefas no System Center Configuration Manager](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).  

11. Para a execução automática dos quiosques, a Joana escreve um script para configurar os dispositivos com as seguintes definições:  

    -   Iniciar sessão automaticamente utilizando uma conta de convidado sem palavra-passe.  

    -   Executar automaticamente o software de apresentação interativa ao iniciar.  

     A Joana utiliza pacotes e programas para implementar este script na coleção de dispositivos Windows Embedded. Quando executa o Assistente de Implementação de Software, seleciona novamente a caixa de verificação **Confirmar alterações dentro do prazo ou durante a janela de manutenção (requer reinicialização)** para tornar persistentes as alterações após um reinício.  

     Para obter mais informações, veja [Pacotes e programas no System Center Configuration Manager](../../../apps/deploy-use/packages-and-programs.md).  

12. Na manhã seguinte, a Joana verifica os dispositivos Windows Embedded e confirma o seguinte:  

    -   A sessão do quiosque foi automaticamente iniciada com a conta de convidado.  

    -   O software de apresentação interativa está em execução.  

    -   O cliente do Endpoint Protection está instalado e tem as definições de atualização de software mais recentes.  

    -   O dispositivo foi reiniciado durante a janela de manutenção.  

     Para obter mais informações, consulte:  

    -   [Como monitorizar o Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md)  

    -   [Monitorizar aplicações com o System Center Configuration Manager](/sccm/apps/deploy-use/monitor-applications-from-the-console)  

13. A Joana monitoriza os quiosques e reporta a gestão bem-sucedida dos mesmos ao seu diretor. Dado o êxito, são encomendados 20 quiosques para o centro de visitantes.  

     Para evitar a instalação manual do cliente do Configuration Manager, o que necessita de desativando manualmente e, em seguida, reativar os filtros de escrita, a Joana garante que a encomenda inclui uma imagem personalizada que já inclua a instalação e atribuição de site do cliente do Configuration Manager. Além disso, o nome dos dispositivos é atribuído de acordo com o formato de nomenclatura da empresa.  

     Os quiosques são entregues para o centro de visitantes uma semana antes da respetiva abertura. Durante este período, os quiosques são ligados à rede, toda a gestão de dispositivos é automática e não é necessário um administrador local. A Joana confirma que os quiosques estão a funcionar conforme necessário:  

    -   Os clientes dos quiosques concluem a atribuição de sites e transferem a chave de raiz fidedigna a partir dos Serviços de Domínio do Active Directory.  

    -   Os clientes dos quiosques são automaticamente adicionados à coleção de dispositivos Windows Embedded e configurados com a janela de manutenção.  

    -   O cliente do Endpoint Protection está instalado e tem as definições de atualização de software mais recentes da proteção antimalware.  

    -   O software de apresentação interativa está instalado e é executado automaticamente (está preparado para os visitantes).  

14. Após esta configuração inicial, quaisquer reinícios que possam ser necessários para atualizações só ocorrerão quando o centro de visitantes estiver fechado.  
