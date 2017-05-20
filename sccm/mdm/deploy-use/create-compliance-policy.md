---
title: "Criar e implementar uma política de conformidade do dispositivo | Documentos do Microsoft"
description: "Saiba como criar e implementar políticas de conformidade do dispositivo no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0fd76043-d7ee-423d-8c5f-aa7e9ed58ce0
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
robots: noindex
ms.translationtype: Machine Translation
ms.sourcegitcommit: 216d288aa7b7f2b98df86f59355d879366dcd44d
ms.openlocfilehash: 4baa6e0fe009f5f7dc33f5ab4adb1ec5e5c5271b
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---

# <a name="create-and-deploy-a-device-compliance-policy"></a>Criar e implementar uma política de conformidade do dispositivo

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


## <a name="create-a-compliance-policy"></a>Criar uma política de conformidade

1.  Na consola do System Center Configuration Manager, escolha **ativos e compatibilidade**.

2.  No **ativos e compatibilidade** área de trabalho, expanda **definições de compatibilidade**e, em seguida, escolha **políticas de conformidade**.

3.  No **base** separador o **criar** grupo, selecione **criar política de conformidade**.

4.  No **geral** página do Assistente de política de conformidade criar, especifique as seguintes informações:

  * **Nome**. Introduza um nome exclusivo para a política de conformidade. Pode utilizar até 256 carateres.

  * **Descrição**. Introduza uma descrição que proporcione uma descrição geral do perfil VPN e ajuda a identificá-la na consola do Configuration Manager. Pode utilizar até 256 carateres.

  * **Tipo de política de conformidade**. Selecione o tipo de política que pretende criar, dependendo se o dispositivo é gerido pelo Configuration Manager. Isto aplica-se à versão ou posterior.<br /><br /> Para dispositivos geridos pelo Intune, escolha a opção **Regras de conformidade de dispositivos geridos com o cliente do Configuration Manager** . Quando seleciona esta opção, também pode selecionar o tipo de plataforma que pretende que esta política para aplicar a.

  * **Gravidade de incompatibilidade para relatórios**. Especifica o nível de gravidade comunicado se esta política de compatibilidade for avaliada como incompatível. Os níveis de gravidade disponíveis são:

     * **Nenhum**. Dispositivos que não obedeçam a esta regra de compatibilidade não reportam uma gravidade de falha para relatórios do Configuration Manager.
     * **Informações**. Dispositivos que não obedeçam a esta regra de compatibilidade reportam uma gravidade de falha de **informações** para relatórios do Configuration Manager.   
     * **Aviso**. Dispositivos que não obedeçam a esta regra de compatibilidade reportam uma gravidade de falha de **aviso** para relatórios do Configuration Manager.
     * **Crítico**. Dispositivos que não obedeçam a esta regra de compatibilidade reportam uma gravidade de falha de **crítico** para relatórios do Configuration Manager.
     * **Crítico com evento**. Dispositivos que não obedeçam a esta regra de compatibilidade reportam uma gravidade de falha de **crítico** para relatórios do Configuration Manager. Este nível de gravidade é também registado como um evento do Windows no registo de eventos de aplicações.      

5.  No **plataformas suportadas** página, selecione as plataformas de dispositivos que esta política de conformidade, serão avaliadas no, ou escolha **Selecionar tudo** para escolher todas as plataformas de dispositivo. As plataformas suportadas são: Windows 7, Windows 8.1 e Windows 10; Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016.

6.  Na página **Regras**, pode definir uma ou mais regras que definem a configuração que os dispositivos têm de ter para serem avaliados como em conformidade. Quando cria uma política de conformidade, algumas regras são ativadas por predefinição, mas pode editá-las ou eliminá-las. Para obter uma lista completa de todas as regras, consulte a secção "Conformidade as regras de política" mais à frente neste tópico.

  > [!NOTE]  
  >  Em Windows PCs, Windows 8.1 de versão do sistema operativo é comunicado como 6.3 em vez de 8.1. Se a regra de versão do SO estiver definida como Windows 8.1 para Windows, em seguida, o dispositivo será considerado como não compatíveis, mesmo que o dispositivo tem o Windows 8.1. Certifique-se de que está a definir à direita *comunicado* versão do Windows para as regras de SO mínimas e máxima. O número da versão tem de corresponder à versão que o **winver** comando devolve. Os dispositivos Windows Phone não têm este problema; a versão é reportada como 8.1 conforme esperado. Para PCs Windows com o sistema operativo do Windows 10, a versão deve ser definida como **10.0** plus a compilação do SO número que o **winver** comando devolve.

7.  No **resumo** página do assistente, reveja as definições que efetuou e, em seguida, conclua o assistente.

 A nova política é apresentada no **políticas de conformidade** nó do **ativos e compatibilidade** área de trabalho.

## <a name="deploy-a-compliance-policy"></a>Implementar uma política de conformidade

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade**.

2.  No **ativos e compatibilidade** área de trabalho, expanda **definições de compatibilidade**e, em seguida, escolha **políticas de conformidade**.

3.  No **base** separador o **implementação** grupo, selecione **implementar**.

4.  No **implementar política de conformidade** diálogo caixa, selecione **procurar** para selecionar a coleção de utilizador para os quais implementar a política.

     Além disso, pode selecionar opções para gerar alertas quando a política não é compatível e para definir o agendamento através do qual esta política será avaliada para compatibilidade.

5.  Quando tiver terminado, selecione **OK**.

## <a name="monitor-the-compliance-policy"></a>Monitorizar a política de conformidade

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Para ver os resultados de compatibilidade na consola do Configuration Manager

1.  Na consola do Configuration Manager, escolha **monitorização**.

2.  No **monitorização** área de trabalho, selecione **implementações**.

3.  Na lista **Implementações** , selecione a implementação de política de conformidade cujas informações de conformidade pretende rever.

4.  Poderá rever as informações de resumo sobre a conformidade da implementação da política na página principal. Para ver informações mais detalhadas, selecione a implementação e, em seguida, no **base** no separador o **implementação** grupo, selecione **Ver estado** para abrir o **estado da implementação** página.

    O **estado da implementação** página tem os seguintes separadores:

    -   **Conformidade**. Mostra a compatibilidade da política baseada no número de ativos afetados. Pode escolher uma regra para criar um nó temporário sob o **utilizadores** ou **dispositivos** nó do **ativos e compatibilidade** área de trabalho, que contém todos os utilizadores ou dispositivos que estejam em conformidade com esta regra. O **detalhes do ativo** painel mostra os utilizadores ou dispositivos que estejam em conformidade com a política. Faça duplo clique de um utilizador ou dispositivo na lista para mostrar informações adicionais.

    -   **Erro**. Mostra uma lista de todos os erros para a implementação da política selecionada com base no número de ativos afetados. Pode escolher uma regra para criar um nó temporário sob o **utilizadores** ou **dispositivos** nó do **ativos e compatibilidade** área de trabalho, que contém todos os utilizadores ou dispositivos que geraram erros com esta regra. Quando seleciona um utilizador ou dispositivo, o **detalhes do ativo** painel mostra os utilizadores ou dispositivos que afeta a um problema. Faça duplo clique de um utilizador ou dispositivo na lista para mostrar informações adicionais sobre o problema.

    -   **Não conformes**. Mostra uma lista de todas as regras não compatíveis na política, com base no número de ativos afetados. Pode escolher uma regra para criar um nó temporário sob o **utilizadores** ou **dispositivos** nó do **ativos e compatibilidade** área de trabalho, que contém todos os utilizadores ou dispositivos que não estejam em conformidade com esta regra. Quando seleciona um utilizador ou dispositivo, o **detalhes do ativo** painel mostra os utilizadores ou dispositivos que afeta a um problema. Faça duplo clique de um utilizador ou dispositivo na lista para mostrar mais informações sobre o problema.

    -   **Desconhecido**. Mostra uma lista de todos os utilizadores e dispositivos que não comunicaram compatibilidade para a implementação da política selecionada, juntamente com o atual estado de cliente dos dispositivos.

#### <a name="to-monitor-the-compliance-status-of-an-individual-device"></a>Para monitorizar o estado de conformidade de um dispositivo individual

1.  Na consola do Configuration Manager, escolha o **ativos e compatibilidade** área de trabalho.

2.  Escolher **dispositivos**.

3.  Faça duplo clique das colunas para ativar a mais colunas.

  Pode adicionar as seguintes colunas:

  - **O ID de dispositivo do Azure Active Directory**.  Identificador exclusivo para o dispositivo no Azure Active Directory.

  - **Detalhes do erro de compatibilidade**.  Detalhes de mensagem de erro quando o processo de ponto-a-ponto fica errado. Se esta coluna estiver em branco, isso significa que não foram encontrados erros, e o estado de compatibilidade com êxito foi reportado.

  - **Localização de erros de compatibilidade**.  Obter mais detalhes sobre onde a compatibilidade falhou. Se esta coluna estiver em branco, isso significa que não foram encontrados erros, e o estado de compatibilidade com êxito foi reportado. Exemplos de onde o processo de compatibilidade poderá falhar: 
      - Cliente do ConfigMgr
      - Ponto de gestão
      - Intune
      - Do Azure Active Directory
<br></br>
  - **Hora de avaliação de compatibilidade**. Hora da última a compatibilidade foi verificada.

  - **Definir o tempo de conformidade**. Última vez que a compatibilidade foi atualizada no Azure Active Directory.

  - **Acesso condicional compatível**.  Se pretende ou não a máquina está em conformidade com políticas de acesso condicional.

  > [!IMPORTANT]
  > Estas colunas não são apresentadas por predefinição.

#### <a name="to-view-intune-compliance-policies-charts"></a>Para ver os gráficos de políticas de conformidade do Intune
1. A partir na versão 1610 do Configuration Manager, na consola do Configuration Manager, escolha **monitorização**.

2. No **monitorização** área de trabalho, aceda a **descrição geral** > **definições de compatibilidade** > **políticas de conformidade**.

   Os gráficos seguintes, são apresentadas:

    - **Conformidade do dispositivo geral**. Mostra a compatibilidade geral dos dispositivos para todas as políticas de conformidade.
    - **Principais razões de não conformidade**. Mostra as políticas de início das quais os dispositivos que não são compatíveis.

3. Selecione uma secção em qualquer gráfico para descer até uma lista de dispositivos dentro dessa categoria.

#### <a name="to-view-a-health-attestation-report"></a>Para visualizar um relatório de atestado de estado de funcionamento

1.  A partir na versão 1602 do Configuration Manager, na consola do Configuration Manager, escolha **monitorização**.

2.  Para ver um relatório de resumo do estado atual de dispositivos ao respetivo estado de conformidade, selecione **segurança**e, em seguida, escolha **atestado de estado de funcionamento**.

3.  Para ver um relatório que lista todos os dispositivos e todos os atributos de atestado de estado de funcionamento, selecione **segurança**e, em seguida, escolha **atestado de estado de funcionamento**.

## <a name="compliance-policy-rules"></a>Regras de política de conformidade
* **Exigir definições de palavra-passe em dispositivos móveis**. É possível requerer que os utilizadores introduzam uma palavra-passe antes de poderem aceder ao respetivo dispositivo.

  **Suportado no:**
    * Windows Phone 8+
    * iOS 6+
    * Android 4.0+
    * Samsung KNOX Standard 4.0+

* **Exigir uma palavra-passe para desbloquear um dispositivo inativo** (1602 atualizar). É possível requerer que os utilizadores introduzam uma palavra-passe para o dispositivo de acesso está bloqueado.

  **Suportado no:**
  * Windows Phone 8+
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Minutos de inatividade antes da palavra-passe é exigida** (1602 atualizar). Pode especificar o tempo de inatividade antes do utilizador tem de reintroduzir a palavra-passe. Defina o valor para uma das opções disponíveis: **1 minute**, **5 minutes**, **15 minutes**, **30 minutes**, **1 hour**.

  Esta regra deve ser utilizada com **exigir uma palavra-passe para desbloquear um dispositivo inativo**. O valor definido aqui determina quando o dispositivo é considerado inativo e está bloqueado. Quando **exigir uma palavra-passe para desbloquear um dispositivo inativo** está definido como **verdadeiro**, o utilizador tem de introduzir uma palavra-passe para aceder ao dispositivo bloqueado.

  **Suportado no:**
  * Windows Phone 8+
  * Windows RT/8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Requerer atualizações automáticas** (1602 atualizar). É possível requerer dispositivos com Windows 8.1 ou posterior para instalar atualizações automaticamente e pode especificar a classe de atualizações.

  O valor deve ser definido como **nenhum** para impedir a instalação automática, **recomendado** para instalar automaticamente recomendadas todas as atualizações, ou ao **importante** para instalar apenas as atualizações classificadas como importantes.

  **Suportado no:**
  * Windows Phone 8+

* **Permitir palavras-passe simples**. Pode permitir que os utilizadores criem palavras-passe simples, tal como "1234" ou "1111". Esta definição está desativada por predefinição.

  **Suportado no:**
  * Windows Phone 8+
  * iOS 6+

* **Comprimento mínimo da palavra-passe**. Pode especificar o número mínimo de dígitos ou carateres que palavra-passe de utilizador têm de ter (6 por predefinição).

  **Suportado no:**
  * Windows Phone 8+
  * Windows 8,1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

  >[!NOTE]
  >Para dispositivos que executam o Windows e estão protegidos com uma conta Microsoft, a política de conformidade não será avaliada corretamente se **comprimento mínimo da palavra-passe** for maior do que 8 carateres ou se **número mínimo de conjuntos de carateres** é mais do que 2.

* **Encriptação de ficheiros em dispositivo móvel**. É possível requerer o dispositivo seja encriptado para se ligar aos recursos. Os dispositivos que executam o Windows Phone 8 são encriptados automaticamente. Os dispositivos que executam o iOS são encriptados quando configura a definição **Exigir definições de palavra-passe em dispositivos móveis**. Esta definição está ativada por predefinição.

  **Suportado no:**
  * Windows Phone 8+
  * Windows 8,1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Dispositivo não deve ser desbloqueado por jailbreak ou rooting**. Se ativar esta definição, (iOS) dispositivos com jailbreak ou (Android) não são compatíveis. Esta definição está desativada por predefinição.

  **Suportado no:**
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Perfil de e-mail tem de ser gerido pelo Intune**. Se definir esta opção como **Sim**, o dispositivo tem de utilizar o perfil de e-mail implementado no dispositivo. O dispositivo é considerado não conforme se o perfil de e-mail não for implementado no mesmo grupo de utilizadores que o grupo de utilizadores visado pela política de conformidade.

  Também é considerado não conforme se o utilizador tiver configurado uma conta de e-mail no dispositivo que corresponda ao perfil de e-mail do Intune implementado no dispositivo. Neste caso, o Intune não pode substituir o perfil aprovisionado pelo utilizador, pelo que não o consegue gerir. O utilizador pode trazer o dispositivo para a compatibilidade através da remoção das definições de e-mail existentes, que lhe permite instalar o perfil de e-mail gerido do Intune.

  Para obter detalhes sobres os perfis de e-mail, veja [Configurar o acesso a e-mail empresarial através de perfis de e-mail com o Microsoft Intune](https://technet.microsoft.com/library/dn800672.aspx). Esta definição está desativada por predefinição.

  **Suportado no:**
  * iOS 6+

* **Perfil de e-mail**. Se **conta de correio eletrónico têm de ser gerida pelo Intune** é selecionado, escolher **selecione** para escolher o perfil de e-mail que dispositivos têm de ser geridos. O perfil de e-mail tem de estar presente no dispositivo.

  **Suportado no:**
  * iOS 6+

* **SO mínimo necessário**. Quando um dispositivo não cumpre o requisito de versão mínimo do SO que especificar, é reportado como não compatível. É apresentada uma ligação com informações sobre como efetuar a atualização. O utilizador pode optar por atualizar o respetivo dispositivo, após o qual poderão aceder a recursos da empresa.

  **Suportado no:**
  * Windows Phone 8+
  * Windows 8,1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Versão do SO máximo permitido**. Quando um dispositivo usa uma versão do SO mais tarde do que aquela que especificou na regra, o acesso aos recursos da empresa é bloqueado e é pedido ao utilizador para contactar o administrador de TI. Até alterar a regra para permitir que a versão do SO, este dispositivo não pode ser utilizado para aceder aos recursos da empresa.

  **Suportado no:**
  * Windows Phone 8+
  * Windows 8,1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Exigir reportadas como bom estado de funcionamento dos dispositivos** (1602 atualizar). Pode definir uma regra para exigir que os dispositivos Windows 10 tem de ser reportados Saudável nas políticas de conformidade de novo ou existente. Se ativar esta definição, os dispositivos Windows 10 são avaliados através do serviço de atestado do Estado de funcionamento (HAS) para os seguintes pontos de dados:

  - **O BitLocker está ativado**. Quando o BitLocker estiver ativada, o dispositivo pode proteger dados que estão armazenados na unidade contra acesso não autorizado, quando o sistema está desativado ou vai para hibernação.

   A Encriptação de Unidade BitLocker do Windows encripta todos os dados armazenados no volume do sistema operativo Windows. BitLocker utiliza o TPM para ajudar a proteger o sistema operativo Windows e os dados de utilizador. Isso ajudará a assegurar que um computador não é adulterado, mesmo que resta autónoma, perdidos ou roubados.
   
   Se o computador estiver equipado com um TPM compatível, o BitLocker utiliza o TPM para bloquear as chaves de encriptação que protegem os dados. Como resultado, as chaves só podem ser acedidas depois de o TPM verificar o estado do computador.

  - **Integridade do código está ativada**. A integridade do código é uma funcionalidade que valida a integridade de um controlador ou ficheiro de sistema sempre que é carregado na memória. Integridade do código Deteta se um controlador de ou sistema de ficheiros não assinados está a ser carregado para o kernel. Também Deteta se um ficheiro de sistema foi alterado por software malicioso que está a ser executado por uma conta de utilizador com privilégios de administrador.

  - **Arranque seguro está ativado**. Quando o arranque seguro está ativado, o sistema é forçado a iniciar-se num Estado fábrica fidedigna. Além disso, quando o arranque seguro está ativado, os componentes do núcleo utilizados para iniciar a máquina tem de ter assinaturas criptográficas corretas que são considerada fidedigna pela organização que fabricado o dispositivo. O firmware UEFI verifica isto antes de permitir que a máquina seja iniciada. Se todos os ficheiros foram adulterados, interrompendo a sua assinatura, o sistema não será iniciada.

  - **Início antecipado antimalware está ativada**. Esta definição aplica-se apenas para PCs. O antimalware de início antecipado (ELAM) fornece proteção para os computadores na sua rede durante o arranque e antes da inicialização de controladores de terceiros.
  
   Esta regra está desativada por predefinição.

  Para obter informações sobre como funciona o serviço HAS, veja [Health Attestation CSP](https://msdn.microsoft.com/library/dn934876.aspx).

  **Suportado no:**
  * Windows 10 e Windows 10 Mobile

- **As aplicações que não podem ser instaladas no dispositivo**. Se os utilizadores instalam uma aplicação na lista de aplicações não compatíveis de administrador, irá ser bloqueados quando tentarem aceder ao e-mail empresarial e outros recursos da empresa que suportam o acesso condicional. Esta regra requer o nome da aplicação e o ID da aplicação ao adicionar uma aplicação à lista de incompatibilidades definida pelo administrador. Também é possível adicionar o publicador de aplicação, mas não é necessário.

    **Suportado no:**
      * iOS 6+
      * Android 4.0+
      * Samsung KNOX Standard 4.0+

### <a name="find-an-app-id"></a>Localizar um ID de aplicação

Um ID de aplicação é um identificador que identifica exclusivamente a aplicação nos serviços de aplicações da Apple e Google. Um exemplo é com.contoso.myapp. Para localizar um:

- **Android**
    - Pode encontrar a aplicação ID no Google Play armazenar URL que foi utilizado para criar a aplicação. Uma aplicação de exemplo é o ID: *…? id=com.companyname.appname & hl = pt*

- **iOS**
    1. Do iTunes armazenar URL, ficará a saber o número de ID, como neste exemplo: */id875948587? mt = 8*

    2. Num browser, vá para o seguinte URL, substituir o número com o número de ID que acabou de (neste caso, o exemplo anterior): https://itunes.apple.com/lookup?id=875948587

    3. Transfira e abra o ficheiro de texto.
  
    4. Procure o texto **bundleId**.

    Uma aplicação de exemplo é o ID: "*bundleId*": "*com.companyname.appname*" 


