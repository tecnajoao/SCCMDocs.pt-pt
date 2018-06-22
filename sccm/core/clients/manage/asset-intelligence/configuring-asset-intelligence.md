---
title: Configurar o Asset Intelligence
titleSuffix: Configuration Manager
description: Configure o Asset Intelligence no System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 182006f0e4fcaf2304570ef4110527a61180c290
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32341020"
---
# <a name="configure-asset-intelligence-in-system-center-configuration-manager"></a>Configurar o Asset Intelligence no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Asset Intelligence fará um inventário dos e gere a utilização de licenças de software.   

## <a name="steps-to-configure-asset-intelligence"></a>Passos para configurar o Asset Intelligence  
   

- **Passo 1**: para recolher os dados de inventário necessários para relatórios do Asset Intelligence, tem de ativar o agente de cliente de inventário de hardware, tal como descrito no [como expandir o inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).
- **Passo 2**: [Ativar inventário de Hardware do Asset Intelligence Classes de relatório](#BKMK_EnableAssetIntelligence).  
- **Passo 3**: [Instalar um ponto de sincronização do Asset Intelligence](#BKMK_InstallAssetIntelligenceSynchronizationPoint)
- **Passo 4**: [Ativar a auditoria de eventos de início de sessão bem-sucedidos](#BKMK_EnableSuccessLogonEvents)  
- **Passo 5**: [Importar informações de licença de Software](#BKMK_ImportSoftwareLicenseInformation)  
- **Passo 6**: [Configurar tarefas de manutenção do Asset Intelligence](#BKMK_ConfigureMaintenanceTasks) 


###  <a name="BKMK_EnableAssetIntelligence"></a> Enable Asset Intelligence hardware inventory reporting classes  
 Para ativar o Asset Intelligence em sites do Configuration Manager, tem de ativar uma ou mais Asset Intelligence inventário de hardware classes de relatório. Pode ativar as classes na home page do **Asset Intelligence** ou, na área de trabalho **Administração** , no nó **Definições do Cliente** , nas propriedades de definições de cliente. Utilize um dos seguintes procedimentos.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>Para ativar classes de relatório de inventário de hardware do Asset Intelligence a partir da home page do Asset Intelligence  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **do Asset Intelligence**.  

3.  No **home page** separador o **do Asset Intelligence** grupo, escolha **editar Classes de inventário**.   

4.  Para ativar os relatórios do Asset Intelligence, selecione **ativar todos os relatório do Asset Intelligence classes** ou **ativar apenas do Asset Intelligence selecionadas classes de relatório**e selecione, pelo menos, uma classe de relatório a partir das classes apresentadas.  

    > [!NOTE]  
    >  Os relatórios do Asset Intelligence que dependem das classes de inventário de hardware que ativar através deste procedimento não apresentam dados até que os clientes tenham analisado e devolvido o inventário de hardware.  


##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>Para ativar classes de relatório de inventário de hardware do Asset Intelligence a partir das propriedades de definições de cliente  

1.  Na consola do Configuration Manager, escolha **administração** >  **as definições de cliente** > **agente predefinições de cliente**. Se tiver criado o cliente personalizado a definições, pode selecionar os em vez disso.  

3.  No **home page** separador > **propriedades** grupo, escolha **propriedades**.   

4.  Escolha **inventário de Hardware** > **definir Classes**. .  

5.  Escolha **filtrar por categoria** > **Classes de relatório do Asset Intelligence**. A lista de classes é atualizada apenas com as classes de relatório de inventário de hardware do Asset Intelligence.  

6.  Selecione pelo menos uma classe de relatório da lista.  

    > [!NOTE]  
    >  Os relatórios do Asset Intelligence que dependem das classes de inventário de hardware que ativar através deste procedimento não apresentam dados até que os clientes tenham analisado e devolvido o inventário de hardware.  
  

###  <a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Install an Asset Intelligence Synchronization Point  

A função de sistema de sites do ponto de sincronização do Asset Intelligence é utilizada para ligar a sites do Configuration Manager para o System Center Online para sincronizar informações de catálogo do Asset Intelligence. O ponto de sincronização do Asset Intelligence só pode ser instalado num sistema de sites localizado no site de nível superior da hierarquia do Configuration Manager e requer acesso à Internet para sincronizar com o System Center Online utilizando a porta TCP 443.

Para além de transferir novas informações do catálogo do Asset Intelligence, o ponto de sincronização do Asset Intelligence pode carregar informações personalizadas de títulos de software para o System Center Online para categorização. A Microsoft trata todos os títulos de software carregados como informações públicas. Certifique-se de que os títulos de software personalizados não contêm informações confidenciais ou proprietárias. Para obter mais informações sobre o pedido de categorização de títulos de software, consulte [pedir uma atualização de catálogo para títulos de software não categorizados](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate).  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>Para instalar uma função de sistema de sites do ponto de sincronização do Asset Intelligence  

1.  Na consola do Configuration Manager, escolha **administração**> **configuração do Site** > **servidores e funções de sistema de sites**.  

3.  Adicione a função de sistema de sites do ponto de sincronização do Asset Intelligence a um servidor de sistema de sites novo ou existente:  

    -  Para um **novo servidor do sistema de sites**: No **home page** separador o **criar** grupo, escolha **criar servidor do sistema de sites** para iniciar o assistente.   

        > [!NOTE]  
        >  Por predefinição, quando uma função de sistema de sites, o Configuration Manager instala os ficheiros de instalação são instalados na primeira disponível formatada com NTFS unidade de disco rígido que tenha o máximo livre no disco rígido. Para impedir que o Configuration Manager instalar em unidades específicas, crie um ficheiro vazio com o nome No_sms_on_drive.sms e copie-o para a pasta raiz da unidade antes de instalar o servidor de sistema de sites.  

    -  Para um **servidor de sistema de sites existente**: Selecione o servidor no qual pretende instalar a função de sistema de sites do ponto de sincronização do Asset Intelligence. Ao escolher um servidor, uma lista das funções de sistema de sites que já se encontram instaladas no servidor são apresentados no painel de detalhes.  

         No **home page** separador o **servidor** grupo, escolha **Adicionar função de sistema de sites** para iniciar o assistente.  

4.  Concluir o **geral** página. Quando adiciona o ponto de sincronização do Asset Intelligence a um servidor do sistema de sites existente, verifique os valores que foram anteriormente configurados.  

5.  No **seleção da função do sistema** página, selecione **ponto de sincronização do Asset Intelligence** da lista de funções disponíveis.  

6.  No **definições de ligação do ponto de sincronização do Asset Intelligence** página, escolha **seguinte**.  

     Por predefinição, a definição **Utilizar este ponto de Sincronização do Asset Intelligence** está selecionada e não pode ser configurada nesta página. O System Center Online aceita tráfego de rede apenas através da porta TCP 443 e, por conseguinte, a definição **Número de porta SSL** não pode ser configurada nesta página do assistente.  

7.  Opcionalmente, pode especificar um caminho para o ficheiro de certificado (. pfx) de autenticação System Center Online. Normalmente, não é necessário especificar um caminho para o certificado porque o certificado de ligação é automaticamente aprovisionado durante a instalação da função de site.  

8.  No **definições do servidor Proxy** página, especifique se o ponto de sincronização do Asset Intelligence irá utilizar um servidor proxy ao ligar ao System Center Online para sincronizar o catálogo e se pretende utilizar credenciais para ligar ao servidor proxy.  

    > [!WARNING]  
    >  Se for necessário um servidor proxy para ligar ao System Center Online, o certificado de ligação também pode ser eliminado se a palavra-passe da conta de utilizador expirar para a conta configurada para autenticação do servidor proxy.  

9. Na página **Agendamento da Sincronização** , especifique se pretende sincronizar catálogo do Asset Intelligence com base num agendamento. Quando ativar o agendamento da sincronização, especifique um agendamento de sincronização simples ou personalizado. Durante a sincronização agendada, o ponto de sincronização do Asset Intelligence liga ao System Center Online para obter o catálogo do Asset Intelligence mais recente. Pode sincronizar manualmente o catálogo do Asset Intelligence a partir do nó Asset Intelligence na consola do Configuration Manager. Para obter os passos sincronizar manualmente o catálogo do Asset Intelligence, consulte o [para sincronizar manualmente o catálogo do Asset Intelligence](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog) secção o [operações do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).  

10. Concluir o assistente 

###  <a name="BKMK_EnableSuccessLogonEvents"></a> Enable auditing of success logon events  
 Quatro relatórios do Asset Intelligence apresentam informações recolhidas a partir de registos de eventos de Segurança do Windows nos computadores cliente. Eis como configurar definições do início de sessão de política de segurança do computador para ativar a auditoria de eventos de início de sessão bem-sucedidos.  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>Para ativar o registo de eventos de início de sessão bem-sucedidos através de uma política de segurança local  

1.  Num computador cliente do Configuration Manager, escolha **iniciar** > **ferramentas administrativas** > **política de segurança Local**.  

2.  No **política de segurança Local** caixa de diálogo em **definições de segurança**, expanda **políticas locais**e, em seguida, escolha **política de auditoria**.  

3.  No painel de resultados, faça duplo clique **auditar eventos de início de sessão**, certifique-se de que o **êxito** caixa de verificação está selecionada e, em seguida, escolha **OK**.  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>Para ativar o registo de eventos de início de sessão bem-sucedidos através de uma política de segurança do domínio do Active Directory  

1.  Num computador de controlador de domínio, escolha **iniciar**, aponte para **ferramentas administrativas**e, em seguida, escolha **política de segurança do domínio**.  

2.  No **política de segurança Local** caixa de diálogo em **definições de segurança**, expanda **políticas locais**e, em seguida, escolha **política de auditoria**.  

3.  No painel de resultados, faça duplo clique **auditar eventos de início de sessão**, certifique-se de que o **êxito** caixa de verificação está selecionada e, em seguida, escolha **OK**.  

###  <a name="BKMK_ImportSoftwareLicenseInformation"></a> Import software license information  
 As secções seguintes descrevem os procedimentos necessários para importar Microsoft e informações de licenciamento de software geral para a base de dados do site do Configuration Manager, utilizando o Assistente para importar licenças de Software. Ao importar informações de licenças de software para a base de dados do site a partir de ficheiros de declaração de licença, a conta do computador do servidor de site requer permissões de **Controlo Total** do sistema de ficheiros NTFS para a partilha de ficheiros utilizada para importar informações de licença de software.  

> [!IMPORTANT]  
>  Quando as informações de licença de software são importadas para a base de dados do site, as informações de licença de software existentes são substituídas. Certifique-se de que o ficheiro de informações de licença de software que utiliza com o Assistente Importar Licenças de Software contém uma lista completa de todas as informações de licença de software necessárias.  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>Para importar informações de licença de software para o catálogo do Asset Intelligence  

1.  No **ativos e compatibilidade** área de trabalho, escolha **do Asset Intelligence**.  

2.  No **home page** separador o **do Asset Intelligence** grupo, escolha **importar licenças de Software**.   

4.  Na página **Importar** , especifique se está a importar um ficheiro de Licenciamento em Volume da Microsoft (MVLS) (.xml ou .csv) ou um ficheiro de Declaração de Licença Geral (.csv). Para obter mais informações sobre a criação de um ficheiro de Declaração de Licença Geral, consulte [Criar um ficheiro de informações de declaração de licença geral para importação](#BKMK_CreateGeneralLicenseStatement) mais à frente neste tópico.  

    > [!WARNING]  
    >  Para transferir um ficheiro MVLS no formato .csv, que pode importar para o catálogo do Asset Intelligence, consulte [Microsoft Volume Licensing Service Center](http://go.microsoft.com/fwlink/p/?LinkId=226547). Para aceder a estas informações, tem de ter uma conta registada no site. Tem de contactar o seu representante de conta Microsoft para obter informações sobre como obter o seu ficheiro MVLS no formato .xml.  

5.  Introduza o caminho UNC para o ficheiro de declaração de licença ou escolha **procurar** selecionar uma rede partilhada ficheiros e pastas.  

    > [!NOTE]  
    >  A pasta partilhada deve estar corretamente protegida para impedir o acesso não autorizado ao ficheiro de informações de licenciamento e a conta de computador do computador no qual o assistente está a ser executado tem de ter permissões de Controlo Total para a partilha que contém o ficheiro de importação de licença.  

6. Conclua o assistente.  

###  <a name="BKMK_CreateGeneralLicenseStatement"></a>Criar um ficheiro de informações de declaração de licença geral para importação  
 Também é possível importar uma declaração de licença geral para o catálogo do Asset Intelligence, utilizando um ficheiro de importação de licença criado manualmente no formato de ficheiro delimitado por vírgulas (.csv).  

> [!NOTE]  
>  Embora apenas os campos **Nome**, **Fabricante**, **Versão**, e **QuantidadeEfetiva** tenham de conter dados, todos os campos têm de ser introduzidos na primeira linha do ficheiro de importação de licença. Todos os campos de data devem ser apresentados no seguinte formato: Mês/dia/ano, por exemplo, 08/04/2008.  

O Asset Intelligence faz corresponder os produtos que especificar na declaração de licença geral, utilizando o nome do produto e a versão do produto, mas não o nome do fabricante. Tem de utilizar um nome de produto na declaração de licença geral que seja uma correspondência exata com o nome de produto armazenado na base de dados do site. Asset Intelligence demora a **Quantidadeefetiva** número fornecido na declaração de licença geral e compara o número com o número de produtos instalados encontrado no inventário do Configuration Manager.  

> [!TIP]  
>  Para obter uma lista completa dos nomes de produtos armazenados na base de dados do site do Configuration Manager, pode executar a consulta seguinte na base de dados do site: SELECT ProductName0 FROM v_GS_INSTALLED_SOFTWARE.  

 Pode especificar as versões exatas de um produto ou especificar parte da versão, como, por exemplo, apenas a versão principal. Os exemplos seguintes fornecem as correspondências de versão resultantes para uma entrada de versão de declaração de licença geral para um produto específico.  

|Entrada de declaração de licença geral|Entradas da base de dados do site correspondentes|  
|-------------------------------------|------------------------------------|  
|Nome: "MySoftware", ProductVersion0: "2"|ProductName0: "Mysoftware", ProductVersion0: "2.01.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.02.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.3579.000"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.10.1234"|  
|Nome: "MySoftware", versão "2.05"|ProductName0: "MySoftware", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "MySoftware", ProductVersion0: "2.05.3579.000"|  
|Nome: "Mysoftware", versão "2"<br /><br /> Nome: "Mysoftware", versão "2.05"|Erro durante a importação. A importação falha quando mais do que uma entrada corresponde à mesma versão de produto.|  
  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>Para criar um ficheiro de importação de declaração de licença geral utilizando o Microsoft Excel  

1.  Abra o Microsoft Excel e crie uma nova folha de cálculo.  

2.  Na primeira linha da nova folha de cálculo, introduza todos os nomes de campos de dados de licença de software.  

3.  Na segunda e subsequentes linhas da nova folha de cálculo, introduza as informações de licença de software conforme necessário. Certifique-se de que, pelo menos, todos os campos de dados de licença de software necessários são introduzidos nas linhas subsequentes para cada licença de software a importar. O nome do título de software introduzido na folha de cálculo tem de ser igual ao título de software que é apresentado no Explorador de Recursos para um computador cliente após a execução do inventário de hardware.  

4.  Guarde o ficheiro no formato. csv.  

5.  Copie o ficheiro .csv para a partilha de ficheiros que é utilizada para importar informações de licença de software para o catálogo do Asset Intelligence.  

6.  Na consola do Configuration Manager, utilize o Assistente para importar licenças de Software para importar o ficheiro. csv recentemente criado.  

7.  Execute o Asset Intelligence **licença 15A - relatório de reconciliação de Software de terceiros** para verificar que as informações de licenciamento foi importadas com êxito para o catálogo do Asset Intelligence.  

> [!NOTE]  
>  Para obter um exemplo de um ficheiro de licença de software geral que pode utilizar para fins de teste, consulte [ficheiro de importação de licença geral de exemplo Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md).  

#### <a name="sample-table-to-describe-software-licenses"></a>Tabela de exemplo para descrever as licenças de software  
 Ao criar um ficheiro de importação de declaração de licença geral, as informações na tabela seguinte podem ser utilizadas para descrever as licenças de software a importar para o catálogo do Asset Intelligence.  

|Nome da coluna|Tipo de dados|Necessário|Exemplo|  
|-----------------|---------------|--------------|-------------|  
|Nome|Até 255 carateres|Sim|Título de software|  
|Fabricante|Até 255 carateres|Sim|Fabricante de software|  
|Versão|Até 255 carateres|Sim|Versão do título de software|  
|Linguagem|Até 255 carateres|Sim|Idioma do título de software|  
|QuantidadeEfetiva|Valor inteiro|Sim|Número de licenças adquiridas|  
|NúmeroDePO|Até 255 carateres|Não|Informações de nota de encomenda|  
|NomeDoRevendedor|Até 255 carateres|Não|Informações do revendedor|  
|DataDeCompra|Valor de data no seguinte formato: MM/DD/AAAA|Não|Data de compra da licença|  
|SuporteAdquirido|Valor de bits|Não|0 ou 1: Introduza 0 para Sim ou 1 para não|  
|DataDeExpiraçãoDoSuporte|Valor de data no seguinte formato: MM/DD/AAAA|Não|Data de fim do suporte adquirido|  
|Comentários|Até 255 carateres|Não|Comentários opcionais|  

###  <a name="BKMK_ConfigureMaintenanceTasks"></a> Configure Asset Intelligence maintenance tasks  
 As seguintes tarefas de manutenção estão disponíveis para o Asset Intelligence:  

-   **Verificar o título da aplicação nas informações de inventário**: Verifica se o título de software comunicado no inventário de software é reconciliado com o título de software no catálogo do Asset Intelligence. Por predefinição, esta tarefa é ativada e agendada para ser executada no Sábado após as 00:00 e antes das 5:00. Esta tarefa de manutenção só está disponível no site de nível superior na hierarquia do Configuration Manager.  

-   **Resumir dados de Software instalado**: Fornece as informações que são apresentadas no **ativos e compatibilidade** área de trabalho, no **Software inventariado** nó, no **do Asset Intelligence** nó. Quando a tarefa é executada, o Configuration Manager recolhe uma contagem de todos os títulos de software inventariados no site primário. Por predefinição, esta tarefa é ativada e agendada para ser executada diariamente após as 00:00 e antes das 5:00. Esta tarefa de manutenção está disponível apenas em sites primários.  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>Para configurar tarefas de manutenção do Asset Intelligence  

1.  Na consola do Configuration Manager, escolha **administração** > **configuração do Site** > **Sites**.  

3.  Selecione o site no qual pretende configurar a tarefa de manutenção do Asset Intelligence.  

4.  No **home page** separador o **definições** grupo, escolha **manutenção do Site**. Selecione uma tarefa e escolha **editar** para modificar as definições. 

    Recomendamos que defina o período de tempo para o horário de pico do site. O período de tempo corresponde ao intervalo de tempo em que a tarefa pode ser executada. É definido pelos campos **Iniciar após** e **Última hora de início** especificados na caixa de diálogo **Propriedades da Tarefa** .  

    Pode iniciar a tarefa de imediato, selecionando o dia atual e definindo a hora em **Iniciar após** para alguns minutos após a hora presente.  

7.  Escolha **OK** para guardar as definições. A tarefa é agora executada de acordo com o respetivo agendamento.  

    > [!NOTE]  
    >  Se não for possível executar na primeira tentativa de uma tarefa, o Configuration Manager tenta executar novamente a tarefa até que a tarefa é executada com êxito ou até ter passado o período de tempo no qual pode executar a tarefa.  
