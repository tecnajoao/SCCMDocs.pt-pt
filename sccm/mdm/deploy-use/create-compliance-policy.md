---
title: "Criar e implementar uma política de conformidade do dispositivo"
titleSuffix: Configuration Manager
description: "Saiba como criar e implementar políticas de conformidade de dispositivos no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0fd76043-d7ee-423d-8c5f-aa7e9ed58ce0
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
robots: noindex
ms.openlocfilehash: bf0099cdf4df1b7421a257e910c8682e63f8ee1e
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="create-and-deploy-a-device-compliance-policy"></a>Criar e implementar uma política de conformidade do dispositivo

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


## <a name="create-a-compliance-policy"></a>Criar uma política de conformidade

1.  Na consola do System Center Configuration Manager, escolha **ativos e compatibilidade**.

2.  No **ativos e compatibilidade** área de trabalho, expanda **as definições de compatibilidade**e, em seguida, escolha **políticas de conformidade**.

3.  No **home page** separador o **criar** grupo, escolha **criar política de conformidade**.

4.  No **geral** página do Assistente de política de conformidade criar, especifique as seguintes informações:

  * **Nome**. Introduza um nome exclusivo para a política de conformidade. Pode utilizar até 256 carateres.

  * **Descrição**. Introduza uma descrição que proporcione uma descrição geral do perfil VPN e ajuda a identificá-la na consola do Configuration Manager. Pode utilizar até 256 carateres.

  * **Tipo de política de conformidade**. Selecione o tipo de política que pretende criar, dependendo se o dispositivo é gerido pelo Configuration Manager. Isto aplica-se a versão ou posterior.<br /><br /> Para dispositivos geridos pelo Intune, escolha a opção **Regras de conformidade de dispositivos geridos com o cliente do Configuration Manager** . Quando seleciona esta opção, também pode selecionar o tipo de plataforma que pretende aplicar a esta política.

  * **Gravidade de incompatibilidade para relatórios**. Especifica o nível de gravidade comunicado se esta política de compatibilidade for avaliada como incompatível. Os níveis de gravidade disponíveis são:

     * **Nenhum**. Dispositivos que não cumpram esta regra de compatibilidade não reportam uma gravidade de falha para relatórios do Configuration Manager.
     * **Informações**. Dispositivos que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **informações** para relatórios do Configuration Manager.   
     * **Aviso**. Dispositivos que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **aviso** para relatórios do Configuration Manager.
     * **Crítico**. Dispositivos que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **crítico** para relatórios do Configuration Manager.
     * **Crítico com evento**. Dispositivos que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **crítico** para relatórios do Configuration Manager. Este nível de gravidade é também registado como um evento do Windows no registo de eventos de aplicações.      

5.  No **plataformas suportadas** página, escolha as plataformas de dispositivos que esta política de conformidade será avaliada ou escolha **Selecionar tudo** para escolher todas as plataformas de dispositivos. As plataformas suportadas são: Windows 7, Windows 8.1 e Windows 10; Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016.

6.  Na página **Regras**, pode definir uma ou mais regras que definem a configuração que os dispositivos têm de ter para serem avaliados como em conformidade. Quando cria uma política de conformidade, algumas regras são ativadas por predefinição, mas pode editá-las ou eliminá-las. Para obter uma lista completa de todas as regras, consulte a secção "Regras de política de conformidade" neste tópico.

  > [!NOTE]  
  >  Em Windows PCs, versão 8.1 do sistema operativo do Windows é reportado como 6.3 em vez de 8.1. Se a regra de versão do SO estiver definida como Windows 8.1 para o Windows, em seguida, o dispositivo será considerado como não conforme mesmo que tenha do dispositivo Windows 8.1. Certifique-se de que define o direito *comunicadas* versão do Windows para as regras de SO mínimas e máxima. O número de versão tem de corresponder à versão que o **winver** comando devolve. Os dispositivos Windows Phone não têm este problema; a versão é reportada como 8.1 conforme esperado. Para PCs Windows com o sistema operativo do Windows 10, a versão deve ser definida como **10.0** plus a compilação do SO número que o **winver** comando devolve.

7.  No **resumo** página do assistente, reveja as definições efetuadas e, em seguida, conclua o assistente.

 A nova política é apresentada no **políticas de conformidade** o nó do **ativos e compatibilidade** área de trabalho.

## <a name="deploy-a-compliance-policy"></a>Implementar uma política de conformidade

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade**.

2.  No **ativos e compatibilidade** área de trabalho, expanda **as definições de compatibilidade**e, em seguida, escolha **políticas de conformidade**.

3.  No **home page** separador o **implementação** grupo, escolha **implementar**.

4.  No **implementar política de conformidade** diálogo caixa, escolha **procurar** para selecionar a coleção de utilizador para o qual pretende implementar a política.

     Além disso, pode selecionar as opções para gerar alertas quando a política não está em conformidade e para definir o agendamento através do qual esta política será avaliada a compatibilidade.

5.  Quando tiver terminado, escolha **OK**.

## <a name="monitor-the-compliance-policy"></a>Monitorizar a política de conformidade

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Para ver os resultados de compatibilidade na consola do Configuration Manager

1.  Na consola do Configuration Manager, escolha **monitorização**.

2.  No **monitorização** área de trabalho, escolha **implementações**.

3.  Na lista **Implementações** , selecione a implementação de política de conformidade cujas informações de conformidade pretende rever.

4.  Poderá rever as informações de resumo sobre a conformidade da implementação da política na página principal. Para ver informações mais detalhadas, selecione a implementação e, em seguida, no **home page** separador o **implementação** grupo, escolha **Ver estado** para abrir o **estado da implementação** página.

    O **estado da implementação** página tem os seguintes separadores:

    -   **Em conformidade**. Mostra a compatibilidade da política com base no número de ativos afetados. Pode escolher uma regra para criar um nó temporário sob o **utilizadores** ou **dispositivos** o nó do **ativos e compatibilidade** área de trabalho, que contém todos os utilizadores ou dispositivos que estão em conformidade com esta regra. O **detalhes do ativo** painel mostra os utilizadores ou dispositivos que estão em conformidade com a política. Faça duplo clique num utilizador ou dispositivo na lista para mostrar informações adicionais.

    -   **Erro**. Mostra uma lista de todos os erros para a implementação da política selecionada com base no número de ativos afetados. Pode escolher uma regra para criar um nó temporário sob o **utilizadores** ou **dispositivos** o nó do **ativos e compatibilidade** área de trabalho, que contém todos os utilizadores ou dispositivos que geraram erros com esta regra. Quando seleciona um utilizador ou dispositivo, o **detalhes do ativo** painel mostra os utilizadores ou dispositivos que um problema afeta. Faça duplo clique num utilizador ou dispositivo na lista para mostrar informações adicionais sobre o problema.

    -   **Não conformes**. Mostra uma lista de todas as regras não compatíveis na política, com base no número de ativos afetados. Pode escolher uma regra para criar um nó temporário sob o **utilizadores** ou **dispositivos** o nó do **ativos e compatibilidade** área de trabalho, que contém todos os utilizadores ou dispositivos que não cumpram esta regra. Quando seleciona um utilizador ou dispositivo, o **detalhes do ativo** painel mostra os utilizadores ou dispositivos que um problema afeta. Faça duplo clique num utilizador ou dispositivo na lista para mostrar mais informações sobre o problema.

    -   **Desconhecido**. Mostra uma lista de todos os utilizadores e dispositivos que não comunicaram compatibilidade para a implementação da política selecionada, juntamente com o estado atual do cliente dos dispositivos.

#### <a name="to-monitor-the-compliance-status-of-an-individual-device"></a>Para monitorizar o estado de conformidade de um dispositivo individual

1.  Na consola do Configuration Manager, escolha o **ativos e compatibilidade** área de trabalho.

2.  Escolha **dispositivos**.

3.  Clique com botão direito uma das colunas para permitir mais colunas.

  Pode adicionar as seguintes colunas:

  - **ID de dispositivo do Azure Active Directory**.  Identificador exclusivo para o dispositivo no Azure Active Directory.

  - **Detalhes do erro de conformidade**.  Detalhes de mensagem de erro quando o processo de ponto-a-ponto não bate certo. Se esta coluna está em branco, significa sem erros foram encontrados e o estado de conformidade foi comunicado com êxito.

  - **Localização de erro de conformidade**.  Obter mais detalhes sobre onde a conformidade falhou. Se esta coluna está em branco, significa sem erros foram encontrados e o estado de conformidade foi comunicado com êxito. Exemplos de onde o processo de compatibilidade poderá falhar: 
      - Cliente do ConfigMgr
      - Ponto de gestão
      - Intune
      - Azure Active Directory
<br></br>
  - **Hora de avaliação de compatibilidade**. Hora da última a compatibilidade tiver sido selecionada.

  - **Definir a hora de conformidade**. Hora da última a compatibilidade foi atualizada para o Azure Active Directory.

  - **Acesso condicional em conformidade**.  Se a máquina está em conformidade com políticas de acesso condicional.

  > [!IMPORTANT]
  > Estas colunas não são apresentadas por predefinição.

#### <a name="to-view-intune-compliance-policies-charts"></a>Para ver gráficos de políticas de conformidade do Intune
1. A partir da versão 1610 do Configuration Manager, na consola do Configuration Manager, escolha **monitorização**.

2. No **monitorização** área de trabalho, aceda a **descrição geral** > **as definições de compatibilidade** > **políticas de conformidade**.

   São apresentados os gráficos seguintes:

    - **Conformidade de dispositivos geral**. Mostra a compatibilidade geral dos dispositivos para todas as políticas de conformidade.
    - **Principais motivos de conformidade não**. Mostra as principais políticas para os dispositivos que estão em conformidade.

3. Escolha uma secção em qualquer gráfico para desagregar para obter uma lista dos dispositivos dentro dessa categoria.

#### <a name="to-view-a-health-attestation-report"></a>Para ver um relatório de atestado de estado de funcionamento

1.  A partir da versão 1602 do Configuration Manager, na consola do Configuration Manager, escolha **monitorização**.

2.  Para ver um relatório de resumo do estado atual de dispositivos por Estado de conformidade, escolha **segurança**e, em seguida, escolha **atestado de estado de funcionamento**.

3.  Para ver um relatório que apresenta uma lista de todos os dispositivos e todos os atributos de atestado de estado de funcionamento, escolha **segurança**e, em seguida, escolha **atestado de estado de funcionamento**.

## <a name="compliance-policy-rules"></a>Regras de política de conformidade
* **Exigir definições de palavra-passe em dispositivos móveis**. Pode exigir que os utilizadores introduzam uma palavra-passe antes de poderem aceder ao respetivo dispositivo.

  **Suportado no:**
    * Windows Phone 8+
    * iOS 6+
    * Android 4.0+
    * Samsung KNOX Standard 4.0+

* **Exigir uma palavra-passe para desbloquear um dispositivo inativo** (atualização 1602). Pode exigir que os utilizadores introduzam uma palavra-passe para aceder ao dispositivo que está bloqueado.

  **Suportado no:**
  * Windows Phone 8+
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Minutos de inatividade antes da palavra-passe é exigida** (atualização 1602). Pode especificar o tempo de inatividade antes do utilizador tem de reintroduzir a palavra-passe. Defina o valor para uma das opções disponíveis: **1 minute**, **5 minutes**, **15 minutes**, **30 minutes**, **1 hour**.

  Esta regra tem de ser utilizada com **exigir uma palavra-passe para desbloquear um dispositivo inativo**. O valor definido aqui determina quando o dispositivo é considerado inativo e é bloqueado. Quando **exigir uma palavra-passe para desbloquear um dispositivo inativo** está definido como **verdadeiro**, o utilizador tem de introduzir uma palavra-passe para aceder ao dispositivo bloqueado.

  **Suportado no:**
  * Windows Phone 8+
  * Windows RT/8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Requerer atualizações automáticas** (atualização 1602). Pode exigir a dispositivos com Windows 8.1 ou posterior para instalar automaticamente as atualizações e pode especificar a classe de atualizações.

  O valor deve ser definido como **nenhum** para impedir a instalação automática, **recomendado** para instalar automaticamente todas as atualizações recomendadas, ou **importante** para instalar apenas as atualizações classificadas como importantes.

  **Suportado no:**
  * Windows Phone 8+

* **Permitir palavras-passe simples**. Pode permitir que os utilizadores criem palavras-passe simples, como "1234" ou "1111." Esta definição está desativada por predefinição.

  **Suportado no:**
  * Windows Phone 8+
  * iOS 6+

* **Comprimento mínimo da palavra-passe**. Pode especificar o número mínimo de dígitos ou carateres que a palavra-passe do utilizador deve ter (6 por predefinição).

  **Suportado no:**
  * Windows Phone 8+
  * Windows 8,1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

  >[!NOTE]
  >Para dispositivos que executam o Windows e estão protegidos com uma conta Microsoft, a política de conformidade não conseguirá avaliar corretamente se **comprimento de palavra-passe mínimo** é superior a 8 carateres ou se **número mínimo de conjuntos de carateres** é mais do que 2.

* **Encriptação de ficheiros no dispositivo móvel**. Pode exigir o dispositivo seja encriptado para se ligar aos recursos. Os dispositivos que executam o Windows Phone 8 são encriptados automaticamente. Os dispositivos que executam o iOS são encriptados quando configura a definição **Exigir definições de palavra-passe em dispositivos móveis**. Esta definição está ativada por predefinição.

  **Suportado no:**
  * Windows Phone 8+
  * Windows 8,1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Dispositivo não pode ter jailbreak ou rooting**. Se ativar esta definição, desbloqueados por jailbreak (iOS) ou rooting (Android) não é compatíveis. Esta definição está desativada por predefinição.

  **Suportado no:**
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Perfil de e-mail tem de ser gerido pelo Intune**. Quando definir esta opção **Sim**, o dispositivo tem de utilizar o perfil de e-mail implementado no dispositivo. O dispositivo é considerado não conforme se o perfil de e-mail não for implementado no mesmo grupo de utilizadores que o grupo de utilizadores visado pela política de conformidade.

  Também é considerado não conforme se o utilizador tiver configurado uma conta de e-mail no dispositivo que corresponda ao perfil de e-mail do Intune implementado no dispositivo. Neste caso, o Intune não pode substituir o perfil aprovisionado pelo utilizador, pelo que não o consegue gerir. O utilizador pode colocar o dispositivo em conformidade, removendo as definições de e-mail existente, que permite instalar o perfil de e-mail gerido do Intune.

  Para obter detalhes sobres os perfis de e-mail, veja [Configurar o acesso a e-mail empresarial através de perfis de e-mail com o Microsoft Intune](https://technet.microsoft.com/library/dn800672.aspx). Esta definição está desativada por predefinição.

  **Suportado no:**
  * iOS 6+

* **Perfil de e-mail**. Se **conta de E-Mail tem de ser gerida pelo Intune** é selecionado, escolher **selecione** para escolher o perfil de e-mail que os dispositivos têm de ser geridos. O perfil de e-mail tem de estar presente no dispositivo.

  **Suportado no:**
  * iOS 6+

* **SO mínimo obrigatório**. Quando um dispositivo não cumpre o requisito de versão mínima do SO que especificar, é reportado como não conforme. É apresentada uma ligação com informações sobre como atualizar. O utilizador pode optar por atualizar o respetivo dispositivo, após o qual será seria capazes de aceder a recursos da empresa.

  **Suportado no:**
  * Windows Phone 8+
  * Windows 8,1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Versão do SO máxima permitida**. Quando um dispositivo utiliza uma versão do SO posterior à especificada na regra, o acesso aos recursos da empresa é bloqueado e é pedido ao utilizador para contactar o administrador de TI. Até que altere a regra para permitir a versão do SO, este dispositivo não pode ser utilizado para aceder a recursos da empresa.

  **Suportado no:**
  * Windows Phone 8+
  * Windows 8,1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Exigir que os dispositivos sejam comunicados como bom** (atualização 1602). Pode definir uma regra para exigir que dispositivos Windows 10 sejam comunicada como bom estado de funcionamento nas políticas de conformidade novas ou existentes. Se ativar esta definição, os dispositivos Windows 10 são avaliados através do serviço de atestado do Estado de funcionamento (HAS) para os seguintes pontos de dados:

  - **BitLocker está ativado**. Quando o BitLocker estiver ativado, o dispositivo pode proteger os dados que são armazenados na unidade contra acesso não autorizado, quando o sistema está desligado ou entra em hibernação.

   A Encriptação de Unidade BitLocker do Windows encripta todos os dados armazenados no volume do sistema operativo Windows. O BitLocker utiliza o TPM para ajudar a proteger os dados de utilizador e o sistema operativo Windows. Ajuda a garantir que um computador não é adulterado, mesmo se for deixado autónoma, perdido ou roubado.
   
   Se o computador estiver equipado com um TPM compatível, o BitLocker utiliza o TPM para bloquear as chaves de encriptação que protegem os dados. Como resultado, as chaves só podem ser acedidas depois de o TPM verificar o estado do computador.

  - **Integridade do código está ativada**. A integridade do código é uma funcionalidade que valida a integridade de um controlador ou ficheiro de sistema sempre que é carregado na memória. Integridade do código Deteta se um controlador ou de sistema de ficheiros não assinados está a ser carregado para o kernel. Também Deteta se um ficheiro de sistema foi alterado por software malicioso, que está a ser executado por uma conta de utilizador com privilégios de administrador.

  - **Arranque seguro está ativado**. Quando o arranque seguro está ativado, o sistema é forçado a iniciar-se num Estado de fábrica fidedigno. Além disso, quando o arranque seguro está ativado, os componentes principais utilizados para iniciar a máquina tem de ter assinaturas criptográficas corretas que sejam consideradas fidedignas pela organização que fabricou o dispositivo. O firmware UEFI verifica isto antes de permitir que a máquina seja iniciada. Se todos os ficheiros tem sido adulterados, danificando a respetiva assinatura, o sistema não será iniciado.

  - **Antimalware de início antecipado está ativado**. Esta definição aplica-se apenas a PCs. O antimalware de início antecipado (ELAM) fornece proteção para os computadores na sua rede durante o arranque e antes da inicialização de controladores de terceiros.
  
   Esta regra está desativada por predefinição.

  Para obter informações sobre como funciona o serviço HAS, veja [Health Attestation CSP](https://msdn.microsoft.com/library/dn934876.aspx).

  **Suportado no:**
  * Windows 10 e Windows 10 Mobile

- **As aplicações que não podem ser instaladas no dispositivo**. Se os utilizadores instalarem uma aplicação da lista de aplicações não conformes admin, irá ser bloqueados quando tentarem aceder a e-mail empresarial e outros recursos da empresa que suportam o acesso condicional. Esta regra requer que o nome da aplicação e o ID da aplicação ao adicionar uma aplicação à lista de incompatibilidades definida pelo administrador. Também pode ser adicionado o fabricante da aplicação, mas não é necessário.

    **Suportado no:**
      * iOS 6+
      * Android 4.0+
      * Samsung KNOX Standard 4.0+
<br></br>
* **Tipo de palavra-passe obrigatório**. Especifique se o utilizador tem de criar uma palavra-passe alfanumérica ou uma palavra-passe numérico. Palavras-passe alfanuméricos, também especificar o número mínimo de conjuntos de carateres que a palavra-passe tem de ter. Os quatro conjuntos de carateres são: Em minúsculas, maiúsculas letras, símbolos e números.

    **Suportado no:**
    * Windows Phone 8+
    * Windows 8.1 +
    * iOS 6+
<br></br>
* **Depuração USB de bloco no dispositivo**. Não é necessário configurar esta definições como a depuração USB já está desativada no Android para dispositivos de trabalho.

    **Suportado no:**
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
<br></br>
* **Impedir que as aplicações a partir de origens desconhecidas**. Exigir que os dispositivos impeçam a instalação de aplicações a partir de origens desconhecidas. Não é necessário configurar esta definição, tal como Android, para dispositivos de trabalho sempre restringir a instalação a partir de origens desconhecidas.

    **Suportado no:**
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
<br></br>
* **Necessária análise de ameaças nas aplicações**. Esta definição especifica que a funcionalidade de aplicações de Verifique está ativada no dispositivo. 

    **Suportado no:**
    * Android 4.2 através de 4.4
    * Samsung KNOX Standard 4.0+

### <a name="find-an-app-id"></a>Localizar um ID de aplicação

Um ID de aplicação é um identificador que identifica exclusivamente a aplicação dentro os serviços de aplicações da Apple e o Google. Um exemplo é com.contoso.myapp. Para localizar um:

- **Android**
    - Pode encontrar a aplicação do ID no Google Play armazenar URL que utilizou para criar a aplicação. Uma aplicação de exemplo é o ID: *…? id=com.companyname.appname & hl = pt*

- **iOS**
    1. Na iTunes armazenar URL, localizar o número de ID, como neste exemplo: */id875948587? mt = 8*

    2. Num browser, aceda ao URL seguinte, substituindo o número com o número de ID localizar (neste caso, o exemplo anterior): https://itunes.apple.com/lookup?id=875948587

    3. Transfira e abra o ficheiro de texto.
  
    4. Pesquisa de texto **bundleId**.

    Uma aplicação de exemplo é o ID: "*bundleId*": "*com.companyname.appname*" 

