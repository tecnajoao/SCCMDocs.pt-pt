---
title: "Tarefas de manutenção | Documentos do Microsoft"
description: "Compreenda o que manutenção tarefas a efetuar para sites do Configuration Manager e hierarquias e quando deve efetuá-los."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 3b56e84cbe9785e280fb02ede6644a8ed2769586
ms.openlocfilehash: 90b6e4434abc5573a364c769bd835e08e5dff16d
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="maintenance-tasks-for-system-center-configuration-manager"></a>Tarefas de manutenção para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager sites e hierarquias necessitam regularmente a manutenção e monitorização para fornecer serviços de forma eficaz e contínua. Manutenção regular assegura que o hardware, software e a base de dados do Configuration Manager continuam a funcionar corretamente e eficiente. Um desempenho ideal reduz significativamente o risco de falha.  

 Para configurar alertas e utilizar o sistema de estado para monitorizar o estado de funcionamento do Configuration Manager, consulte o artigo [utilizar alertas e o sistema de estado para o System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   [Tarefas de manutenção](#bkmk_MTs)  

##  <a name="bkmk_MTs"></a>Tarefas de manutenção  
 Manutenção regular é importante garantir o funcionamento correto do site. Manter um registo de manutenção que documente manutenção as datas, quem foram manutenção e quaisquer comentários relacionados com a manutenção as tarefas.  

### <a name="when-to-do-common-maintenance-tasks"></a>Quando efetuar tarefas de manutenção comuns  
 Para manter o seu site, considere manutenção diária ou semanal. Algumas tarefas podem exigir um calendário diferente. A manutenção comum pode incluir as tarefas de manutenção incorporadas e outras tarefas, como manutenção de conta para manter a conformidade com as políticas da empresa.  

 Utilize as seguintes informações como guia para ajudar a planear para diferentes tarefas de manutenção. Utilize estas listas como ponto de partida e adicione tarefas que poderá necessitar.  

**Tarefas diárias**   
Seguem-se tarefas de manutenção que pode considerar para uma agenda diária:  

-   Verifique se as tarefas de manutenção predefinidas que se encontram agendadas para ser executada diariamente estão a ser executada com êxito.  

-   Verifique o estado de base de dados do Configuration Manager.  

-   Verificar o estado do servidor de site.  

-   Verifique as pastas de sistema de site do Configuration Manager de ficheiros pendentes.  

-   Verificar o estado de sistemas de sites.  

-   Verifique os registos de eventos do sistema operativo nos sistemas de sites.  

-   Verifique o registo de erros do SQL Server no computador de base de dados do site.  

-   Verificar o desempenho do sistema.  

-   Verifique os alertas do Configuration Manager.  

**Tarefas semanais**   
Seguem-se tarefas de manutenção que pode considerar para um agendamento semanal:  

-   Verifique se tarefas de manutenção predefinidas que se encontram agendadas para serem realizadas semanalmente estão a ser executada com êxito.  

-   Elimine ficheiros desnecessários dos sistemas de sites.  

-   Produzir e distribuir relatórios do utilizador final, se necessário.  

-   Agregar registos de eventos de aplicações, segurança e do sistema e limpar estes registos.  

-   Verificar o tamanho de base de dados do site e verificar que existe espaço em disco disponível suficiente no servidor de base de dados do site para permitir que a base de dados do site cresça.  

-   Efetue a manutenção de base de dados do SQL Server na base de dados de site, de acordo com o plano de manutenção do SQL Server.  

-   Verifique o espaço em disco disponível em todos os sistemas de sites.  

-   Execute as ferramentas de desfragmentação de disco em todos os sistemas de sites.  

**Tarefas periódicas**   
Algumas tarefas que não necessitam de manutenção diária ou semanal são importantes para garantir o estado de funcionamento global do site. Estas tarefas também Certifique-se de que os planos de recuperação de segurança e de desastres estão atualizados. Seguem-se tarefas de manutenção que pode considerar para uma agenda ainda mais periódica que as tarefas diárias ou semanais:  

-   Alterar contas e palavras-passe, se for necessário, de acordo com o plano de segurança.  

-   Rever o plano de manutenção para verificar que tarefas de manutenção agendadas estão agendadas correta e eficaz dependendo das definições de site configuradas.  

-   Reveja a estrutura da hierarquia do Configuration Manager para efetuar quaisquer alterações necessárias.  

-   Verificar o desempenho de rede para se certificar de que não foram efetuadas alterações que afetem as operações do site.  

-   Verifique se as definições do Active Directory que afetem as operações do site não foram alteradas. Por exemplo, verifique se as sub-redes que estejam atribuídos a sites do Active Directory e que são utilizadas como limites para o site do Configuration Manager não foram alteradas.  

-   Rever o plano de recuperação de desastres para efetuar quaisquer alterações necessárias.  

-   Efetue uma recuperação de site, de acordo com o plano de recuperação de desastres num laboratório de teste, utilizando uma cópia de segurança da cópia de segurança mais recente que criou a tarefa de manutenção cópia de segurança do servidor do Site.

-   Verificar se o hardware quaisquer erros ou atualizações de hardware disponíveis.  

-   Verifique o estado de funcionamento global do site.  

###  <a name="BKMK_UseMTs"></a>Manter o estado de funcionamento operacional da sua base de dados do site  
 Enquanto o site do Configuration Manager e a hierarquia efetuar as tarefas por si agendadas e configura, componentes do site adicionam constantemente dados à base de dados do Configuration Manager. À medida que aumenta a quantidade de dados, o desempenho de base de dados e o espaço de armazenamento livre na base de dados diminui. Pode configurar tarefas de manutenção do site para remover dados antigos que já não necessita.  

 O Configuration Manager oferece tarefas de manutenção predefinidas que pode utilizar para manter o estado de funcionamento da base de dados do Configuration Manager. Nem todas as tarefas de manutenção estão disponíveis em cada site, por predefinição. Várias tarefas estão ativadas e alguns não foram, e todas suportam uma agenda que pode configurar.  

 A maioria das tarefas de manutenção removem periodicamente dados desatualizados da base de dados do Configuration Manager. Reduzir o tamanho da base de dados removendo dados desnecessários otimiza o desempenho e a integridade da base de dados, o que aumenta a eficiência do site e da hierarquia. Outras tarefas, como **reconstruir índices**, ajudar a manter a eficiência da base de dados. Outras tarefas, como o **cópia de segurança do servidor do Site** tarefa, ajudam a preparar-se para a recuperação após desastre.  

> [!IMPORTANT]  
>  Quando planear a agenda de qualquer tarefa que elimine dados, considere a utilização desses dados ao longo da hierarquia. Quando uma tarefa elimina dados é executada num site, as informações são removidas da base de dados do Configuration Manager e esta alteração é replicada para todos os sites na hierarquia. Esta eliminação pode afetar outras tarefas que dependem desses dados. Por exemplo, no site de administração central, poderá configurar o deteção para ser executada uma vez por mês para identificar computadores não clientes. Planear instalar o cliente do Configuration Manager para estes computadores dentro da deteção de duas semanas. No entanto, num site da hierarquia, um administrador configura a tarefa eliminar dados de deteção desatualizados para ser executada a cada sete dias. O resultado é que sete dias após são computadores não clientes, estes sejam eliminados da base de dados do Configuration Manager. Voltar ao site de administração central, prepara-se emitir instalar o cliente do Configuration Manager nestes novos computadores no dia 10. No entanto, uma vez que a tarefa eliminar dados de deteção desatualizados foi recentemente executada e eliminou dados que é sete dias ou mais, os computadores recentemente detetados já não estão disponíveis na base de dados.  

Depois de instalar um site do Configuration Manager, reveja as tarefas de manutenção disponíveis e ative as tarefas as operações necessitam. Reveja a agenda predefinida de cada tarefa e quando for necessário, configurar a agenda para otimizar a tarefa de manutenção para se ajustar a sua hierarquia e ambiente. Apesar da agenda predefinida de cada tarefa se adequar maior parte dos ambientes, monitorize o desempenho dos seus sites e a base de dados, podendo ser necessário otimizar tarefas para aumentar a eficiência da sua implementação. Planeie a revisão do desempenho do site e base de dados e reconfigurar as tarefas de manutenção e respetivas agendas para manter essa eficiência periodicamente.  

#### <a name="set-up-maintenance-tasks"></a>Configurar tarefas de manutenção  
 Cada site do Configuration Manager suporta tarefas de manutenção que ajudam a manter a eficiência operacional da base de dados do site. Por predefinição, várias tarefas de manutenção estão ativadas em cada site e todas as tarefas suportam agendas independentes. Tarefas de manutenção estão configuradas individualmente para cada site e aplicam-se a base de dados desse site. No entanto, algumas tarefas, como **eliminar dados de deteção desatualizados**, afetar as informações que estão disponíveis em todos os sites numa hierarquia.  

 Apenas as tarefas de manutenção que pode configurar um site são apresentadas na consola do Configuration Manager. Para obter uma lista completa das tarefas de manutenção por tipo de site, consulte o artigo [referência para a manutenção de tarefas para o System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 Utilize o procedimento seguinte para ajudar a configurar as definições comuns de tarefas de manutenção.  

###### <a name="to-set-up-maintenance-tasks-for-configuration-manager"></a>Para configurar as tarefas de manutenção do Configuration Manager  

1.  Na consola do Configuration Manager, aceda a **administração** > **configuração do Site** >**Sites**.  

2.  Selecione o site que tenha a tarefa de manutenção que pretende configurar.  

3.  No **base** separador o **definições** grupo, selecione **manutenção do Site**e, em seguida, selecione a tarefa de manutenção que pretende configurar.  

    > [!TIP]  
    >  São apresentadas apenas as tarefas que estão disponíveis no site selecionado.  

4.  Para configurar a tarefa, selecione **editar**, certifique-se a **ativar esta tarefa** caixa de verificação está selecionada e configurar uma agenda para quando a tarefa for executada. Se a tarefa também elimina dados antigos, configure a idade de dados que serão eliminados da base de dados quando a tarefa for executada. Escolher **OK** para fechar a tarefa **propriedades**.  

    > [!NOTE]  
    >  Para **eliminar mensagens de estado desatualizados**, configurar a idade de dados para eliminar quando configurar regras do filtro de estado.  

5.  Para ativar ou desativar a tarefa sem editando as propriedades de tarefas, selecione o **ativar** ou **desativar** botão. As alterações de etiqueta de botão consoante a configuração atual da tarefa.  

6.  Quando tiver terminado de configurar as tarefas de manutenção, escolha **OK** para concluir o procedimento.

