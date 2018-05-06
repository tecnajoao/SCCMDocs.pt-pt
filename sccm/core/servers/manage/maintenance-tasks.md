---
title: Tarefas de manutenção
titleSuffix: Configuration Manager
description: Compreenda que manutenção de tarefas a efetuar para sites do Configuration Manager e hierarquias e quando deve efetuá-los.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1491f12768e6ca523c3cd4a6ae80fb75f4a9ab6a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="maintenance-tasks-for-system-center-configuration-manager"></a>Tarefas de manutenção para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager sites e hierarquias necessitam de manutenção regular e monitorização para fornecer serviços de forma eficaz e contínua. Manutenção regular assegura que o hardware, software e base de dados do Configuration Manager continuam a funcionar corretamente e de forma eficiente. Um desempenho ideal reduz significativamente o risco de falha.  

 Para configurar alertas e utilizar o sistema de estado para monitorizar o estado de funcionamento do Configuration Manager, consulte [utilizar alertas e o sistema de estado para o System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   [Tarefas de manutenção](#bkmk_MTs)  

##  <a name="bkmk_MTs"></a> Tarefas de manutenção  
 Manutenção regular é importante certificar-se operações do site correto. Manter um registo de manutenção que documente manutenção as datas, que foram manutenção e quaisquer comentários relacionados com a manutenção sobre as tarefas.  

### <a name="when-to-do-common-maintenance-tasks"></a>Quando efetuar tarefas de manutenção comuns  
 Para manter o seu site, considere manutenção diária ou semanal. Algumas tarefas poderão exigir uma agenda diferentes. A manutenção comum pode incluir as tarefas de manutenção incorporadas e outras tarefas, como a conta de manutenção para manter a conformidade com as políticas da empresa.  

 Utilize as seguintes informações como guia para ajudar a planear a realizar tarefas de manutenção diferente. Utilize estas listas como ponto de partida e adicione as tarefas que poderá necessitar.  

**Tarefas diárias**   
Seguem-se tarefas de manutenção que pode considerar para uma agenda diária:  

-   Verifique se as tarefas de manutenção agendadas para serem realizadas diariamente estão a funcionar com êxito.  

-   Verifique o estado de base de dados do Configuration Manager.  

-   Verifique o estado do servidor de site.  

-   Verifique o Configuration Manager site sistema nas pastas a receber de ficheiros pendentes.  

-   Verificar o estado de sistemas de sites.  

-   Verifique os registos de eventos do sistema operativo nos sistemas de sites.  

-   Verifique o registo de erros do SQL Server no computador da base de dados do site.  

-   Verificar o desempenho do sistema.  

-   Verifique os alertas do Configuration Manager.  

**Tarefas semanais**   
Seguem-se tarefas de manutenção que pode considerar para uma agenda semanal:  

-   Verifique se as tarefas de manutenção agendadas para serem realizadas semanalmente estão a funcionar com êxito.  

-   Elimine ficheiros desnecessários dos sistemas de sites.  

-   Produzir e distribuir relatórios do utilizador final, se necessário.  

-   Cópia de segurança de registos de eventos de aplicações, segurança e do sistema e limpar estes registos.  

-   Verifique o tamanho de base de dados do site e verifique que existe espaço em disco disponível suficiente no servidor de base de dados do site para permitir que a base de dados do site cresça.  

-   Faça a manutenção de base de dados do SQL Server na base de dados de site, de acordo com o plano de manutenção do SQL Server.  

-   Verificar o espaço em disco disponível em todos os sistemas de sites.  

-   Execute as ferramentas de desfragmentação de disco em todos os sistemas de sites.  

**Tarefas periódicas**   
Algumas tarefas que não necessitam de manutenção diária ou semanal são importantes para garantir o estado de funcionamento global do site. Estas tarefas também Certifique-se de que os planos de recuperação de segurança e desastre estão atualizados. Seguem-se tarefas de manutenção que pode considerar para uma agenda mais periódica que as tarefas diárias ou semanais:  

-   Alterar contas e palavras-passe, se for necessário, de acordo com o plano de segurança.  

-   Rever o plano de manutenção para verificar que tarefas de manutenção agendadas estão agendadas correta e eficaz dependendo das definições de site configuradas.  

-   Rever a estrutura de hierarquia do Configuration Manager para efetuar quaisquer alterações necessárias.  

-   Verificar o desempenho de rede para se certificar de que não foram feitas alterações que afetem as operações do site.  

-   Certifique-se de que as definições do Active Directory que afetem as operações do site não foram alteradas. Por exemplo, verifique se as sub-redes que estão atribuídos a sites do Active Directory e que são utilizadas como limites de site do Configuration Manager não foram alteradas.  

-   Rever o plano de recuperação de desastre para as alterações necessárias.  

-   Efetue uma recuperação de site, de acordo com o plano de recuperação de desastres num laboratório de teste utilizando uma cópia de segurança da cópia de segurança mais recente que a tarefa de manutenção cópia de segurança servidor do Site criada.

-   Verificar se o hardware quaisquer erros ou atualizações de hardware disponíveis.  

-   Verifique o estado de funcionamento global do site.  

###  <a name="BKMK_UseMTs"></a> Manter o estado de funcionamento operacional da sua base de dados do site  
 Ao efetuar as tarefas agendadas e configurar a sua hierarquia e site do Configuration Manager, os componentes do site adicionam constantemente dados à base de dados do Configuration Manager. À medida que aumenta a quantidade de dados, desempenho de base de dados e o espaço de armazenamento livre na base de dados diminui. Pode configurar tarefas de manutenção do site para remover dados antigos que já não necessita.  

 Configuration Manager fornece tarefas de manutenção predefinidas que pode utilizar para manter o estado de funcionamento da base de dados do Configuration Manager. Nem todas as tarefas de manutenção estão disponíveis em cada site, por predefinição. Várias tarefas ativadas e alguns não foram e todas suportam uma agenda que pode configurar.  

 A maioria das tarefas de manutenção removem periodicamente dados desatualizados da base de dados do Configuration Manager. Reduzir o tamanho da base de dados removendo dados desnecessários melhora o desempenho e a integridade da base de dados, o que aumenta a eficiência do site e da hierarquia. Outras tarefas, como **reconstruir índices**, ajudar a manter a eficiência da base de dados. Outras tarefas, como o **cópia de segurança do servidor do Site** tarefa, ajudam a preparar-se para a recuperação de desastre.  

> [!IMPORTANT]  
>  Quando planear a agenda de qualquer tarefa que elimine dados, considere a utilização de dados em toda a hierarquia. Quando é executada uma tarefa elimina dados num site, as informações são removidas da base de dados do Configuration Manager e esta alteração é replicada para todos os sites na hierarquia. Esta eliminação pode afetar outras tarefas que dependem desses dados. Por exemplo, no site de administração central, poderá configurar deteção para ser executada uma vez por mês de forma a identificar computadores não clientes. Planeia instalar o cliente do Configuration Manager para estes computadores no prazo de duas semanas da deteção. No entanto, num site na hierarquia, um administrador configura a tarefa eliminar dados de deteção desatualizados para ser executada a cada sete dias. O resultado é que sete dias após são computadores não clientes, estes sejam eliminados da base de dados do Configuration Manager. Volta ao site de administração central, prepara-se para push instalar o cliente do Configuration Manager nestes novos computadores no dia 10. No entanto, porque a tarefa eliminar dados de deteção desatualizados foi recentemente executada e eliminou dados que é sete dias ou mais antiga, os computadores recentemente detetados já não estão disponíveis na base de dados.  

Depois de instalar um site do Configuration Manager, reveja as tarefas de manutenção disponíveis e ative as tarefas necessárias às suas operações. Reveja a agenda predefinida de cada tarefa e, quando necessário, configure a agenda para otimizar a tarefa de manutenção para se ajustar a sua hierarquia e ambiente. Embora a agenda predefinida de cada tarefa se adequar maior parte dos ambientes, monitorizar o desempenho dos seus sites e a base de dados e ser necessário otimizar tarefas para aumentar a eficiência da sua implementação. Planear periodicamente rever o desempenho do site e base de dados e reconfigurar tarefas de manutenção e respetivas agendas para manter essa eficiência.  

#### <a name="set-up-maintenance-tasks"></a>Configurar tarefas de manutenção  
 Cada site do Configuration Manager suporta tarefas de manutenção que ajudam a manter a eficiência operacional da base de dados do site. Por predefinição, várias tarefas de manutenção estão ativadas em cada site e todas as tarefas suportam agendamentos independentes. Tarefas de manutenção são configuradas individualmente para cada site e aplicam-se a base de dados desse site. No entanto, algumas tarefas, como **eliminar dados de deteção desatualizados**, afeta as informações que está disponíveis em todos os sites numa hierarquia.  

 Apenas as tarefas de manutenção que pode configurar um site são apresentadas na consola do Configuration Manager. Para obter uma lista completa das tarefas de manutenção por tipo de site, consulte [tarefas de referência para a manutenção do System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 Utilize o procedimento seguinte para o ajudar a configurar as definições comuns de tarefas de manutenção.  

###### <a name="to-set-up-maintenance-tasks-for-configuration-manager"></a>Para configurar tarefas de manutenção para o Configuration Manager  

1.  Na consola do Configuration Manager, vá para **administração** > **configuração do Site** >**Sites**.  

2.  Escolha o site que tenha a tarefa de manutenção que pretende configurar.  

3.  No **home page** separador o **definições** grupo, escolha **manutenção do Site**e, em seguida, escolha a tarefa de manutenção que pretende configurar.  

    > [!TIP]  
    >  São apresentadas apenas as tarefas que estão disponíveis no site selecionado.  

4.  Para configurar a tarefa, escolha **editar**, certifique-se a **ativar esta tarefa** caixa de verificação está selecionada e configurar uma agenda para quando a tarefa é executada. Se a tarefa também elimina dados antigos, configure a idade dos dados que serão eliminadas da base de dados quando a tarefa é executada. Escolha **OK** para fechar a tarefa **propriedades**.  

    > [!NOTE]  
    >  Para **eliminar mensagens de estado Desatualizadas**, configurar a idade dos dados para eliminar quando configurar regras de filtro de estado.  

5.  Para ativar ou desativar a tarefa sem editar as propriedades de tarefas, escolha o **ativar** ou **desativar** botão. A etiqueta do botão muda, consoante a configuração atual da tarefa.  

6.  Quando tiver terminado de configurar as tarefas de manutenção, escolha **OK** para concluir o procedimento.
