---
title: Criar e implementar uma política de conformidade do dispositivo
titleSuffix: Configuration Manager
description: Saiba como criar e implementar políticas de conformidade no Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 0fd76043-d7ee-423d-8c5f-aa7e9ed58ce0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b0179de8cc96f885236178c70b7e834672ee1d5b
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898584"
---
# <a name="create-and-deploy-a-device-compliance-policy"></a>Criar e implementar uma política de conformidade do dispositivo

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


## <a name="create-a-compliance-policy"></a>Criar uma política de conformidade

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade**.  

2. Na **ativos e compatibilidade** área de trabalho, expanda **definições de compatibilidade**e, em seguida, escolha **políticas de conformidade**.  

3. Sobre o **home page** separador a **criar** de grupo, escolha **criar política de conformidade**.  

4. Sobre o **gerais** página do Assistente de política de conformidade criar, especifique as seguintes informações:  

    - **Nome**: Introduza um nome exclusivo para a política de conformidade. Pode utilizar até 256 carateres.  

    - **Descrição**: Introduza uma descrição que proporcione uma descrição geral do perfil VPN e ajuda a identificá-la na consola do Configuration Manager. Pode utilizar até 256 carateres.  

    - **Tipo de política de conformidade**: Selecione o tipo de política que pretende criar, dependendo se o dispositivo é gerido pelo Configuration Manager.  
    
    Para dispositivos geridos pelo Intune, escolha a opção **Regras de conformidade de dispositivos geridos com o cliente do Configuration Manager** . Quando seleciona esta opção, também pode selecionar o tipo de plataforma que pretende que esta política se aplique.  

    - **Gravidade de incompatibilidade para relatórios** -especifique o nível de gravidade reportado se esta política de conformidade for avaliada como não conforme. Os níveis de gravidade disponíveis são:  

        - **Nenhum**: Dispositivos que não cumpram esta regra de compatibilidade não reportam uma gravidade de falha para relatórios do Configuration Manager.  

        - **Informações**: Dispositivos que não cumpram esta regra de compatibilidade comunicam uma gravidade de falha **informações** para relatórios do Configuration Manager.  

        - **Aviso**: Dispositivos que não cumpram esta regra de compatibilidade comunicam uma gravidade de falha **aviso** para relatórios do Configuration Manager.  

        - **Crítico**: Dispositivos que não cumpram esta regra de compatibilidade comunicam uma gravidade de falha **crítico** para relatórios do Configuration Manager.  

        - **Crítico com evento**: Dispositivos que não cumpram esta regra de compatibilidade comunicam uma gravidade de falha **crítico** para relatórios do Configuration Manager. O **crítica com evento** nível de gravidade é também registado como um evento do Windows no log de eventos do aplicativo.  

5. Sobre o **plataformas suportadas** página, selecione as plataformas de dispositivos que esta política de conformidade será avaliada. Também pode **Selecionar tudo** para escolher todas as plataformas de dispositivo. As plataformas suportadas são: O Windows 7, Windows 8.1 e Windows 10; Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016.  

6. Na página **Regras**, pode definir uma ou mais regras que definem a configuração que os dispositivos têm de ter para serem avaliados como em conformidade. Quando cria uma política de conformidade, algumas regras estão ativadas por predefinição, mas pode editar ou eliminar estas regras. Para obter uma lista completa de todas as regras, consulte a secção "Regras de política de conformidade" mais adiante neste artigo.  

    > [!NOTE]  
    > Em Windows PCs, Windows 8.1 de versão é reportada como 6.3. Se a regra de versão do SO estiver definida como Windows 8.1 para Windows, em seguida, o dispositivo será comunicado como não conforme mesmo que o dispositivo tiver o Windows 8.1. Certifique-se de que estiver configurando o direito *reportado* versão do Windows para as regras de SO mínimas e máxima. O número de versão tem de corresponder à versão que o **winver** comando. Windows Mobile não tem este problema; a versão é reportada como 8.1 conforme esperado.  
    > 
    > Para PCs com Windows com o Windows 10, a versão deve ser definida como **10.0** mais a número de compilação do SO a **winver** comando.  

7. Sobre o **resumo** página do assistente, reveja as definições efetuadas e, em seguida, conclua o assistente.  

    A nova política é apresentada no **políticas de conformidade** nó da **ativos e compatibilidade** área de trabalho.  


## <a name="deploy-a-compliance-policy"></a>Implementar uma política de conformidade

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade**.  

2. Na **ativos e compatibilidade** área de trabalho, expanda **definições de compatibilidade**e, em seguida, escolha **políticas de conformidade**.  

3. Na **home page** separador a **implantação** de grupo, escolha **implementar**.  

4. Na **implementar a política de conformidade** caixa de diálogo caixa, escolha **procurar** para selecionar a coleção de utilizador ao qual pretende implementar a política.  

    Além disso, pode selecionar as opções para gerar alertas quando a política não estiver em conformidade e para definir a agenda pela qual esta política será avaliada relativamente à conformidade.  

5. Quando tiver terminado, escolha **OK**.  



## <a name="monitor-the-compliance-policy"></a>Monitorizar a política de conformidade

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Para ver os resultados de compatibilidade na consola do Configuration Manager

1. Na consola do Configuration Manager, escolha **monitorização**.  

2. Na **monitorização** área de trabalho, escolha **implementações**.  

3. Na lista **Implementações** , selecione a implementação de política de conformidade cujas informações de conformidade pretende rever.  

4. Poderá rever as informações de resumo sobre a conformidade da implementação da política na página principal. Para ver informações mais detalhadas, selecione a implementação e, em seguida, no **home page** separador o **implantação** de grupo, escolha **ver o estado** para abrir o  **Estado da implementação** página.  

    O **estado de implementação** página tem os seguintes separadores:  

    - **Em conformidade**: Mostra a conformidade de política com base no número de ativos afetados. Pode escolher uma regra para criar um nó temporário sob o **usuários** ou **dispositivos** nó do **ativos e compatibilidade** área de trabalho, que contém todos os utilizadores ou dispositivos que está em conformidade com esta regra. O **detalhes do ativo** painel mostra os utilizadores ou dispositivos que estejam em conformidade com a política. Para mostrar informações adicionais, faça duplo clique num utilizador ou dispositivo na lista.  

    - **Erro**: Mostra uma lista de todos os erros de implementação da política selecionada com base no número de ativos afetados. Pode escolher uma regra para criar um nó temporário sob o **usuários** ou **dispositivos** nó do **ativos e compatibilidade** área de trabalho, que contém todos os utilizadores ou dispositivos que geraram erros com esta regra. Quando seleciona um utilizador ou dispositivo, o **detalhes do ativo** painel mostra os utilizadores ou dispositivos que um problema afeta. Para mostrar informações adicionais sobre o problema, faça duplo clique num utilizador ou dispositivo na lista.  

    - **Não compatível**: Mostra uma lista de todas as regras não compatíveis na diretiva, com base no número de ativos afetados. Pode escolher uma regra para criar um nó temporário sob o **usuários** ou **dispositivos** nó do **ativos e compatibilidade** área de trabalho, que contém todos os utilizadores ou dispositivos que não está em conformidade com esta regra. Quando seleciona um utilizador ou dispositivo, o **detalhes do ativo** painel mostra os utilizadores ou dispositivos que um problema afeta. Para mostrar mais informações sobre o problema, faça duplo clique num utilizador ou dispositivo na lista.  

    - **Desconhecido**: Mostra uma lista de todos os utilizadores e dispositivos que não comunicaram compatibilidade para a implementação da política selecionada, juntamente com o estado atual do cliente dos dispositivos.  

#### <a name="to-monitor-the-compliance-status-of-an-individual-device"></a>Para monitorizar o estado de conformidade de um dispositivo individual

1. Na consola do Configuration Manager, escolha o **ativos e compatibilidade** área de trabalho.  

2. Escolher **dispositivos**.  

3. Para ativar mais colunas, faça duplo clique das colunas. Pode adicionar as seguintes colunas:  

    > [!Note]  
    > Estas colunas não são apresentadas por predefinição.  

    - **ID de dispositivo do Azure Active Directory**: Identificador exclusivo para o dispositivo no Azure Active Directory.  

    - **Detalhes do erro de conformidade**: Detalhes da mensagem de erro quando o processo de corra mal. Se esta coluna está em branco, significa que não foram encontrados erros e o estado de conformidade foi comunicado com êxito.  

    - **Localização do erro de conformidade**: Obter mais detalhes sobre onde a conformidade falhou. Se esta coluna está em branco, significa que não foram encontrados erros e o estado de conformidade foi comunicado com êxito. Exemplos de onde o processo de compatibilidade poderá falhar:  

        - Cliente do ConfigMgr  
        - Ponto de gestão  
        - Intune  
        - Azure Active Directory  

    - **Hora de avaliação de compatibilidade**: Hora da última foi verificada a compatibilidade.  

    - **Tempo da definição de conformidade**: Hora da última a compatibilidade foi atualizada para o Azure Active Directory.  

    - **Conformidade do acesso condicional**: Se pretende ou não a máquina está em conformidade com políticas de acesso condicional.  

#### <a name="to-view-intune-compliance-policies-charts"></a>Para ver os gráficos de políticas de conformidade do Intune
1. Na consola do Configuration Manager, escolha **monitorização**. 

2. Na **monitorização** área de trabalho, aceda a **descrição geral** > **definições de compatibilidade** > **políticas de conformidade**. São apresentados os gráficos seguintes:  

    - **Conformidade do dispositivo global**: Mostra a conformidade geral dos dispositivos para todas as políticas de conformidade.  

    - **Principais motivos de não conformidade**: Mostra as principais políticas para os dispositivos que não estão em conformidades.  

3. Escolha uma secção em qualquer gráfico para desagregar para obter uma lista dos dispositivos dentro dessa categoria.  

#### <a name="to-view-a-health-attestation-report"></a>Para ver um relatório de atestado de estado de funcionamento

1. Na consola do Configuration Manager, escolha **monitorização**.  

2. Para ver um relatório de resumo do estado atual dos dispositivos por Estado de conformidade, escolha **Security**e, em seguida, escolha **atestado de estado de funcionamento**.  

3. Para ver um relatório que lista todos os dispositivos e todos os atributos de atestado de estado de funcionamento, escolha **Security**e, em seguida, escolha **atestado de estado de funcionamento**.  



## <a name="compliance-policy-rules"></a>Regras de política de conformidade

- **Exigir definições de palavra-passe em dispositivos móveis**: Pode exigir que os utilizadores introduzam uma palavra-passe antes de poderem aceder ao respetivo dispositivo.  

    **Suportado em**:  
    - Windows Phone 8+  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Exigir uma palavra-passe para desbloquear um dispositivo inativo**: Pode exigir que os utilizadores introduzam uma palavra-passe para aceder ao dispositivo que está bloqueado.  

    **Suportado em**:  
    - Windows Phone 8+  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Minutos de inatividade antes de palavra-passe é exigida**: Pode especificar o tempo de inatividade antes do utilizador ter de reintroduzir a palavra-passe. Defina o valor como uma das opções disponíveis: **1 minuto**, **5 minutos**, **15 minutos**, **30 minutos**, **1 hora**.  

    Esta regra tem de ser utilizada com **exigir uma palavra-passe para desbloquear um dispositivo inativo**. O valor definido aqui determina quando o dispositivo é considerado inativo e é bloqueado. Quando **exigir uma palavra-passe para desbloquear um dispositivo inativo** está definida como **verdadeiro**, o utilizador tem de introduzir uma palavra-passe para aceder ao dispositivo bloqueado.  

    **Suportado em**:  
    - Windows Phone 8+  
    - Windows RT/8.1  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Exigir atualizações automáticas**: Pode exigir que os dispositivos com Windows 8.1 ou posterior para instalar automaticamente atualizações, e pode especificar a classe de atualizações.  

    O valor deve ser definido como **None** para impedir a instalação automática. Defina como **recomendado** instalar automaticamente todas as atualizações recomendadas. Para instalar apenas as atualizações classificadas como importantes, defina como **importante**.  

    **Suportado em**:  
    - Windows Phone 8+  

- **Permitir palavras-passe simples**: Pode permitir que os utilizadores criem palavras-passe simples, como "1234" ou "1111". Esta definição está desativada por predefinição.  

    **Suportado em**:  
    - Windows Phone 8+  
    - iOS 6+  

- **Comprimento mínimo da palavra-passe**: Pode especificar o número mínimo de dígitos ou carateres que a senha do usuário têm de ter (6 por predefinição).  

    **Suportado em**:  
    - Windows Phone 8+  
    - Windows 8,1  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

    > [!NOTE]  
    > Para dispositivos que executam o Windows e estão protegidos com uma conta Microsoft, a política de conformidade não será avaliada corretamente se **comprimento mínimo da palavra-passe** é superior a 8 carateres ou se **número mínimo de carateres Define** é mais do que 2.  

- **Encriptação de ficheiros no dispositivo móvel**: Pode exigir que o dispositivo sejam encriptados para ligar aos recursos. Os dispositivos que executam o Windows Phone 8 são encriptados automaticamente. Os dispositivos que executam o iOS são encriptados quando configura a definição **Exigir definições de palavra-passe em dispositivos móveis**. Esta definição está ativada por predefinição.  

    **Suportado em**:  
    - Windows Phone 8+  
    - Windows 8,1  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Dispositivo não tem de ser desbloqueado por jailbreak ou ROOT**: Se ativar esta definição, desbloqueados por jailbreak (iOS) ou de dispositivos (Android) de raiz não em conformidade. Esta definição está desativada por predefinição.  

    **Suportado em**:  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Perfil de e-mail tem de ser gerido pelo Intune**: Quando define esta opção como **Sim**, o dispositivo tem de utilizar o perfil de e-mail implementado no dispositivo. O dispositivo é considerado não conforme se o perfil de e-mail não for implementado no mesmo grupo de utilizadores que o grupo de utilizadores visado pela política de conformidade.  

    Também está em conformidade se o utilizador já tiver configurado uma conta de e-mail no dispositivo que corresponda ao perfil de e-mail do Intune, que é implementado no dispositivo. Neste caso, o Intune não é possível substituir o perfil aprovisionado pelo utilizador e, portanto, não o consegue gerir. O utilizador pode colocar o dispositivo em conformidade, removendo a definição de e-mail existente, o que permite ao Intune instalar o perfil de e-mail gerido.  

    Para obter mais informações sobre perfis de e-mail, consulte [ativar o acesso a e-mail empresarial através de perfis de e-mail com o Microsoft Intune](https://docs.microsoft.com/intune/email-settings-configure). Esta definição está desativada por predefinição.  

    **Suportado em**:  
    - iOS 6+  

- **Perfil de e-mail**: Se **conta de E-Mail tem de ser gerenciada pelo Intune** é selecionado, escolha **selecione** para escolher o perfil de e-mail que os dispositivos têm de ser geridos. O perfil de e-mail tem de estar presente no dispositivo.  

    **Suportado em**:  
    - iOS 6+  

- **SO mínimo obrigatório**: Quando um dispositivo não cumpre o requisito de versão mínima do SO que especificar, é reportado como não conforme. É apresentada uma hiperligação com informações sobre como atualizar. O utilizador pode optar por atualizar o dispositivo, após o qual poderão aceder aos recursos empresariais.  

    **Suportado em**:  
    - Windows Phone 8+  
    - Windows 8,1  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Versão do SO máxima permitida**: Quando um dispositivo utiliza uma versão do SO posterior à especificada na regra, o acesso aos recursos da empresa é bloqueado e é pedido ao utilizador que contacte o administrador de TI. Até que a alterar a regra para permitir a versão do SO, este dispositivo não pode ser utilizado para aceder a recursos da empresa.  

    **Suportado em**:  
    - Windows Phone 8+  
    - Windows 8,1  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Exigir que os dispositivos sejam comunicados como bom estado de funcionamento**: Pode definir uma regra para exigir que dispositivos Windows 10 sejam comunicados como bom estado de funcionamento nas políticas de conformidade novas ou existentes. Se ativar esta definição, os dispositivos Windows 10 são avaliados através do serviço de atestado de estado de funcionamento para os seguintes pontos de dados:  

    - **O BitLocker está ativado**: Quando o BitLocker estiver ativado, o dispositivo pode proteger os dados que são armazenados na unidade contra acesso não autorizado, quando o sistema é desligado ou entra em hibernação.  

        A Encriptação de Unidade BitLocker do Windows encripta todos os dados armazenados no volume do sistema operativo Windows. O BitLocker usa o TPM para ajudar a proteger o sistema de operativo do Windows e os dados de utilizador. Ele ajuda a garantir que um computador não estiver adulterado, mesmo se for deixado autônoma, perdidos ou roubados.  

        Se o computador estiver equipado com um TPM compatível, o BitLocker utiliza o TPM para bloquear as chaves de encriptação que protegem os dados. Como resultado, as chaves não podem ser acedidas até que o TPM ter verificado o estado do computador.  

    - **Integridade do código está ativada**: Integridade do código é uma funcionalidade que valida a integridade de um ficheiro de controlador ou de sistema sempre que é carregado na memória. Integridade do código Deteta se um ficheiro de controlador ou de sistema não assinado está a ser carregado para o kernel. Também Deteta se um ficheiro de sistema foi alterado por software malicioso que está a ser executado por uma conta de utilizador com privilégios de administrador.  

    - **Arranque seguro está ativado**: Quando o arranque seguro estiver ativado, o sistema é forçado a iniciar num Estado de fábrica fidedigno. Além disso, quando o arranque seguro estiver ativado, os componentes do núcleo utilizados para iniciar a máquina tem de ter assinaturas criptográficas corretas e que sejam consideradas fidedignas pela organização que fabricou o dispositivo. O firmware UEFI verifica isto antes de permitir que a máquina seja iniciada. Se todos os ficheiros tenham sido adulterados, danificando a respetiva assinatura, o sistema não inicia.  

    - **O antimalware de início antecipado está ativado**: Esta definição aplica-se apenas a PCs. O antimalware de início antecipado (ELAM) fornece proteção para os computadores na sua rede durante o arranque e antes da inicialização de controladores de terceiros.  

        Esta regra está desativada por predefinição.  

    Para obter mais informações, consulte [CSP de atestado de estado de funcionamento](https://msdn.microsoft.com/library/dn934876.aspx).  

    **Suportado em**:  
    - Windows 10 e Windows 10 Mobile  

    > [!NOTE]  
    > Começando na versão 1802 do Gestor de configuração, o Centro de Software mostra o item de atestado de estado de funcionamento do dispositivo não estiver em conformidade com. <!--1235616-->   
    > ![Conformidade de dispositivo de atestado de estado de funcionamento do dispositivo no Centro de Software](./media/Software-Center-noncompliant.PNG)  

- **Aplicações que não podem ser instaladas no dispositivo**: Se os utilizadores instalarem uma aplicação de lista de aplicações não conformes de administrador, vai ser bloqueados quando tentarem aceder a e-mail empresarial e outros recursos da empresa que suportam o acesso condicional. Esta regra requer o nome da aplicação e o ID da aplicação ao adicionar uma aplicação à lista de não conforme definida pelo administrador. O fabricante da aplicação também pode ser adicionado, mas não seja necessário.  

    **Suportado em**:  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Tipo de palavra-passe obrigatório**: Especifique se o utilizador tem de criar uma palavra-passe de alfanumérica ou de uma palavra-passe numérica. Para as palavras-passe de alfanuméricas, também especificar o número mínimo de conjuntos de carateres que a palavra-passe tem de ter. São os quatro conjuntos de carateres: letras em minúsculas, letras maiúsculas, símbolos e números.  

    **Suportado em**:  
    - Windows Phone 8+  
    - Windows 8.1+  
    - iOS 6+  

- **Depuração de USB de bloco no dispositivo**: Não tem de configurar esta definição, como a depuração USB já se encontra desativada em dispositivos Android para dispositivos de trabalho.  

    **Suportado em**:  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Bloquear aplicações de origens desconhecidas**: Exigir que os dispositivos impeçam a instalação de aplicações de origens desconhecidas. Não tem de configurar esta definição como dispositivos Android for Work restringem sempre a instalação de origens desconhecidas.  

    **Suportado em**:  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Exigir análise de ameaças nas aplicações**: Esta definição especifica que a funcionalidade de aplicações Verifique se está ativada no dispositivo.  

    **Suportado em**:  
    - Android 4.2 a 4.4 através de  
    - Samsung KNOX Standard 4.0+  


### <a name="find-an-app-id"></a>Encontrar um ID de aplicação

Um ID de aplicação é um identificador que identifica exclusivamente a aplicação nos serviços de aplicação da Apple e a Google. Um exemplo é `com.contoso.myapp`. Para localizar um:

- **Android**: Localize a aplicação de URL que foi utilizado para criar a aplicação da loja de ID na Google Play. Um ID de aplicação de exemplo é: `...?id=com.companyname.appname&hl=en`  

- **iOS**  
    1. Determinar o número de ID no URL da loja do iTunes. Por exemplo: `/id875948587?mt=8`  

    2. Num browser, aceda ao URL seguinte, substituindo o número com o número de ID que acabou de encontrar. Por exemplo, `https://itunes.apple.com/lookup?id=875948587`  

    3. Transfira e abra o ficheiro de texto.  

    4. Pesquisa de texto **bundleId**. Por exemplo: `"bundleId":"com.companyname.appname"`  

