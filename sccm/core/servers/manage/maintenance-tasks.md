---
title: Tarefas de manutenção
titleSuffix: Configuration Manager
description: Compreenda quais manutenção de tarefas a efetuar para sites do Configuration Manager e hierarquias e quando executá-los.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bee46ea8eba968c0714478ff0921b0d9b3447621
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123176"
---
# <a name="maintenance-tasks-for-system-center-configuration-manager"></a>Tarefas de manutenção para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Sites do System Center Configuration Manager e hierarquias do necessitam de manutenção regular e monitorização para fornecer serviços de forma eficaz e contínua. Manutenção regular assegura que o hardware, software e banco de dados do Configuration Manager continuam a funcionar corretamente e de forma eficiente. Desempenho ideal reduz significativamente o risco de falha.  

 Para configurar alertas e utilizar o sistema de estado para monitorizar o estado de funcionamento do Configuration Manager, veja [utilizar alertas e o estado do sistema do System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   [Tarefas de manutenção](#bkmk_MTs)  

##  <a name="bkmk_MTs"></a> Tarefas de manutenção  
 Manutenção regular é importante para garantir o funcionamento correto do site. Mantenha um registo de manutenção para datas de manutenção de documento, que fizeram a manutenção e comentários sobre as tarefas relacionadas com a manutenção.  

### <a name="when-to-do-common-maintenance-tasks"></a>Quando realizar tarefas de manutenção comuns  
 Para manter o site, considere a manutenção diária ou semanal. Algumas tarefas podem exigir uma programação diferente. A manutenção comum pode incluir as tarefas de manutenção incorporadas e outras tarefas como manutenção de conta para manter a conformidade com as políticas da empresa.  

 Utilize as seguintes informações como guia para ajudar a planear a realizar tarefas de manutenção diferentes. Utilize estas listas como ponto de partida e adicionar tarefas que poderá precisar.  

**Tarefas diárias**   
Seguem-se tarefas de manutenção que pode considerar para com base numa agenda diária:  

-   Verifique se as tarefas de manutenção agendadas para serem realizadas diariamente estão a funcionar com êxito.  

-   Verificar o estado de banco de dados do Configuration Manager.  

-   Verificar o estado do servidor de site.  

-   Verifique inboxes de sistema de site do Configuration Manager para ficheiros pendentes nas.  

-   Verificar o estado de sistemas de sites.  

-   Verifique os registos de eventos do sistema operativo nos sistemas de sites.  

-   Verifique o registo de erros do SQL Server no computador de base de dados do site.  

-   Verificar o desempenho do sistema.  

-   Verifique os alertas do Configuration Manager.  

**Tarefas semanais**   
Seguem-se tarefas de manutenção que pode considerar numa base semanal:  

-   Verifique se as tarefas de manutenção agendadas para serem realizadas semanalmente estão a funcionar com êxito.  

-   Elimine ficheiros desnecessários dos sistemas de sites.  

-   Produzir e distribuir relatórios do utilizador final, se necessário.  

-   Fazer cópias de segurança de registos de eventos de aplicações, segurança e do sistema e limpar estes registos.  

-   Verificar o tamanho de base de dados do site e verifique se existe espaço em disco disponível suficiente no servidor de base de dados do site, para que a base de dados do site cresça.  

-   Fazer manutenção de banco de dados do SQL Server na base de dados do site, de acordo com seu plano de manutenção do SQL Server.  

-   Verifique o espaço em disco disponível em todos os sistemas de sites.  

-   Execute as ferramentas de desfragmentação de disco em todos os sistemas de sites.  

**Tarefas periódicas**   
Algumas tarefas que não necessitam de manutenção diária ou semanal são importantes para garantir o estado de funcionamento global do site. Estas tarefas também garantem que os planos de recuperação após desastre e de segurança estão atualizados. Seguem-se tarefas de manutenção que pode considerar para uma agenda periódica mais do que as tarefas diárias ou semanais:  

-   Alterar contas e palavras-passe, se for necessário, de acordo com o plano de segurança.  

-   Rever o plano de manutenção para verificar que tarefas de manutenção agendadas estão agendadas corretamente e eficaz dependendo das definições de site configuradas.  

-   Rever a estrutura de hierarquia do Configuration Manager para todas as alterações necessárias.  

-   Verificar o desempenho de rede para se certificar de que não foram feitas alterações que afetem as operações do site.  

-   Verifique que não foram alteradas as definições do Active Directory que afetem as operações do site. Por exemplo, verifique que a sub-redes que estão atribuídos a sites do Active Directory e que são utilizadas como limites de site do Configuration Manager não foram alterados.  

-   Rever o plano de recuperação de desastres para todas as alterações necessárias.  

-   Fazer uma recuperação de site, de acordo com o plano de recuperação de desastres num laboratório de teste, utilizando um exemplar da mais recente cópia de segurança que criou a tarefa de manutenção do servidor do Site de cópia de segurança.

-   Verificar se o hardware apresenta quaisquer erros ou atualizações de hardware disponíveis.  

-   Verifique o estado de funcionamento global do site.  

###  <a name="BKMK_UseMTs"></a> Manter o estado de funcionamento operacional da sua base de dados do site  
 Embora o site do Configuration Manager e a hierarquia fazem as tarefas por si agendadas e configura, componentes do site adicionam constantemente dados na base de dados do Configuration Manager. À medida que aumenta a quantidade de dados, recusar o desempenho de base de dados e o espaço de armazenamento livre na base de dados. Pode configurar tarefas de manutenção do site para remover dados antigos que já não precisa.  

 O Configuration Manager fornece tarefas de manutenção predefinidas que pode utilizar para manter o estado de funcionamento da base de dados do Configuration Manager. Nem todas as tarefas de manutenção estão disponíveis em cada site, por predefinição. Várias tarefas estão ativadas, enquanto outros não são, e todas suportam uma agenda que pode configurar.  

 A maioria das tarefas de manutenção removem periodicamente dados desatualizados da base de dados do Configuration Manager. Reduzir o tamanho da base de dados removendo dados desnecessários melhora o desempenho e a integridade da base de dados, o que aumenta a eficiência do site e da hierarquia. Outras tarefas, como **reconstruir índices**, ajudar a manter a eficiência da base de dados. Outras tarefas, como o **servidor do Site de cópia de segurança** tarefa, ajudam a preparar para recuperação após desastre.  

> [!IMPORTANT]  
>  Quando planear a agenda de qualquer tarefa que elimine dados, considere a utilização desses dados transversalmente na hierarquia. Quando é executada uma tarefa elimina dados num site, as informações são removidas da base de dados do Configuration Manager e esta alteração é replicada para todos os sites na hierarquia. Esta exclusão pode afetar outras tarefas que dependem desses dados. Por exemplo, no site de administração central, pode configurar a deteção para executar uma vez por mês para identificar computadores não clientes. Planeja instalar o cliente do Configuration Manager para estes computadores dentro de duas semanas de sua descoberta. No entanto, um site na hierarquia, um administrador configura a tarefa eliminar dados de deteção desatualizados para ser executado a cada sete dias. O resultado é que sete dias após o que são descobertos computadores não clientes, eles são eliminados da base de dados do Configuration Manager. Novamente no site de administração central, se preparar para push instalar o cliente do Configuration Manager nestes novos computadores no dia 10. No entanto, uma vez que a tarefa eliminar dados de deteção desatualizados foi recentemente executada e eliminou dados que é de sete dias ou mais, os computadores recentemente detetados já não estão disponíveis na base de dados.  

Depois de instalar um site do Configuration Manager, reveja as tarefas de manutenção disponíveis e ative as tarefas que necessitam de suas operações. Reveja a agenda predefinida de cada tarefa e, quando for necessário, configure a agenda para otimizar a tarefa de manutenção de acordo com sua hierarquia e ambiente. Embora a agenda predefinida de cada tarefa se adequar a maioria dos ambientes, monitorize o desempenho dos seus sites e a base de dados e esperam necessário otimizar tarefas para aumentar a eficiência da sua implementação. Planear para periodicamente rever o desempenho de site e base de dados e reconfigurar tarefas de manutenção e respetivas agendas para manter essa eficiência.  

#### <a name="set-up-maintenance-tasks"></a>Configurar tarefas de manutenção  
 Cada site do Configuration Manager suporta tarefas de manutenção que ajudam a manter a eficiência operacional da base de dados do site. Por predefinição, várias tarefas de manutenção estão ativadas em cada site e todas as tarefas suportam agendamentos independentes. Tarefas de manutenção são configuradas individualmente para cada site e aplicam-se a base de dados desse site. No entanto, algumas tarefas, como **eliminar dados de deteção desatualizados**, afeta as informações que está disponíveis em todos os sites numa hierarquia.  

 Apenas as tarefas de manutenção que pode configurar num site são apresentadas na consola do Configuration Manager. Para obter uma lista completa das tarefas de manutenção por tipo de site, consulte [tarefas de manutenção para o System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 Utilize o procedimento seguinte para ajudar a configurar as definições comuns de tarefas de manutenção.  

###### <a name="to-set-up-maintenance-tasks-for-configuration-manager"></a>Configurar tarefas de manutenção para o Configuration Manager  

1.  Na consola do Configuration Manager, aceda a **Administration** > **configuração do Site** >**Sites**.  

2.  Escolha o site que tem a tarefa de manutenção que pretende configurar.  

3.  Na **home page** separador a **definições** de grupo, escolha **manutenção do Site**e, em seguida, selecione a tarefa de manutenção que pretende configurar.  

    > [!TIP]  
    >  São apresentadas apenas as tarefas que estão disponíveis no site selecionado.  

4.  Para configurar a tarefa, escolha **edite**, certifique-se a **ativar esta tarefa** caixa de verificação é verificada e configurar uma agenda para quando a tarefa é executada. Se a tarefa também eliminar dados antigos, configure a idade dos dados que vão ser eliminados da base de dados quando a tarefa é executada. Escolher **OK** para fechar a tarefa **propriedades**.  

    > [!NOTE]  
    >  Para **eliminar mensagens de estado Desatualizadas**, configurar a idade dos dados para eliminar quando configurar regras de filtro de estado.  

5.  Para ativar ou desativar a tarefa sem editar as propriedades de tarefas, escolha o **habilitar** ou **desativar** botão. A etiqueta do botão muda consoante a configuração atual da tarefa.  

6.  Quando tiver terminado de configurar as tarefas de manutenção, escolha **OK** para concluir o procedimento.
