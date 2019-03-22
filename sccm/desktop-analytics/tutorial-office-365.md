---
title: Tutorial - implementar o Office 365
titleSuffix: Configuration Manager
description: Um tutorial sobre como utilizar a análise de ambiente de trabalho e o Configuration Manager para implementar o Office 365 para um grupo piloto.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: tutorial
ms.assetid: 0b2b633a-91d7-4497-8c2a-1fc7aa310bb1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: b8102e426e4737efdd5ca77de2824c1465b382ec
ms.sourcegitcommit: 5f17355f954b9d9e10325c0e9854a9d582dec777
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/21/2019
ms.locfileid: "58329503"
---
# <a name="tutorial-deploy-office-365-to-pilot"></a>Tutorial: Implementar o Office 365 para piloto 

> [!Note]  
> Estas informações se relaciona com o serviço de pré-visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft faz não oferece quaisquer garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Este tutorial utiliza a análise de ambiente de trabalho e o Configuration Manager para implementar o Office 365 ProPlus para um grupo piloto. Ele destaca a integração do serviço cloud para fornecer informações para implementar a aplicação com o produto no local. Utilize a análise de ambiente de trabalho para determinar os melhor dispositivos para colocar num grupo piloto. Em seguida, utilize o Configuration Manager para obter atual com o Office.

Neste tutorial, ficará a saber como:  

> [!div class="checklist"]  
> * Configurar a análise de ambiente de trabalho no portal do Azure  
> * Ligar o Configuration Manager e configure as definições do dispositivo  
> * Criar um plano de implantação de análise de ambiente de trabalho do Office 365 ProPlus  
> * Implementar o Office 365 ProPlus no Configuration Manager no grupo piloto  

Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar. Quando configurado corretamente, uso de análise de ambiente de trabalho não incorrem em quaisquer custos do Azure. 

Análise de área de trabalho utiliza uma *área de trabalho do Log Analytics* na sua subscrição do Azure. Uma área de trabalho é essencialmente um contentor que inclui informações da conta e informações de configuração simples para a conta. Para obter mais informações, consulte [gerir áreas de trabalho](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json).



## <a name="prerequisites"></a>Pré-requisitos

Antes de começar este tutorial, certifique-se de que tem os seguintes pré-requisitos:  

- Uma subscrição do Azure Active Directory, com **administrador de empresa** permissões  

- Versão 1810 com o update rollup 4486457 ou posterior, com o Configuration Manager, **administrador total** função  

- Pelo menos um dispositivo de Windows 10 com as seguintes configurações:  

    - Windows 10, versão 1709 ou posterior

    - A atualização de qualidade cumulativa mais recente do Windows 10  

    - Configuration Manager versão de cliente 1810 com update rollup 4486457 ou posterior  

    - Uma versão do Windows baseados no instalador do Office, como o Office 2013  

- Aprovação de negócios para configurar o nível de dados de diagnóstico do Windows para **avançado (limitado)** nos dispositivos pilotos  

    Para obter mais informações, consulte [privacidade de análise de ambiente de trabalho](/sccm/desktop-analytics/privacy).

- Conectividade de rede do dispositivo para os seguintes pontos finais da internet:

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://www.msftncsi.com`  
    - `https://www.msftconnecttest.com`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://nexusrules.officeapps.live.com`  
    - `https://nexus.officeapps.live.com`  
    - `https://office.pipe.aria.microsoft.com`  
    - `https://graph.windows.net` (na apenas a função de servidor do Configuration Manager)
    - `https://fef.msua06.manage.microsoft.com` (na apenas a função de servidor do Configuration Manager)

    Para obter mais informações, consulte [como ativar a partilha para a área de trabalho de análise de dados](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

> [!Important]  
> Estes pré-requisitos são para os fins deste tutorial. Para obter mais informações sobre os pré-requisitos gerais para a análise de ambiente de trabalho com o Configuration Manager, consulte [pré-requisitos](/sccm/desktop-analytics/overview#prerequisites).  



## <a name="set-up-desktop-analytics"></a>Configurar a Análise de Computadores

Utilize este procedimento para iniciar sessão no ambiente de trabalho de análise e configurá-lo na sua subscrição. Este procedimento é um processo de uso individual para configurar a análise de ambiente de trabalho para a sua organização.  

1. Abra o portal da análise de ambiente de trabalho na gestão de dispositivos do Microsoft 365 como um utilizador com **administrador de empresa** permissões. Selecione **iniciar**.  

2. Sobre o **aceitar o contrato de serviço** página, verifique o contrato de serviço e selecione **Accept**.  

3. Sobre o **confirmar a sua subscrição** página, a lista de licenças elegíveis necessárias são para funcionalidades de estado de funcionamento do dispositivo de Windows de análise de ambiente de trabalho. Selecione **seguinte** para continuar.  

4. Sobre o **conceder aos utilizadores acesso** página, análise de ambiente de trabalho previamente configura dois grupos de segurança no Azure Active Directory:  

    - **Os proprietários de área de trabalho**: Criar e gerir áreas de trabalho. Estas contas precisam de acesso de proprietário à subscrição do Azure.  

    - **Os contribuintes da área de trabalho**: Criar e gerir planos de implantação nesta área de trabalho. Não precisam de acesso do Azure adicional.  
  
   Para adicionar um utilizador a qualquer grupo, escreva o nome ou endereço de email no **introduza o nome ou endereço de e-mail** secção do grupo adequado. Quando terminar, selecione **seguinte**. 

5. Na página para **configurar a sua área de trabalho**:  

    - Para utilizar uma área de trabalho existente para a análise de ambiente de trabalho, selecione-a e continuar com a próxima etapa.  

    - Para criar uma área de trabalho para análise de ambiente de trabalho, selecione **adicionar área de trabalho**.  

        1. Introduza um **nome da área de trabalho**.  

        2. Selecione a lista pendente para **selecione o nome de subscrição do Azure para esta área de trabalho**e escolha a subscrição do Azure para esta área de trabalho.  

        3. Selecione o **região** na lista e, em seguida, selecione **Add**.  

6. Selecione uma área de trabalho nova ou existente e, em seguida, selecione **definido como área de trabalho de análise de ambiente de trabalho**.  Em seguida, selecione **continuar** no **confirmar e conceder acesso** caixa de diálogo.  

7. No separador do browser nova, escolha uma conta a utilizar para iniciar sessão. Selecione a opção para **consentir em nome da sua organização** e selecione **Accept**.  

8. Na página para **configurar a sua área de trabalho**, selecione **próxima**.  

9. Sobre o **últimos passos** página, selecione **aceda à área de trabalho de análise**. O portal do Azure mostra a área de trabalho de análise **home page** página.  


### <a name="create-an-app-in-azure-ad-for-configuration-manager"></a>Criar uma aplicação no Azure AD para o Configuration Manager  

1. Na [portal do Azure](https://portal.azure.com), aceda à **Azure Active Directory**e selecione **registos das aplicações**. Em seguida, selecione **novo registo de aplicação**.  

2. Na **criar** painel, configure as seguintes definições:  

    - **Nome**: um nome exclusivo que identifica a aplicação, por exemplo: `Desktop-Analytics-Connection`  

    - **Tipo de aplicação**: **Aplicação Web / API**  

    - **Início de sessão no URL**: este valor não é utilizado pelo Configuration Manager, mas necessários pelo Azure AD. Introduza um URL exclusivo e válido, por exemplo: `https://configmgrapp`  
  
    Selecione **Criar**.  

3. Selecione a aplicação e tome nota da **ID da aplicação**. Este valor é um GUID que é utilizado para configurar a ligação do Configuration Manager.  

4. Selecione **configurações** na aplicação e, em seguida, selecione **chaves**. Na **palavras-passe** , digite um **descrição da chave**, especifique uma vencimento **duração**e, em seguida, selecione **guardar**. Copiar o **valor** da chave, que é utilizada para configurar a ligação do Configuration Manager. 

    > [!Important]  
    > Esta é a oportunidade única para copiar o valor da chave. Se não copiá-lo agora, terá de criar outra chave.  
    > 
    > Guarde o valor da chave numa localização segura.  

5. Na aplicação **configurações** painel, selecione **permissões obrigatórias**.  

    1. Sobre o **permissões obrigatórias** painel, selecione **Add**.  

    2. Na **adicionar acesso à API** painel, **selecionar uma API**.  

    3. Procure o **Microsserviço do Configuration Manager** API. Selecione-o e, em seguida, escolha **selecione**.  

    4. Sobre o **ativar o acesso ao** painel, selecione ambas as permissões de aplicação: **Escrever dados de coleta do CM** e **ler os dados de coleção do CM**. Em seguida, escolha **selecione**.  

    5. Sobre o **adicionar acesso à API** painel, selecione **feito**.  

6. Sobre o **permissões obrigatórias** página, selecione **conceder permissões**. Selecione **Sim**.  

7. Copie o ID de inquilino do Azure AD. Este valor é um GUID que é utilizado para configurar a ligação do Configuration Manager. Selecione **do Azure Active Directory** no menu principal e, em seguida, selecione **propriedades**. Copiar o **ID de diretório** valor.  



## <a name="connect-configuration-manager"></a>Ligar o Configuration Manager

Utilize este procedimento para atualizar o Configuration Manager, ligar à análise de ambiente de trabalho e configurar as definições do dispositivo. Este procedimento é um processo único para anexar a hierarquia para o serviço em nuvem.  


### <a name="update-configuration-manager"></a>Atualizar o Configuration Manager

Instale o Configuration Manager versão 1810 update rollup (4486457) para suportar a integração com a análise de ambiente de trabalho. Para obter mais informações sobre esta atualização, consulte [Update rollup para o ramo atual do Configuration Manager, versão 1810](https://support.microsoft.com/help/4486457).

1. Atualize o site com o update rollup para a versão 1810. Para obter mais informações, consulte [instalar atualizações na consola](/sccm/core/servers/manage/install-in-console-updates).  

2. Atualize clientes. Para simplificar este processo, considere a utilização de atualização automática de cliente. Para obter mais informações, consulte [atualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  


### <a name="connect-to-the-service"></a>Ligar ao serviço

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **serviços Cloud**e selecione o **dos serviços do Azure** nó. Selecione **configurar os serviços do Azure** na faixa de opções.  

2. Sobre o **dos serviços do Azure** página do Assistente de serviços do Azure, configure as seguintes definições:  

    - Especifique um **nome** para o objeto no Configuration Manager  

    - Especifique um opcional **Descrição** para ajudar a identificar o serviço  

    - Selecione **Analytics de ambiente de trabalho** na lista de serviços disponíveis  
  
   Selecione **Seguinte**.  

3. Sobre o **aplicação** , selecione o adequado **ambiente do Azure**. Em seguida, selecione **importação** para a aplicação web. Configure as seguintes definições no **importar aplicações** janela:  

    - **Nome de inquilino do Azure AD**: Este nome é como ele é chamado no Configuration Manager  

    - **ID de inquilino do Azure AD**: O **ID de diretório** que copiou do Azure AD   

    - **ID de cliente**: O **ID da aplicação** que copiou a partir da aplicação do Azure AD   

    - **Chave secreta**: A chave **valor** que copiou a partir da aplicação do Azure AD   

    - **Expiração da chave secreta**: A mesma data de expiração da chave   

    - **URI de ID de aplicação**: Esta definição deve preencher automaticamente com o seguinte valor: `https://cmmicrosvc.manage.microsoft.com/`  
  
   Selecione **Verifique se**e, em seguida, selecione **OK** para fechar a janela de aplicações de importação. Selecione **seguinte** na página da aplicação do Assistente de serviços do Azure.  

4. Sobre o **dados de diagnóstico** página, configure as seguintes definições:  

    - **ID comercial**: este valor deve preencher automaticamente com o ID da sua organização  

    - **Nível de dados de diagnóstico do Windows 10**: selecione, pelo menos, **avançado (limitado)**  

    - **Permite que o nome de dispositivo em dados de diagnóstico**: selecione **ativar**  
  
   Selecione **Seguinte**. O **funcionalidade disponível** página mostra a funcionalidade de análise de ambiente de trabalho que está disponível com as definições de dados de diagnóstico da página anterior. Selecione **Seguinte**.  

5. Sobre o **coleções** página, configure as seguintes definições:  

    - **Nome a apresentar**: O portal de análise de ambiente de trabalho apresenta esta ligação do Configuration Manager com este nome. Usá-lo para diferenciar entre hierarquias diferentes. Por exemplo, *laboratório de teste* ou *produção*.  

    - **Coleção de destino**: Esta coleção inclui todos os dispositivos que configura o Configuration Manager com o seu ID comercial e as definições de dados de diagnóstico. É o conjunto completo de dispositivos do Configuration Manager liga-se para o serviço de análise de ambiente de trabalho.  

    - **Os dispositivos da coleção de destino utilizar um proxy de usuário autenticado para comunicações de saída**: Por predefinição, este valor é **não**. Se for necessário no seu ambiente, definido como **Sim**.   

    - **Selecione as coleções específicas para sincronizar com a análise de ambiente de trabalho**: Selecione **adicionar** para incluir coleções adicionais. Essas coleções estão disponíveis no portal do Analytics de ambiente de trabalho para o agrupamento com planos de implantação. Certifique-se incluir coleções de exclusão de piloto e piloto.  

        Essas coleções continuam a sincronizar como as alterações de associação. Por exemplo, o seu plano de implementação utiliza uma coleção com uma regra de associação do Windows 7. À medida que esses dispositivos atualizar para o Windows 10 e do Configuration Manager avalia a associação à coleção, esses dispositivos soltem fora de coleta e ao plano de implantação.  

6. Conclua o assistente.  

O Configuration Manager cria uma política de definições para configurar os dispositivos da coleção de destino. Esta política inclui as definições de dados de diagnóstico para permitir que os dispositivos enviar dados à Microsoft. Por predefinição, clientes de atualização de política de cada hora. Depois de receber as novas definições, pode ser mais de várias horas antes dos dados estão disponíveis no ambiente de trabalho de análise.

Monitorize a configuração dos seus dispositivos para análise de ambiente de trabalho. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda o **manutenção do Microsoft 365** nó e selecione o **estado de funcionamento da ligação** dashboard.  

O Configuration Manager sincroniza os planos de implementação de análise de ambiente de trabalho em menos de 15 minutos a criar a ligação. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda o **manutenção do Microsoft 365** nó e selecione o **planos de implantação** nó. 



## <a name="create-a-desktop-analytics-deployment-plan"></a>Criar um plano de implantação de área de trabalho de análise

Utilize este procedimento para criar um plano de implantação no ambiente de trabalho de análise.

1. Abra o [do portal da análise de ambiente de trabalho](https://aka.ms/m365aprod). Utilize as credenciais que têm, pelo menos, **contribuidores de área de trabalho** permissões.  

2. Selecione **planos de implantação** no grupo gerenciar.  

3. Na **planos de implementação** painel, selecione **criar**.  

4. Na **criar plano de implantação** painel, configure as seguintes definições:  

    - **Nome**: Planear um nome exclusivo para a implementação, por exemplo `Office 365 pilot`  

    - **Produtos e versões**: Selecione o **Office** produto e a versão mais recente disponível recomendada. Por exemplo, **clientes do Office 365, versão 1808 (recomendado)**.  

    - **Grupos de dispositivos**: Selecione um ou mais grupos e, em seguida, selecione **definido como grupos de destino**. Grupos com **sccm** como a origem são coleções sincronizadas a partir do Configuration Manager.  

    - **Regras de preparação**: Estas regras ajudam a determinar quais os dispositivos que está qualificado para atualização. Selecione **aplicações do Office** e configure as seguintes definições:  

        - Atualização do Office 365 ProPlus de 32 bits para 64 bits. Esta definição só se aplica a dispositivos que executam uma versão de 64 bits do Windows. A predefinição é **Sim**.  

        - Ao atualizar a partir de uma versão mais antiga do Office, deixe mais antigo preterido aplicações do Office. Este comportamento aplica-se mesmo que essas aplicações não existem na versão mais recente do Office. A predefinição é **não**.  

        - Baixa instalar o limiar de contagem de seus suplementos Office. O limiar predefinido é `2%`. Suplementos abaixo deste limiar são definidos automaticamente como *baixa instalar contagem*. Análise de área de trabalho não será validado esses suplementos durante o piloto. 

            Se estiver instalado um suplemento numa porcentagem maior de computadores a este limiar, o plano de implantação marca o suplemento como *Noteworthy*. Em seguida, pode decidir sua importância para testar durante a fase piloto.   

    - **Data de conclusão**: Escolha a data através do qual Office deve ser totalmente implementado em todos os dispositivos visados.  

5. Selecione **Criar**. O novo plano é apresentada na lista de planos de implantação ao seu a ser processado. Processamento pode demorar até 48 horas antes de poder prosseguir para o passo seguinte.  

6. Abra o plano de implantação, selecionando o seu nome.  

7. No menu de plano de implementação, na **Prepare** grupo, selecione **identificar importância**.  

    1. Sobre o **suplementos do Office** separador, selecione para mostrar apenas **não revisto** ativos.  

    2. Selecione cada suplemento e, em seguida, selecione **editar**. Pode selecionar mais do que uma aplicação para editar ao mesmo tempo.   

    3. Escolha um nível de importância do **importância** lista. Se pretender que o ambiente de trabalho de análise para validar o suplemento durante o piloto, selecione **crítico** ou **importante**. Ele não será validado suplementos marcados como **não importante**. Considere o risco de compatibilidade e outras informações de plano ao atribuir níveis de importância.  

        Ao atribuir níveis de importância, também pode escolher o decisão de atualização.  

    4. Selecione **guardar** quando terminar.  

8. No menu de plano de implementação, na **Prepare** grupo, selecione **identificar piloto**.  

    1. Reveja os dispositivos recomendados para o piloto.  

    2. Selecione cada dispositivo e selecione **adicionar ao projeto-piloto**. Se discordar com a recomendação, selecione **substitua**.  

        Para obter mais informações sobre como o ambiente de trabalho de análise torna estas recomendações, selecione o ícone de informações no canto superior direito do **identificar piloto** painel.



## <a name="deploy-office-365-in-configuration-manager"></a>Implementar o Office 365 no Configuration Manager

Utilize este procedimento para implementar o Office 365 ProPlus no Configuration Manager no grupo piloto.

- Se ainda não tiver um, primeiro [criar uma aplicação do Office 365 ProPlus](#bkmk_create-app)  

- [Implementar a aplicação](#bkmk_deploy-app) com o plano de implantação de área de trabalho de análise  

- [Instalar a aplicação](#bkmk_install-app) do Centro de Software num dispositivo de destino  

<!-- 
- [Monitor](#bkmk_monitor-app) status in Configuration Manager  
 -->

### <a name="bkmk_create-app"></a> Criar uma aplicação para o Office 365 ProPlus

1. Na consola do Configuration Manager, vá para o **biblioteca de Software**e selecione o **gestão de clientes do Office 365** nó. Selecione o **Office 365 instalador** mosaico no dashboard.  

2. Sobre o **as configurações do aplicativo** , indique um **nome** para esta aplicação. Por exemplo, `Office 365 ProPlus`. Opcionalmente, especifique um **Descrição**. Especifique a **localização do conteúdo** para os ficheiros de instalação e, em seguida, selecione **próxima**.  

3. Sobre o **as configurações do Office** página, selecione **vá para a ferramenta de personalização do Office**. Configure as definições de implementação necessários para a sua instalação do Office 365:  

    1. Na **produtos e versões** grupo, selecione **Office 365 ProPlus** da lista e selecione **Add**.  

    2. Na **linguagem** de grupo, selecione o idioma principal.  

    3. Na **atualização e de atualização** de grupo, certifique-se a definição para **desinstala qualquer versão MSI do Office, incluindo o Visio e o projeto** é **no**.  

    4. Configure outras definições conforme necessário pela sua organização.  

    5. Quando terminar, selecione **revisão** no canto superior direito. Reveja as definições configuradas e, em seguida, selecione **submeter**.  

5. Selecione **Seguinte**. Sobre o **implantação** página, selecione **não** implantá-lo agora. (O procedimento seguinte utiliza o plano de implantação de área de trabalho de análise para a implementação.) Selecione **seguinte** e conclua o assistente.  


### <a name="bkmk_deploy-app"></a> Implementar o Office 365 com o plano de implantação de área de trabalho de análise

1. Na consola do Configuration Manager, vá para o **biblioteca de Software**, expanda **manutenção de análise de ambiente de trabalho**e selecione o **planos de implantação** nó.  

2. Selecione o seu plano de implantação piloto do Office 365 e, em seguida, selecione **detalhes do plano de implementação** na faixa de opções.  

3. Na **criar um piloto do estado** mosaico, escolha **aplicativo** na lista pendente e, em seguida, selecione **implementar**.  

4. No **gerais** página do Assistente de implementação Software, selecione **procurar** junto a **Software** campo. Selecione a sua aplicação do Office 365, por exemplo, **Office 365 ProPlus**. Com a integração de análises de ambiente de trabalho, o Configuration Manager cria automaticamente uma coleção para o plano de implantação piloto. Selecione **Seguinte**.  

5. Sobre o **conteúdo** página, selecione **Add**e, em seguida, selecione **ponto de distribuição**. Selecione um ponto de distribuição disponíveis para alojar o conteúdo de instalação e selecione **OK**. Em seguida, selecione **seguinte**.  

6. Sobre o **definições de implementação** página, selecione **próxima** para aceitar as predefinições. (Uma instalação disponível).  

7. Sobre o **agendamento** página, selecione **próxima** para aceitar as predefinições. (Disponível logo que possível.)  

8. Sobre o **experiência de utilizador** página, selecione **próxima** para aceitar as predefinições. (A apresentar no Centro de Software e apenas mostrar as notificações de reinícios de computador).  

9. Sobre o **alertas** página, selecione **próxima** para aceitar as predefinições.  

10. Conclua o assistente.  


### <a name="bkmk_install-app"></a> Instalar o Office 365 a partir do Centro de Software

1. Inicie sessão para um dispositivo que seja membro do plano de implantação piloto.  

2. Open **Centro de Software** e instalar a aplicação disponível para o Office 365.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->




## <a name="next-steps"></a>Passos seguintes

Avance para o artigo seguinte para saber mais sobre os planos de implantação de área de trabalho de análise.
> [!div class="nextstepaction"]  
> [Planos de implantação](/sccm/desktop-analytics/deployment-plans)  

