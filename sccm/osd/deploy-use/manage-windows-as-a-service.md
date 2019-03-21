---
title: Gerir o Windows como um serviço
titleSuffix: Configuration Manager
description: Ver o estado do Windows como um serviço (WaaS) com o Configuration Manager, criar planos de manutenção para formar anéis de implementação e ver alertas quando os clientes do Windows 10 estiverem ao fim de suporte.
ms.date: 03/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: da1e687b-28f6-43c4-b14a-ff2b76e60d24
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 614ccc06a3fef5cca54c7eb1c32952e8531aedfa
ms.sourcegitcommit: d71e558db2da124357b840332e2da671b3810507
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58269069"
---
# <a name="manage-windows-as-a-service-using-system-center-configuration-manager"></a>Gerir o Windows como um serviço com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 No Configuration Manager, pode ver o estado do Windows como um serviço (WaaS) no seu ambiente. Crie planos de manutenção para formar anéis de implementação e certifique-se de que os sistemas de Windows 10 são mantidos atualizados quando são lançadas novas compilações. Também pode ver alertas quando os clientes do Windows 10 estão a chegar ao fim do suporte para a respetiva compilação da via de atualizações Semianuais.  

 Para obter mais informações sobre as opções de manutenção do Windows 10, consulte [descrição geral do Windows como um serviço](/windows/deployment/update/waas-overview#servicing-channels).  

 Utilize as secções seguintes para gerir o Windows como um serviço.



##  <a name="BKMK_Prerequisites"></a> Pré-requisitos  
 Para ver dados no dashboard de manutenção do Windows 10, terá de efetuar as seguintes ações:  

-   Computadores Windows 10 tem de utilizar as atualizações de software do Configuration Manager com o Windows Server Update Services (WSUS) para gerenciamento de atualizações de software. Quando os computadores utilizam o Windows Update para empresas (ou Windows Insiders) para gerenciamento de atualizações de software, o computador não é avaliado nos planos de manutenção do Windows 10. Para obter mais informações, veja [Integration with Windows Update for Business in Windows 10 (Integração com o Windows Update for Business no Windows 10)](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

-   O WSUS 4.0 com a [correção 3095113](https://support.microsoft.com/kb/3095113) tem de estar instalado nos pontos de atualização de software e nos servidores do site. Esta correção adiciona a **atualizações** classificação de atualização de software. Para obter mais informações, consulte [pré-requisitos para atualizações de software](../../sum/plan-design/prerequisites-for-software-updates.md).  

-   WSUS 4.0 com o [correção 3159706](https://support.microsoft.com/kb/3159706) tem de estar instalado nos seus pontos de atualização de software e servidores para atualizar computadores para a atualização de aniversário do Windows 10, bem como para versões de subsequente do site. Há etapas manuais descritas no artigo de suporte que deve usar para instalar esta correção. Para obter mais informações, consulte a [blogue Enterprise Mobility and Security](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/05/update-your-configmgr-1606-sup-servers-to-deploy-the-windows-10-anniversary-update/).

-   Ative a Deteção Heartbeat. Os dados apresentados no dashboard de manutenção do Windows 10 são encontrados através da deteção. Para obter mais informações, veja [Configure Heartbeat Discovery (Configurar a Deteção de Heartbeat)](../../core/servers/deploy/configure/configure-discovery-methods.md#BKMK_ConfigHBDisc).  

     Do Windows 10 informações de canal e compilação são detetadas e armazenadas nos seguintes atributos:  

    -   **Ramo de preparação do sistema operativo**: Especifica o canal de sistema operativo. Por exemplo, **0** = canal Semianual - direcionado (não difere atualizações), **1** = via de atualizações Semianuais (diferir atualizações), **2** = canal de manutenção de longo prazo (LTSC)

    -   **Compilação do sistema operativo**: Especificar a compilação do sistema operativo. Por exemplo, **10.0.10240** (RTM) ou **10.0.10586** (versão 1511)  

-   O ponto de ligação de serviço tem de estar instalado e configurado para **Online, ligação persistente** modo para ver dados no dashboard de manutenção do Windows 10. Quando estiver no modo offline, não verá as atualizações de dados no dashboard até obter as atualizações de serviço do Configuration Manager. Para obter mais informações, consulte [sobre o ponto de ligação de serviço](../../core/servers/deploy/configure/about-the-service-connection-point.md).  


-   Internet Explorer 9 ou posterior tem de estar instalado no computador que executa a consola do Configuration Manager.  

-   As atualizações de software têm de ser configuradas e sincronizadas. Selecione o **atualizações** classificação e sincronizar as atualizações de software antes de quaisquer atualizações de funcionalidades do Windows 10 estão disponíveis na consola do Configuration Manager. Para obter mais informações, consulte [gestão de atualizações de preparação para a software](../../sum/get-started/prepare-for-software-updates-management.md).  

##  <a name="BKMK_ServicingDashboard"></a> Dashboard de manutenção do Windows 10  
 O dashboard de manutenção do Windows 10 fornece informações sobre computadores Windows 10 no seu ambiente, planos de manutenção ativos, informações de compatibilidade, etc. Os dados no dashboard de manutenção do Windows 10 estão dependentes de ter um Ponto de Ligação de Serviço instalado. O dashboard tem os seguintes mosaicos:  

-   **Mosaico utilização do Windows 10**: Fornece uma análise detalhada das compilações públicas do Windows 10. As compilações do Windows Insiders estão listadas como **outras** , bem como as outras compilações ainda desconhecidas pelo seu site. O ponto de ligação de serviço transfere metadados que informam sobre o Windows cria, e, em seguida, estes dados são comparados aos dados de deteção.  

-   **Mosaico anéis do Windows 10**: Fornece uma análise detalhada do Windows 10 por canal e estado de preparação. O segmento LTSC inclui todas as versões LTSC. O primeiro mosaico divide as versões específicas, por exemplo, Windows 10 LTSC 2015.   

-   **Criar plano do serviço de mosaico**: Fornece uma forma rápida de criar um plano de manutenção. Especifique o nome, coleção (mostra apenas os 10 principais coleções por tamanho, a mais pequena primeiro), o pacote de implementação (mostra apenas os 10 principais pacotes por mais recentemente modificação) e o estado de preparação. Os valores predefinidos são utilizados para as outras definições. Clique em **Definições Avançadas** para iniciar o assistente Criar Plano de Manutenção, onde poderá configurar todas as definições do plano de manutenção.  

-   **Mosaico expirado**: Apresenta a percentagem de dispositivos que estão numa compilação do Windows 10 que passou o respetivo final de vida. O Configuration Manager determina a percentagem dos metadados que o ponto de ligação de serviço transfere e compara-os aos dados de deteção. Uma compilação que passou o respetivo final de vida já não está a receber atualizações cumulativas mensais, que incluem atualizações de segurança. Os computadores nesta categoria devem ser atualizados para a próxima versão de compilação. O Configuration Manager Arredonda por excesso para o número inteiro seguinte. Por exemplo, se tiver de 10.000 computadores e apenas um de uma compilação expirada, o mosaico apresenta 1%.  

-   **Mosaico expirar em breve**: Apresenta a percentagem de computadores que estão numa compilação que está perto do final de vida (dentro de, aproximadamente, quatro meses), semelhante a **expirado** mosaico. O Configuration Manager Arredonda por excesso para o número inteiro seguinte.  

-   **Mosaico alertas**: Apresenta os alertas ativos.  

-   **Mosaico monitorização do plano de serviço**: Mostra os planos que tenha criado de manutenção e um gráfico da conformidade para cada um. Este mosaico dá-lhe uma rápida visão geral do estado atual das implementações de plano de manutenção. Se um anel de implementação anterior for ao encontro das suas expectativas em termos de conformidade, poderá selecionar um plano de manutenção posterior (anel de implementação) e clicar em **Implementar Agora** em vez de aguardar que as regras do plano de manutenção sejam acionadas automaticamente.  

-   O **mosaico compilações do Windows 10**: Exibição é um momento de imagem fixa linha que que cria uma visão geral do Windows 10 lançadas atualmente e dá-lhe uma ideia geral de quando cria a transição para Estados diferentes.  

> [!IMPORTANT]  
>  As informações mostradas no dashboard de manutenção do Windows 10 (por exemplo, o ciclo de vida de suporte para as versões do Windows 10) são fornecidas para sua comodidade e apenas para utilização interna na empresa. Não deverá confiar apenas nestas informações para confirmar a compatibilidade de atualização. Certifique-se de que verifica a exatidão das informações que lhe são fornecidas.  

## <a name="servicing-plan-workflow"></a>Fluxo de trabalho do plano de manutenção  
 Planos de manutenção do Windows 10 no Configuration Manager são muito, como regras de implementação automática para atualizações de software. Criar um plano de manutenção com os seguintes critérios que o Configuration Manager avalia:  

- **Atualiza a classificação**: Apenas as atualizações que estão a **atualizações** são avaliadas.  

- **Estado de preparação**: O estado de preparação definido no plano de manutenção é comparado com o estado de preparação para a atualização. Os metadados para a atualização são obtidos quando o ponto de ligação de serviço verifica a existência de atualizações.  

- **Diferimento por tempo**: O número de dias que especificou para **quantos dias depois da Microsoft ter publicado uma nova atualização gostaria de aguardar antes de implementar no seu ambiente** no plano de manutenção. Se a data atual for posterior à data de lançamento mais o número de dias configurado, o Configuration Manager avalia se pretende incluir uma atualização na implementação.  

  Quando uma atualização cumpre os critérios, o plano de manutenção adiciona a atualização ao pacote de implementação, distribui o pacote por pontos de distribuição e implementa a atualização na coleção com base nas definições configuradas no plano de manutenção. Pode monitorizar as implementações no mosaico Monitorização do Plano de Serviço no Dashboard de Manutenção do Windows 10. Para obter mais informações, consulte [monitorizar atualizações de software](../../sum/deploy-use/monitor-software-updates.md).  

##  <a name="BKMK_ServicingPlan"></a> Plano de manutenção do Windows 10  
 À medida que implementa o canal Semianual do Windows 10, pode criar um ou mais planos de manutenção para definir os anéis de implementação que pretende no seu ambiente e, em seguida, monitorizá-los no dashboard de manutenção do Windows 10. Os planos de serviço utilizam apenas a classificação de atualizações de software **Atualizações** e não atualizações cumulativas para o Windows 10. No caso dessas atualizações, ainda tem de implementar com o fluxo de trabalho de atualizações de software. A experiência do utilizador final com um plano de manutenção é idêntica à das atualizações de software, incluindo as definições configuradas no plano de manutenção.  

> [!NOTE]  
>  Pode utilizar uma sequência de tarefas para implementar uma atualização para cada compilação do Windows 10, mas requer mais trabalho manual. Terá de importar os ficheiros de origem atualizados como um pacote de atualização do sistema operativo e, em seguida, criar e implementar a sequência de tarefas para o conjunto adequado de computadores. No entanto, uma sequência de tarefas fornece opções personalizadas adicionais, tais como as ações de pré-implementação e pós-implementação.  

 Pode criar um plano de manutenção básico a partir do dashboard de manutenção do Windows 10. Depois de especificar o nome, coleção (mostra apenas os 10 principais coleções por tamanho, a mais pequena primeiro), o pacote de implementação (mostra apenas os 10 principais pacotes por mais recentemente modificação) e preparação para o estado, o plano de manutenção com o Configuration Manager cria valores predefinidos para as outras definições. Também pode iniciar o assistente Criar Plano de Manutenção para configurar todas as definições. Utilize o procedimento seguinte para criar um plano de manutenção utilizando o assistente Criar Plano de Manutenção.  

> [!NOTE]  
>  Pode gerir o comportamento de implementações de alto risco. Uma implementação de alto risco é uma implementação que é automaticamente instalada e que tem o potencial de causar resultados indesejados. Por exemplo, uma sequência de tarefas que tenha o objetivo **Obrigatório** que implemente o Windows 10 é considerada uma implementação de alto risco. Para obter mais informações, consulte [definições para gerir implementações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

#### <a name="to-create-a-windows-10-servicing-plan"></a>Para criar um plano de manutenção do Windows 10  

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2. Na área de trabalho Biblioteca de Software, expanda **Manutenção do Windows 10**e, em seguida, clique em **Planos de Manutenção**.  

3. No separador **Home page** , no grupo **Criar** , clique em **Criar Plano de Manutenção**. O assistente Criar Plano de Manutenção abre.  

4. Na página **Geral** , configure as seguintes definições:  

   -   **Nome**: Especifique o nome do plano de manutenção. O nome tem de ser exclusivo, ajudam a descrever o objetivo da regra e identificá-la de outras pessoas no site do Configuration Manager.  

   -   **Descrição**: Especifique uma descrição para o plano de manutenção. A descrição deve fornecer uma visão geral do plano de manutenção e outras informações relevantes que ajudem a identificar e a distinguir o plano dos restantes no site do Configuration Manager. O campo de descrição é opcional, tem um limite de 256 caracteres e está em branco por predefinição.  

5. Na página Plano de Manutenção, configure as seguintes definições:  

   -   **Coleção de destino**: Especifica a coleção de destino a ser utilizado para o plano de manutenção. Os membros da coleção recebem as atualizações do Windows 10 definidas no plano de manutenção.  

       > [!NOTE]  
       >  Ao implementar uma implementação de alto risco, como plano de manutenção, o **selecionar coleção** janela exibe apenas as coleções personalizadas que cumprem as definições de verificação de implementação que estão configuradas nas propriedades do site.
       >    
       > As implementações de alto risco são sempre limitadas a coleções personalizadas, coleções criadas por si e à coleção incorporada **Computadores Desconhecidos** . Quando cria uma implementação de alto risco, não pode selecionar uma coleção incorporada, como **Todos os Sistemas**. Desmarque **ocultar coleções com um membro contagem superiores à configuração de tamanho mínimo do site** para ver todas as coleções personalizadas que incluem menos clientes do que o tamanho máximo configurado. Para obter mais informações, consulte [definições para gerir implementações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md).  
       >  
       > As definições de verificação da implementação são baseadas na associação atual da coleção. Após implementar o plano de manutenção, a associação da coleção não é reavaliada relativamente às definições de implementação de alto risco.  
       >  
       > Por exemplo, digamos que definiu **tamanho predefinido** para 100 e o **tamanho máximo** a 1000. Quando cria uma implementação de alto risco, a janela **Selecionar Coleção** só apresenta as coleções com menos de cem clientes. Se desmarcar a **ocultar coleções com um membro contagem superiores à configuração de tamanho mínimo do site** definição, a janela apresentará as coleções que contenham menos de 1 000 clientes.  
       >
       > Quando seleciona uma coleção que contém uma função de site, aplica-se os seguintes critérios:    
       >   
       >    - Se a coleção contiver um servidor do sistema de sites e nas definições de verificação de implementação configurar o bloqueio das coleções com servidores do sistema de sites, ocorrerá um erro e não conseguirá continuar.    
       >    - Se a coleção contiver um servidor do sistema de sites e nas definições de verificação da implementação configurar a apresentação de um aviso caso as coleções incluam servidores do sistema de sites, se a coleção ultrapassar o valor do tamanho predefinido ou se a coleção contiver um servidor, o Assistente de Implementação de Software apresentará um aviso de alto risco. Tem de aceitar criar uma implementação de alto risco e é criada uma mensagem de estado de auditoria.  

6. Na página Anel de Implementação, configure as seguintes definições:  

   -   **Especificar o estado de preparação do Windows ao qual este plano de manutenção deve ser aplicada**: Selecione uma das seguintes opções:  

       -   **Via de atualizações Semianuais (direcionada)**: Neste modelo de manutenção, as atualizações de funcionalidades estão disponíveis assim que a Microsoft lança-los.

       -   **Canal semi-anual**: Este canal de manutenção é normalmente utilizado para uma implementação abrangente. Clientes de Windows 10 na via de atualizações Semianuais recebem a mesma compilação do Windows 10 como esses dispositivos no canal de destino, apenas num momento posterior.

       Para obter mais informações sobre a manutenção de canais e que opções são melhores para, consulte [canais de serviço](/windows/deployment/update/waas-overview#servicing-channels).

   -   **Quantos dias depois de a Microsoft ter publicado uma nova atualização gostaria de aguardar antes de implementar no seu ambiente**: Se a data atual for posterior à data de lançamento mais o número de dias que configurar para esta definição, o Configuration Manager avalia se pretende incluir uma atualização na implementação.


7. Na página de atualizações, configure os critérios de pesquisa para filtrar as atualizações que são adicionadas ao plano de serviço. Apenas as atualizações que cumprem os critérios especificados são adicionadas à implementação associada. Estão disponíveis os seguintes filtros de propriedade: <!--3098809, 3113836, 3204570 -->

   - **Arquitectura de** (começando na versão 1810)
   - **Idioma**
   - **Categoria do produto** (começando na versão 1810)
   - **Necessário**
      > [!Important]    
      > Recomendamos que como parte de seus critérios de pesquisa, que defina os **necessários** campo com um valor de **> = 1**. Usar este critério garante que as atualizações aplicáveis apenas adicionadas ao plano de serviço.
   - **Substituído** (começando na versão 1810)
   - **Título**

    Clique em **Pré-visualizar** para ver as atualizações que cumprem os critérios especificados.  

8. Na página Agenda de Implementação, configure as seguintes definições:  

   -   **Avaliação da agenda**: Especifique se o Configuration Manager avalia o tempo disponível e o prazo de instalação utilizando a hora UTC ou na hora local do computador que executa a consola do Configuration Manager.  

       > [!NOTE]  
       >  Quando selecionar a hora local e, em seguida, selecione **logo que possível** para o **hora de disponibilização do Software** ou **prazo de instalação**, a hora atual no computador com o consola do Configuration Manager é utilizada para calcular quando estão disponíveis atualizações ou quando são instaladas num cliente. Se o cliente tiver um fuso horário diferente, estas ações irão ocorrer quando a hora do cliente corresponder à hora de avaliação.  

   -   **Hora de disponibilização do software**: Selecione uma das seguintes definições para especificar quando as atualizações de software são disponibilizadas aos clientes:  

       -   **Assim que possível**: Selecione esta definição para disponibilizar as atualizações de software que estão incluídas na implementação aos computadores cliente logo que possível. Quando criar a implementação com esta definição selecionada, o Configuration Manager atualiza a política de cliente. Em seguida, durante o ciclo seguinte de consulta da política de cliente, os clientes ficarão informados da implementação e poderão obter as atualizações que estiverem disponíveis para instalação.  

       -   **Hora específica**: Selecione esta definição para disponibilizar as atualizações de software que estão incluídas na implementação aos computadores cliente numa data e hora específicas. Quando criar a implementação com esta definição ativada, o Configuration Manager atualiza a política de cliente. Em seguida, durante o ciclo de consulta seguinte da política de cliente, os clientes estarão informados da implementação. No entanto, as atualizações de software da implementação não ficarão disponíveis para instalação antes da data e hora configuradas.  

   -   **Prazo de instalação**: Selecione uma das seguintes definições para especificar o prazo de instalação das atualizações de software da implementação:  

       -   **Assim que possível**: Selecione esta definição para instalar automaticamente as atualizações de software na implementação logo que possível.  

       -   **Hora específica**: Selecione esta definição para instalar automaticamente as atualizações de software da implementação numa hora e data específicas. O Configuration Manager determina o prazo de instalação de atualizações de software ao adicionar configurada **hora específica** intervalo para o **hora de disponibilização do Software**.  

           > [!NOTE]  
           >  A hora real do prazo de instalação corresponde à hora apresentada acrescida de um período de tempo aleatório de até 2 horas. Desta forma, reduzirá o impacto potencial da instalação das atualizações na implementação ao mesmo tempo em todos os computadores cliente da coleção de destino.  
           >   
           >  Pode configurar a definição de cliente **Agente do Computador** **Desativar a aleatoriedade de prazos** para desativar o atraso da aleatoriedade da instalação para as atualizações necessárias. Para obter mais informações, veja [Agente do Computador](../../core/clients/deploy/about-client-settings.md#computer-agent).  

9. Na página Experiência de Utilizador, configure as seguintes definições:  

    -   **Notificações do utilizador**: Especifique se pretende apresentar a notificação de atualizações no Centro de Software no computador cliente à configurada **hora de disponibilização do Software** e se pretende apresentar as notificações de utilizador nos computadores cliente.  

    -   **Comportamento do prazo**: Especifique o comportamento a adotar quando é atingido o prazo para a implementação da atualização. Especifique se pretende instalar as atualizações na implementação. Especifique também se pretende reiniciar o sistema após a instalação da atualização, independentemente de uma janela de manutenção configurada. Para obter mais informações sobre janelas de manutenção, consulte [como utilizar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamento do reinício do dispositivo**: Especifique se pretende suprimir um reinício do sistema nos servidores e estações de trabalho após as atualizações são instaladas e é necessário reiniciar o sistema para concluir a instalação.  

    -   **Processamento para dispositivos Windows Embedded do filtro de escrita**: Ao implementar atualizações em dispositivos Windows Embedded que tenham um filtro de escrita ativado, pode especificar a instalar a atualização na sobreposição temporária e a confirmar as alterações mais tarde ou por confirmar as alterações no prazo de instalação ou durante uma janela de manutenção. Ao consolidar alterações no momento da instalação ou durante uma janela de manutenção, será necessário um reinício para que as alterações sejam mantidas no dispositivo.  

        > [!NOTE]  
        >  Ao implementar uma atualização num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada.  

10. Na página Pacote de Implementação, selecione um pacote de implementação existente ou configure as seguintes definições para criar um novo pacote de implementação:  

    1.  **Nome**: Especifique o nome do pacote de implementação. Este nome tem de ser exclusivo e descreve o conteúdo do pacote. Está limitado a 50 carateres.  

    2.  **Descrição**: Especifique uma descrição que disponibilize informações sobre o pacote de implementação. A descrição está limitada a 127 caracteres.  

    3.  **Origem do pacote**: Especifica a localização dos ficheiros de origem de atualização do software. Escreva um caminho de rede para a localização de origem, como, por exemplo, **\\\server\sharename\path**ou clique em **Procurar** para procurar a localização de rede. Crie a pasta partilhada para os ficheiros de origem do pacote de implementação antes de prosseguir para a página seguinte.  

        > [!NOTE]  
        >  A localização de origem do pacote de implementação que especificar não poderá ser utilizada por outro pacote de implementação de software.  

        > [!IMPORTANT]  
        >  Tanto a conta de computador do Fornecedor de SMS, como o utilizador que executar o assistente para transferir as atualizações de software, têm de ter permissões NTFS de **Escrita** na localização de transferência. Deverá restringir cuidadosamente o acesso à localização de transferência para reduzir o risco de adulteração dos ficheiros de origem de atualização de software por parte de atacantes.  

        > [!IMPORTANT]  
        >  Pode alterar a localização de origem do pacote nas propriedades do pacote de implementação depois do Configuration Manager cria o pacote de implementação. Mas se o fizer, terá primeiro de copiar o conteúdo da origem inicial do pacote para a nova localização de origem do pacote.  

    4.  **Prioridade de envio**: Especifique a prioridade de envio para o pacote de implementação. O Configuration Manager utiliza a prioridade de envio para o pacote de implementação quando envia o pacote para pontos de distribuição. Pacotes de implementação são enviados por ordem de prioridade: Alta, média ou baixa. Os pacotes com prioridades idênticas são enviados pela ordem em que foram criados. Se não houver nenhum registo de segurança, o pacote de processos imediatamente, independentemente de sua prioridade.  

11. Na página pontos de distribuição, especifique os pontos de distribuição ou grupos de pontos de distribuição que alojam os ficheiros de atualização. Para obter mais informações sobre pontos de distribuição, consulte [configurar um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_configs).

    > [!NOTE]  
    >  Esta página apenas está disponível ao criar um novo pacote de implementação da atualização de software.  

12. Na página Localização de Transferência, especifique se pretende transferir os ficheiros de atualização a partir da Internet ou da rede local. Configure as seguintes definições:  

    -   **Transferir atualizações de software a partir da Internet**: Selecione esta definição para transferir as atualizações a partir de uma localização especificada na Internet. Esta definição está ativada por predefinição.  

    -   **Transferir atualizações de software a partir de uma localização na rede local**: Selecione esta definição para transferir as atualizações a partir de um diretório local ou uma pasta compartilhada. Esta definição é útil se o computador que executa o assistente não tiver acesso à Internet. Qualquer computador que disponha de acesso à Internet poderá transferir provisoriamente as atualizações e armazená-las numa localização da rede local que esteja acessível ao computador que executa o assistente.  

13. Na página Seleção de Idioma, selecione os idiomas para os quais serão transferidas as atualizações selecionadas. As atualizações apenas são transferidas se estiverem disponíveis nos idiomas selecionados. As atualizações que não sejam específicas do idioma serão sempre transferidas. Por predefinição, o assistente seleciona os idiomas que tiver configurado nas propriedades do ponto de atualização de software. Terá de estar selecionado pelo menos um idioma para que possa prosseguir para a página seguinte. Se selecionar apenas idiomas que não são suportados por uma atualização, o download falha para a atualização.  

14. Na página Resumo, reveja as definições e clique em **Seguinte** para criar o plano de manutenção.  

    Depois de concluir o assistente, o plano de manutenção será executado. Ele adiciona as atualizações que cumprem os critérios especificados a um grupo de atualização de software, transferir as atualizações para a biblioteca de conteúdos no servidor do site, distribuir as atualizações para os pontos de distribuição configurados e, em seguida, implementar o grupo de atualizações de software nos clientes das coleção de destino.  

##  <a name="BKMK_ModifyServicingPlan"></a> Modificar um plano de manutenção  
Depois de criar um plano de manutenção básico a partir do dashboard de manutenção do Windows 10 ou precisar de alterar as definições para um plano de manutenção existente, pode aceder às propriedades do plano de manutenção.

> [!NOTE]
> Pode configurar as definições nas propriedades do plano de manutenção que não estão disponíveis no assistente quando cria o plano de manutenção. O assistente utiliza as predefinições para as definições para o seguinte: transferir as definições, definições de implementação e alertas.  

Utilize o procedimento seguinte para modificar as propriedades de um plano de manutenção.  

#### <a name="to-modify-the-properties-of-a-servicing-plan"></a>Para modificar as propriedades de um plano de manutenção  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho Biblioteca de Software, expanda **Manutenção do Windows 10**, clique em **Planos de Manutenção**e, em seguida, selecione o plano de manutenção que pretende modificar.  

3.  No separador **Home page** , clique em **Propriedades** para abrir as propriedades do plano de manutenção selecionado.

    As seguintes definições estão disponíveis nas propriedades do plano de manutenção que não foram configuradas no assistente:

    **Definições de implementação**: No separador Definições de implementação, configure as seguintes definições:  

    -   **Tipo de implementação**: Especifique o tipo de implementação para a implementação de atualização de software. Selecione **Necessário** para criar uma implementação de atualização de software obrigatória através da qual as atualizações de software são automaticamente instaladas nos clientes antes de um prazo de instalação configurado. Selecione **Disponível** para criar uma implementação de atualização de software opcional que estará disponível para ser instalada pelos utilizadores a partir do Centro de Software.  

        > [!IMPORTANT]  
        >  Após criar a implementação de atualização de software, não poderá alterar o tipo de implementação mais tarde.  

        > [!NOTE]  
        >  Um grupo de atualização de software implementado como **necessário** é transferido em segundo plano e respeita as definições de BITS, se configurado.  
        >  
        > No entanto, os grupos de atualização de software implementados como **disponível** são transferidos em primeiro plano e ignorar as definições de BITS.  

    -   **Usar o Wake-on-LAN para reativar os clientes para as implementações necessárias**: Especifique se pretende ativar a reativação por LAN na data limite para o envio de pacotes de reativação para computadores que necessitem de uma ou mais atualizações de software na implementação. Todos os computadores que estejam no modo de suspensão quando for atingido o prazo de instalação são despertados, de modo pode iniciar a instalação de atualização de software. Os clientes que se encontrem no modo de suspensão e que não necessitem de quaisquer atualizações de software no âmbito da implementação não serão iniciados. Por predefinição, esta definição não está ativada e só estará disponível se **Tipo de implementação** estiver definido como **Necessário**.  

        > [!WARNING]  
        >  Para poder utilizar esta opção, os computadores e redes terão de estar configurados para Reativação por LAN.  

    -   **Nível de detalhe**: Especifique o nível de detalhe para as mensagens de estado que são enviadas pelos computadores cliente.  

    **Transferir definições**: No separador Definições de transferência, configure as seguintes definições:  

    - Especifique se o cliente transfere e instala as atualizações de software, quando um cliente está ligado a uma rede lenta ou estiver a utilizar uma localização de conteúdo de contingência.  

    - Especifique se pretende que o cliente transfira e instale as atualizações de software a partir de um ponto de distribuição de contingência quando o conteúdo das atualizações de software não estiver disponível num ponto de distribuição preferencial.  

    -   **Permitir que os clientes partilhem conteúdos com outros clientes na mesma sub-rede**: Especifique se pretende ativar a utilização do BranchCache para transferências de conteúdos. Para obter mais informações sobre o BranchCache, consulte [conceitos fundamentais da gestão de conteúdos](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    -   Especifique se pretende que os clientes a transferir software de atualizações do Microsoft Update se as atualizações de software não estiverem disponíveis nos pontos de distribuição.
        > [!IMPORTANT]
        > Não utilize esta definição para atualizações de manutenção do Windows 10. O Configuration Manager (pelo menos por meio da versão 1610) não conseguir transferir as atualizações de manutenção do Windows 10 do Microsoft Update.

    -   Especifique se pretende permitir que os clientes efetuem a transferência após um prazo de instalação se estiverem a utilizar ligações à Internet com tráfego limitado. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando se encontra numa ligação à Internet com tráfego limitado.   

    **Alertas**: No separador de alertas, configure como o Configuration Manager e o System Center Operations Manager geram alertas para esta implementação. Só poderá configurar alertas quando o **Tipo de implementação** está definido como **Necessário** na página Definições de Implementação.  

    > [!NOTE]  
    >  Pode rever os alertas de atualizações de software recentes a partir do nó **Atualizações de Software** da área de trabalho **Biblioteca de Software** .  

**Para obter mais informações:** <br/>
[Conceitos básicos do Configuration Manager como um serviço e o Windows como um serviço](/sccm/core/understand/configuration-manager-and-windows-as-service.md)
